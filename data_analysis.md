Fitbit Data Analysis
================

``` r
# Importing the packages
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.1.3

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.8
    ## v tidyr   1.2.0     v stringr 1.4.0
    ## v readr   2.1.2     v forcats 0.5.1

    ## Warning: package 'ggplot2' was built under R version 4.1.3

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
```

``` r
# Loading the dataset
daily_activity <- read_csv("fitabase_data/dailyActivity_merged.csv")
```

    ## Rows: 940 Columns: 15
    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (1): ActivityDate
    ## dbl (14): Id, TotalSteps, TotalDistance, TrackerDistance, LoggedActivitiesDi...
    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Viewing the data
head(daily_activity)
```

    ## # A tibble: 6 x 15
    ##        Id ActivityDate TotalSteps TotalDistance TrackerDistance LoggedActivitie~
    ##     <dbl> <chr>             <dbl>         <dbl>           <dbl>            <dbl>
    ## 1  1.50e9 4/12/2016         13162          8.5             8.5                 0
    ## 2  1.50e9 4/13/2016         10735          6.97            6.97                0
    ## 3  1.50e9 4/14/2016         10460          6.74            6.74                0
    ## 4  1.50e9 4/15/2016          9762          6.28            6.28                0
    ## 5  1.50e9 4/16/2016         12669          8.16            8.16                0
    ## 6  1.50e9 4/17/2016          9705          6.48            6.48                0
    ## # ... with 9 more variables: VeryActiveDistance <dbl>,
    ## #   ModeratelyActiveDistance <dbl>, LightActiveDistance <dbl>,
    ## #   SedentaryActiveDistance <dbl>, VeryActiveMinutes <dbl>,
    ## #   FairlyActiveMinutes <dbl>, LightlyActiveMinutes <dbl>,
    ## #   SedentaryMinutes <dbl>, Calories <dbl>

``` r
# Getting the column names
colnames(daily_activity)
```

    ##  [1] "Id"                       "ActivityDate"            
    ##  [3] "TotalSteps"               "TotalDistance"           
    ##  [5] "TrackerDistance"          "LoggedActivitiesDistance"
    ##  [7] "VeryActiveDistance"       "ModeratelyActiveDistance"
    ##  [9] "LightActiveDistance"      "SedentaryActiveDistance" 
    ## [11] "VeryActiveMinutes"        "FairlyActiveMinutes"     
    ## [13] "LightlyActiveMinutes"     "SedentaryMinutes"        
    ## [15] "Calories"

``` r
# Inspecting the structure of data
str(daily_activity)
```

    ## spec_tbl_df [940 x 15] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ Id                      : num [1:940] 1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
    ##  $ ActivityDate            : chr [1:940] "4/12/2016" "4/13/2016" "4/14/2016" "4/15/2016" ...
    ##  $ TotalSteps              : num [1:940] 13162 10735 10460 9762 12669 ...
    ##  $ TotalDistance           : num [1:940] 8.5 6.97 6.74 6.28 8.16 ...
    ##  $ TrackerDistance         : num [1:940] 8.5 6.97 6.74 6.28 8.16 ...
    ##  $ LoggedActivitiesDistance: num [1:940] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveDistance      : num [1:940] 1.88 1.57 2.44 2.14 2.71 ...
    ##  $ ModeratelyActiveDistance: num [1:940] 0.55 0.69 0.4 1.26 0.41 ...
    ##  $ LightActiveDistance     : num [1:940] 6.06 4.71 3.91 2.83 5.04 ...
    ##  $ SedentaryActiveDistance : num [1:940] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveMinutes       : num [1:940] 25 21 30 29 36 38 42 50 28 19 ...
    ##  $ FairlyActiveMinutes     : num [1:940] 13 19 11 34 10 20 16 31 12 8 ...
    ##  $ LightlyActiveMinutes    : num [1:940] 328 217 181 209 221 164 233 264 205 211 ...
    ##  $ SedentaryMinutes        : num [1:940] 728 776 1218 726 773 ...
    ##  $ Calories                : num [1:940] 1985 1797 1776 1745 1863 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Id = col_double(),
    ##   ..   ActivityDate = col_character(),
    ##   ..   TotalSteps = col_double(),
    ##   ..   TotalDistance = col_double(),
    ##   ..   TrackerDistance = col_double(),
    ##   ..   LoggedActivitiesDistance = col_double(),
    ##   ..   VeryActiveDistance = col_double(),
    ##   ..   ModeratelyActiveDistance = col_double(),
    ##   ..   LightActiveDistance = col_double(),
    ##   ..   SedentaryActiveDistance = col_double(),
    ##   ..   VeryActiveMinutes = col_double(),
    ##   ..   FairlyActiveMinutes = col_double(),
    ##   ..   LightlyActiveMinutes = col_double(),
    ##   ..   SedentaryMinutes = col_double(),
    ##   ..   Calories = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
# Finding number of unique participants in the dataset
n_distinct(daily_activity$Id)
```

    ## [1] 33

``` r
# Getting quick summary of data
daily_activity %>% 
  select(TotalSteps, TotalDistance, SedentaryMinutes, Calories) %>% 
  summary()
```

    ##    TotalSteps    TotalDistance    SedentaryMinutes    Calories   
    ##  Min.   :    0   Min.   : 0.000   Min.   :   0.0   Min.   :   0  
    ##  1st Qu.: 3790   1st Qu.: 2.620   1st Qu.: 729.8   1st Qu.:1828  
    ##  Median : 7406   Median : 5.245   Median :1057.5   Median :2134  
    ##  Mean   : 7638   Mean   : 5.490   Mean   : 991.2   Mean   :2304  
    ##  3rd Qu.:10727   3rd Qu.: 7.713   3rd Qu.:1229.5   3rd Qu.:2793  
    ##  Max.   :36019   Max.   :28.030   Max.   :1440.0   Max.   :4900

By this we can see that each of the four variables have Min. value of 0,
this could mean that the tracker was off at time during the data
collection.  
The average total steps is 7638. Average total distance is 5.490 miles
which is 8.83 km, this could mean that the participants were mostly
active. Average sedentary minutes is 991.2 i.e. 16.51 hour.

Average sedentary minutes doesn’t agree with the average total distance,
this could mean that the data has outliers.

``` r
# Plotting total distance vs sedentary minutes
ggplot(data = daily_activity) + 
  geom_point(mapping = aes(x = TotalDistance, y = SedentaryMinutes), color= "skyblue") +
  labs(title = "Sedentary Minutes vs Distance", y = "Sedentary Minutes", x = "Distance")
```

![](data_analysis_files/figure-gfm/total%20distance%20vs%20sedentary%20minutes-1.png)<!-- -->

``` r
# To investigate the relationship between Sedentary minutes and total steps. plotting a chart.
ggplot(data = daily_activity) + 
  geom_point(mapping = aes(x = TotalSteps, y = SedentaryMinutes), color = "violet") +
  labs(title = "Sedentary Minutes vs Steps", x = "Steps", y = "Sedentary Minutes")
```

![](data_analysis_files/figure-gfm/total%20steps%20vs%20sedentary%20minutes-1.png)<!-- -->

``` r
daily_activity_v2 <- daily_activity %>% 
  mutate(SedentaryHours = SedentaryMinutes/ 60)
head(daily_activity_v2)
```

    ## # A tibble: 6 x 16
    ##        Id ActivityDate TotalSteps TotalDistance TrackerDistance LoggedActivitie~
    ##     <dbl> <chr>             <dbl>         <dbl>           <dbl>            <dbl>
    ## 1  1.50e9 4/12/2016         13162          8.5             8.5                 0
    ## 2  1.50e9 4/13/2016         10735          6.97            6.97                0
    ## 3  1.50e9 4/14/2016         10460          6.74            6.74                0
    ## 4  1.50e9 4/15/2016          9762          6.28            6.28                0
    ## 5  1.50e9 4/16/2016         12669          8.16            8.16                0
    ## 6  1.50e9 4/17/2016          9705          6.48            6.48                0
    ## # ... with 10 more variables: VeryActiveDistance <dbl>,
    ## #   ModeratelyActiveDistance <dbl>, LightActiveDistance <dbl>,
    ## #   SedentaryActiveDistance <dbl>, VeryActiveMinutes <dbl>,
    ## #   FairlyActiveMinutes <dbl>, LightlyActiveMinutes <dbl>,
    ## #   SedentaryMinutes <dbl>, Calories <dbl>, SedentaryHours <dbl>

The relationship between sedentary minutes and total distance cannot be
interpreted more at this point. To explore further, I will make a new
column as SedentaryHours

``` r
# Plotting total steps vs SedentaryHours
ggplot(data = daily_activity_v2) +
  geom_point(mapping = aes(x = TotalSteps ,y = SedentaryHours), color = "magenta") +
  labs(title = "Sedentary Hours vs Steps In a Day", x = "Steps", y = "Sedentary Hours") +
  geom_rect(xmin = 100, ymin = 7.5, xmax = 15000, ymax = 22.5, alpha= 0.01) +
  annotate("text", label="More Sedentary hours show less steps", x = 20000, y = 5, color = "blue")
```

![](data_analysis_files/figure-gfm/SedenatryHours%20bar%20chart-1.png)<!-- -->

We can clearly see that **more sedentary hours show fewer steps**. This
can be used to market the product. This could mean that **people who sit
more tend to walk less**.

``` r
# Plotting graph of VeryActiveMinutes vs Calories
ggplot(data = daily_activity) +
  geom_point(mapping = aes(x = Calories, y = VeryActiveMinutes), color = "purple") +
  geom_rect(aes(xmin = 1300, ymin = 5, xmax = 3200, ymax = 60), alpha =0.01) +
  labs(title = "(Very) Active Minutes vs Calories", y = "(Very) Active Minutes", x = "Calories") +
  annotate("text", x = 1200, y = 100, label = "Burned 3200 Calories or less", color= "blue") 
```

![](data_analysis_files/figure-gfm/VeryActiveMinutes%20vs%20Calories-1.png)<!-- -->

From the visualization we can see that people who have Very active
minutes less than 60 have burned 3200 calories or less while people with
very active minutes greater than 60 have burned more calories.

``` r
# Importing the sleep data
sleep_day <- read_csv("fitabase_data/sleepDay_merged.csv")
```

    ## Rows: 413 Columns: 5
    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (1): SleepDay
    ## dbl (4): Id, TotalSleepRecords, TotalMinutesAsleep, TotalTimeInBed
    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(sleep_day)
```

    ## # A tibble: 6 x 5
    ##           Id SleepDay           TotalSleepRecor~ TotalMinutesAsl~ TotalTimeInBed
    ##        <dbl> <chr>                         <dbl>            <dbl>          <dbl>
    ## 1 1503960366 4/12/2016 12:00:0~                1              327            346
    ## 2 1503960366 4/13/2016 12:00:0~                2              384            407
    ## 3 1503960366 4/15/2016 12:00:0~                1              412            442
    ## 4 1503960366 4/16/2016 12:00:0~                2              340            367
    ## 5 1503960366 4/17/2016 12:00:0~                1              700            712
    ## 6 1503960366 4/19/2016 12:00:0~                1              304            320

By looking at the data it is clear that the time in the *SleepDay*
column is useless. let’s remove it.

``` r
sleep_day_v2 <- sleep_day %>% 
  separate(SleepDay, c("SleepDay", "time2"), sep= " ")
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 413 rows [1, 2, 3, 4,
    ## 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, ...].

``` r
# Deleting the time2 column
sleep_day_v2 <- sleep_day_v2 %>% 
  select(-time2)
head(sleep_day_v2)
```

    ## # A tibble: 6 x 5
    ##           Id SleepDay  TotalSleepRecords TotalMinutesAsleep TotalTimeInBed
    ##        <dbl> <chr>                 <dbl>              <dbl>          <dbl>
    ## 1 1503960366 4/12/2016                 1                327            346
    ## 2 1503960366 4/13/2016                 2                384            407
    ## 3 1503960366 4/15/2016                 1                412            442
    ## 4 1503960366 4/16/2016                 2                340            367
    ## 5 1503960366 4/17/2016                 1                700            712
    ## 6 1503960366 4/19/2016                 1                304            320

``` r
# Plotting TotalMinutesAsleep vs TotalTimeInBed 
ggplot(data = sleep_day_v2) +
  geom_point(mapping = aes(x = TotalMinutesAsleep, y = TotalTimeInBed, color = TotalSleepRecords)) +
   scale_color_gradient(low = "#800080", high = "#FF00FF") +
  labs(title = "Time In Bed vs Minutes Asleep", x = "Minutes Asleep", y = "Time In Bed", col = "Sleep Record(s)")
```

![](data_analysis_files/figure-gfm/TotalMinutesAsleep%20vs%20TotalTimeInBed-1.png)<!-- -->

Instead of getting a linear relationship we got a somewhat dispersed
relationship. This means that **more time in bed doesn’t necessarily
represent more sleep**.

## Analysis Results

-   More sedentary hours show fewer steps.
-   People who have Very active minutes less than 60 have burned 3200
    calories or less while people with very active minutes greater than
    60 have burned more calories.
-   More time in bed doesn’t necessarily represent more sleep.
