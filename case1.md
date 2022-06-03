---
title: "CaseStudy#1"
author: "Veysel Bugra Demir"
date: "01 06 2022"
output: 
  html_document: 
    toc: yes
    keep_md: true
---



## Google Divvy Case Study

Required packeges

```r
library(tidyverse) 
```

```
## Warning: package 'tidyverse' was built under R version 3.6.2
```

```
## -- Attaching packages --------------------------------------------------------------------------------- tidyverse 1.3.0 --
```

```
## <U+221A> ggplot2 3.2.1     <U+221A> purrr   0.3.3
## <U+221A> tibble  2.1.3     <U+221A> dplyr   0.8.3
## <U+221A> tidyr   1.0.0     <U+221A> stringr 1.4.0
## <U+221A> readr   1.3.1     <U+221A> forcats 0.4.0
```

```
## Warning: package 'ggplot2' was built under R version 3.6.2
```

```
## Warning: package 'tibble' was built under R version 3.6.2
```

```
## Warning: package 'tidyr' was built under R version 3.6.2
```

```
## Warning: package 'readr' was built under R version 3.6.2
```

```
## Warning: package 'purrr' was built under R version 3.6.2
```

```
## Warning: package 'dplyr' was built under R version 3.6.2
```

```
## Warning: package 'stringr' was built under R version 3.6.2
```

```
## Warning: package 'forcats' was built under R version 3.6.2
```

```
## -- Conflicts ------------------------------------------------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(lubridate)  
```

```
## Warning: package 'lubridate' was built under R version 3.6.2
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following object is masked from 'package:base':
## 
##     date
```

```r
library(ggplot2)  
```

# STEP 1: Data Collection

```r
q1_2019 <- read_csv("C:\\Users\\Buğra\\Desktop\\bike data\\data\\Divvy_Trips_2019_Q1.csv")
```

```
## Parsed with column specification:
## cols(
##   trip_id = col_double(),
##   start_time = col_datetime(format = ""),
##   end_time = col_datetime(format = ""),
##   bikeid = col_double(),
##   tripduration = col_number(),
##   from_station_id = col_double(),
##   from_station_name = col_character(),
##   to_station_id = col_double(),
##   to_station_name = col_character(),
##   usertype = col_character(),
##   gender = col_character(),
##   birthyear = col_double()
## )
```

```r
q2_2019 <- read_csv("C:\\Users\\Buğra\\Desktop\\bike data\\data\\Divvy_Trips_2019_Q2.csv")
```

```
## Parsed with column specification:
## cols(
##   `01 - Rental Details Rental ID` = col_double(),
##   `01 - Rental Details Local Start Time` = col_datetime(format = ""),
##   `01 - Rental Details Local End Time` = col_datetime(format = ""),
##   `01 - Rental Details Bike ID` = col_double(),
##   `01 - Rental Details Duration In Seconds Uncapped` = col_number(),
##   `03 - Rental Start Station ID` = col_double(),
##   `03 - Rental Start Station Name` = col_character(),
##   `02 - Rental End Station ID` = col_double(),
##   `02 - Rental End Station Name` = col_character(),
##   `User Type` = col_character(),
##   `Member Gender` = col_character(),
##   `05 - Member Details Member Birthday Year` = col_double()
## )
```

```r
q3_2019 <- read_csv("C:\\Users\\Buğra\\Desktop\\bike data\\data\\Divvy_Trips_2019_Q3.csv")
```

```
## Parsed with column specification:
## cols(
##   trip_id = col_double(),
##   start_time = col_datetime(format = ""),
##   end_time = col_datetime(format = ""),
##   bikeid = col_double(),
##   tripduration = col_number(),
##   from_station_id = col_double(),
##   from_station_name = col_character(),
##   to_station_id = col_double(),
##   to_station_name = col_character(),
##   usertype = col_character(),
##   gender = col_character(),
##   birthyear = col_double()
## )
```

```r
q4_2019 <- read_csv("C:\\Users\\Buğra\\Desktop\\bike data\\data\\Divvy_Trips_2019_Q4.csv")
```

```
## Parsed with column specification:
## cols(
##   trip_id = col_double(),
##   start_time = col_datetime(format = ""),
##   end_time = col_datetime(format = ""),
##   bikeid = col_double(),
##   tripduration = col_number(),
##   from_station_id = col_double(),
##   from_station_name = col_character(),
##   to_station_id = col_double(),
##   to_station_name = col_character(),
##   usertype = col_character(),
##   gender = col_character(),
##   birthyear = col_double()
## )
```
# STEP 2: Wrangle and Combine
Renaming the columns for consistency.

```r
q1_2019 <- rename(q1_2019, ride_id=trip_id,
                  rideable_type=bikeid,
                  started_at = start_time,
                  ended_at = end_time,
                  start_station_name = from_station_name,
                  start_station_id = from_station_id,
                  end_station_name = to_station_name,
                  end_station_id = to_station_id,
                  member_casual = usertype)

q2_2019 <- rename(q2_2019, ride_id="01 - Rental Details Rental ID",
                  rideable_type="01 - Rental Details Bike ID",
                  started_at = "01 - Rental Details Local Start Time" ,
                  ended_at = "01 - Rental Details Local End Time",
                  start_station_name = "03 - Rental Start Station Name",
                  start_station_id = "03 - Rental Start Station ID",
                  end_station_name = "02 - Rental End Station Name",
                  end_station_id = "02 - Rental End Station ID",
                  member_casual = "User Type")

q3_2019 <- rename(q3_2019, ride_id=trip_id,
                  rideable_type=bikeid,
                  started_at = start_time,
                  ended_at = end_time,
                  start_station_name = from_station_name,
                  start_station_id = from_station_id,
                  end_station_name = to_station_name,
                  end_station_id = to_station_id,
                  member_casual = usertype)

q4_2019 <- rename(q4_2019, ride_id=trip_id,
                  rideable_type=bikeid,
                  started_at = start_time,
                  ended_at = end_time,
                  start_station_name = from_station_name,
                  start_station_id = from_station_id,
                  end_station_name = to_station_name,
                  end_station_id = to_station_id,
                  member_casual = usertype)
```


```r
str(q1_2019)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	365069 obs. of  12 variables:
##  $ ride_id           : num  21742443 21742444 21742445 21742446 21742447 ...
##  $ started_at        : POSIXct, format: "2019-01-01 00:04:37" "2019-01-01 00:08:13" ...
##  $ ended_at          : POSIXct, format: "2019-01-01 00:11:07" "2019-01-01 00:15:34" ...
##  $ rideable_type     : num  2167 4386 1524 252 1170 ...
##  $ tripduration      : num  390 441 829 1783 364 ...
##  $ start_station_id  : num  199 44 15 123 173 98 98 211 150 268 ...
##  $ start_station_name: chr  "Wabash Ave & Grand Ave" "State St & Randolph St" "Racine Ave & 18th St" "California Ave & Milwaukee Ave" ...
##  $ end_station_id    : num  84 624 644 176 35 49 49 142 148 141 ...
##  $ end_station_name  : chr  "Milwaukee Ave & Grand Ave" "Dearborn St & Van Buren St (*)" "Western Ave & Fillmore St (*)" "Clark St & Elm St" ...
##  $ member_casual     : chr  "Subscriber" "Subscriber" "Subscriber" "Subscriber" ...
##  $ gender            : chr  "Male" "Female" "Female" "Male" ...
##  $ birthyear         : num  1989 1990 1994 1993 1994 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   trip_id = col_double(),
##   ..   start_time = col_datetime(format = ""),
##   ..   end_time = col_datetime(format = ""),
##   ..   bikeid = col_double(),
##   ..   tripduration = col_number(),
##   ..   from_station_id = col_double(),
##   ..   from_station_name = col_character(),
##   ..   to_station_id = col_double(),
##   ..   to_station_name = col_character(),
##   ..   usertype = col_character(),
##   ..   gender = col_character(),
##   ..   birthyear = col_double()
##   .. )
```

```r
str(q2_2019)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	1108163 obs. of  12 variables:
##  $ ride_id                                         : num  22178529 22178530 22178531 22178532 22178533 ...
##  $ started_at                                      : POSIXct, format: "2019-04-01 00:02:22" "2019-04-01 00:03:02" ...
##  $ ended_at                                        : POSIXct, format: "2019-04-01 00:09:48" "2019-04-01 00:20:30" ...
##  $ rideable_type                                   : num  6251 6226 5649 4151 3270 ...
##  $ 01 - Rental Details Duration In Seconds Uncapped: num  446 1048 252 357 1007 ...
##  $ start_station_id                                : num  81 317 283 26 202 420 503 260 211 211 ...
##  $ start_station_name                              : chr  "Daley Center Plaza" "Wood St & Taylor St" "LaSalle St & Jackson Blvd" "McClurg Ct & Illinois St" ...
##  $ end_station_id                                  : num  56 59 174 133 129 426 500 499 211 211 ...
##  $ end_station_name                                : chr  "Desplaines St & Kinzie St" "Wabash Ave & Roosevelt Rd" "Canal St & Madison St" "Kingsbury St & Kinzie St" ...
##  $ member_casual                                   : chr  "Subscriber" "Subscriber" "Subscriber" "Subscriber" ...
##  $ Member Gender                                   : chr  "Male" "Female" "Male" "Male" ...
##  $ 05 - Member Details Member Birthday Year        : num  1975 1984 1990 1993 1992 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   `01 - Rental Details Rental ID` = col_double(),
##   ..   `01 - Rental Details Local Start Time` = col_datetime(format = ""),
##   ..   `01 - Rental Details Local End Time` = col_datetime(format = ""),
##   ..   `01 - Rental Details Bike ID` = col_double(),
##   ..   `01 - Rental Details Duration In Seconds Uncapped` = col_number(),
##   ..   `03 - Rental Start Station ID` = col_double(),
##   ..   `03 - Rental Start Station Name` = col_character(),
##   ..   `02 - Rental End Station ID` = col_double(),
##   ..   `02 - Rental End Station Name` = col_character(),
##   ..   `User Type` = col_character(),
##   ..   `Member Gender` = col_character(),
##   ..   `05 - Member Details Member Birthday Year` = col_double()
##   .. )
```

```r
str(q3_2019)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	1640718 obs. of  12 variables:
##  $ ride_id           : num  23479388 23479389 23479390 23479391 23479392 ...
##  $ started_at        : POSIXct, format: "2019-07-01 00:00:27" "2019-07-01 00:01:16" ...
##  $ ended_at          : POSIXct, format: "2019-07-01 00:20:41" "2019-07-01 00:18:44" ...
##  $ rideable_type     : num  3591 5353 6180 5540 6014 ...
##  $ tripduration      : num  1214 1048 1554 1503 1213 ...
##  $ start_station_id  : num  117 381 313 313 168 300 168 313 43 43 ...
##  $ start_station_name: chr  "Wilton Ave & Belmont Ave" "Western Ave & Monroe St" "Lakeview Ave & Fullerton Pkwy" "Lakeview Ave & Fullerton Pkwy" ...
##  $ end_station_id    : num  497 203 144 144 62 232 62 144 195 195 ...
##  $ end_station_name  : chr  "Kimball Ave & Belmont Ave" "Western Ave & 21st St" "Larrabee St & Webster Ave" "Larrabee St & Webster Ave" ...
##  $ member_casual     : chr  "Subscriber" "Customer" "Customer" "Customer" ...
##  $ gender            : chr  "Male" NA NA NA ...
##  $ birthyear         : num  1992 NA NA NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   trip_id = col_double(),
##   ..   start_time = col_datetime(format = ""),
##   ..   end_time = col_datetime(format = ""),
##   ..   bikeid = col_double(),
##   ..   tripduration = col_number(),
##   ..   from_station_id = col_double(),
##   ..   from_station_name = col_character(),
##   ..   to_station_id = col_double(),
##   ..   to_station_name = col_character(),
##   ..   usertype = col_character(),
##   ..   gender = col_character(),
##   ..   birthyear = col_double()
##   .. )
```

```r
str(q4_2019)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	704054 obs. of  12 variables:
##  $ ride_id           : num  25223640 25223641 25223642 25223643 25223644 ...
##  $ started_at        : POSIXct, format: "2019-10-01 00:01:39" "2019-10-01 00:02:16" ...
##  $ ended_at          : POSIXct, format: "2019-10-01 00:17:20" "2019-10-01 00:06:34" ...
##  $ rideable_type     : num  2215 6328 3003 3275 5294 ...
##  $ tripduration      : num  940 258 850 2350 1867 ...
##  $ start_station_id  : num  20 19 84 313 210 156 84 156 156 336 ...
##  $ start_station_name: chr  "Sheffield Ave & Kingsbury St" "Throop (Loomis) St & Taylor St" "Milwaukee Ave & Grand Ave" "Lakeview Ave & Fullerton Pkwy" ...
##  $ end_station_id    : num  309 241 199 290 382 226 142 463 463 336 ...
##  $ end_station_name  : chr  "Leavitt St & Armitage Ave" "Morgan St & Polk St" "Wabash Ave & Grand Ave" "Kedzie Ave & Palmer Ct" ...
##  $ member_casual     : chr  "Subscriber" "Subscriber" "Subscriber" "Subscriber" ...
##  $ gender            : chr  "Male" "Male" "Female" "Male" ...
##  $ birthyear         : num  1987 1998 1991 1990 1987 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   trip_id = col_double(),
##   ..   start_time = col_datetime(format = ""),
##   ..   end_time = col_datetime(format = ""),
##   ..   bikeid = col_double(),
##   ..   tripduration = col_number(),
##   ..   from_station_id = col_double(),
##   ..   from_station_name = col_character(),
##   ..   to_station_id = col_double(),
##   ..   to_station_name = col_character(),
##   ..   usertype = col_character(),
##   ..   gender = col_character(),
##   ..   birthyear = col_double()
##   .. )
```
Converting data.

```r
q1_2019 <- mutate(q1_2019, ride_id = as.character(ride_id), rideable_type = as.character(rideable_type))

q2_2019 <- mutate(q2_2019, ride_id = as.character(ride_id), rideable_type = as.character(rideable_type))

q3_2019 <- mutate(q3_2019, ride_id = as.character(ride_id), rideable_type = as.character(rideable_type))

q4_2019 <- mutate(q4_2019, ride_id = as.character(ride_id), rideable_type = as.character(rideable_type))
```
Concatenating the all data.

```r
all_trips <- bind_rows(q1_2019, q2_2019, q3_2019, q4_2019)
```
Dropping unnecessary columns.

```r
all_trips <- all_trips %>% 
  select(-c(birthyear, gender,"01 - Rental Details Duration In Seconds Uncapped", "05 - Member Details Member Birthday Year", "Member Gender", "tripduration"))
```
# STEP 3: CLEAN UP

```r
colnames(all_trips)
```

```
## [1] "ride_id"            "started_at"         "ended_at"          
## [4] "rideable_type"      "start_station_id"   "start_station_name"
## [7] "end_station_id"     "end_station_name"   "member_casual"
```

```r
nrow(all_trips)
```

```
## [1] 3818004
```

```r
dim(all_trips)
```

```
## [1] 3818004       9
```

```r
head(all_trips) 
```

```
## # A tibble: 6 x 9
##   ride_id started_at          ended_at            rideable_type start_station_id
##   <chr>   <dttm>              <dttm>              <chr>                    <dbl>
## 1 217424~ 2019-01-01 00:04:37 2019-01-01 00:11:07 2167                       199
## 2 217424~ 2019-01-01 00:08:13 2019-01-01 00:15:34 4386                        44
## 3 217424~ 2019-01-01 00:13:23 2019-01-01 00:27:12 1524                        15
## 4 217424~ 2019-01-01 00:13:45 2019-01-01 00:43:28 252                        123
## 5 217424~ 2019-01-01 00:14:52 2019-01-01 00:20:56 1170                       173
## 6 217424~ 2019-01-01 00:15:33 2019-01-01 00:19:09 2437                        98
## # ... with 4 more variables: start_station_name <chr>, end_station_id <dbl>,
## #   end_station_name <chr>, member_casual <chr>
```

```r
str(all_trips)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	3818004 obs. of  9 variables:
##  $ ride_id           : chr  "21742443" "21742444" "21742445" "21742446" ...
##  $ started_at        : POSIXct, format: "2019-01-01 00:04:37" "2019-01-01 00:08:13" ...
##  $ ended_at          : POSIXct, format: "2019-01-01 00:11:07" "2019-01-01 00:15:34" ...
##  $ rideable_type     : chr  "2167" "4386" "1524" "252" ...
##  $ start_station_id  : num  199 44 15 123 173 98 98 211 150 268 ...
##  $ start_station_name: chr  "Wabash Ave & Grand Ave" "State St & Randolph St" "Racine Ave & 18th St" "California Ave & Milwaukee Ave" ...
##  $ end_station_id    : num  84 624 644 176 35 49 49 142 148 141 ...
##  $ end_station_name  : chr  "Milwaukee Ave & Grand Ave" "Dearborn St & Van Buren St (*)" "Western Ave & Fillmore St (*)" "Clark St & Elm St" ...
##  $ member_casual     : chr  "Subscriber" "Subscriber" "Subscriber" "Subscriber" ...
```

```r
summary(all_trips)
```

```
##    ride_id            started_at                     ended_at                  
##  Length:3818004     Min.   :2019-01-01 00:04:37   Min.   :2019-01-01 00:11:07  
##  Class :character   1st Qu.:2019-05-29 15:49:26   1st Qu.:2019-05-29 16:09:28  
##  Mode  :character   Median :2019-07-25 17:50:54   Median :2019-07-25 18:12:23  
##                     Mean   :2019-07-19 21:47:37   Mean   :2019-07-19 22:11:47  
##                     3rd Qu.:2019-09-15 06:48:05   3rd Qu.:2019-09-15 08:30:13  
##                     Max.   :2019-12-31 23:57:17   Max.   :2020-01-21 13:54:35  
##  rideable_type      start_station_id start_station_name end_station_id 
##  Length:3818004     Min.   :  1.0    Length:3818004     Min.   :  1.0  
##  Class :character   1st Qu.: 77.0    Class :character   1st Qu.: 77.0  
##  Mode  :character   Median :174.0    Mode  :character   Median :174.0  
##                     Mean   :201.7                       Mean   :202.6  
##                     3rd Qu.:289.0                       3rd Qu.:291.0  
##                     Max.   :673.0                       Max.   :673.0  
##  end_station_name   member_casual     
##  Length:3818004     Length:3818004    
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
## 
```
Replacing values in the "member_casual" column

```r
table(all_trips$member_casual) # How many observations.
```

```
## 
##   Customer Subscriber 
##     880637    2937367
```

```r
all_trips <-all_trips %>% mutate(member_casual = recode(member_casual, "Subscriber" = "member",
                                            "Customer" = "casual"))
```

```r
table(all_trips$member_casual)
```

```
## 
##  casual  member 
##  880637 2937367
```
Creating new date, month, day, year and day of week columns to aggregate the results more granular level.

```r
all_trips$date <- as.Date(all_trips$started_at)
all_trips$month <- format(as.Date(all_trips$date), "%m")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%A")
```
Calculating trip durations.

```r
all_trips$ride_length <- difftime(all_trips$ended_at, all_trips$started_at)
```

```r
str(all_trips)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	3818004 obs. of  15 variables:
##  $ ride_id           : chr  "21742443" "21742444" "21742445" "21742446" ...
##  $ started_at        : POSIXct, format: "2019-01-01 00:04:37" "2019-01-01 00:08:13" ...
##  $ ended_at          : POSIXct, format: "2019-01-01 00:11:07" "2019-01-01 00:15:34" ...
##  $ rideable_type     : chr  "2167" "4386" "1524" "252" ...
##  $ start_station_id  : num  199 44 15 123 173 98 98 211 150 268 ...
##  $ start_station_name: chr  "Wabash Ave & Grand Ave" "State St & Randolph St" "Racine Ave & 18th St" "California Ave & Milwaukee Ave" ...
##  $ end_station_id    : num  84 624 644 176 35 49 49 142 148 141 ...
##  $ end_station_name  : chr  "Milwaukee Ave & Grand Ave" "Dearborn St & Van Buren St (*)" "Western Ave & Fillmore St (*)" "Clark St & Elm St" ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
##  $ date              : Date, format: "2019-01-01" "2019-01-01" ...
##  $ month             : chr  "01" "01" "01" "01" ...
##  $ day               : chr  "01" "01" "01" "01" ...
##  $ year              : chr  "2019" "2019" "2019" "2019" ...
##  $ day_of_week       : chr  "Salı" "Salı" "Salı" "Salı" ...
##  $ ride_length       : 'difftime' num  6.5 7.35 13.8166666666667 29.7166666666667 ...
##   ..- attr(*, "units")= chr "mins"
```
day_of_week was returned in Turkish
to make it in English use:
Sys.setlocale("LC_TIME","English United States")

```r
typeof(all_trips$ride_length)
```

```
## [1] "double"
```
Changing the data type for further calculations.

```r
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))
```
typeof(all_trips$ride_length)

```r
typeof(all_trips$ride_length)
```

```
## [1] "double"
```

```r
is.numeric(all_trips$ride_length)
```

```
## [1] TRUE
```
Deleting the rows that has minus ride length.  

```r
all_trips_v2 <- all_trips[!(all_trips$start_station_name == "HQ QR" | all_trips$ride_length<0),]
```
# STEP 4: Analysis

```r
mean(all_trips_v2$ride_length)
```

```
## [1] 24.17443
```

```r
median(all_trips_v2$ride_length)
```

```
## [1] 11.81667
```

```r
max(all_trips_v2$ride_length)
```

```
## [1] 177200.4
```

```r
min(all_trips_v2$ride_length)
```

```
## [1] 1.016667
```

```r
summary(all_trips_v2$ride_length)
```

```
##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
##      1.02      6.85     11.82     24.17     21.40 177200.37
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = mean) # is as the same as all_trips_v2 %>% group_by(member_casual) %>% summarise(mean(ride_length))
```

```
##   all_trips_v2$member_casual all_trips_v2$ride_length
## 1                     casual                 57.01802
## 2                     member                 14.32780
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = median)
```

```
##   all_trips_v2$member_casual all_trips_v2$ride_length
## 1                     casual                 25.83333
## 2                     member                  9.80000
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = max)
```

```
##   all_trips_v2$member_casual all_trips_v2$ride_length
## 1                     casual                 177200.4
## 2                     member                 150943.9
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = min)
```

```
##   all_trips_v2$member_casual all_trips_v2$ride_length
## 1                     casual                 1.016667
## 2                     member                 1.016667
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN=mean)
```

```
##    all_trips_v2$member_casual all_trips_v2$day_of_week all_trips_v2$ride_length
## 1                      casual                     Cuma                 60.17561
## 2                      member                     Cuma                 13.89748
## 3                      casual                Cumartesi                 54.06111
## 4                      member                Cumartesi                 16.30271
## 5                      casual                 Çarşamba                 60.33407
## 6                      member                 Çarşamba                 13.80984
## 7                      casual                    Pazar                 56.18519
## 8                      member                    Pazar                 15.40290
## 9                      casual                Pazartesi                 54.49989
## 10                     member                Pazartesi                 14.24928
## 11                     casual                 Perşembe                 59.95112
## 12                     member                 Perşembe                 13.77979
## 13                     casual                     Salı                 57.41328
## 14                     member                     Salı                 14.15259
```

```r
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, levels=c("Pazar", "Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma", "Cumartesi"))
```

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
```

```
##    all_trips_v2$member_casual all_trips_v2$day_of_week all_trips_v2$ride_length
## 1                      casual                    Pazar                 56.18519
## 2                      member                    Pazar                 15.40290
## 3                      casual                Pazartesi                 54.49989
## 4                      member                Pazartesi                 14.24928
## 5                      casual                     Salı                 57.41328
## 6                      member                     Salı                 14.15259
## 7                      casual                 Çarşamba                 60.33407
## 8                      member                 Çarşamba                 13.80984
## 9                      casual                 Perşembe                 59.95112
## 10                     member                 Perşembe                 13.77979
## 11                     casual                     Cuma                 60.17561
## 12                     member                     Cuma                 13.89748
## 13                     casual                Cumartesi                 54.06111
## 14                     member                Cumartesi                 16.30271
```

```r
all_trips_v2 %>% 
  mutate(weekday= wday(started_at, label=TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n(), average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday)
```

```
## # A tibble: 14 x 4
## # Groups:   member_casual [2]
##    member_casual weekday number_of_rides average_duration
##    <chr>         <ord>             <int>            <dbl>
##  1 casual        Paz              170173             56.2
##  2 casual        Pzt              101489             54.5
##  3 casual        Sal               88655             57.4
##  4 casual        Çar               89745             60.3
##  5 casual        Per              101372             60.0
##  6 casual        Cum              121141             60.2
##  7 casual        Cmt              208056             54.1
##  8 member        Paz              256234             15.4
##  9 member        Pzt              458780             14.2
## 10 member        Sal              497025             14.2
## 11 member        Çar              494277             13.8
## 12 member        Per              486915             13.8
## 13 member        Cum              456966             13.9
## 14 member        Cmt              287163             16.3
```
Visualize the data

```r
all_trips_v2 %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n(), average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday) %>% 
  ggplot(aes(x=weekday, y=average_duration)) + geom_col(position="dodge", aes(fill=member_casual))
```

![](case1_files/figure-html/unnamed-chunk-26-1.png)<!-- -->

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
```

```
##    all_trips_v2$member_casual all_trips_v2$day_of_week all_trips_v2$ride_length
## 1                      casual                    Pazar                 56.18519
## 2                      member                    Pazar                 15.40290
## 3                      casual                Pazartesi                 54.49989
## 4                      member                Pazartesi                 14.24928
## 5                      casual                     Salı                 57.41328
## 6                      member                     Salı                 14.15259
## 7                      casual                 Çarşamba                 60.33407
## 8                      member                 Çarşamba                 13.80984
## 9                      casual                 Perşembe                 59.95112
## 10                     member                 Perşembe                 13.77979
## 11                     casual                     Cuma                 60.17561
## 12                     member                     Cuma                 13.89748
## 13                     casual                Cumartesi                 54.06111
## 14                     member                Cumartesi                 16.30271
```
