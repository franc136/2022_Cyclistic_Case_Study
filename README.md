# 2022 Cyclistic Case Study
## Table of Contents
1. [Introduction](README.md#introduction)
2. [Business Task](README.md#business-task)
3. [Data Processing](README.md#data-processing)
4. [Data Cleaning & Manipulation](README.md#data-cleaning-&-manipulation)
5. [Analysis & Visualiztions](README.md#analysis-&-visualizations)
6. [Summary & Business Recommendations](README.md#summary-&-business-recommendations)

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

#### Data Liscensing
The raw DIVVY data was made available under the following [license.](https://divvybikes.com/data-license-agreement)

#### Data Organization
Once the raw data was downloaded, I reanamed the data files with a common date-based naming convention and stored the files locally on my computer to begin cleaning and minupulating the data. 

#### Issues with the Data
After taking an initial look at the data, I noticed two major items that I would normally follow-up with the stakeholder to get further clarification on before preceeding with the analysis:

1. Much of the data had missing "start_station_name" or "end_station_name" column data. In these instances, the "stat_station_id" or "end_station_id" was also missing so there was no way to find the missing information with the data provided. In a real business situation, I would reach out to the stakeholder to see the reason this data was missing and if new data could possibly be provided.
2. Many of the data rows listed the "bike_type" as a docked bike. In order to take a bike for a ride, the bike needs to leave the dock to begin a ride, so this led me to belive that the "docked bike" type may be an error with the data. The ride durations for bikes listed as "docked_bike" also ranged widely from 00:00 to up to 400+hrs. In a real business situation, I would reach out to the stakeholder to get further clarification on the meaning of a "docked bike" and move forward with the data accordingly. 

## Data Cleaning & Manipulation


## Analysis & Visualizations
## Summary & Business Recommendations

![Average Ride in Min](/Viz/Avg_ride_min.png)
