# 2022 Cyclistic Case Study
## Table of Contents
1. [Introduction](README.md#introduction)
2. [Business Task](README.md#business-task)
3. [Data Processing](README.md#data-processing)
4. [Data Cleaning and Manipulation](README.md#data-cleaning-and-manipulation)
5. [Analysis and Visualizations](README.md#analysis-and-visualizations)
6. [Summary and Business Recommendations](README.md#summary-and-business-recommendations)

## Introduction

The following is a case study prepared by Sean Francis for the fictional company Cyclistic. Cyclistic is a bicycle rideshare company based in Chicago, IL, but the actual data is pulled from the real rideshare company DIVVY. The case study looks at annual rideshare data collected in 2022 to answer questions posed by the marketing team, to assist in targeting their efforts for their upcoming digital marketing campaign.

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

1. Much of the data had missing "start_station_name" or "end_station_name" column data. In these instances, the "start_station_id" or "end_station_id" was also missing, so there was no way to find the missing information with the data provided. In a real business situation, I would reach out to the stakeholders to see the reason this data was missing and if new data could be provided.
2. Many of the data rows listed the "bike_type" as a docked bike. To take a bike for a ride, the bike needs to leave the dock to begin a ride, so this led me to believe that the "docked bike" type may be an error with the data. The ride durations for bikes listed as "docked_bike" also ranged widely from 00:00 to up to 400+hrs. In a real business situation, I would reach out to the stakeholders to get further clarification on the meaning of a "docked bike" and move forward with the data accordingly. 

## Data Cleaning and Manipulation
All changes that were made to the original raw data files are documented in my [change log.](https://github.com/franc136/2022_Cyclistic_Case_Study/blob/main/Case_Study_Rideshare_Change_Log.csv)

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

All visualizations were made using Tableau Public.

### How Many Riders Were There?

#### Total Rides by Rider Type

To help define the difference between member and casual riders, I first looked at total rides by each rider type and found member riders made up the greater majority of total rides taken. Of the 5,661,784 unique rides, member riders took about 20% more rides than casual riders.

![Total rides by member type](/Viz/Total_rides_by_member.png)

### How Long Were Riders Riding?

#### Average Ride Time

I next looked at how long each of the rider groups was averaging their respective ride durations. Despite member riders taking more rides, I found that casual riders were taking much longer rides, which were averaging almost twice as long as member riders. 

![Average Ride in Min](/Viz/Avg_ride_min.png)

#### Average Ride by Day of Week

Looking at the daily average ride times across both groups, it became clear that rides taken over the weekends were consistently longer than rides throughout the week. 

![Avg ride DOW](/Viz/DOW_rides_in_min.png)

#### Most Popular Ride Durations by Member Type

To further explore how long each group was riding the Cyclistic bikes, I broke ride times into minute and hour segments and sorted each rider group's rides into these segments. Though both groups took the majority of their rides in the 5-15min time segment, member riders took considerably more rides under 5min than casual riders. 

This data was also sorted by bike type used by each rider group. When compared, the member riders used a considerably larger amount of electric bikes versus the casual riders.

![Member rides by time segment](/Viz/Member_rides_by_min_segment.png)

![Casual rides by time segment](/Viz/Casual_rides_by_min_segment.png)

### What Were Riders Riding?

#### Bike Type By Group
Looking at what type of bikes the two different groups were riding, you can see that member riders were pretty even in their rides on both classic and electric bikes. However, casual riders chose to ride the electric bikes more often than the classic option. Additionally, only casual riders tracked docked bikes in their data compared to members. As stated before, clarification on the validity of the docked bike data would need to be checked with the proper stakeholders. 

![Bike type by group](/Viz/Rides_by_bike_type.png)

### When Were Riders Riding?

#### Rides Per Quarter

Next, I identified the most popular times that riders were taking out the bikes over the year. Focussing on rides by quarter, the most popular ride frequency occurred during Q2 and Q3, with a sharp drop in ridership during Q1 and Q4. Despite lower ride counts in Q1 and Q4, across the board, member riders outnumbered casual riders during the whole year. 

![Rides per quarter](/Viz/Rides_per_quarter.png)

#### Rides Per Month

Breaking down the most popular ride times further, I looked at the most popular rider months per group. The summer months of June and July were the most popular with casual riders, accounting for almost as many rides as member riders. Ridership across both groups was high from May to October, but per month, member riders still outrode casual riders in all months. 

![Rides per month](/Viz/Rides_per_month.png)

#### Rides Per Week

Focussing on weekdays versus weekends, I could see a stark difference between the two rider groups. Member riders have a much higher number of rides during the weekdays, whereas casual riders take more rides over the weekends. Saturdays were the only day of the week where casual riders outnumbered member rides, however, Sunday was about equal with both groups. 

![Rides per week](/Viz/Total_rides_DOW.png)

### Where Were Riders Leaving From?

#### Top 25 Start Stations

After looking at differences in time and bike type, I focussed on the geographical differences between rider groups, specifically from where they started their rides. Honing in on the top 25 start stations, you can notice that the casual riders' most popular stations tend to be near the lakeshore, popular tourist destinations (like Navy Pier or the Magnificient Mile (Michigan Ave.)), or in and around the Loop. In contrast, member riders' top stations were much more spread out across the city. 

![top 25 stations](/Viz/Top_25_Start_Stations.png)

Looking closer at downtown Chicago, as stated earlier, casual riders frequent more stations at popular tourist destinations like the beach (Dusable Lake Shore Dr. and North Blvd, Michigan Ave. and Oak St.) and Navy Pier (Streeter Dr. and Grand Ave..)

Popular member-rider stations that are near downtown, are not concentrated near tourist locations but at transportation and workplace hubs such as Union Station (Canal St. and Adams St.) and the Merchandise Mart (Kingsbury St. and Kinzie St..) Of the overall top 25 start stations, none of the popular member stations were located within the boundaries of the Loop. 

![top 25 loop](/Viz/Top_25_Start_Stations_loop.png)

Outside of downtown, popular stations that were furthest north (Lakeview neighborhood) and furthest south (Hyde Park neighborhood) were both popular member-rider stations, not casual riders.

![top 25 NS](/Viz/Top_25_Start_Stations_NS.png)

![top 25 Hyde Park](/Viz/Top_25_Start_Stations_HydePark.png)

#### Top 25 Start Stations Casual Members

As we saw with the overall top 25 stations, when the top 25 casual-rider stations were pulled, the trend of casual riders starting rides from locations near the lakeshore or popular tourist areas was consistent. 

![Top 25 casual](/Viz/Top_25_Start_Stations_CasualMembers.png)

![Top 25 casual loop](/Viz/Top_25_Start_Stations_Casual_Members_Loop_Detail.png)

#### Top 25 Start Stations Members

Also consistent with the overall top 25 stations, the top 25 member-rider stations were predominantly associated with transportation hubs like Ogilvey Transportation Center and Union Station (Clinton St. and Washington Blvd, Canal St. and Adams St.), in proximity to popular L-train stations (Clark St. and Division St. (Red Line), Wells St. stations in River North and Near North neighborhoods (Brown Line), and work/education hubs (Hyde Park stations (University of Chicago), Loomis St. and Lexington St. (University of Illinois at Chicago/Illinois Medical District), Kingsbury St. and Kinzie St. (Merchandise Mart).)

![Top 25 member](/Viz/Top_25_Start_Stations_Members.png)

![Top 25 member loop](/Viz/Top_25_Start_Stations_Members_Commuter_Detail.png)

## Summary and Business Recommendations

#### How are Member Riders and Casual Riders Different?

Member Riders:
1. Took more rides than casual riders, but on average, rode for shorter amounts of time.
2. Ride more often on weekdays and use electric and classic bikes consistently.
3. Took the bulk of their rides during the months of May-Oct.
4. Had the greatest number of rides taken from start stations near transportation hubs/lines and employment/education centers.

Casual Riders:
1. Took fewer rides than member riders, but on average, rode for longer amounts of time.
2. Ride more often on weekends and use electric bikes more frequently than classic bikes.
3. Took the bulk of their rides during the months of May-Oct, with very few in Q1 and Q4.
4. Had the greatest number of rides taken from start stations near the lakefront and tourist attractions.

#### Why Would a Casual Rider Buy an Annual Membership?

1. Since casual riders take longer rides but less frequently than members, one reason to purchase an annual membership would be to take more bike rides in Chicago cost-effectively.
2. With member riders often using the service associated with commuting, casual riders could benefit from purchasing an annual membership if they would like to start commuting to work via bicycle.
3. A casual rider would benefit from purchasing an annual membership if they would like to have greater access to transportation across more areas of the city when compared to classic modes of public transit (L-train and bus.)
4. Casual riders looking to exercise more often, would benefit from purchasing an annual membership by taking more bicycle trips and using electric bicycles less frequently. 

#### Digital Marketing Campaign Recommendations

1. With the bulk of casual riders, riding near the lakeshore/tourist locations, a digital campaign would need to target casual riders that either live in Chicago or near the city, as it is unlikely that a traveling tourist will buy an annual membership. To target these customers, Cyclistic could run geo-targeted ads focusing on the collar counties of Chicago where the bulk of the suburbs exist. Within the city of Chicago, digital outdoor advertising could be targeted along the lakeshore and at popular tourist attractions where the base of casual riders rent bicycles. Messaging for this campaign would focus on exploring other less popular but notable neighborhoods and destinations in Chicago, outside the scope of typical tourist locations. This would encourage suburban casual riders to visit the city more often and justify the cost of purchasing an annual membership by taking more rides. The same campaign messaging would also encourage Chicago resident casual riders to take more rides and provide a reason to upgrade their Cyclistic membership. 

2. A significant draw for casual riders to switch to an annual membership would be if they were looking to use a bicycle to commute to work. To target new bicycle commuters, Cyclistic could run a digital advertising campaign with digital outdoor advertising at bus shelters and L-train station platforms/display ads in L-cars. Messaging could focus on avoiding downtime waiting for transportation and emphasize the flexibility and freedom of commuting on one's own time via a bicycle.

3. To target seasonal dropoff casual riders, Cyclstic could run a digital campaign with seasonal membership promotions occurring in the spring and fall. Spring promotions would help to boost Q2 membership conversions before the peak ridership season, while time-sensitive year-end fall promotions could help kickstart membership sales for the following year.
