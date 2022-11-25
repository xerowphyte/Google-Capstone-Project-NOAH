# Googgle Data Capstone Porject - (Cyclistic Data)
I Noah Owootori finished this case study in November 2022 for the Google Data Analytics Professional Certificate capstone project. This case study was finished in R, and it was then published online through git.


Introduction
 
The main purpose of this study is to analyze well cleaned and processed data and get insights. These insights would enable the Cyclistic Executive team make data driven decisions as regards marketing strategies that would be aimed at converting casual riders into annual riders.
Background
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.
Scenario
“You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.”
Theories/Assumptions
•	Annual members are much more profitable than casual riders.
•	Based on the information provided, it would be easier to convert existing casual riders to annual members than on boarding new clients as annual members
Stakeholders
•	Cyclistic Executive Team
•	Cyclistic Marketing Analytics Team
•	Lili Moreno – Director of Marketing
Business task
To determine the differences in how both annual members and casual riders use Cyclistic bikes and to use the insights derived from this to determine best marketing strategies that would convert casual riders to annual members.
Data Source
The data used would cover rider information spanning a one-year period from January 2020 to January 2022.
The data has been made available by Motivate International Inc. with license, and is originally stored in separate CSV files organized by the different months of the year here!

Data Processing & Analysis
1.	Document description
This paper describes the processes taken to clean and modify Cyclistic's raw datasets in preparation for the next round of analysis. Only data acquired between August 2020 and July 2021 will be evaluated for the purposes of this case study. The dataset description is available here.
Please keep in mind that Cyclistic is a fictitious company. Motivate International Inc, the firm that manages the City of Chicago's Divvy bicycle sharing service, gathered raw data. This public dataset's license may be found here
library(tidyverse)
library(data.table)
.
2.	Combine Datasets
2.1	Load raw data
Aug_20 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202008-divvy-tripdata.csv")
Sep_20 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202009-divvy-tripdata.csv")
Oct_20 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202010-divvy-tripdata.csv")
Nov_20 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202011-divvy-tripdata.csv")
Dec_20 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202012-divvy-tripdata.csv")
Jan_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202101-divvy-tripdata.csv")
Feb_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202102-divvy-tripdata.csv")
Mar_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202103-divvy-tripdata.csv")
Apr_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202104-divvy-tripdata.csv")
May_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202105-divvy-tripdata.csv")
Jun_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202106-divvy-tripdata.csv")
Jul_21 <- read.csv("C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\Bike - Share Data\\202107-divvy-tripdata.csv")









2.2	Check the Data Structure
The structure summary outputs will assist in determining whether any of the individual raw datasets have distinct string types, column names, and so on.
str(Aug_20)
str(Sep_20)
str(Oct_20)
str(Nov_20)
str(Dec_20)
str(Jan_21)
str(Feb_21)
str(Mar_21)
str(Apr_21)
str(May_21)
str(Jun_21)
str(Jul_21)

2.3	Change String Types
The structure outputs revealed that the start_station_id and end_station_id columns in the Aug 20 through Nov 20 datasets were listed as 'int' string types rather than 'chr' string types. Before combining the raw datasets, all of their string types should be the same.
# Aug_20
Aug_20 <- mutate(
  Aug_20, 
  start_station_id = as.character(start_station_id),
  end_station_id = as.character(end_station_id)
  )

# Sep_20
Sep_20 <- mutate(
  Sep_20, 
  start_station_id = as.character(start_station_id),
  end_station_id = as.character(end_station_id)
  )

# Oct_20
Oct_20 <- mutate(
  Oct_20, 
  start_station_id = as.character(start_station_id),
  end_station_id = as.character(end_station_id)
  )

# Nov_20
Nov_20 <- mutate(
  Nov_20, 
  start_station_id = as.character(start_station_id),
  end_station_id = as.character(end_station_id)
  )

2.4	Merge Datasets
# Merge all 12 individual datasets into one 
all_trips <- bind_rows(
  Aug_20, Sep_20, Oct_20, Nov_20, Dec_20, 
  Jan_21, Feb_21, Mar_21, Apr_21, May_21, Jun_21, Jul_21
  )




3.	Prepare Datasets
3.1	Change date string types
# Change started_at string type 
all_trips$started_at <- as.POSIXct(
  all_trips$started_at, 
  format = "%Y-%m-%d %H:%M:%S"
  )

# Change ended_at string type 
all_trips$ended_at <- as.POSIXct(
  all_trips$ended_at, 
  format = "%Y-%m-%d %H:%M:%S"
  )

# Order by date 
all_trips <- all_trips %>%
  arrange(started_at)

3.2	Calculate ride length
Ride length as a number string type will be useful not just for future analysis but will also help to identify any incorrect data points, i.e. ride lengths less than 0.
# Calculate time difference in seconds 
all_trips$ride_length <- difftime(
  all_trips$ended_at, 
  all_trips$started_at,
  units = "secs"
  ) 

# Change string type to numeric 
all_trips$ride_length <- as.numeric(
  as.character(all_trips$ride_length)
  )

3.3	Summarize by date variables
Separate columns for the year, month, day of the week, and so on will be helpful for future analysis.
# Year 
all_trips$year <- format(
    all_trips$started_at, 
    "%Y"
    )

# Month 
all_trips$month <- format(
    all_trips$started_at, 
    "%m"
    )

# Week 
all_trips$week <- format(
  all_trips$started_at,
  "%W"
  )

# Day
all_trips$day <- format(
  all_trips$started_at, 
  "%d"
  )

# Day of week 
all_trips$day_of_week <- format(
  all_trips$started_at, 
  "%A"
  )

# Date, YYYY-MM-DD
all_trips$YMD <- format(
  all_trips$started_at, 
  "%Y-%m-%d"
  )

# Time of Day, HH:MM:SS
all_trips$ToD <- format(
  all_trips$started_at, 
  "%H:%M:%S"
  )

4.	Clean Dataset
4.1	Remove rows with ride length < 0
There were a few invalid data points with ride lengths less than 0, as identified in section 3.2. These information should be removed from the cleaned dataset.
# Remove ride lengths < 0
all_trips_cleaned <- all_trips %>%
  filter(!(ride_length < 0))

4.2	Remove incomplete rows
There were a few instances where no station names were reported. These missing data rows should be eliminated.
# Remove start_station_name and end_station_name blank results 
all_trips_cleaned <- all_trips_cleaned %>%
    filter(
      !(is.na(start_station_name) |
          start_station_name == "")
      ) %>% 
  
  filter(
    !(is.na(end_station_name) |
        end_station_name == "")
    )





4.3	Remove Tests
Further investigation of the all_trips_cleaned  dataset in the R console revealed a few station names that are completely capitalized text strings rather than adhering to the string type of opening capital letter followed by all lowercase characters. Furthermore, the capitalized station names looked to have the term 'TEST' within their string. The following code was used to investigate the observation that test rides have all capital letters as their  station_name:
# Create a data frame to check if capitalized station names are test rides 
capitalized_station_name_check <- all_trips_cleaned %>%
  
  filter(
    str_detect(start_station_name, "[:upper:]")
    & !str_detect(start_station_name,"[:lower:]")
    ) %>%
  
  group_by(
    start_station_name
    ) %>%
  
  count(
    start_station_name
    )
Further investigation of the discovered capitalized station name row outputs using the R console revealed that the results were for test and maintenance purposes. These findings should be removed from the dataset all_trips_cleaned.
# Remove capitalized station name results from the cleaned dataset 
all_trips_cleaned <- all_trips_cleaned %>%
    filter(
      !(str_detect(start_station_name, "[:upper:]")
        & !str_detect(start_station_name, "[:lower:]"))
      )


4.4	Remove Duplicates
Each ride has its own  ride_id column. This column should be checked to see if there are any duplicates that should be removed.
# Create a data frame to check that there are no duplicates 
ride_id_check <- all_trips_cleaned %>%
  count(ride_id) %>%
  filter(n > 1)

The above code yielded no results, and no duplicates were found in the cleansed dataset.


5.	Understand Dataset
5.1	Check Reliable Type
unique(all_trips_cleaned$rideable_type)

The code above returned three bike types from the cleaned dataset. The following code was run to see if a bike       type was later added to the dataset.

# Create a data frame to see when a unique bike type was added to the dataset
rideable_type_check <-all_trips_cleaned %>%
  
  mutate(
    year = year(started_at), 
    month = month(started_at)
    ) %>%
  
  group_by(
    month, 
    year
    ) %>%
  
  select(
    rideable_type, 
    month, 
    year
    ) %>%
  
  count(
    rideable_type
    )


The R console's rideable type check output revealed that  “classic_bikes”  were added to the dataset beginning in December 2020. This should be noted for future reference.















5.2	Check Station Name
Stations may have occasionally been added to or withdrawn from Cyclistic's portfolio. These lines of code can be used to review this:
First, a data frame listing the distinctive station names needs to be made.
# Create a data frame which lists the unique station names 
station_name_check <- all_trips_cleaned %>%
  group_by(start_station_name) %>%
  count(start_station_name) 

Following this, data frames which list the unique station names used each month should be created.
# Aug 2020 data frame which lists the unique station names used that month
Aug_2020_filter <- all_trips_cleaned %>%
  filter(
    month == "08"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Sep 2020 data frame which lists the unique station names used that month
Sep_2020_filter <- all_trips_cleaned %>%
  filter(
    month == "09"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Oct 2020 data frame which lists the unique station names used that month
Oct_2020_filter <- all_trips_cleaned %>%
  filter(
    month == "10"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Nov 2020 data frame which lists the unique station names used that month
Nov_2020_filter <- all_trips_cleaned %>%
  filter(
    month == "11"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Dec 2020 data frame which lists the unique station names used that month
Dec_2020_filter <- all_trips_cleaned %>%
  filter(
    month == "12"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Jan 2021 data frame which lists the unique station names used that month
Jan_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "01"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Feb 2021 data frame which lists the unique station names used that month
Feb_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "02"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Mar 2021 data frame which lists the unique station names used that month
Mar_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "03"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Apr 2021 data frame which lists the unique station names used that month
Apr_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "04"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# May 2021 data frame which lists the unique station names used that month
May_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "05"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Jun 2021 data frame which lists the unique station names used that month
Jun_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "06"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
    )

# Jul 2021 data frame which lists the unique station names used that month
Jul_2021_filter <- all_trips_cleaned %>%
  filter(
    month == "07"
    ) %>%
  group_by(
    start_station_name
    ) %>%
  count(
    start_station_name
               )
Each unique station name can be tested against the monthly filter data frames to assess which unique station was used in a particular month.
# Create columns for each month in the station name check data frame to check if the station name appears in the individual month filter data frames created earlier
station_name_check$Aug_2020 <- as.integer(station_name_check$start_station_name
                                          %in% Aug_2020_filter$start_station_name)

station_name_check$Sep_2020 <- as.integer(station_name_check$start_station_name 
                                          %in% Sep_2020_filter$start_station_name)

station_name_check$Oct_2020 <- as.integer(station_name_check$start_station_name 
                                          %in% Oct_2020_filter$start_station_name)

station_name_check$Nov_2020 <- as.integer(station_name_check$start_station_name 
                                          %in% Nov_2020_filter$start_station_name)

station_name_check$Dec_2020 <- as.integer(station_name_check$start_station_name 
                                          %in% Dec_2020_filter$start_station_name)

station_name_check$Jan_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Jan_2021_filter$start_station_name)

station_name_check$Feb_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Feb_2021_filter$start_station_name)

station_name_check$Mar_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Mar_2021_filter$start_station_name)

station_name_check$Apr_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Apr_2021_filter$start_station_name)

station_name_check$May_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% May_2021_filter$start_station_name)

station_name_check$Jun_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Jun_2021_filter$start_station_name)

station_name_check$Jul_2021 <- as.integer(station_name_check$start_station_name 
                                          %in% Jul_2021_filter$start_station_name)

# Add sum column 
station_name_check$count <- rowSums(station_name_check[,3:14])

When we filter the  station_name_check data frame by count <  12, it is possible to see which stations were not used in a given month as well as which stations were added and/or withdrawn from Cyclistic's portfolio between August 2020 and July 2021. The following two data frames were then created to review which stations were most likely added (check_A) or removed (check_B) from Cyclistic’s portfolio during the analysis period. To eliminate any anomalies when a station was just not used for the month rather than being totally removed or added to Cyclistic's portfolio, two months were used in each filter.
# Check A 
station_name_check_A <- station_name_check %>%
  filter(
    Aug_2020<1 & Sep_2020<1
    )

# Check B
station_name_check_B <- station_name_check %>%
  filter(
    Jul_2021<1 & Jun_2021<1
    )
The retrieved data frames revealed that Cyclistic's portfolio has had a few stations added or withdrawn. For instance, station_name_test_A revealed that from the month of July 2021 onward, Avenue L & 114th St was only used five times.
It should be highlighted for future analyses that a few stations were probably added to or withdrawn from Cyclistic's portfolio throughout the analysis period.





6.	Save the Dataset
6.1	Save the cleaned dataset
A csv file should be used to store the cleaned dataset.
C:\Users\Emmanuel O\Documents\Portfolio\R Programming\01\02
# Cleaned dataset
fwrite(
  all_trips, 
  "C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\02\\Analysis\\Final Analysis\\01-03-04 all_trips_cleaned.csv",
  col.names = TRUE, 
  row.names = FALSE
  )
		
		# Rideable type check dataset (section 5.1)
fwrite(
  rideable_type_check, 
  "C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\02\\Analysis\\01-03-05 rideable_type_check.csv",

  col.names = TRUE, 
  row.names = FALSE
  )

		# Station name check dataset (section 5.2)
fwrite(
 station_name_check, 
 "C:\\Users\\Emmanuel O\\Documents\\Portfolio\\R Programming\\01\\02\\Analysis\\01-03-06 station_name_check.csv",
  col.names = TRUE, 
  row.names = FALSE
  )

