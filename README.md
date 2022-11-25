# Googgle Data Capstone Porject - (Cyclistic Data)
I Noah Owootori finished this case study in November 2022 for the Google Data Analytics Professional Certificate capstone project. This case study was finished in R, and it was then published online through git.


##Introduction
 
 ![logo](data_viz/logo.jpeg)
 
The main purpose of this study is to analyze well cleaned and processed data and get insights. These insights would enable the Cyclistic Executive team make data driven decisions as regards marketing strategies that would be aimed at converting casual riders into annual riders.

##Background

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

##Scenario

“You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.”

##Theories/Assumptions

*	Annual members are much more profitable than casual riders.
*	Based on the information provided, it would be easier to convert existing casual riders to annual members than on boarding new clients as annual members

##Stakeholders

*	Cyclistic Executive Team
*	Cyclistic Marketing Analytics Team
*	Lili Moreno – Director of Marketing

##Business task

To determine the differences in how both annual members and casual riders use Cyclistic bikes and to use the insights derived from this to determine best marketing strategies that would convert casual riders to annual members.
Data Source
The data used would cover rider information spanning a one-year period from January 2020 to January 2022.
The data has been made available by Motivate International Inc. with license, and is originally stored in separate CSV files organized by the different months of the year here!

##Process

Cyclistic have provided historical trip data to be analysed. For the purpose of this analysis, only data between August 2020 and July 2021 will be assessed. The data has already been processed to remove trips that were below 60 seconds in length (potentially false starts or users trying to re-dock a bike to ensure it was secure). The license to use this dataset can be located here.

There are around 100,000 - 500,000 entries for each month saved under their own MS Excel CSV. Due to the large file sizes, R has been used to clean and process the large datasets. There is minimal human error and data bias since the primary, structured, historical data is taken from the bikes themselves. However, due to data privacy rules, there is no data relating to the type of user.

The data has been cleaned by way of merging all 12 datasets into one, deleting incomplete data elements, removing test station results, removing negative ride lengths and summarising the dataset by date and time variables. The full data cleaning process has been documented in “Data Cleaning Process”.

The data cleaning process highlighted that the “classic” bike type was added to Cyclistic’s portfolio from December 2020 onwards and that there are a few stations which have been added and/or removed from Cyclistic’s portfolio during the analysis time frame.

The cleaned dataset has been saved under the file name “all_trips_cleaned”.

##Analysis

#Most popular stations
![Plot Most Popular Stations](https://github.com/xerowphyte/github.io/blob/main/Data%20Viz/Rplot.png)

The interactive map shows that the Navy Pier and nearby coastline bike stations are the busiest, with Streeter Dr. & Grand Ave. being Cyclistic's busiest station with 64,998 trips. This supports Cyclistic's own estimate that most of its users ride bikes for recreation.

Despite the stations' extensive surface area, interaction with the map reveals that the southern stations are Cyclistic's least favored stations. This suggests that the bulk of cyclists utilize the bikes to travel between and within Chicago's central, touristy neighborhoods, as opposed to the small percentage of cyclists who commute to and from more residential regions.

##Most Popular Time of the Year
![Most Pop Time](https://github.com/xerowphyte/github.io/blob/main/Data%20Viz/Rplot01.png)

The heat map up top reveals that Cyclistic is most popular during the summer. The heat map also shows that the weekends are the busiest time of the week. Similar to section 3.1, this emphasizes that most riders are doing so for pleasure.

This dataset's statistical analysis revealed that Saturday, July 17, 2021, was Cyclistic's most popular date during the analysis period, with 31,877 journeys taking place in a single day. As a result of the COVID-19 pandemic, there will be more travel during the summer of 2021 than there was during the summer of 2020.

##Member Riders
![Member Riders](https://github.com/xerowphyte/github.io/blob/main/Data%20Viz/Rplot03.png)

Members utilize the Cyclistic service more frequently throughout the year, but casual riders typically only use the bike service on the weekends during the summer, according to the heat map segmented by member and non-member users.

With 12,448 trips on Saturday, August 29, 2020, it was the most popular day for member cyclists. It might be argued that member riders reached their peak in August 2020 as a result of not using their paid memberships while the stay at home order was in effect, following a protracted period of inactivity caused by the state of Illinois imposing a stay at home order in March 2020. This information contrasts sharply with that of casual riders, whose busiest day in 2021 was Saturday, July 17, with 20,269 trips.This might be because casual motorcyclists will feel more at ease visiting tourist locations in 2021 as opposed to 2020. It's interesting to note that while Saturday was the most popular day for casual riders, Wednesday was the most popular day for members. This would mean that, in contrast to casual users who use the service mostly for leisure, members use the Cyclistic service for their daily commute to work and other activities.

Most Popular Time of the Day
![Most Pop Time of Day](https://github.com/xerowphyte/github.io/blob/main/Data%20Viz/Rplot04.png)

The circular bar plot reveals that 5 pm is the busiest hour for cyclists, with 17:19:15 and 17:20:37 being the most frequent times for casual riders and members, respectively. It appears that many member riders are using the Cyclistic service for their daily commutes based on the sharp increase in member riders using the bikes at 8 am and later at approximately 5 pm.

Interestingly, between 9pm and 5am, non-members use the service more frequently than members do. This may indicate that infrequent users are forgoing cab rides home after a night out in favor of the bike share program. This is further evidenced by the fact that casual cyclists cycle on average at 15:11:59 while members often bike at 14:32:12. Casual riders typically cycle for 37.62 minutes, whereas members typically ride for 14.39 minutes. Again, this supports the claim that casual riders use bicycles for recreational purposes.

##Recommendations
According to the client brief, the marketing advice derived from this case study's findings should not be concentrated on luring new users to the Cyclistic bike service but rather on persuading casual users to upgrade to annual memberships.

The following are the three probable marketing suggestions for Cyclistic:

##A digital advertisement that depicts a resident of Chicago using a bicycle in daily life
We discovered that 5 pm was the most popular time of day for both casual and member riders. Although non-members use the bikes slightly more frequently than non-members in the late evening and early morning, the most popular time of day for non-members is still during the day, with a minor increase during commuting periods. This realization shows that there are occasional riders who use the Cyclistic service to get to work without paying a yearly membership fee. A digital campaign that helps Chicagoans to see how Cyclistic integrates into their daily lives would be advantageous to persuade casual riders to join. Additionally, this would contribute to dispelling the notion that Cyclistic is only a tourist service. Additionally, it will assist in spreading customer demand throughout the city rather than concentrating bike usage at Chicago's Navy Pier.

##Emails or notifications to remind casual riders to compare the cost-savings of annual memberships
Phone notifications and email reminders should be used to remind regular casual riders (likely Chicago locals) of the long-term pricing benefit from investing in an annual membership rather than purchasing regular casual trips, similar to the insight noted in recommendation 1. This will encourage them to choose an annual membership rather than regularly purchasing casual trips with Cyclistic.

##Digital advertisement highlighting the advantages of cycling in post-COVID-19 society
Following the COVID-19 Illinois stay at home order, more members are using the bike service, according to the member riders' discussion. Cyclistic might take advantage of this understanding by emphasizing the advantages of riding bicycles outside as opposed to in a car with other people or inside a stuffy gym.
