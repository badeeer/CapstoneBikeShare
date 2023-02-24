Case Study: How Does a Bike-Share Navigate Speedy Success?
============================================================

## introduction 
This is a case study about the **Cyclistic bike-share analysis**, in this case, I will be analyzed by following the steps of **the data analysis process: ask, prepare, process, analyze, share, and act**.

### About the Company
In 2016, **Cyclistic** launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system at any time.

### Business task:
Analyze the Cyclistic data set for one year to understand how annual members and casual riders use Cyclistic bikes differently.

### Stakeholders:

**Lily Moreno**: The director of marketing. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program.
**Cyclistic marketing analytics team: ** A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy.
**Cyclistic executive team**: The executive team will decide whether to approve the recommended marketing program.

### Deliverables:

> - A description of all data sources used
> - Documentation of any cleaning or manipulation of data
> - A summary of the analysis
> - Supporting visualizations and key findings
> - Top three to four recommendations based on the analysis

## STEP ONE: **ASK**
**Lily Moreno**(The director of marketing and my manager) has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. To do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends by asking three questions that will guide the future marketing program:

**1.** How do annual members and casual riders use Cyclistic bikes differently?

**2.** Why would casual riders buy Cyclistic annual memberships?

**3.** How can Cyclistic use digital media to influence casual riders to become members?

**Moreno** has assigned you the first question to answer: **How do annual members and casual riders use Cyclistic bikes differently?**, to answer this question I should prepare data by collecting it from a trusted source.

## STEP TWO: PREPARE
the raw data is located in [here](https://divvy-tripdata.s3.amazonaws.com/index.html), and it is publicly available under this [license](https://ride.divvybikes.com/data-license-agreement) with some privacy restriction.


**ROCCC data**

> - **Reliable**: this dataset is complete, accurate and it is from a trusted source

> - **Original:** the data collected from the first part means it is Original 

> - **Comprehensive:** the data contain information that we need to do the analysis

> -  **Current:** I choose the period from September 2021 to August 2022 

> - **Cited:** the data is [here](https://divvy-tripdata.s3.amazonaws.com/index.html)

before downloading the raw data we need to install some dependencies

***install the libraries***

```
install.packages("tidyverse")
install.packages("dplyr")
install.packages("janitor")
install.packages("skimr")
install.packages("ggplot2")
install.packages("lubridate")
install.packages("tibble")
install.packages("rmarkdown")
install.packahes("viridis")

```



1. tidyverse: a core system of packages for data manipulation, visualization, and other things. To see more visit the following link  [https://www.tidyverse.org/](https://www.tidyverse.org/)

2. dplyr: is a library about data manipulation, providing a consistent set of verbs that help you solve the most common data manipulation challenges. For more info you can [https://dplyr.tidyverse.org/](https://dplyr.tidyverse.org/)

3. Janitor: is a simple library for cleaning dirty data, you can read more about it in this source, [janitor documentation](https://rdocumentation.org/packages/janitor/versions/2.1.0)

4. skimr: is a comprehensive statistic summary for a data frame, for more [skimr](https://cran.r-project.org/web/packages/skimr/vignettes/skimr.html)

5. ggplot2: is a data visualization library, that visually provides a more flexible show. more of it check this link [https://ggplot2.tidyverse.org/](https://ggplot2.tidyverse.org/)

6. lubridate: is a date-time library dealing with formats and separators to handle the changing time zone. See this link [https://lubridate.tidyverse.org/](https://lubridate.tidyverse.org/)

7. Tibble: is a modern data frame that is lazy and surly: they do less, check this useful documents [https://tibble.tidyverse.org/](https://tibble.tidyverse.org/)

8. markdown: is a library that provides your analyses into high-quality documents, again and last see this source  [https://rmarkdown.rstudio.com/](https://rmarkdown.rstudio.com/)

***load the libraries***

```{r library}

library(tidyverse)
library(dplyr) 
library(janitor) 
library(skimr) 
library(ggplot2) 
library(lubridate) 
library(tibble)
library(rmarkdown)

```


***then, I download the dataset that are from September 2021 to August 2022***



```{r}

df_01 <- read_csv("dataset/divvy-tripdata_202109.csv") 
df_02 <- read_csv("dataset/divvy-tripdata_202110.csv")
df_03 <- read_csv("dataset/divvy-tripdata_202111.csv")
df_04 <- read_csv("dataset/divvy-tripdata_202112.csv")
df_05 <- read_csv("dataset/divvy-tripdata_202201.csv")
df_06 <- read_csv("dataset/divvy-tripdata_202202.csv")
df_07 <- read_csv("dataset/divvy-tripdata_202203.csv")
df_08 <- read_csv("dataset/divvy-tripdata_202204.csv")
df_09 <- read_csv("dataset/divvy-tripdata_202205.csv")
df_10 <- read_csv("dataset/divvy-tripdata_202206.csv")
df_11 <- read_csv("dataset/divvy-tripdata_202207.csv")
df_12 <- read_csv("dataset/divvy-tripdata_202208.csv")

```


But before the check for missing values and duplication, I will check every dataset for consistency because I need to combine data into one.

1. see if we have the same columns **(colnames)** in all datasets

```{r}

#df_01
colnames(df_01)
#df_02
colnames(df_02) 
#df_03
colnames(df_03)
#df_04
colnames(df_04)
#df_05
colnames(df_05)
#df_06
colnames(df_06)
#df_07
colnames(df_07)
#df08
colnames(df_08)
#df_09
colnames(df_09)
#df_10
colnames(df_10)
#df_11
colnames(df_11)
#df_12
colnames(df_12)

```

2. A Structure of each dataset, we want to see each column and it's a datatype

```{r}

str(df_01)
str(df_02)
str(df_03)
str(df_04)
str(df_05)
str(df_06)
str(df_07)
str(df_08)
str(df_09)
str(df_10)
str(df_11)
str(df_12)

```

All dataset have the same columns ***(ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_id, start_lat, start_lng, end_lat, end_lng, member_casual)***,  I didn't to rename some dataset's becaue they have same columns name

#STEP THREE: PROCESSING 
before combining all datasets into one, first clean every dataset by the filter's out the duplicated value and looking for missing numeric values, then we can combine all datasets into one after that, I will add more columns that beneficial to my analysis.

1- Find the duplicated value

```{r}

sum(duplicated(df_01$ride_id))
sum(duplicated(df_02$ride_id))
sum(duplicated(df_03$ride_id))
sum(duplicated(df_04$ride_id))
sum(duplicated(df_05$ride_id))
sum(duplicated(df_06$ride_id))
sum(duplicated(df_07$ride_id))
sum(duplicated(df_08$ride_id))
sum(duplicated(df_09$ride_id))
sum(duplicated(df_10$ride_id))
sum(duplicated(df_11$ride_id))
sum(duplicated(df_12$ride_id))

```

-as you can see there's no duplication in ride_id, so now let's keep forward and deal with the missing value

2- check if there is a missing value.

> - df_01: there is six columns that have missing value, and this columns is **start_station_name, end_station_name, start_station_id, end_station_id, end_lat, end_lng**.
here is the table showing the percentage of all missing values by each value.

-missing values for df_01
```
  
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |    12.31%        |       87.69%         |
  | End_station_name   |    13.13%        |       87.86%         |
  | Start_station_id   |    12.31%        |       87.69%         |
  | End_station_id     |    13.13%        |       86.87%         |
  | End_lat            |    0.08%         |       99.92%         |               
  | End_lng            |    0.08%         |       99.92%         |
```

  -missing value for df_02
```
  
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |   17.14%         |      82.86%          |
  | End_station_name   |   18.2%          |      81.8%           |
  | Start_station_id   |   17.14%         |      82.86%          |
  | End_station_id     |   18.2%          |      82.86%          |
  | End_lat            |   0.08%          |     99.92%           |               
  | End_lng            |   0.08%          |     99.92%           |
```

  -missing value for df_03
```
  
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |     21%          |        79%           |
  | End_station_name   |     22%          |        78%           |
  | Start_station_id   |     21%          |        79%           |
  | End_station_id     |     22%          |        78%           |
  | End_lat            |     0.05%        |       99.95%         |               
  | End_lng            |     0.05%        |       99.95%         |
```

  -missing value for df_04
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      21%         |       79%            |
  | End_station_name   |      22%         |       78%            |
  | Start_station_id   |      21%         |       79%            |
  | End_station_id     |      22%         |       78%            |
  | End_lat            |      0.06%       |       99.94%         |               
  | End_lng            |      0.06%       |       99.94%         |
```

  -missing value for df_05
  
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      16%         |       84%            |
  | End_station_name   |      17%         |       83%            |
  | Start_station_id   |      16%         |       84%            |
  | End_station_id     |      17%         |       83%            |
  | End_lat            |      0.08%       |       99.92%         |
  | End_lng            |      0.08%       |       99.92%         |
```

  -missing value for df_06
  
``` 
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      16%         |        84%           |
  | End_station_name   |      18%         |        82%           |
  | Start_station_id   |      16%         |        84%           |
  | End_station_id     |      18%         |        82%           |
  | End_lat            |      0.07%       |        99.93%        |
  | End_lng            |      0.07%       |        99.93%        |
```

  -missing value for df_07
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |     17%          |        83%           |
  | End_station_name   |     18%          |        82%           |
  | Start_station_id   |     17%          |        83%           |
  | End_station_id     |     18%          |        82%           |
  | End_lat            |     0.09%        |        99.91%        |
  | End_lng            |     0.09%        |        99.91%        |
```  
  -missing value for df_08
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      19%         |         81%          |
  | End_station_name   |      20%         |         80%          |
  | Start_station_id   |      19%         |         81%          |
  | End_station_id     |      20%         |         80%          |
  | End_lat            |      0.09%       |         99.91%       |
  | End_lng            |      0.09%       |         99.91%       |
```
  -missing value for df_09
  
``` 
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      14%         |       86%            |
  | End_station_name   |      15%         |       85%            |
  | Start_station_id   |      14%         |       86%            |
  | End_station_id     |      15%         |       85%            |
  | End_lat            |      0.1%        |       99.9%          |
  | End_lng            |      0.1%        |       99.9%          |
``` 
  -missing value for df_10
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      12%         |      88%             |
  | End_station_name   |      13%         |      87%             |
  | Start_station_id   |      12%         |      88%             |
  | End_station_id     |      13%         |      87%             |
  | End_lat            |      0.14%       |      99.86%          |
  | End_lng            |      0.14%       |      99.86%          |
```  
  -missing value for df_11
```
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |      14%         |      86%             |
  | End_station_name   |      15%         |      85%             |
  | Start_station_id   |      14%         |      86%             |
  | End_station_id     |      15%         |      85%             |
  | End_lat            |      0.1%        |      99.9%           |
  | End_lng            |      0.1%        |      99.9%           |
```  
   -missing value for df_12
```  
  |   Columns          | Missing value by | Not missing value by |
  |                    |  Percentage %    |   Percentage %       |
  | ------------------ | ------------     |--------------------- |
  | Start_station_name |     14%          |       86%            |
  | End_station_name   |     15%          |       85%            |
  | Start_station_id   |     14%          |       86%            |
  | End_station_id     |     15%          |       85%            |
  | End_lat            |     0.1%         |       99.9%          |
  | End_lng            |     0.1%         |       99.9%          |
```  
3- Combine all the df's into one

```{r}
df <- bind_rows(df_01, df_02, df_03, df_04, df_05, df_06,
                df_07, df_08, df_09, df_10, df_11, df_12)

```

4- Because I have computational limitation I created a sample size that represents the population size.

> - Population size: 5,883,043
> - Confidence level: 99%
> - Margin of error: 0.5%
> - Sample size: 65,820

```{r}

sample_df <- sample_n(df, 65820, replace= TRUE)

sample_df <- write_csv(sample_df, "sample_df.csv")

```


5- Add more columns by converting the started_at to date and splitting the day, month, year, and day of the week.

```{r}
# Add  more columns that list the date, month, day, and year of each ride
sample_df$date <- as.Date(sample_df$started_at) #The default format is yyyy-mm-dd
sample_df$month <- format(as.Date(sample_df$date), "%m")
sample_df$day <- format(as.Date(sample_df$date), "%d")
sample_df$year <- format(as.Date(sample_df$date), "%Y")
sample_df$day_of_week <- format(as.Date(sample_df$date), "%A")
head(sample_df)
str(sample_df)

```

6- Add another column to ride_length by calculating the difference between ended_at and started_at, convert the datatype of ride_length, and than check if ride_length is numeric.

```{r}
sample_df <- sample_df %>% 
  mutate(ride_length = ended_at - started_at)

head(sample_df$ride_length)
str(sample_df$ride_length)
```

- convert to numeric 

```{r}

sample_df$ride_length <- as.numeric(sample_df$ride_length)
```

7- Check for error's in ride_length (in seconds), the ride_length must be greater or equal to 0

```{r}

#remove bad data
sample_df_v2 <- sample_df[!(sample_df$ride_length<0),]

#error's in ride_length 
sum(sample_df_v2$ride_length < 0)

```

8 -  let's see if more then casual and member in casual_member, and I doing some calculation.

```{r}
table(sample_df$member_casual)

sample_df %>% 
    group_by(member_casual) %>% 
    summarise(total = length(ride_length),
              'percentage' = (length(ride_length) / nrow(sample_df_v2)) * 100)
              
```

9- Create a new version that is cleaning and processed

```{r}

write_csv(sample_df, "sample_df_v2.csv")

```

After this long step of processing data, now I can do the analysis step

**STEP FOUR: ANALYSIS**

-Before jumping to the analysis, we must read the new version(sample_df) that we created in the chunk above, and then convert it to the tibble data frame because it is easier than the classic data frame, and take a  glimpse of seen a summary (skim_without_charts) and the structure (str) of the new version, the columns must be 19, and the rows must be 65,820

```{r}

sample_df_v2 <- read_csv("sample_df_v2.csv")
# using tibble 
as_tibble(sample_df_v2)

#summary
skim_without_charts(sample_df_v2)
#str 
str(sample_df_v2)
#number of rows
nrow(sample_df_v2)
#number of columns 
ncol(sample_df_v2)

```



-As mentioned before the member (58%) have a greater portion than casual (42%), this result give us a sense of the comparison between the member and casual, cannot be equally and we can do more comparison by taking the average(mean,  median), min,and a max of ride_length  of each member and casual, than comparing it by each day

```{r}

# Compare members and casual users
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = mean)
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = median)
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = max)
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = min)
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = sd)
aggregate(sample_df_v2$ride_length ~ sample_df_v2$member_casual, FUN = sum)

```

-**FINDING (1)**
-In general, before diving in you can see in the tables above the casual have great (mean, max) values, and they also varied (standard deviation) than members even if the sum of the member greater than casual, maybe this is because there are a few users (42%) using the bike's for a long ride but they are not a member.

```{r}
sample_df_v2 %>% 
  group_by(member_casual) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length), sum_ride_length = sum(ride_length)) %>% 
  arrange(member_casual)

```

-**FINDING (2)**
- > here in the table above we can take an intuition about why the mean of casual is greater than member but the number of rides is way less than that of the member, that's because the ride length sum of casual(44517203) is greater of the ride sum of member(29342886). conversely, the length of rides of casual is less than the ride length of the member, this explains why the mean of the casual ride is greater than that of member.

**chart(1)**
-the sum of each member and casual 

```{r}
sample_df_v2 %>% 
  group_by(member_casual) %>% 
  summarise(number_of_rides = n()) %>% 
  arrange(member_casual) %>% 
  ggplot(aes(member_casual, number_of_rides, fill=member_casual)) +
    geom_col(position="dodge") 
```

-**FINDING (3)**
- > As you can see in chart(1)  above, the number of members is more than the number of casual, this is because ~58% use bikes as member.


**chart(2)**
- the mean of ride length of each member and casual 
- 
```{r}
sample_df_v2 %>% 
  group_by(member_casual) %>% 
  summarise(average_ride_length= mean(ride_length)) %>% 
  arrange(member_casual) %>% 
  ggplot(aes(x = member_casual, y = average_ride_length, fill = member_casual)) +
  geom_col(position = "dodge") + ggtitle("The mean of ride length of each member and casual")

```

-**FINDING (4)**
- > In chart(2), the mean ride length of the casual is up to 1500, while the member didn't reach 1000.

**chart(3)**
-the sum of ride length of each member and casual

```{r}

sample_df_v2 %>% 
  group_by(member_casual) %>% 
  summarise(total_ride_length= sum(ride_length)) %>% 
  arrange(member_casual) %>% 
  ggplot(aes(x = member_casual, y = total_ride_length, fill = member_casual)) +
  geom_col(position = "dodge") + ggtitle("The mean of ride length of each member and casual")

```

-**FINDING (5)**
-> the sum of ride length in chart(3) above, of the casual, is more than the member, and with less casual users who use bikes effect the mean.

-Now  let's see the number of ride length in member and casual at hours

```{r}

sample_df_v2 %>% 
  mutate(hour= hour(started_at)) %>% 
  group_by(member_casual, hour) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length), sum_rides = sum(ride_length)) %>% 
  arrange(hour)

```

**chart(4)**
-the number of member and casual at hours 

```{r}

sample_df_v2 %>% 
  mutate(hours= hour(started_at)) %>% 
  group_by(member_casual, hours) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(hours) %>% 
  ggplot(aes(x=hours, y=number_of_rides, fill=member_casual))+
  geom_col(position = "dodge")

```


**chart(5)**
-the ride length mean of each member and casual at an hourly scale.

```{r}

sample_df_v2 %>% 
  mutate(hours= hour(started_at)) %>% 
  group_by(member_casual, hours) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(hours) %>% 
  ggplot(aes(x=hours, y=average_duration, fill=member_casual))+
  geom_col(position = "dodge")

```

-**FINDING (5)**
- > the number of members is more than casual on an hourly scale.
- > as you can see in chart(4) above, there are two peaks one at 8 am (2266) and two at 5 pm (3957) for the member, which indicate their high demand at times from casual.
- > both the member and casual are greater at 5 pm (member=3957, casual=2602)
- > the mean of casual is always greater than the mean of member 
- > at 3 am there are some casuals use their bike for a long rides, because the of the ride is equal to 1769783 and the number or length of the ride is equal to 156	

-The number of member and casual in day of week.
```{r}

sample_df_v2 %>% 
  mutate(weekday=wday(started_at, label=TRUE)) %>% 
  group_by(member_casual, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(weekday) 
  

```


**chart(6)**
-the number of the member and casual at weekend scale 
```{r}
sample_df_v2 %>% 
  mutate(weekday=wday(started_at, label=TRUE)) %>% 
  group_by(member_casual, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(weekday) %>% 
  ggplot(aes(x=weekday, y=number_of_rides, fill=member_casual))+
  geom_col(position = "dodge")

```

**chart(7)**
-The mean of each member and casual at weekday scale.

```{r}

sample_df_v2 %>% 
  mutate(weekday=wday(started_at, label=TRUE)) %>% 
  group_by(member_casual, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(weekday) %>% 
  ggplot(aes(x=weekday, y=average_duration, fill=member_casual))+
  geom_col(position = "dodge")

```

-**FINDING (6)**

- > So in the table above the sum of member are more than the sum of casual from Monday to Friday, but that is different on the weekend that indicates the casual use bikes more at weekend (we need some more data like surveys to see reasons why casual user prefer using bikes at weekend) because also the mean of casual at weekend is greater than another day


-Now let's see the numbers and  the mean between the member and casual by days 

```{r}

sample_df_v2 %>% 
  mutate(day = mday(started_at)) %>% 
  group_by(member_casual, day) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(day)
  
```


**chart(8)**
-the number of members and casual by day.

```{r}

sample_df_v2 %>% 
  mutate(day = mday(started_at)) %>% 
  group_by(member_casual, day) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(day)  %>% 
  ggplot(aes(x = day, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")

```


**Chart(9)**
-the mean of the member and casual by day

```{r}

#Bar chart
sample_df_v2 %>% 
  mutate(day = mday(started_at)) %>% 
  group_by(member_casual, day) %>% 
  summarise(average_duration = mean(ride_length)) %>% 
  arrange(member_casual, day)  %>% 
  ggplot(aes(x = day, y = average_duration , fill = member_casual)) +
  geom_col(position = "dodge")

```

**chart(10)**
-the number of member and casual at days

```{r}
sample_df_v2 %>% 
  mutate(day = mday(started_at)) %>% 
  group_by(member_casual, day) %>% 
  summarise(number_rides = n()) %>% 
  arrange(member_casual, day)  %>% 
  ggplot(aes(x = day, y = number_rides, fill = member_casual, color=member_casual)) +
  geom_line()

```

-**FINDING (7)**
- > as usual the length of member are greater than casual 
- > in the number of casuals roughly for every 7 or 8 days there are peaks
- > again the mean of the member didn't reach 1000, the mean of casual is more than 2000 on some days
- > the member and casual follow the same pattern (chart(9))

-let's see how the member and casual be different in a monthly scale.
```{r}

sample_df_v2 %>% 
  mutate(month = month(started_at, label = TRUE)) %>% 
  group_by(member_casual, month) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(month)

```


**chart(11)**
- the number of member and causal at monthly scale.
```{r}
sample_df_v2 %>% 
  mutate(months = month(started_at, label = TRUE)) %>% 
  group_by(member_casual, months) %>%
  summarise(number_of_rides = n()) %>% 
  arrange(months) %>% 
  ggplot(aes(x = months,  y = number_of_rides , fill = member_casual)) +
  geom_col(position = "dodge") 

```


**chart(12)**
-the average member and casual at monthly scale.
```{r}
sample_df_v2 %>% 
  mutate(month = month(started_at, label = TRUE)) %>% 
  group_by(member_casual, month) %>%
  summarise(average_duration = mean(ride_length)) %>% 
  arrange(month) %>% 
  ggplot(aes(x = month,  y =average_duration, fill = member_casual)) +
  geom_col(position = "dodge") 

```

**chart(13)**

-the number of the member and casual at monthly scale by using line.
```{r}
sample_df_v2 %>% 
  mutate(months = month(started_at, label = TRUE)) %>% 
  group_by(member_casual, months) %>%
  summarise(number_of_rides = n()) %>% 
  arrange(months) %>% 
  ggplot(aes(x = months,  y = number_of_rides, group = member_casual,  color = member_casual)) + 
  geom_path()

```

-**FINDING (8)**
- > First thing is the demand for bikes keep rising from May to August and then declining to December 
- > as you can see there is a huge difference between the member and casual from January to April and from October to  December, but the difference keeps shrinking from May to September, especially in summer (June, July, August ) 
- > in a chart(11) as you can see there is a big difference in the mean ride length of each member and casual 
- > this difference becomes huge in December this is because as you can see in the table above, the number of ride lengths is small, there is a small number in January too but the sum of ride lengths is also small, as the opposite of December the number of ride length is small but the sum of ride length is big, because of that the mean of December is the greater one 

-let's see in year scale
```{r}
sample_df_v2 %>% 
  mutate(year= year(started_at)) %>% 
  group_by(member_casual, year) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(year)

```

**chart(14)**
-the number of member and casual at year 
```{r}

sample_df_v2 %>% 
  mutate(year= year(started_at)) %>% 
  group_by(member_casual, year) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(year) %>% 
  ggplot(aes(x=year, y=number_of_rides, fill=member_casual))+
  geom_col(position = "dodge")
  
```


#chart(15)
the number of member and casual at year scale
```{r}
sample_df_v2 %>% 
  mutate(year= year(started_at)) %>% 
  group_by(member_casual, year) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(year) %>% 
  ggplot(aes(x=year, y=number_of_rides, fill=member_casual))+
  geom_col(position = "dodge")

```


**chart(16)**
-the mean of member and casual at annual scale
```{r}
sample_df_v2 %>% 
  mutate(year= year(started_at)) %>% 
  group_by(member_casual, year) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(year) %>% 
  ggplot(aes(x=year, y=average_duration, fill=member_casual))+
  geom_col(position = "dodge")

```

-**FINDING (9)**
- > first as you can see in the table above or in a chart(11) the member are more than casual both in 2021, and  2022
- > there are some differences between 2021 and 2022 for both users (member and casual),  let's see this with some details.
- > the sum of the casual was equal in 2021 to *8958* and in 2022(august) is equal to *18799*, and the difference is *9841*
- > the sum of the member was equal in 2021 to *13433* and in 2022(august) is equal to *24630*, and the difference is *11197*
- > based on the two notes above we can see that there is a huge difference in both members and casual, and both are growing up.
-the mean ride length is grow up a little bit from 2021 to 2022, with members ~ 49.19 and casual ~ 23.38, let's see this also with some details 
- > the mean of the ride for the casual in 2021 was equal to *1587.9831*, in 2022(august) is equal to *1611.3650*, and the difference is equal to *23.3819*
- > the mean of the ride for the member in 2021 was equal to *739.4429*, in 2022(august) is equal to *788.0613*, and the difference is equal to *48.6184*


**RECOMMENDATIONS**
-Based on the findings 
- > first thing of my recommendations is we need to do more surveys on times that the casual is more or equal to member because it is important to know why some casual users didn't prefer to be casual 
- > we need to do some marketing campings at times that there huge demand by casual 
- > offer some discount for the membership especially for long rides and during summer and increasing the cost of casual for the long ride
