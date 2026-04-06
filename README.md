# The Anatomy of a Hit: Decoding Spotify's Most Streamed Songs (2013-2023)

## Project Overview
This project is an end-to-end data analytics pipeline analyzing the acoustic characteristics (BPM, energy, danceability) of Spotify's top-streamed tracks. The goal is to extract and rank the defining audio signatures that correlate with mega-hit status over the last decade.

## Architecture & Tools
* **Data Extraction & Cleaning:** Python (Pandas)
* **Storage & Analytical Engine:** MySQL
* **Visualization:** Python (Matplotlib / Seaborn)
* **Documentation:** Excel (Data Dictionary)

## How to Reproduce this Project

**1. Clone / Download Repository:**
* Clone or download this repository to your computer

**2. Install Required Python Libraries:**  
```py -m pip install pandas mysql-connector-python sqlalchemy```

**3. Download Kaggle Library:**
* Download the kaggle library using the link below and put it into your project directory
* https://www.kaggle.com/datasets/arnavvvvv/spotify-music

**4. Configure MySQL Password:**
* Look for the line of code near the bottom of the notebook that says update this password and add your MySQL password.
``` mysql_password = 'YOURPASSWORDHERE' ```
