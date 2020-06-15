# Data Modeling with Postgres
### Project Overview
###### A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.
###### This project focuses on building an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables  for their analytics team to continue finding insights in what songs their users are listening to. 

### Project Description
###### In this project, data modeling is designed with Postgres database hosted on Redshift and and AWS to build an ETL pipeline using Python. Fact and dimension tables are defined and an ETL pipeline that transfers data from S3 into these tables in Postgres using Python and SQL.

### Project Dataset
###### The  dataset is an each file in JSON format that reside in S3. Here are the S3 links for each.
*Song data: s3://udacity-dend/song_data*
*Log data: s3://udacity-dend/log_data*

### Song Dataset
###### The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.
*song_data/A/B/C/TRABCEI128F424C983.json*
*song_data/A/A/B/TRAABJL12903CDCF1A.json*
###### And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
*{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}*
### Log Dataset
###### The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.
###### The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset
*log_data/2018/11/2018-11-12-events.json*
*log_data/2018/11/2018-11-13-events.json*
###### And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.
![Log data format ](/log-data.png)

### Schema for Song Play Analysis
###### Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables
###### Fact Table
* songplays - records in log data associated with song plays i.e. records with page NextSong
      * songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
###### Dimension Tables
* users - users in the app
      * user_id, first_name, last_name, gender, level
* user_id, first_name, last_name, gender, level
      song_id, title, artist_id, year, duration
* artists - artists in music database
      * artist_id, name, location, latitude, longitude
* time - timestamps of records in songplays broken down into specific units
      start_time, hour, day, week, month, year, weekday

### Project repository details
###### In addition to the data files, the project includes six files:
1. create_tables.py drops and creates tables. You run this file to reset your tables before each time you run your ETL scripts.
2. etl.py etracts the data from S3 copies into staging tables on Redshift and then process that data into analytics tables on Redshift.
5. sql_queries.py contains all your sql queries, and is imported into two other files above.
6. README.md provides discussion on your project.
      
### Database Design
Below is the ER diagram to understand the data base model implemented. 
![Song project ERD](/Song_ERD.png)

### ETL Process (pipeline)
###### Create_tables.py creates the all the fact and dimension tables required for the processing.  etl.py performs the major processing by extracting json input file from s3 and for further ptocessing stages them in Redshift, and transforms data into a fact and dimensional tables.

### Project execution
###### Run create_tables.py to create the postgre table ddl definitions and then run etl.py which extacts the json files from s3 bucket and stages in Redshift and then inserts into all fact and dimension tables. 
