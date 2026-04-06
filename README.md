# The Anatomy of a Hit: Decoding Spotify's Most Streamed Songs (2013-2023)

## Project Overview
This project is an end-to-end data analytics pipeline analyzing the acoustic characteristics (BPM, energy, danceability) of Spotify's top-streamed tracks. The goal is to extract and rank the defining audio signatures that correlate with mega-hit status over the last decade.

## Architecture & Tools
* **Data Extraction & Cleaning:** Python (Pandas)
* **Storage & Analytical Engine:** MySQL
* **Visualization:** Excel
* **Documentation:** Google Docs, Excel (Data Dictionary)

## How to Reproduce this Project

**1. Clone / Download Repository:**
* Clone or download this repository to your computer

**2. Install Required Python Libraries:**     
```py -m pip install pandas mysql-connector-python sqlalchemy```

**3. Download Kaggle Library:**
* Download the kaggle library using the link below and put it into the raw folder: project directory > data > raw  
* Note: Make sure the kaggle file is named Popular_Spotify_Songs.csv     
* https://www.kaggle.com/datasets/arnavvvvv/spotify-music

**4. Configure MySQL Password:**
* Look for the line of code near the bottom of the notebook that says update this password and add your MySQL password   
``` mysql_password = 'YOURPASSWORDHERE' ```

**5. Create the Database in MySQL:**   
* Open the MySQL console and enter the command   
```CREATE DATABASE spotify_db;```

**6. Run the Entire Notebook:**
* If all works, the .csv file should be properly cleaned and sent to your MySQL folder

**7. Run SQL Commands:**
* Open up your MySQL command line   
* Run the command ``` SHOW databases; ``` and look for spotify_db  
* Run the command ``` USE spotify_db; ```
* Run the following SQL commands to replicate our data analysis:
     

* Count the number of songs in each key   
``` SELECT `key`, COUNT(*) AS count FROM top_songs GROUP BY `key` ORDER BY count DESC; ```
* Count the number of songs in each mode (chord major/minor)   
``` SELECT `mode`, COUNT(*) AS count FROM top_songs GROUP BY `mode` ORDER BY count DESC; ```
* Count the number of songs in each BPM range      
``` 
SELECT 
    CASE 
        WHEN bpm < 100 THEN 'Slow (<100)'
        WHEN bpm BETWEEN 100 AND 130 THEN 'Medium (100-130)'
        ELSE 'Fast (>130)'
    END AS tempo_range,
    COUNT(*) AS song_count
FROM top_songs
GROUP BY tempo_range
ORDER BY song_count DESC;
```
* Average all used columns for all songs
```   
SELECT 
    ROUND(AVG(bpm), 2) AS avg_bpm,
    ROUND(AVG(`danceability_%`), 2) AS avg_danceability,
    ROUND(AVG(`valence_%`), 2) AS avg_valence,
    ROUND(AVG(`energy_%`), 2) AS avg_energy,
    ROUND(AVG(`acousticness_%`), 2) AS avg_acousticness,
    ROUND(AVG(`instrumentalness_%`), 2) AS avg_instrumentalness,
    ROUND(AVG(`liveness_%`), 2) AS avg_liveness,
    ROUND(AVG(`speechiness_%`), 2) AS avg_speechiness
FROM top_songs;
```
* Year by year averages for all used columns for all songs   
``` 
SELECT 
    released_year, 
    COUNT(*) AS total_hits,
    ROUND(AVG(bpm), 1) AS avg_bpm,
    ROUND(AVG(`danceability_%`), 1) AS avg_danceability,
    ROUND(AVG(`valence_%`), 1) AS avg_valence,
    ROUND(AVG(`energy_%`), 1) AS avg_energy,
    ROUND(AVG(`instrumentalness_%`), 1) AS avg_instrumentalness,
    ROUND(AVG(`liveness_%`), 1) AS avg_liveness,
    ROUND(AVG(`speechiness_%`), 1) AS avg_speechiness
FROM top_songs
GROUP BY released_year
ORDER BY released_year ASC;
```
* Statistics on archetype combinations   
``` 
SELECT 
    CASE 
        WHEN `danceability_%` >= 70 AND `energy_%` >= 70 THEN 'The Club Banger (High Dance/Energy)'
        WHEN `danceability_%` < 60 AND `acousticness_%` >= 50 THEN 'The Acoustic Ballad (Low Dance/High Acoustic)'
        ELSE 'Standard Pop / Other'
    END AS song_archetype,
    COUNT(*) AS total_songs,
    ROUND(AVG(CAST(streams AS UNSIGNED)), 0) AS average_streams
FROM top_songs
GROUP BY song_archetype
ORDER BY average_streams DESC;
```
