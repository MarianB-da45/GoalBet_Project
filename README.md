# GoalBet_Project
- As Data Engineers, our primary responsibility is to design and implement robust data pipelines that facilitate the seamless flow of data from various sources into our analytical systems.  We would be building an ETL pipeline to Extract, Transform and Load data into PostgreSQL. 

## Project Overview
- GoalBet is a leading sports data analytics company dedicated to
providing comprehensive insights into various sporting events.
By leveraging historical data and advanced analytical
techniques, GoalBet aims to enhance the understanding of
sports performance and facilitate informed decision-making for
its clients.

## Introduction
-Typically, we retrieve information relating to sports (football,
tennis, horse racing) results from both public web sites and
commercial data providers. The information is usually in a semi
structured format such as CSV, JSON or Microsoft Excel. We
then transform the data and put it in a persistent store, such as a
database. Later on, this data is used by our data science team.

## Project Objective
-As a data engineer, our primary responsibility is to design and implement robust data pipelines that
facilitate the seamless flow of data from various sources into our analytical systems.
We would be building an ETL pipeline to Extract, Transform and Load data into PostgreSQL.

The importance of this process is to ensure:

-- automation of data retrieval,

-- Data Quality

-- Data Reliability

-- Storage in PostgreSQL

## Data Source
- The data will be sourced from: https://www.football-data.co.uk/englandm.php

- Format of data retrieved (CSV)

- The CSV file has 106 columns from which we are to extract data

  ## ETL Process Overview 1
 -  ETL Stage 1 - Extract

   - Source:
      - The data is retrieved from the website football-data.co.uk, which provides CSV files for various football leagues.

   - How
     - The script constructs URLs dynamically based on the current season (e.g., E0.csv for the Premiership).It uses the requests
       library to send an HTTP GET request to the specified URLs.The script checks the HTTP response status. If the status is 200
       (OK), it proceeds to read the CSV data. If not, it logs an error.

   ## ETL Process Overview 2
  --  ETL Stage 2 - Transform

     -- Cleaning:

       - The script reads the CSV data into a Pandas DataFrame while specifying the columns to extract, thus ignoring any unnecessary data.

       - We also convert the 'Date' column into a proper datetime format, ensuring consistency in date handling.

       - Time Column Handling: Any missing 'Time' values are filled with a default value of '15:00'

       - Goal Columns: The 'FTHG' (Full-Time Home Goals) and 'FTAG' (Full-Time Away Goals) columns are converted to integers.

       - Handling Missing Values: The script drops any rows that are entirely empty and resets the index of the DataFrame.

    -- Formatting

       - A new column, 'season', is added to the DataFrame to indicate the season for each record.

       - The DataFrame is structured according to the specified fields (['Div’, ‘Season’, 'Date', 'Time', 'HomeTeam','AwayTeam', 'FTHG', 'FTAG’]

     -- Merging

        - After extraction, individual CSV files for each league are merged into single file for loading to the DB
 
  ## ETL Process Overview 3
 --  ETL Stage 3 - Load

  -- DB Connection – PostgreSQL:

    - The script establishes a connection to a PostgreSQL database using SQLAlchemy's create_engine(), utilizing credentials
       stored in environment variables.

  -- Data Loading
    - The cleaned merged file is loaded into the PostgreSQL database using the to_sql() method. The method appends new records to the specified table (one for each league) 
      and handles any necessary schema definitions, based on the DataFrame structure.

## Staging Area
     -- Windows OS File Explorer is used as the staging area for historical data

     -- Windows OS File Explorer is used as the transformation area for historical data

## ETL Pipeline Architecture
     -- Architecture Diagram

## ETL Process - New Data
   -- ETL Stage 1 - Transform

      -- Cleaning:

      - The script reads the CSV data into a Pandas DataFrame while specifying the columns to extract, thus ignoring any unnecessary data.

      - We also convert the 'Date' column into a proper datetime format, ensuring consistency in date handling.

    -- Filtering

     - The script constructs URLs dynamically based on the current season (e.g., E0.csv for the Premiership).It uses the requests library to send an HTTP GET request to the 
       specified URLs.The script checks the HTTP response status. If the status is 200 (OK), it proceeds to read the CSV data. If not, it logs an error.


