# 2022 Cyclistic Case Study
## Table of Contents
1. [Introduction](README.md#introduction)
2. [Business Task](README.md#business-task)
3. [Data Processing](README.md#data-processing)
4. [Data Cleaning and Manipulation](README.md#data-cleaning-and-manipulation)
5. [Analysis and Visualiztions](README.md#analysis-and-visualizations)
6. [Summary and Business Recommendations](README.md#summary-and-business-recommendations)

## Introduction

The following is a Case Study prepared by Sean Francis for the fictional company Cyclistic. Cyclistic is a bicycle rideshare company based in Chicago, IL, but the actual data is pulled from the real rideshare company DIVVY. The case study looks at annual rideshare data collected in 2022 to answer questions posed by the marketing team, to assist in targeting their efforts for their upcoming digital marketing campaign.

## Business Task

The questions posed by the marketing team that this case study will be exploring are the following:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy a Cyclistic annual membership?
3. How can Cyclistic use digital media to influence casual riders to become members?

Casual riders are defined as rideshare customers who purchase one-off single rides or full-day rides with the Cyclistic service. Member riders are defined as customers who have purchased an annual membership with Cyclistic and can use the bikes as many times as they want within the calendar year of their membership. This case study will examine similarities, trends, and differences between these two groups, and make recommendations based on the findings to the marketing team. 
   
## Data Processing

#### Raw Data
All original DIVVY data was downloaded from this [source.](https://divvy-tripdata.s3.amazonaws.com/index.html) 

#### Data Licensing
The raw DIVVY data was made available under the following [license.](https://divvybikes.com/data-license-agreement)

#### Data Organization
Once the raw data was downloaded, I renamed the data files with a common date-based naming convention and stored the files locally on my computer to begin cleaning and manipulating the data. 

#### Issues with the Data
After taking an initial look at the data, I noticed two major items that I would normally follow up with the stakeholder to get further clarification on before proceeding with the analysis:

1. Much of the data had missing "start_station_name" or "end_station_name" column data. In these instances, the "stat_station_id" or "end_station_id" was also missing so there was no way to find the missing information with the data provided. In a real business situation, I would reach out to the stakeholders to see the reason this data was missing and if new data could be provided.
2. Many of the data rows listed the "bike_type" as a docked bike. To take a bike for a ride, the bike needs to leave the dock to begin a ride, so this led me to believe that the "docked bike" type may be an error with the data. The ride durations for bikes listed as "docked_bike" also ranged widely from 00:00 to up to 400+hrs. In a real business situation, I would reach out to the stakeholders to get further clarification on the meaning of a "docked bike" and move forward with the data accordingly. 

## Data Cleaning and Manipulation
To clean the data, I used Microsoft Excel and logged all my changes in a [change log.](https://github.com/franc136/2022_Cyclistic_Case_Study/blob/main/Case_Study_Rideshare_Change_Log.csv)

Major changes that were applied to all 12 data files include:
1. Removal of duplicate "ride_id" rows along with rows that did not include a unique "ride_id."
2. Added a "ride_duration" column with a formula ("ended_at" - "started_at" columns) to calculate the length of each ride. This new column was formatted as TIME, HH:MM:SS.
3. Added a "day_of_week" column to extract the day of the week from each ride.
4. The data was sorted by "ride_duration" and any ride with a duration of 00:00:00 was deleted.
5. According to DIVVY bike policy, any bike that is not docked after 24hrs is then classified as stolen. In the data, there were many rides over 24 hours, so I sorted the data by "ride_duration" and any row where the ride duration was greater than 23:59:00 was deleted.
6. The "started_at" column was separated and I created two new columns, "start_date" and "start_time."

## Analysis and Visualizations

All 12 cleaned monthly data files were uploaded to BigQuery where I used SQL to conduct all analysis. 

All SQL queries used in my analysis can be accessed [here.](https://github.com/franc136/2022_Cyclistic_Case_Study/blob/main/Rideshare_data_exploration_SQLcode) 

All visualizations were made using Microsoft Excel and Tableau.

### How Many Riders Were There?

#### Total Rides by Member Type

To help define the difference between member and casual riders, I first looked at total rides by each member type and found member riders made up the greater majority of total rides taken. 

![Total rides by member type](/Viz/Total_rides_by_member.png)

### How Long Were Riders Riding?

#### Average Ride Time

I next looked at how long each of the member groups was averaging their respective ride durations. Despite member riders taking more rides, I found that casual riders were taking much longer rides, which were averaging almost twice as long as member riders. 

![Average Ride in Min](/Viz/Avg_ride_min.png)

#### Most Popular Ride Durations by Member Type

To further explore how long each group was riding the Cyclistic bikes, I broke ride times into minute and hour segments and sorted each member group's rides into these segments. Though both groups took the majority of their rides in the 5-15min time segment, member riders took considerably more rides under 5min than casual riders. 

This data was also sorted by bike type used by each member group. When compared, the member riders used a considerably larger amount of electric bikes versus the casual riders.

![Member rides by time segment](/Viz/Member_rides_by_min_segment.png)

![Casual rides by time segment](/Viz/Casual_rides_by_min_segment.png)

### What Were Riders Riding?

#### Bike Type By Group
Looking at what type of bikes the two different groups were riding, you can see that member riders were pretty even in their rides on both classic and electric bikes. However, casual riders chose to ride the electric bikes more often than the classic option. Additionally, only casual riders tracked docked bikes in their data compared to members. As stated before, clarification on the validity of the docked bike data would need to be checked with the proper stakeholders. 

![Bike type by group](/Viz/Rides_by_bike_type.png)




## Summary and Business Recommendations


