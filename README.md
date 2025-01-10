# Cyclistic-Case-Study
 Case Study: How does a Bike-Share Navigate Speedy Success?

Adebola Peter Balogun
2024-12-19

Background
Cyclistic Bike-Share is a fictional and flexible ride-share company with three (3) types of bikes – namely docked, electric and classical - that are available for riders to pick up from one of their 600 docking stations. Undocked bikes may be returned to any of the 600 stations. In addition to being an inclusive company offering bike rides to disabled customers, Cyclistic has over 5800 bicycles for its two types of clienteles: casual riders who purchase single-ride or day tickets and full members with annual memberships.  



Ask

Business Plan: The future growth of Cyclistic Bike-Share hinges on maximizing its number of annual memberships in the Bike-Share company. Although, the plan is to convert casual membership to annual members, the team task is to first understand how annual members and casual members use Cyclistic bikes differently.
Stakeholders in this report:
Cyclistic Executive Team
Director of Marketing - Lily Moreno
Cyclistic’s Marketing Analytics Team



Prepare

Cyclistic Bike-Share public data source is available at Index of “divvy-tripdata”. The data is under the  License Agreement between Bikeshare and the City of Chicago. For this Case Study, I have chosen to use the 2023 January to December Cyclistic trip data for this analysis.
Although the company Cyclistic Bike-Share is fictional, I am still obligated to ensure that the 2023 dataset I have chosen for this study ROCCCs. Data that ROCCS is reliable, original, comprehensive, is current and also well-cited. 

Cyclistic’s Data Structure

The comma-delimited (.csv) files I downloaded have 15 columns that include the following: ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng, and member_casual.
While prepping the data, I needed to join all the .csv files together. I have chosen to use SQL Server queries for this step. Doing this within RStudio requires the rodbc package!
I prepared the 2023 .CSV files by creating a database called “Cyclistic Bike-Share”. I imported all 12 .CSV files and merged them into a table named “Cyclistic_Bike-Share_2023”. While importing the flat files into SQLEXPRESS, I verified and changed the datatypes of the following columns: ride_id(nvarchar(50)), rideable_type(nvarchar(50)), started_at(datetime2), ended_at(datetime2), start_station_name(varchar(MAX)), end_station_name(varchar(MAX)), member_casual(nvarchar(50)).



Process

Again, I started this phase of the Study using SQL Statements. I needed to identify and remove NULL Values from the table I created from the Prepare Phase - Cyclistic_Bike-Share_2023.
I wanted to keep the table created from the merged 12 flat (.csv) files intact. Therefore, I created a copy of that table, and from that copy, I deleted the NULL Values. The result showed 1387808 rows contained NULL Values. There was also the need to verify and remove duplicate records. But I found no duplicate records in the 2023 files.



Analyze

The first 3 Phases of this analysis were completed using Microsoft SQLEXPRESS - SQL Server 15.0.2130. Now it is time to continue the next phase in RStudio. I use the Desktop Version of RStudio 2024.12.0+467 “Kousa Dogwood” Release (cf37a3e5488c937207f992226d255be71f5e3f41, 2024-12-11) for windows.
I have chosen to continue this exercise in the stable environment that RStudio offers and to take advantage of R Markdown in sharing my analysis to the Stakeholders. RStudio also provides a functionality for database connectivity. 
In this phase, I need to aggregate the 2023 trip data, make calculations that help identify what trends and relationships the cleaned data presents. In order to analyze the 2023 ride-share data, I have to connect to SQLEXPRESS by opening an RODBC channel, as well as set default choices for RStudio. Thus, all required R packages like tidyverse, ggplot2, RODBC, lubridate, dplyr, tidyr, and readr were installed and loaded.

Summary of the table


![image](https://github.com/user-attachments/assets/1408b24b-02ab-4fc2-a8a0-053c7731e074)


Verifying Column Names

![image](https://github.com/user-attachments/assets/f77ff38f-73b0-4870-addc-cd229049b532)

Structure of the table

![image](https://github.com/user-attachments/assets/08a35b0d-be12-4cf9-b7f9-4261f996f731)

I also verified that there were just the two user types that will be considered in this case study. This information indicates that there were over 2.8 million trips by full members in the year in review, while casual trips numbers were slightly above 1.5 million trips. 


![image](https://github.com/user-attachments/assets/bbf2e4ac-d89c-4cd1-a9fd-8db18ab1276a)



In order to properly aggregate ride-share data, I needed analyze the date stamps for the rides according to their dates and time (https://sparkbyexamples.com/r-programming/dates-and-times-in-r/), and format the calculated "ride length" using the difftime() ](https://docs.google.com/document/d/1TzCqk59_J23D5zNCvwAPSgK-5osp-wVnifsc-VOpCaI/template/preview)

Aggregation of Cyclistic's 2023 Ride Data

![image](https://github.com/user-attachments/assets/6270f15d-1fca-41fb-9797-02ff37eaee24)


The next stage aggregates the numbers of members and casual riders. Averagely, casual members spend more time on each trip compared to full members. The difference in time is almost 10 minutes averagely per ride. The median ride length also showed casual riders with the larger ride length of over 12 minutes per ride compared with the 8.6 minutes of full members.


![image](https://github.com/user-attachments/assets/c85aa761-fa0e-4b10-a288-64435028ea7d)


Weekly ride summary were ordered by customer type in order to have an idea how the weekly and monthly numbers compare between the customer types. The numbers show that casual users spend more time averagely on their ride and the most preferred day for spending time on the bikes is Sundays. The second-best day of the week is Saturdays.

Numbers by days of the week for each User Type


![image](https://github.com/user-attachments/assets/3e1d9e24-cf11-463d-ba74-53f79fa03508)



Monthly numbers for the year 2023


![image](https://github.com/user-attachments/assets/0b1ac04f-e59f-49d9-a8d7-0ecaa690dd4c)


Riders spend more leisure time on the bikes during the warmer months of May, June, July, August and September. We can see the numbers go down drastically in the colder months of the year. 


Mean, Max and Median Numbers

Furthers distinctions were calculated to reveal the monthly mean, max, and median numbers by the rider types.


Average Trips Ordered by Months


![image](https://github.com/user-attachments/assets/c21a2cf4-a84b-4939-b8c2-498cf2fdfeb6)


Max Trips Ordered by Months


![image](https://github.com/user-attachments/assets/f347bb2f-545a-4a1a-a36e-57a6e7beb9c0)


Median Trips Ordered by Months


![image](https://github.com/user-attachments/assets/ad8fd694-e221-4c06-91b9-5ec954ccd809)



The Busiest Stations

The analysis proceeds further to determining the busiest docking stations for the year.  




![image](https://github.com/user-attachments/assets/1af7b3b7-65cd-4c24-a3b0-ba4cf6b05289)



![image](https://github.com/user-attachments/assets/31cc9552-b4c8-43f3-84a2-e3b4d85301df)


Above we see the top ten (10) locations in the list for both the pickup and return of the bikes. It appears that majority of casual riders prefer a specific location (Streeter Dr & Grand Ave) to pick up and return their bikes.


Share

The astute RStudio visualizations below present my findings for this study.



![image](https://github.com/user-attachments/assets/ddcaf237-195d-4584-bed0-113edbbcb61a)


The graph above shows that casual users are most active during the weekends. Their rides are usually for leisure. Members started off very strong from the weekend and grow steadily during the week while choosing Stylistic's bikes as a means of transportation. Usage rises above 400,000 between Tuesday and Friday and taper off over the weekend with the weekend usage dropping to above 300,000 rides. For casual customers, they start slowly during the week and then see their usage increase also steadily from slightly below 200,000 rides on Mondays and Tuesdays to above 200,000 by Friday. Usage then rises above 300,000 rides during the weekend.

Moreover, the trend is also showing that casual members spend averagely more time (about 10 more minutes) on the bikes than annual members do:


![image](https://github.com/user-attachments/assets/3f4f7648-aea0-4076-832c-c913ca3251d8)



![image](https://github.com/user-attachments/assets/c4584a76-640a-4cf1-9450-f19b82aed047)


Monthly ride stats show casual riders with longer average ride shares all year round. The month of July recorded the largest average number of rides followed by the month May. [Statista.com](https://www.statista.com/statistics/1316398/top-summer-travel-months-us/) indicates that the leading months that people travel in the USA fall between the months of May and September. The 2023 bike ride shares in those months by both casual and full members speak to the seasonal nature of bike rides.


![image](https://github.com/user-attachments/assets/1526c1da-a9d5-476f-9946-66b0c2f41ce4)


This visualization showed us that casual members spent on average 27 minutes per ride while members spent on average 13 minutes each ride.



![image](https://github.com/user-attachments/assets/2895ad5a-bd7d-4235-b392-558d3bafeef5)



![image](https://github.com/user-attachments/assets/b4fe7b26-ba71-403d-9ff5-a5825b88adb6)


In both the Weekly and monthly graphs, Casual riders consistently have the longer rides on the bikes, especially during the warmer months.



Act


Observations


1.	Casual members spend averagely 27.1 minutes per ride. Members spend 14 minutes averagely per ride.
2.	Out of a total 4,332,003 members recorded by Cyclistic in the year 2023, members make 65% (or 2800098). While casual riders make 35% (or 1531905).
3.	Major reason casual riders use Stylistic’s bikes is for leisure and do so majorly during the summer or warmer season.


Recommendations


Cyclistic Bike-Share should launch a marketing campaign targeted at casual users:

1.	The fact that casual users are recreational riders, the company should consider a thoughtful and strategic summer campaign that is family-friendly. Including investing in cargo bikes that can carry between 2 and 5 riders at the same time. 
2.	Develop campaign offerings that benefit seasonal memberships. The membership can be renewable every first month of the seasonal months (April or May) unless the member cancels the commitment.
3.	Design a reward program for the busiest stations. The incentive program could provide membership discounts for new members, coffee, meal coupons and charity donations for the (top 20) busiest stations.



Conclusion

In the process of this case study, I consulted a number of sources that have contributed to largely to completing the work. The following refences were consulted:

Data License Agreement. https://divvybikes.com/data-license-agreement
Dates and Times in R with Examples. https://sparkbyexamples.com/r-programming/dates-and-times-in-r/
Divvy Exercise R Script. https://docs.google.com/document/d/1TzCqk59_J23D5zNCvwAPSgK-5osp-wVnifsc-VOpCaI/template/preview
Statista.com. Leading months adults plan to travel on vacation in summer in the United States as of March 2022. https://www.statista.com/statistics/1316398/top-summer-travel-months-us/
Wickham, H. 2009. Ggplot2. Elegant Graphics for Data Analysis. Springer.

