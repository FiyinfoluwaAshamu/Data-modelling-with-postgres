 	<h1> **Data Modelling with Postgres**</h1>
    
 	<h2> **Introduction**</h2>

<p>A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.</p>

<p>They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results</p>

 	<h2>**Project Description**</h2>
<p>In this project, I will apply what I have learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, I had to define fact and dimension tables for a star schema for a particular analytic focus, and wrote an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.</p>
    
 	<h2>**Running the Python script**</h2>
 > Terminal
 >
 > -python create_tables.py
 > -python etl.py
 >
 > Python
 >
 > -run create_tables.py
 > -run et.py

 	<h2>**Database Schema**</h2>

After examining the JSON files, a Star schema as shown below was created. It includes one Fact table (songplays) and 4 Dimension tables(songs, artists, time, users).

![star_schema](/images/star_schema.png)

	<h2>**Dataset**</h2>
    
	<h3>**Song dataset**</h3>
<p>The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are file paths to two files in this dataset. In other words, they are used to populate Dimension tables for Songs and Artists..</p>

>song_data/A/B/C/TRABCEI128F424C983.json
>
>song_data/A/A/B/TRAABJL12903CDCF1A.json

<p>Below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like (It is parsed to populate the Songs and Artists Dimension tables.).</p>

> {"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}


	<h3>**Log dataset**</h3>
<p> The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.</p>

<p> The log files are partitioned by year and month. For example, here are filepaths to two files in this dataset.</p>

>log_data/2018/11/2018-11-12-events.json
>
>log_data/2018/11/2018-11-13-events.json

<p>This data contains information about the songs Users listened to at a specific time. Information is parsed to provide data for the Songplays Fact table, the Users and Time Dimension tables. The songplays.artist_id and songplays.song_id columns are populated based on the Song Title, Artist Name and song Duration. In other words, they files are used to populate Dimension tables for Songs and Artists.</p>


	<h2>**Data files**</h2>
    
> test.ipynb - displays the first few rows of each table to let me check my database.
>
> create_tables.py - This Python script recreates the database and tables used to store the data.
>
> etl.ipynb - reads and processes a single file from song_data and log_data and loads the data into the tables. This notebook contains detailed instructions on the ETL process for each of the tables.
>
> etl.py - reads and processes files from song_data and log_data and loads them into the tables. 
>
> sql_queries.py - contains all my sql queries, and is imported into the last three files above.
