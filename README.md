# Capstone - Google Data Analytics Course
This is the final project (capstone) of the Google Data Analytics certification that group all the key elements seen through the course. A case study is provided, where the fictional company (Cyclistic) needs to answer to a series of key business questions using data. In this imaginary situation, I am part of the marketing analytics team. My goal is to apply all the knowledge acquired in the Google Analytics course to find the answers to the questions posed. The introductory documentation can be read [here](/docs/case_study_definition.md).


## Prepare step

### About this dataset
The data regarding this case study has been made available by Motivate International Inc under this [licence](https://ride.divvybikes.com/data-license-agreement). It is presented in a series of csv files, one per each month. For this case, the data used is from June 2021 to July 2022, the last 12 month from the creation of this project. Each row of this dataset represents a trip from a client of the company, and it contains 13 columns (or features) providing the different details.

### ROCCC  
For a propper analysis, I followed the ROCCC guideline that ensures the data used follow this aspects:

* **Reliable**: GOOD. Our dataset has more than a million examples, it is data from all the users from Chicago city, without regard sex, nationality, culture or any other aspect that can bias the result.
* **Original**: GOOD. The data has been extracted directly from a real rental-bike company.
* **Comprehensive**: GOOD. It seems to have all the key elements to answer the business question posed.
* **Current**: GOOD. It is recently added data that ensures relevancy, and data is continuously published each month.
* **Cited**: GOOD. We know the source of all the data and who we need to address if we have any question.



## Process step
One important step is to clean the data on those errors and missing values to ensure integrity and consistency. Some techniques were applied in order to find discrepancies and to expand the available data (data aggregation).  

### Data Integrity
Importing the csv files into a relational database using SQL or as a dataframe in R offers the oportunity to check integrity easily. With this tools can be seen that some examples don't follow the rest of the sample: missing data, IDs too longs, GPS coordinates in different formats...
/
This problems must be solved in order to ensure data integrity and start working on the business task.
/


### Data aggregation
Some new columns were created to better understand the business case:
* **ride_length**: Duration of the total ride (in seconds).
* **day_of_week**: Day of the week of the ride (1 = Sunday, 2 = Monday, ..., 7 = Saturday).
* **day**: Only the day number of the start of the ride.
* **month**: Only the month number of the start of the ride.
* **year**: Only the year number of the start of the ride.

### Missing values
As for the missing values, the features related with the station (start_station_name, start_station_id, end_station_name, end_station_id) have between 836018 and 892103 missing values, this is represents a 15% of the total set.
/
"end_lat" and "end_lng" also present missing values: 5374 values, this is a total of 0.09%. 
/
As this data was unable to replace with other stadistical operations, it was dropped from the dataset.
The rest of the available data remains completed.


### Wrong data

Doing the cleaning phase of the dataset, some wrong data arrised. This errors can be found in the columns related with the dates of the trip. Some trips ended in a previous (or same) time than the start! A quick verification is to find negative and 0 values on the newly created "ride_length" column. 646 values were detected.
/
At this point we may ask, it is logical to have trips with a duration of a few seconds? For this case, a trip duration of less than a minute was dropped of the analysis. This criteria elevated the number of values to drop to 100420 (1.70%).
/
The rest of the data didn't present any other complication, and other serval techniques where applied in order to check its integrity. For example, the "ride_id" column was used as a primary key, and it was checked that all of its values where unique and had a similar structure (alphanumerical values with 16 characters long).

### Data transformation

It is important to ensure that each data is represented with the correct type. As for the "member_casual" feature, the unique values are "member" and "casual". A better representation is to map this values to a boolean type: member = True, casual = False. This column was renamed as "is_member".