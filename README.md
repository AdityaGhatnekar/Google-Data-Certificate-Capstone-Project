## Google Data Certificate Capstone Project

### Case Study Summary

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geo tracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One 2 approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

### Business Task

Understanding user preferences and usage patterns for different bikes within the fleet. By gaining insights into user preferences and usage patterns, the company aims to tailor marketing strategies to enhance user activity and encourage membership subscriptions. 

#### Goals

•	To identify and categorise different user segments from the Cyclistic community

•	Classify various bikes available in the fleet

•	Advise marketing department of potential promotional campaigns or encourage users to try different bike types

#### Data Analytics Tools

The project uses Google Bigquery to manipulate data and Tableau for data visualisation. 

#### Data Sources

The data was sourced from open data made available my Motivate International Inc under this [license](https://divvybikes.com/data-license-agreement). There is historical trip data of year 2022 used to analyse for the project. 
The data can be found by clicking [here](https://divvy-tripdata.s3.amazonaws.com/index.html). 

### Data Preparation

Twelve monthly ride records encompassing the entirety of the year 2022 were procured in the form of .csv files and subsequently archived on the local drive. Certain files exceeded the size threshold of 100 megabytes, rendering a direct upload to BigQuery unfeasible. Consequently, the data was uploaded to Google Drive, whereupon a seamless connection with BigQuery was established to facilitate the integration of the voluminous datasets. 

A new table was created with all twelve months data combined named as ‘Cyclist_2022_combined’. Total number of rows recorded 5,667,717 with 774 MB size of the table. Columns used were ride_id, rideable_type, started_at, ended_at, start_station_id, start_station_name, end_station_id, end_station_name, member_casual.

Data was further explored on BigQuery, please find queries [here](#I.-Data-Preparation). Below listed are different characteristics of the data found:

•	There was a total of 833,064 *NULL* values in start_station_id and start_station_name, and a total of 892,742 *NULL* values in end_station_id and end_station_name. 
Further when the data was explored it was found both start and end station names and ids had a combined *NULL* values of 1,298,357.

•	Ride_id is a unique value of the dataset with no duplicate fields and all the records with 16 characters. 

•	The company has three types of bikes in their fleet docked, classic and electric.

•	The company distinguishes type of riders in causal and members.

### Data Cleaning
The process involved the addition of new columns, computation of ride durations, identification and removal of outliers, assignment of days of the week, and the creation of a cleaned dataset. The effectiveness of the cleaning process is demonstrated through the removal of approximately 1.3 million records based on specified conditions. Please clcik [here](#J.-Data-Cleaning) to view all SQL queries.

•	Two new columns ‘ride_time’ (representing ride duration) and ‘day_of_week' (representing day of the week the ride started) were added to the existing dataset.

•	The ride duration was computed with ‘TIMESTAMP_DIFF’ function between ‘started_at’ and ‘ended_at’ in seconds. 
Ride durations were further filtered, and outliers were excluded with 531 entries recorded as ‘0’ or negative duration and 5360 entries with durations more than 24 hours. 

•	A new table ‘Cyclist_2022_cleaned’ was created with conditions on presence of start and end station information and ride duration greater than 1 second and smaller than 24 hours.

### Data Analysis
The analysis stage focused on rider behaviour, patterns, and trends with different rider types. The investigation includes an exploration of the total number of trips by member type, rideable type, start and end stations, day of the week, hour of the day, and monthly trends. The findings offer valuable insights into the dynamics of member and casual rider usage, rideable type preferences, station popularity, and temporal variations. Please find analysis queries [here](#K.-Data-Analysis).

Below are findings with supported visualisations for all the queries processed.

#### Number of rides by rider types

Members recorded more rides than casual riders in year 2022. Specifically, members account for 2,610,617 trips, while casual riders contribute 1,757,698 trips. This distinction highlights the significant disparity in the usage patterns between the two rider categories. Please refer to the bar graph in appendix [A](#A.-Number-of-rides-by-rider-types) to further understand the disparity. 

#### Usage of different fleet by rider type

Data shows that members predominantly use electric and classic bikes, whereas casual riders exhibit a more diverse range of rideable type preferences, including docked bikes. This information provides valuable insights into the distinct preferences and behaviours of the two rider categories. Additionally, it is seen that docked bikes averages the highest ride time in the fleet for casual riders, followed by classical and electric bikes. 
Visualizations can be found in the appendices [B](#B.-Rides-with-different-bikes-for-member-types) and [C](C.-Average-ride-time-for-different-bikes-in-the-fleet-with-rider-types). 

#### Popularity of stations within rider categories

Analysis determines ideally the top four stations where rides initiate is by casual riders. Similarly, top five stations where rides conclude are also from casual riders. It reflects destination preferences with rider categories. The showcased stations can be indicated as leisure attractions in city of Chicago where casual riders commute to and from. 
Please refer to the appendices [D](#D.-Top-10-start-station-names-by-rider-type) and [E](#E.-Top-10-end-station-names-by-rider-types) for comparitive bar charts by rider types and popularity of the end and start stations.

#### Day of the week analysis

The data shades lights on ride distribution over the days of the week. Members tend to have more rides on weekdays, especially from Monday to Thursday, while casual riders show a preference for weekends. This finding shed light on the different usage patterns based on the day of the week. On the contrary, it was also seen casual riders banked a significantly more average ride time than members on each day of the week, with weekends recording highest (appendices [F](#F.-Rides-by-day-of-the-week)
and [G](#G.-Average-ride-times-by-day-of-the-week)).

#### Rides per month

There is a consistent and notable variation in ride counts across the months for members. The peak occurs in August, with 335,148 rides, and the trough in December, with 103,876 rides. Casual riders exhibit different patterns, with a gradual increase from January to May. The peak is observed in May, with 220,171 rides, followed by a slight decrease in subsequent months. Members maintain relatively stable average ride times throughout the year, with a slight decline from April to December. Casual riders show a distinctive pattern, with a noticeable increase in average ride times from January to May, reaching a peak in the month of May. Subsequently, there is a gradual decline in average ride times for casual riders. The observed fluctuations in average ride times indicate potential changes in user behaviour. For casual riders, longer average ride times in the spring and summer months may reflect a preference for extended leisure rides during pleasant weather (appendix [H](#H.-Number-of-rides-and-average-ride-time-per-month-by-rider-type)). 

### Recommendations

#### Seasonal Promotions

As seen in the analysis, demand rises over the months of April to October, and with June and July being the peak. Company can form seasonal promotions to boost casual riders join memberships and retain members during peak time. 

#### Weekend/ weekday membership campaigns

Similarly, to seasonal promotions, casual riders can be targeted with weekend only memberships. Company can also implement discounted rate strategies for weekdays to encourage user activity from Monday to Friday.  

#### Membership campaigns for different bike

Company requires to manage inventory by understanding the user preferences to increase and reduce inventory of different bike types to manage the demand. Additionally, low demand bikes such as electric bikes for casual riders or docked bikes with members can be promoted more to increase the usage.  

#### Collaboration with other businesses in the locality of popular stations

Taking into consideration the popularity of the stations for casual riders, company can manage more resources in these locations. The amount of traffic could indicate locations to leisure attractions of the city of Chicago. Company can collaborate with other businesses in the area and can advertise experience packages to gain more casual riders. 

### Appendices

#### A.	Number of rides by rider types

![Number of rides by rider types](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/4cead376-7b72-409c-93d4-7d32762a3920)

#### B.	Rides with different bikes for member types

![Pie Chart by rideable type](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/7928ad27-9c33-4287-b5e6-8ca5664494a7)

#### C.	Average ride time for different bikes in the fleet with rider types

![Average ride time for rideable types](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/4edabc50-74b1-4848-907d-a6a3dfeb572d)

#### D.	Top 10 start station names by rider type

![Top 10 start station names](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/6fbd9850-38d7-41a0-8fc8-fce851776c62)

#### E.	Top 10 end station names by rider types

![Top 10 end station names](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/8930d25d-c05c-49c8-890f-faa6aff252f3)

#### F.	Rides by day of the week

![Rides by day of the week](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/b33eaf5f-a71e-44f1-b454-4ee7a7973a79)

#### G.	Average ride times by day of the week

![Avg Ride Time ](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/32c01f9e-b441-42e2-87c1-617aa513f70d)

#### H.	Number of rides and average ride time per month by rider type

![Rides per month by member type](https://github.com/AdityaGhatnekar/Google-Data-Certificate-Capstone-Project/assets/128510160/db72c021-804d-4cc6-a391-093747492df0)

#### I. Data Preparation

```SELECT
  COUNT(ride_id) AS ride_id,
  COUNT(rideable_type) AS rideable_id,
  COUNT(started_at) AS started_at,
  COUNT(ended_at) AS ended_at,
  COUNT(start_station_id) AS start_station_id,
  COUNT(start_station_name) AS start_station_name,
  COUNT(end_station_id) AS end_station_id,
  COUNT(end_station_name) AS end_station_name,
  COUNT(member_casual) AS member_casual
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`

## all data variables count to 5667717 except start_station_id and start_station_name are 4834653 and end_station_id and end_sation_name 4774975 recorded

Select DISTINCT COUNT (ride_id) as total_rides
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`

## No duplicate ids

SELECT LENGTH(ride_id) AS ride_id_length
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
GROUP BY ride_id

## ride_ids all have 16 characters

SELECT rideable_type, COUNT (*) as number_of_rides
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
GROUP BY rideable_type 
ORDER BY number_of_rides

## 3 different bikes used docked (177474), classic (2601214) and electric (2889029)

SELECT COUNT (ride_id) AS rides_without_station_info
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
WHERE start_station_id IS NULL
  OR start_station_name is NULL
  OR end_station_id is NULL
  OR end_station_name is NULL

## 1298357 NULL values for start and end station info

SELECT member_casual, COUNT(*) AS total_rides
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
GROUP BY member_casual
ORDER BY total_rides

## 2 types of rides mumber and casual accounting to 3345685 and 2322032 respectively
```

#### J. Data Cleaning

```SELECT
ALTER TABLE `cyclists-case-study-400507.2022.Cyclist_2022_combined`
ADD COLUMN ride_time FLOAT64
 
# Added new column ride_length

UPDATE `cyclists-case-study-400507.2022.Cyclist_2022_combined`
SET ride_time = (
  TIMESTAMP_DIFF(ended_at, started_at, SECOND))
WHERE ride_id IS NOT NULL

SELECT ride_time
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
WHERE ride_time < 1

## 531 entries recorded 0 or in negative

SELECT ride_time
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
WHERE ride_time > 86400

## 5360 entries recorded with more than 86400 seconds of time difference between started_at and ended_at

ALTER TABLE `cyclists-case-study-400507.2022.Cyclist_2022_combined`
ADD COLUMN day_of_week STRING

UPDATE `cyclists-case-study-400507.2022.Cyclist_2022_combined`
SET day_of_week = 
    CASE EXTRACT(DAYOFWEEK FROM started_at) 
      WHEN 1 THEN 'SUNDAY'
      WHEN 2 THEN 'MONDAY'
      WHEN 3 THEN 'TUESDAY'
      WHEN 4 THEN 'WEDNESDAY'
      WHEN 5 THEN 'THURSDAY'
      WHEN 6 THEN 'FRIDAY'
      WHEN 7 THEN 'SATURDAY' 
      END   
WHERE ride_id IS NOT NULL

## Create a new table with cleaned data conditions

CREATE TABLE IF NOT EXISTS `cyclists-case-study-400507.2022.Cyclist_2022_cleaned` AS
SELECT ride_id, rideable_type, started_at, ended_at, ride_time, day_of_week, start_station_id, start_station_name, end_station_id, end_station_name, member_casual
FROM `cyclists-case-study-400507.2022.Cyclist_2022_combined`
WHERE start_station_id IS NOT NULL AND
start_station_name IS NOT NULL AND
end_station_id IS NOT NULL AND
end_station_name IS NOT NULL AND
ride_time > 1 AND ride_time < 86400

SELECT COUNT(*)
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`

## Total count 4368315, that is 1299402 removed
```

#### K. Data Analysis

```SELECT member_casual, COUNT(*) as total_trips
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY member_casual
ORDER BY total_trips

## Members have more rides than casual riders with 2610617 and 1757698 respectively

SELECT member_casual, rideable_type, COUNT(*) as Total_trips
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
Group By member_casual, rideable_type
ORDER BY member_casual, total_trips

## Members only use electric and classic bike, where as casual riders do ride with docked bikes as well

SELECT start_station_name, member_casual, COUNT(*) as total_trips
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY start_station_name, member_casual
ORDER BY total_trips DESC

## Top 4 stations to have highest amount of rides started at are from casual riders

SELECT end_station_name, member_casual, COUNT (*) AS total_trips
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY end_station_name, member_casual
ORDER BY total_trips DESC

## Top 5 stations to have highest amount of rides ended at are from causal riders

SELECT day_of_week, member_casual, COUNT (*) AS total_trips
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY day_of_week, member_casual
ORDER BY day_of_week

## Members have recorded more rides than casual riders on weekdays with Monday to Thursday recording a big surge, whereas casual riders have more rides on weekends

SELECT day_of_week, member_casual, AVG(ride_time) AS avg_ride_time -- Average in seconds
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY day_of_week, member_casual
ORDER BY avg_ride_time DESC

## Casual riders on an average have more ride_time on each day of week, with top 2 to be on the weekend

SELECT EXTRACT(HOUR FROM started_at) AS hour_of_the_day, member_casual, COUNT(ride_id) AS no_of_rides, AVG(ride_time) AS average_ride_time
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY hour_of_the_day, member_casual
ORDER by member_casual DESC, hour_of_the_day

SELECT EXTRACT(MONTH FROM started_at) AS monthly_rides, member_casual, COUNT(ride_id) AS no_of_rides, AVG(ride_time) AS average_ride_time
FROM `cyclists-case-study-400507.2022.Cyclist_2022_cleaned`
GROUP BY monthly_rides, member_casual
ORDER by member_casual DESC, monthly_rides
```







