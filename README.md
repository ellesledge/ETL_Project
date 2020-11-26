ETL Project

Group #10:  Danielle Sledge, Garrett Watkins, Laurel Whitten

Datasets provided by kaggle.com:  https://www.kaggle.com/usdot/flight-delays?select=flights.csv

The original data came from the Department of Transportation's Bureau of Statistics.  
The user who posted this on kaggle.com was trying to determine what airline you should fly to avoid significant delays in 2015.

Data Cleanup & Analysis

Original csv files:

airlines.csv
airports.csv
flights.csv

The airlines file contains 14 different airlines that serve domestic routes in the US.
The airports file contains 322 airports in 50 states.  It lists the airport name, airport code, city, state, longitude and latitude.
The flights file contains every commercial flight from every airport in the US on every day of 2015.  This file contains over 1 million rows.

Right away, we knew we needed to reduce the size of our flights.  Excel wouldn't load the entire file and in some cases, it was crashing.
First, we decided to pare down the airlines.  We removed all the airlines except Delta, United, USAirways, and American.  This removed about 75% of our rows, but the file was still too big.
We decided to go with just Delta.

We still wanted to reduce the file, so we discussed what would be the best option.  We thought about removing some of the dates, maybe only looking at a few months.
We decided to only look at flights that originated in Atlanta.  Why?  Atlanta is the world's busiest airport and Delta's main hub.

This brought our file down to a more manageable size.

Cleaning, Joining, Filtering, Aggregating

We used a relational database for the final production.  Why?  We are more comfortable with PostGres.  It seems more user-friendly and intuitive.


ETL process

Extraction:

We downloaded our datasets from https://www.kaggle.com/usdot/flight-delays?select=flights.csv.  The data was formatted in 3 csv files.

Transform:

We used jupyter notebook to clean our data and create our tables.
Our cleaning process was as followed:

Flights CSV Cleaning
-Removed any column with missing data.  This resulted in 1,048,575 rows and 13 columns
-Removed columns CANCELLED and DIVERTED, because most flights were not cancelled nor diverted, but landed at the airport expected
-Removed all airlines except Delta.  This reduced our file to 147,486 rows
-Filtered out all originating airports except ATL.  This brought our file down to 42,197 rows
-Added Weekday column
-Changed integers to whole numbers

Airports CSV Cleaning
-Removed columns 
-Renamed columns IATA_CODE to match Flights CSV for merging

After we finished cleaning our data we merged the Airports CSV file and Flights CSV file.  At this time we decided that the Airlines file was unneeded. 

Load:
-First we created a database in PostGres and a table containing all our columns.
-We then loaded our cleaned data into PostGres. 
-We encountered an error while making the connection in jupyter notebook and found that our columns in jupyter notebook and the table we created in PostGres was case senstive. 




