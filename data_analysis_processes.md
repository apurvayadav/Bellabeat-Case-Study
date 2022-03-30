Data Analysis Processes
================
Apurva Yadav
2022-03-26

## The Ask Phase

### Guiding questions

1.  What is the problem you are trying to solve?  
    *Bellabeat wants to take insights from the smart device usage data
    and than apply these insights to on of their products.*

2.  How can your insights drive business decisions?  
    *Insights will help in driving decisions by providing necessary
    information about the deficiencies in the Bellabeat smart devices
    compared to other smart devices. By applying the insights to one
    Bellabeat device, It will be more clear as to where Bellabeat
    devices lag.*

### Business Task

*Analyze smart device usage data in order to gain insight into how
consumers use non-Bellabeat smart devices. Apply the insights to one
Bellabeat Device.*

### Key Stakeholders

-   **Urška Sršen** : Bellabeat’s cofounder and Chief Creative Officer
-   **Sando Mur**: Mathematician and Bellabeat’s cofounder; key member
    of the Bellabeat executive team
-   **Bellabeat marketing analytics team**: A team of data analysts
    responsible for collecting, analyzing, and reporting data that helps
    guide Bellabeat’s marketing strategy.

## The Prepare Phase

### Guiding questions

1.  Where is your data stored?  
    *Data is stored in multiple .csv files.*

2.  How is the data organized? Is it in long or wide format?  
    *Data is organanized in such a way that different participants have
    unique id and the dailyactivity_merged.csv file contains data for
    different dates of the users. Also it is in long format.*

3.  Are there issues with bias or credibility in this data? Does your
    data ROCCC?  
    *The data is credible as it is collected by amazon mechanical Turk.
    The number of participants is very less i.e. 30 so there can be
    sampling bias. Only fitbit trackers are used therefore more data
    should be collected to compare Bellabeat devices with other brands’
    devices. The data ROCCC.*

4.  How are you addressing licensing, privacy, security, and
    accessibility?  
    *The dataset is a part of [CC0: Public
    Domain](https://creativecommons.org/publicdomain/zero/1.0/).
    Therefore, one can copy, modify, distribute and perform the work,
    even for commercial purposes, all without asking permission.*

5.  How did you verify the data’s integrity?  
    *The data is downloaded from Kaggle, which makes it reliable for
    analysis and also it is collected by Amazon Mechanical Turk. The
    data has no metadata that makes it doubtful.*

6.  Are there any problems with the data?  
    *The data is stored in multiple files and in long format which makes
    it less accessible. Also the format is inconsistent at many places.*

## The Process Phase

### Guiding questions

1.  What tools are you choosing and why?  
    *I am using R. Because dailyactivity_merged.csv is a large dataset
    and cannot be handled by Google sheets.*

2.  Have you ensured your data’s integrity?  
    *I have ensured data’s integrity in the prepare phase.*

### Key tasks

-   *Checked data for errors.*
-   *Choosed R for the task.*
-   *Inspected the structure of data*
-   *Documented the process in R notebook.*

## The Analyze phase

### Key tasks

-   *Analyzed the data using R and documented the analysis process in R
    notebook.*

### Analysis Insights

-   More sedentary hours show less steps.
-   People who have Very active minutes less than 60 have burned 3200
    calories or less while people with very active minutes greater than
    60 have burned more calories.
-   More time in bed doesn’t necessary represent more sleep.

## The Share phase

### Guiding questions

1.  Were you able to answer the business questions?  
    *Yes, I was able to find some insights from the data that could help
    Bellabeat’s marketing strategy.*

2.  What story does your data tell?  
    *Looking at the data it could be clearly seen that people who are
    mostly sitting throughout the day are less active and tend to burn
    less calories. Also, the time in bed and time of sleep doesn’t
    correlate well, this shows that may be the users couldn’t sleep
    well. These insights can be used to influence marketing strategy of
    Bellabeat.*

3.  How do your findings relate to your original question?  
    *My findings relate well with the original question.*

4.  Who is your audience? What is the best way to communicate with
    them?  
    *The audience include Bellabeat’s Chief Creative Officer, A
    statistician and the marketing team of bellabeat. The best way to
    communicate them would be showing them graphs developed during the
    analysis phase. This wouldn’t be difficult to understand for the
    audience.*

### Key Tasks

-   *Created a Powerpoint presentation to share my findings.*
-   *Included the visualizations created during the analysis phase.*
-   *Tried to keep descriptive text very less on slides.*
-   *Added some speaker notes.*
