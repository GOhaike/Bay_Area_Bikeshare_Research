# Project 1: Query Project

- In the Query Project, you will get practice with SQL while learning about
  Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven
  questions using public datasets housed in GCP. To give you experience with
  different ways to use those datasets, you will use the web UI (BiqQuery) and
  the command-line tools, and work with them in Jupyter Notebooks.

#### Problem Statement

- You're a data scientist at Lyft Bay Wheels (https://www.lyft.com/bikes/bay-wheels), formerly known as Ford GoBike, the
  company running Bay Area Bikeshare. You are trying to increase ridership, and
  you want to offer deals through the mobile app to do so. 
  
- What deals do you offer though? Currently, your company has several options which can change over time.  Please visit the website to see the current offers and other marketing information. Frequent offers include: 
  * Single Ride 
  * Monthly Membership
  * Annual Membership
  * Bike Share for All
  * Access Pass
  * Corporate Membership
  * etc.

- Through this project, you will answer these questions: 

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- Please note that there are no exact answers to the above questions, just like in the proverbial real world.  This is not a simple exercise where each question above will have a simple SQL query. It is an exercise in analytics over inexact and dirty data. 

- You won't find a column in a table labeled "commuter trip".  You will find you need to do quite a bit of data exploration using SQL queries to determine your own definition of a communter trip.  In data exploration process, you will find a lot of dirty data, that you will need to either clean or filter out. You will then write SQL queries to find the communter trips.

- Likewise to make your recommendations, you will need to do data exploration, cleaning or filtering dirty data, etc. to come up with the final queries that will give you the supporting data for your recommendations. You can make any recommendations regarding the offers, including, but not limited to: 
  * market offers differently to generate more revenue 
  * remove offers that are not working 
  * modify exising offers to generate more revenue
  * create new offers for hidden business opportunities you have found
  * etc. 

#### All Work MUST be done in the Google Cloud Platform (GCP) / The Majority of Work MUST be done using BigQuery SQL / Usage of Temporary Tables, Views, Pandas, Data Visualizations

A couple of the goals of w205 are for students to learn how to work in a cloud environment (such as GCP) and how to use SQL against a big data data platform (such as Google BigQuery).  In keeping with these goals, please do all of your work in GCP, and the majority of your analytics work using BigQuery SQL queries.

You can make intermediate temporary tables or views in your own dataset in BigQuery as you like.  Actually, this is a great way to work!  These make data exploration much easier.  It's much easier when you have made temporary tables or views with only clean data, filtered rows, filtered columns, new columns, summary data, etc.  If you use intermediate temporary tables or views, you should include the SQL used to create these, along with a brief note mentioning that you used the temporary table or view.

In the final Jupyter Notebook, the results of your BigQuery SQL will be read into Pandas, where you will use the skills you learned in the Python class to print formatted Pandas tables, simple data visualizations using Seaborn / Matplotlib, etc.  You can use Pandas for simple transformations, but please remember the bulk of work should be done using Google BigQuery SQL.

#### GitHub Procedures

In your Python class you used GitHub, with a single repo for all assignments, where you committed without doing a pull request.  In this class, we will try to mimic the real world more closely, so our procedures will be enhanced. 

Each project, including this one, will have it's own repo.

Important:  In w205, please never merge your assignment branch to the master branch. 

Using the git command line: clone down the repo, leave the master branch untouched, create an assignment branch, and move to that branch:
- Open a linux command line to your virtual machine and be sure you are logged in as jupyter.
- Create a ~/w205 directory if it does not already exist `mkdir ~/w205`
- Change directory into the ~/w205 directory `cd ~/w205`
- Clone down your repo `git clone <https url for your repo>`
- Change directory into the repo `cd <repo name>`
- Create an assignment branch `git branch assignment`
- Checkout the assignment branch `git checkout assignment`

The previous steps only need to be done once.  Once you your clone is on the assignment branch it will remain on that branch unless you checkout another branch.

The project workflow follows this pattern, which may be repeated as many times as needed.  In fact it's best to do this frequently as it saves your work into GitHub in case your virtual machine becomes corrupt:
- Make changes to existing files as needed.
- Add new files as needed
- Stage modified files `git add <filename>`
- Commit staged files `git commit -m "<meaningful comment about your changes>"`
- Push the commit on your assignment branch from your clone to GitHub `git push origin assignment`

Once you are done, go to the GitHub web interface and create a pull request comparing the assignment branch to the master branch.  Add your instructor, and only your instructor, as the reviewer.  The date and time stamp of the pull request is considered the submission time for late penalties. 

If you decide to make more changes after you have created a pull request, you can simply close the pull request (without merge!), make more changes, stage, commit, push, and create a final pull request when you are done.  Note that the last data and time stamp of the last pull request will be considered the submission time for late penalties.

---

## Parts 1, 2, 3

We have broken down this project into 3 parts, about 1 week's work each to help you stay on track.

**You will only turn in the project once  at the end of part 3!**

- In Part 1, we will query using the Google BigQuery GUI interface in the cloud.

- In Part 2, we will query using the Linux command line from our virtual machine in the cloud.

- In Part 3, we will query from a Jupyter Notebook in our virtual machine in the cloud, save the results into Pandas, and present a report enhanced by Pandas output tables and simple data visualizations using Seaborn / Matplotlib.

---

## Part 1 - Querying Data with BigQuery

### SQL Tutorial

Please go through this SQL tutorial to help you learn the basics of SQL to help you complete this project.

SQL tutorial: https://www.w3schools.com/sql/default.asp

### Google Cloud Helpful Links

Read: https://cloud.google.com/docs/overview/

BigQuery: https://cloud.google.com/bigquery/

Public Datasets: Bring up your Google BigQuery console, open the menu for the public datasets, and navigate to the the dataset san_francisco.

- The Bay Bike Share has two datasets: a static one and a dynamic one.  The static one covers an historic period of about 3 years.  The dynamic one updates every 10 minutes or so.  THE STATIC ONE IS THE ONE WE WILL USE IN CLASS AND IN THE PROJECT. The reason is that is much easier to learn SQL against a static target instead of a moving target.

- (USE THESE TABLES!) The static tables we will be using in this class are in the dataset **san_francisco** :

  * bikeshare_stations

  * bikeshare_status

  * bikeshare_trips

- The dynamic tables are found in the dataset **san_francisco_bikeshare**

### Some initial queries

Paste your SQL query and answer the question in a sentence.  Be sure you properly format your queries and results using markdown. 

- What's the size of this dataset? (i.e., how many trips)

 - SQL query:


   ```
   SELECT count(*) FROM `bigquery-public-data.san_francisco.bikeshare_trips`
   ```

 - Answer :**983648**

- What is the earliest start date and time and latest end date and time for a trip?

  - SQL query:
  
    ```
    SELECT min(start_date) AS earliest_Start_date_and_time, max(end_date) AS latest_end_date_and_time
	 FROM `bigquery-public-data.san_francisco.bikeshare_trips`
   ```


   - Answer: 
			
  	 | earliest_startr_date_and_time | latest_end_date_and_time|
 	 |:------------------------------| :-----------------------| 
 	 | 2013-08-29 09:08:00 UTC       | 2016-08-31 23:48:00 UTC |

- How many bikes are there?

  - SQL query: 

  
    ```
     SELECT count(distinct bike_number) AS number_of_bikes 
	FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    ```

 -  Answer: number_of_bikes :**700**

### Questions of your own

  - Make up 3 questions and answer them using the Bay Area Bike Share Trips Data.  These questions MUST be different than any of the questions and queries you ran above.

  - Question 1: How many stations are there in San Jose?

   - Answer:**18**

- SQL query:

  ```
  SELECT count(station_id) FROM `bigquery-public-data.san_francisco.bikeshare_stations` 
	WHERE landmark = "San Jose"
  ```

- Question 2: what are the top three stations names and landmark with the highest number of dock count?

  - Answer

 		|           name              | landmark      | dockcount |
 		| :---------------------------| :------------ | :---------|
 		| Cyril Magnin St at Ellis St | San Francisco |     35    |
 		| 5th St at Folsom St         | San Francisco |     31    |
 		| Market at 10th              | San Francisco |     27    |
	
 - SQL query:

 
   ```
   SELECT name,landmark,dockcount, FROM `bigquery-public-data.san_francisco.bikeshare_stations` ORDER BY (dockcount) DESC LIMIT 3
   ```


-  Question 3: What is the oldest installation date and what are the stations_id ,name and dockcount?

 - Answer:

   * oldest station :**2013-08-05**

- SQL query: 


  ```
  SELECT min(installation_date) as min_date
	FROM `bigquery-public-data.san_francisco.bikeshare_stations`
  ```


### Bonus activity queries (optional - not graded - just this section is optional, all other sections are required)

The bike share dynamic dataset offers multiple tables that can be joined to learn more interesting facts about the bike share business across all regions. These advanced queries are designed to challenge you to explore the other tables, using only the available metadata to create views that give you a broader understanding of the overall volumes across the regions(each region has multiple stations)

We can create a temporary table or view against the dynamic dataset to join to our static dataset.

Here is some SQL to pull the region_id and station_id from the dynamic dataset.  You can save the results of this query to a temporary table or view.  You can then join the static tables to this table or view to find the region:
```sql

#standardSQL
select distinct region_id, station_id
from `bigquery-public-data.san_francisco_bikeshare.bikeshare_station_info`
```

- Top 5 popular station pairs in each region

- Top 3 most popular regions(stations belong within 1 region)

- Total trips for each short station name in each region

- What are the top 10 used bikes in each of the top 3 region. these bikes could be in need of more frequent maintenance.

---

## Part 2 - Querying data from the BigQuery CLI 

- Use BQ from the Linux command line:

  * General query structure


    ```
    bq query --use_legacy_sql=false '
        SELECT count(*)
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
    ```


### Queries

1. Rerun the first 3 queries from Part 1 using bq command line tool (Paste your bq
   queries and results here, using properly formatted markdown):

  * What's the size of this dataset? (i.e., how many trips)


    ``` 
    bq query --use_legacy_sql=false 'SELECT count(*) as freq FROM `bigquery-public-data.san_francisco.bikeshare_trips`'  
    ```

	
    	|freq    |
     	|:-------|
     	| 983648 |

 
  * What is the earliest start time and latest end time for a trip?
  

   ```
   bq query --use_legacy_sql=false 'SELECT min(start_date) AS earliest_Start_date_and_time,max(end_date) AS latest_end_date_and_time FROM `bigquery-public-data.san_francisco.bikeshare_trips`'  
   ``` 



  	|earliest_Start_date_and_time | latest_end_date_and_time |
  	|:----------------------------|--------------------------|
  	| 2013-08-29 09:08:00         |      2016-08-31 23:48:00 |
    
    

  * How many bikes are there?


    ```
    bq query --use_legacy_sql=false 'SELECT count(distinct bike_number) AS number_of_bikes FROM `bigquery-public-data.san_francisco.bikeshare_trips`' 
    ```  



   	| number_of_bikes |
   	|:----------------|
   	|     700         |


2. New Query (Run using bq and paste your SQL query and answer the question in a sentence, using properly formatted markdown):

    * How many trips are in the morning vs in the afternoon?

    
      ```
      bq query --use_legacy_sql=false 'SELECT COUNTIF(EXTRACT(HOUR FROM start_date) IN (5,6,7,8,9)) AS morning_trip, 
      	COUNTIF(EXTRACT(HOUR FROM start_date) IN (12,13,14,15)) AS afternoon_trip,
      		COUNTIF(EXTRACT(HOUR FROM start_date) IN (16,18,19,20)) AS evening_trip,
     			 FROM `bigquery-public-data.san_francisco.bikeshare_trips`'
      ```



  * Output  

  
+--------------+----------------+--------------+
| morning_trip | afternoon_trip | evening_trip |
+--------------+----------------+--------------+
|       321730 |         176142 |       237142 |
+--------------+----------------+--------------+

### Project Questions
Identify the main questions you'll need to answer to make recommendations (list
below, add as many questions as you need).

- Question 1: What are the stations id with less than 3 bikes available and more than 10 dock available limiit to 10

- Question 2: what are the counts of subscriber type

- Question 3: what are the first 10 highest trip time in sec, the stations id and the subscibers

- Question 4: What are the lest 10 station id with least number of start trips?

- Question 5: What are the number of bikeshare stations as per landmark

- Question 6: What is the average trip time 

- Question 7: What is the minimum and maximum trip time

- Question 8: What is the minimum and maximum bike available

- Question 9: What are the top 5 busiest hours from the start date

- Question 10: What are the top 5 busiest hours from the end date?

- Question 11:Extract commute hours and filter trips between 5 to 60 minutes

- Question 12: What is the peak trip Hours and days of the week most trips occurs and the station?

- Question 13 What is the number of trips recorded at by region

### Answers

 Answer at least 4 of the questions you identified above You can use either
 BigQuery or the bq command line tool.  Paste your questions, queries and
 answers below.

-  Question 1: What are the stattionid with less than 3 bikes available and more than 10 dock available limit to 10

  - Answer:

  		|station_id|bikes_available|docks_available        |time                    |	
  		|:---------|:--------------|:----------------------|:-----------------------|
  		|91        |1              |34                     |2016-08-25 18:15:00 UTC |	
  		|91        |1              |34                     |2016-08-25 17:24:54 UTC |	
  		|91        |1              |34                     |2016-08-25 15:50:54 UTC |	
  		|91        |1              |34                     |2016-08-25 17:39:01 UTC |	
  		|91        |1              |34                     |2016-08-25 20:16:49 UTC |
  		|91        |1              |34                     |2016-08-25 17:52:59 UTC |	
  		|91        |1              |34                     |2016-08-25 14:04:51 UTC |	
  		|91        |1              |30                     |2016-08-30 17:04:01 UTC |
  		|91        |1              |34                     |2016-08-25 19:28:51 UTC |	
  		|91        |1              |34                     |2016-08-25 16:36:54 UTC |


  - SQL query:


    ```
   SELECT * FROM `bigquery-public-data.san_francisco.bikeshare_status` WHERE bikes_available < 2 AND docks_available > 10 LIMIT 10
   ```

 
- Question 2: What are the number different subscribers

  -  Answer:

  		|subscriber_type|count |
  		|:--------------|:-----|			
  		|Customer       |136809|	
  		|Subscriber     |846839|

  - SQL query:
 
  
    ```
    SELECT subscriber_type , COUNT(*) FROM `bigquery-public-data.san_francisco.bikeshare_trips` GROUP BY subscriber_type
    ```


 - Question 3: What are the first 10 highest trips time in sec, the station id, and the subscribers 

  -  Answer:

 	 	|duration_sec|bike_number|start_station_id|end_station_id|subscriber_type|
 	 	|:-----------|:----------|:---------------|:-------------|:--------------|	
  	 	|17270400    |535        |66              |62            |Customer       |	
  	 	|2137000     |466        |77              |68            |Customer       |	
  	 	|1852590     |680        |31              |32            |Subscriber     |
 	 	|1133540     |262        |35              |35            |Customer       |	
 	 	|722236      |247        |35              |35            |Customer       |	
 	 	|720454      |692        |22              |25            |Customer       |	
 	 	|716480      |633        |50              |72            |Subscriber     |	
 	 	|715339      |251        |14              |5             |Customer       |	
 	 	|688899      |230        |34              |36            |Customer       |	
 	 	|655939      |132        |3               |12            |Customer       |


  - SQL query: 


  
    ```
    SELECT duration_sec, bike_number,start_station_id,end_station_id,subscriber_type 
  	FROM `bigquery-public-data.san_francisco.bikeshare_trips`
 	  	ORDER BY duration_sec DESC LIMIT 10		 
    ```


- Question 4: What are the least 10 station id with least number of start trips

  -  Answer:


  		|start_station_id|freq |
  		|:---------------|-----|	
  		|88              |20   |	
  		|91              |69   |	
  		|89              |84   |	
  		|90              |173  |	
  		|21              |241  |	
  		|24              |272  |	
  		|23              |373  |	
  		|26              |463  |	
  		|83              |467  |	
  		|25              |931  |


  - SQL query:


  
    ```
    SELECT  start_station_id, COUNT(*) as freq FROM `bigquery-public-data.san_francisco.bikeshare_trips` GROUP BY start_station_id ORDER BY 2 LIMIT 10
  
     ```



 - Question 5: What are the number of bikeshare stations as per landmark

  - Answer:


    
 		| landmark     |freq |
 		|:-------------|:----|		
 		|San Francisco |37   |	
 		|San Jose      |18   |	
 		|Redwood City  |7    |	
 		|Mountain View |7    |	
 		|Palo Alto     |5    |


  * SQL query:


    ```
    SELECT landmark, COUNT(*) as freq  FROM `bigquery-public-data.san_francisco.bikeshare_stations`  
	GROUP BY landmark ORDER BY 2 DESC LIMIT 10
    ```



-  Question 6: What is the average trip time

 * Answer:


   		|avg_trip_time     |	
   		|:-----------------|	
   		|1018.9323467338004|

- SQL query:



  ```

  SELECT AVG(duration_sec) as avg_trip_time 
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
 ```


- Question 7: What is the minimum and maximum trip time

 - Answer


 		| min_duration_trip|max_duration_trip|
 		|:-----------------|:----------------|	
 		|60                |17270400         |

 
   - SQL Query:

   
    ```
    SELECT min(duration_sec) as min_duration_trip, max(duration_sec) as max_duration_trip FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    ```

- Question 8: What is the manimum and maximum bikes available

 * Answer



   		| min_bike_available|max_bike_available|
   		|:------------------|:-----------------|	
   		|0                  |29                |



 - SQL query :
 


   ```
   SELECT min(bikes_available) as min_bike_available, max(bikes_available) as max_bike_available FROM `bigquery-public-data.san_francisco.bikeshare_status`
   ```


- Question 9: What are the top 5 busiest trip hours from the start date?

   * Answer



   		|Hour|trip_count|
   		|:---|:---------|
   		|8   |132464    |	
   		|17  |126302    |	
   		|9   |96118     |	
   		|16  |88755     |	
   		|18  |84569     |


- SQL query: 



 ```
 SELECT EXTRACT(HOUR FROM start_date) as Hour, count(EXTRACT(HOUR FROM start_date)) as trip_count
   FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    GROUP BY Hour
       ORDER BY trip_count DESC LIMIT 5
   ```


- Question 10: What are the top 5 busiest trip hours from the end date?

 * Answer:



   		|Hour|trip_count|
   		|:---|:---------|		
   		|17  |129072    |	
   		|8   |123941    |	
   		|9   |108459    |	
   		|18  |96317     |	
   		|16  |81238     |


 - SQL query:


 
   ```
   SELECT EXTRACT(HOUR FROM end_date) as Hour, count(EXTRACT(HOUR FROM end_date)) as trip_count
     FROM `bigquery-public-data.san_francisco.bikeshare_trips`
       GROUP BY Hour
        ORDER BY trip_count DESC LIMIT 5
   ```



- Question 11:Extract commute hours and filter trips between 5 to 60 minutes

 - Answer 
 

   		|HR |MIN|duration_sec|	start_date           |	end_date             |
   		|:--|:--|:-----------|:----------------------|:----------------------|		
   		|16 |18 |3600        |2014-04-19 16:18:00 UTC|2014-04-19 17:18:00 UTC|	
   		|16 |4  |3598        |2014-04-07 16:04:00 UTC|2014-04-07 17:04:00 UTC|	
   		|16 |41 |3598        |2016-03-24 16:41:00 UTC|2016-03-24 17:41:00 UTC|	
   		|17 |15 |3596        |2015-05-16 17:15:00 UTC|2015-05-16 18:15:00 UTC|	
   		|16 |0  |3595        |2016-05-05 16:00:00 UTC|2016-05-05 17:00:00 UTC|


- SQL query:



   ```
    SELECT EXTRACT(HOUR FROM start_date) AS HR, EXTRACT(MINUTE FROM start_date) AS MIN, duration_sec, start_date, end_date
   	 FROM `bigquery-public-data.san_francisco.bikeshare_trips`
      		 WHERE ((EXTRACT(HOUR FROM start_date) IN (6,7,8)) OR (EXTRACT(HOUR FROM start_date) IN (16,17,18,19))) AND (duration_sec >= 300 AND duration_sec <= 3600)
        		ORDER BY duration_sec DESC LIMIT 5
   ```



- Question 12: What is the peak trip Hours and days of the week most trips occurs and the station?

* Answer 



 		|hour|weekday|start_station_name                     |end_station_name   | duration_sec|subscriber_type|frequency|
 		|:---|:------|:--------------------------------------|:------------------|:------------|:--------------|:--------|
 		|8   |3      |Harry Bridges Plaza (Ferry Building)   |2nd at Townsend    |466          |Subscriber     |12       |	
 		|9   |2      |San Francisco Caltrain 2 (330 Townsend)|Townsend at 7th    |248          |Subscriber     |10       |	
 		|8   |2      |Harry Bridges Plaza (Ferry Building)   |2nd at Townsend    |485          |Subscriber     |9	 |
 		|17  |3      |Townsend at 7th                        |Townsend at 4th    |210          |Subscriber     |9        |	
 		|9   |5      |Mountain View Caltrain Station         |M View City Hall   |243          |Subscriber     |9        | 	 
 		|6   |8      |Harry Bridges Plaza (Ferry Building)   |2nd at Townsend    |481          |Subscriber     |9        | 	
 		|8   |4.     |Harry Bridges Plaza (Ferry Building).  |2nd at Townsend    |455          |Subscriber     |9        |  	
 		|16  |3      |2nd at Townsend                        |Harry Bridges Plaza|418          |Subscriber     |9        |	
 		|9   |3      |Mountain View Caltrain Station         |Mt View City Hall  |232          |Subscriber     |9        |	 
 		|8   |3      |San Francisco Caltrain 2 (330 Townsend)|Townsend at 7th    |214          |Subscriber     |9        |
	 	 

- SQL query:

  ```
  SELECT  EXTRACT(HOUR from start_date) AS hour, EXTRACT(DAYOFWEEK from start_date) as weekday,start_station_name, end_station_name,duration_sec,subscriber_type, COUNT(*) as frequeny
	 FROM `bigquery-public-data.san_francisco.bikeshare_trips`
		WHERE EXTRACT(DAYOFWEEK from start_date) IN (2,3,4,5,6,7) AND EXTRACT(HOUR from start_date) IN (6,7,8,9,16,17,18,19)
			GROUP BY start_station_name,subscriber_type, end_station_name,duration_sec,hour,weekday
				ORDER BY frequency DESC LIMIT 10
  ```



## Part 3 - Employ notebooks to synthesize query project results

### Get Going

Create a Jupyter Notebook against a Python 3 kernel named Project_1.ipynb in the assignment branch of your repo.

#### Run queries in the notebook 

At the end of this document is an example Jupyter Notebook you can take a look at and run.  

You can run queries using the "bang" command to shell out, such as this:


```
! bq query --use_legacy_sql=FALSE '<your-query-here>'
```

- NOTE: 
- Queries that return over 16K rows will not run this way, 
- Run groupbys etc in the bq web interface and save that as a table in BQ. 
- Max rows is defaulted to 100, use the command line parameter `--max_rows=1000000` to make it larger
- Query those tables the same way as in `example.ipynb`

Or you can use the magic commands, such as this:

```sql
%%bigquery my_panda_data_frame

select start_station_name, end_station_name
from `bigquery-public-data.san_francisco.bikeshare_trips`
where start_station_name <> end_station_name
limit 10
```

```python
my_panda_data_frame
```

#### Report in the form of the Jupter Notebook named Project_1.ipynb

- Using markdown cells, MUST definitively state and answer the two project questions:

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- For any temporary tables (or views) that you created, include the SQL in markdown cells

- Use code cells for SQL you ran to load into Pandas, either using the !bq or the magic commands

- Use code cells to create Pandas formatted output tables (at least 3) to present or support your findings

- Use code cells to create simple data visualizations using Seaborn / Matplotlib (at least 2) to present or support your findings

### Resource: see example .ipynb file 

[Example Notebook](example.ipynb)

