# The Anatomy of a Hit: Decoding Spotify's Most Streamed Songs (2013-2023)

## Project Overview
This project is an end-to-end data analytics pipeline analyzing the acoustic characteristics (BPM, energy, danceability) of Spotify's top-streamed tracks. The goal is to extract and rank the defining audio signatures that correlate with mega-hit status over the last decade.

## Architecture & Tools
* **Data Extraction & Cleaning:** Python (Pandas)
* **Storage & Analytical Engine:** MySQL
* **Visualization:** Python (Matplotlib / Seaborn)
* **Documentation:** Excel (Data Dictionary)

## How to Reproduce this Project

**1. Database Setup:**
* Install MySQL.
* Run the scripts in the `/sql` folder in order:
  * Execute `01_schema.sql` to build the database tables.

**2. Data Pipeline:**
* Download the raw dataset from [Kaggle Link] and place it in a local `/data/raw` folder (Note: Raw data is excluded from this repo via .gitignore).
* Open `/notebooks/01_data_cleaning.ipynb` and run all cells to clean the data and push it to the MySQL database.
* Execute `02_analysis.sql` within your SQL environment to perform the core information extraction and ranking.

**3. Visualization:**
* Open `/notebooks/02_visualizations.ipynb` to pull the aggregated SQL insights and generate the final dashboards.
