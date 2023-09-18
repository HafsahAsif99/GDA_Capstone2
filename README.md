# GDA_Capstone2
Case Study 2: How Can a Wellness Technology Company Play It Smart?

---
title: 'DataAnalysisCaseStudy2: FitBit'
author: "Hafsah Asif"
date: "`r Sys.Date()`"
output: html_document
cran: https://cran.rstudio.com/
---

**HELP WAS TAKEN FROM GITHUB**

###Company Details and my role
Bellabeat is a high-tech manufacturer of health-focused products for women. My role in the company is as Junior Data Analyst and I am working with the marketing analyst team. Urška Sršen, co founder and Chief Creative Officer (CEO) of Bellabeat, believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. I have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices.

Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.

### Business Task 

Analyze smart device data to gain insight into how consumers are using their smart devices. I am also required to present the  analysis to the Bellabeat executive team along with high-level recommendations for Bellabeat’s marketing strategy.

### Introduction 

This is the capstone project for the Google Data Analytics Certification. Bellabeat data analysis case study includes all the data analysis process : 

  * Ask Phase
  * Prepare Phase
  * Process Phase
  * Analyze Phase
  * Share Phase
  * Act Phase
  
##Phase 1:** Inquiry Phase**
The Ask Phase involves a concise overview of the business objective, which revolves around the analysis of smart device data to extract insights into the usage patterns of Bellabeat's smart devices. This phase centers on achieving the following key objectives:

*Identifying prevailing trends in the utilization of smart devices.
*Assessing the potential relevance of these trends to Bellabeat's customer base.
*Exploring how these trends can inform and shape Bellabeat's marketing strategies.

Additionally, it is essential to define the primary recipients of the proposed solutions. Our primary stakeholders encompass:

***Urška Sršen:** Co-founder and Chief Creative Officer of Bellabeat.
***Sando Mur:**Mathematician and Co-founder of Bellabeat, occupying a pivotal role within the company's executive team.
***Bellabeat Marketing Analytics Team:** A specialized team of data analysts tasked with the responsibility of gathering, scrutinizing, and presenting data that serves as a guiding force for Bellabeat's marketing endeavors.

###Phase 2: Preparation Phase

The Preparation Phase revolves around the systematic organization of data, amalgamating information from diverse sources. Sršen has suggested leveraging a publicly accessible dataset that delves into the daily habits of smart device users. Specifically, we have chosen the "FitBit Fitness Tracker Data" dataset, accessible at (https://www.kaggle.com/datasets/arashnic/fitbit), and made accessible through Mobius.

This Kaggle dataset encompasses personal fitness tracker data from thirty Fitbit users who willingly contributed their personal tracker data, including minute-by-minute records pertaining to physical activity, heart rate, and sleep monitoring. The dataset encompasses details about daily activity levels, step counts, and heart rate metrics, facilitating a comprehensive exploration of user habits. The data is distributed across 18 CSV files.

Data Reliability & Limitations:

*Reliability: This data might be subject to sample selection bias as it may not be 
entirely representative of the broader population.

*Originality: The dataset comprises third-party information.

*Comprehensiveness: It offers comprehensive insights, encompassing all pertinent data for addressing the core business question.

*Currency: The data is somewhat dated, being six years old.

*Citations: The original sources of the data are unspecified.

Overall, the data source has been assessed as having certain limitations; however, it remains relevant for the purposes of this capstone project.

### Phase 3 : **Process Phase**

Process Phase includes processing the data by cleaning and ensuring that it is correct,relevant,complete and error free.

**Tools Used**

I am using **RStudio** for verifying data integrity, cleaning, transformation, analysis and visualization.

Firstly, need to install and read the packages we need for analysis.

I am using the "sqldf" package, which will allow us to emulate SQL syntax when looking at data.

```{r installing, echo=TRUE, eval=TRUE, cache=TRUE}
install.packages("sqldf", repos = "https://cran.rstudio.com/")
```
**Installing other packages:**

```{r installing2, echo = FALSE, warnings = FALSE, cache=TRUE}
install.packages("tidyverse",repos = "https://cran.rstudio.com/")
install.packages("lubridate",repos = "https://cran.rstudio.com/")
install.packages("ggplot2",repos = "https://cran.rstudio.com/")
install.packages("dplyr",repos = "https://cran.rstudio.com/")
install.packages("skimr",repos = "https://cran.rstudio.com/")
install.packages("janitor",repos = "https://cran.rstudio.com/")
install.packages("plotrix",repos = "https://cran.rstudio.com/")
```

**Loading the packages**
```{r echo = FALSE, warnings = FALSE, cache=TRUE}
library(sqldf)
library(tidyverse)
library(lubridate)
library(ggplot2)
library(dplyr)
library(skimr)
library(janitor)
library(plotrix)
```

**Loading the CSV Files:**
```{r echo = FALSE, warnings = FALSE, cache=TRUE}
daily_activity <- read.csv("C:\\Users\\Hafsah\\Downloads\\FitBit data\\Fitabase Data 4.12.16-5.12.16\\dailyActivity_merged.csv")
sleep_day <- read.csv("C:\\Users\\Hafsah\\Downloads\\FitBit data\\Fitabase Data 4.12.16-5.12.16\\sleepDay_merged.csv")
weight_log <- read.csv("C:\\Users\\Hafsah\\Downloads\\FitBit data\\Fitabase Data 4.12.16-5.12.16\\weightLogInfo_merged.csv")
daily_calories <- read.csv("C:\\Users\\Hafsah\\Downloads\\FitBit data\\Fitabase Data 4.12.16-5.12.16\\dailyCalories_merged.csv")
daily_steps <- read.csv("C:\\Users\\Hafsah\\Downloads\\FitBit data\\Fitabase Data 4.12.16-5.12.16\\dailySteps_merged.csv")
```

**Exploring the Data:**

### Daily Activity Data

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
colnames(daily_activity)
head(daily_activity)
str(daily_activity)
skim(daily_activity)
```

Creating month and day of week column as it is used in analysis.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
daily_activity$Rec_Date <- as.Date(daily_activity$ActivityDate,"%m/%d/%y")
daily_activity$month <- format(daily_activity$Rec_Date,"%B")
daily_activity$day_of_week <- format(daily_activity$Rec_Date,"%A")

colnames(daily_activity)
```

### Daily Calories Data

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
colnames(daily_calories)
head(daily_calories)
str(daily_calories)
skim(daily_calories)
```

### Sleeping Data

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
colnames(sleep_day)
head(sleep_day)
str(sleep_day)
skim(sleep_day)
```

###Weight Logs

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
colnames(weight_log)
head(weight_log)
str(weight_log)
skim(weight_log)
```

After Executing these commands we found out:

* Number of records and columns
* Number of null and non null values
* Data type of every columns

Also,

* There are no null values present in any of the data set, So there is no requirement to clean the data.
* The date column is in character format, so we need to convert it into datetime64 type

Counting unique IDs to confirm whether data has 30 IDs as claimed by the survey

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
n_distinct(daily_activity$Id)
```

There are **33** unique IDs, instead of 30 unique IDs as expected. Some users may have created additional IDs during the survey period.

Now the data cleaning and manipulation is done.
Now data is ready to be analyzed.

### Phase 4: **Analyze Phase**

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
daily_activity %>%  select(TotalSteps,TotalDistance,SedentaryMinutes,VeryActiveMinutes) %>% summary()
```

Based on the Summary of the daily_activity data:

* The average total steps per day is 7638 which is less than recommended 10000 steps.
* The average total distance per day is 5.490 km.
* The average sedentary minutes is 991.2 minutes or 16.52 hours which is very high as it should be at most 7 hours.(source: HealthyWA article)
* The average of very active minutes is 21.16 which is less than target of 30 minutes per day. (source:verywell fit)

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
summary(daily_calories)
```
* The daily average calories expended is 2304.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
summary(weight_log)

```
* The average of BMI is 25.19 which is slightly grater than the healthy BMI range which is between 18 and 24.9.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
n_distinct(weight_log$Id)
```

* Only 8 people weight_log is present.

### Phase 5 : ** Share Phase**

In this step, we will create some visualizations based on our analysis and goal of project.


```{r echo = FALSE, warnings = FALSE, cache=TRUE}
daily_activity$day_of_week <- ordered(daily_activity$day_of_week,levels=c("Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"))

ggplot(data=daily_activity) + geom_bar(mapping = aes(x=day_of_week),fill="black") +
  labs(x="Day of week",y="Count",title="No. of times users used tracker across week")
```

**Observation : ** 

As we can see, the frequency of usage of FitBit fitness tracker application is high on sunday, monday and tuesday than other week days.I think this behaviour is because people get busier in week end days due to work pressure and they don’t get enough time to track their activity.That’s why people are more active on sunday and starting 2 days of week.

#### The relationship between Steps taken in a day and Sedentary(people were inactive) minutes.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
ggplot(data=daily_activity, aes(x=TotalSteps, y=SedentaryMinutes, color = Calories)) + geom_point() +
geom_smooth(method = "loess",color="green") + 
labs(x="Total Steps",y="Sedentary Minutes",title="Total Steps vs Sedentary Minutes")
```

**Observations :**

Total steps taken vs sedentary minutes

I was expecting a totally inverse relationship between steps taken and sedentary minutes.

* At the start when the steps taken are less than 10000 the relation between them is inverse, but as number of steps increases beyond 10000 there is no drastic change in relation.
* I got surprised watching the relation between steps and sedentary minutes after 15000 steps as it becomes slightly positive.

#### The relationship between Very Active Minutes and Calories Burned.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
ggplot(data=daily_activity,aes(x = VeryActiveMinutes, y = Calories, color = Calories)) + geom_point() + 
geom_smooth(method = "loess",color="orange") +
labs(x="Very Active Minutes",y="Calories",title = "Very Active Minutes vs Calories Burned")
```

**Observations :**

Relation between very active minutes and calories burned

As we can see,very active minutes and calories burned are highly correlated with each other with some outliers at bottom left and top left of the plot.

#### The relationship between Sedentary Minutes and Calories Burned.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
ggplot(data=daily_activity,aes(x=SedentaryMinutes,y=Calories,color=Calories)) + geom_point() + 
geom_smooth(method="loess",color="red") + 
labs(y="Calories", x="Sedentary Minutes", title="Sedentary Minutes vs. Calories Burned")
```

**Observations :**

I was expecting the relation between sedentary minutes and calories burned to be totally inverse in nature.

* The data is showing positive correlation up to 1000 sedentary minutes.
* After 1000 sedentary minutes the relation is inverse as I expected.

#### The relationship between Sleep and Time in bed.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
ggplot(data=sleep_day, aes(x=TotalMinutesAsleep, y=TotalTimeInBed)) + geom_point() + stat_smooth(method = lm) +
  labs(x="Total Minutes a sleep", y="Total Time in Bed", title = "Sleep Time vs Time in Bed")
```

**Observations :**

* As we can see, there is a strong positive correlation between TotalMinutesAsleep and TotalTimeInBed, but there are some outliers in data in the middle and top of plot.
* The outliers are one who spend lot of time in bed but didn’t actually sleep. There can be different reasons for that.


#### Calculating the sum of individual minute column from daily activity data.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
activity_minute <- sqldf("SELECT SUM(VeryActiveMinutes),SUM(FairlyActiveMinutes),
SUM(LightlyActiveMinutes),SUM(SedentaryMinutes) 
FROM daily_activity")

activity_minute
```

Now, we will use these values to plot a 3D pie chart to compare the percentage of activity by minutes.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
x <- c(19895,12751,181244,931738)
x
piepercent <- round(100*x / sum(x), 1)
colors = c("red","blue","green","yellow")
 
pie3D(x,labels = paste0(piepercent,"%"),col=colors,main = "Percentage of Activity in Minutes")
legend("bottom",c("VeryActiveMinutes","FairlyActiveMinutes","LightlyActiveMinutes","SedentaryMinutes"),cex=0.6,fill = colors)
```

**Observations : **

As we can see,

* The percentage of sedentary minutes is very high than all other, which covers 81.3 % of pie this indicates that people are inactive for longer period of time.
* The percentage of very active and fairly active minutes is very less ie. 1.7%,1.1% respectively, which is very less compared to other activities.

#### Calculating sum of different distance values from daily activity data.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
activity_distance <- sqldf("SELECT SUM(ModeratelyActiveDistance),SUM(LightActiveDistance),
      SUM(VeryActiveDistance),SUM(SedentaryActiveDistance)
      FROM daily_activity")

activity_distance
```
**NOTE:** As we can see that the values of sedentaryActiveDistance is very less as compare to other distances,So I am excluding it in drawing a 3D pie chart to compare the percentage of activity in minutes.

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
y <- c(533.49,3140.37,1412.52)
y
piepercent <- round(100*y / sum(y), 1)
colors = c("orange","green","blue")
pie3D(y,labels = paste0(piepercent,"%"),col=colors,main = "Percentage of Activity in Distance",labelcex=1)
legend("bottom",c("ModeratelyActiveDistance","LightlyActiveDistance","VeryActiveDistance"),cex=0.6, fill = colors,y.intersp=1.5,)
```

**Observations : **

* The percentage of lightly active distance is highest with 61.7% and that of moderately active distance is 10.5%.
* The percentage of very active distance is 27.8% which is good, but it can be increased further so that people can achieve there fitness goals.

#### Calculating the count of people with over weight.

The BMI for healthy person is between 18.5 and 24.9 and the persons who’s BMI is above 24.9 are considered to be overweight.(source:CDC)
```{r echo = FALSE, warnings = FALSE, cache=TRUE}
count_overweight <- sqldf("SELECT COUNT(DISTINCT(Id))
                          FROM weight_log
                          WHERE BMI > 24.9")
count_overweight

```
*Plotting 3D pie chart to compare the percentage of people with overweight vs healthy weight.*

```{r echo = FALSE, warnings = FALSE, cache=TRUE}
z <- c(5,3)
piepercent <- round(100*z / sum(z),1)
colors = c("red","green")
pie3D(z,labels=paste0(piepercent,"%"),explode=0.1,col=colors,radius=1,main="Percentage of people with Over Weight vs Healthy Weight")
legend("bottom",c("OverWeight","HealthyWeight"),cex=0.6,fill=colors)

```

**Observations :**

* The percentage of people with over weight is 62.5% which is high as compared to percentage of people with healthy weigh which is 37.5%. So, there is a very good opportunity to increase the percentage of people with healthy weight.

### Phase 5 : **Act Phase**

**Based on our analysis I have following recommendations:**

1. We have analysed that most of the people use application to track the steps and calories burned;less number of people use it to track sleep and very few use it to track weight records.So, I will suggest to focus on step,calories and sleep tracking more in application.

2. People prefer to track their activities on sunday, monday and tuesday than other week days.I think this behaviour is because people get busier in week end days due to work pressure and they don’t get enough time to track their activity.That’s why people are more active on sunday and starting 2 days of week.

3. The relation between steps taken vs calories burned and very active minutes vs calories burned shows positive correlation.So, this can be a good marketing strategy.

4. Majority of users 81.3% who are using the FitBit app are inactive for longer period of time and not using it for tracking their health habits.So, this can be a great chance to use this information for market strategy as Bellabeat can alert people about their sedentary behaviour time to time either on application or on tracker itself .

5. Majority of the users 62.5% who are using fitness tracker are overweight.So, there is an opportunity to influence the people so that they can become healthier.

6. Bellabeat marketing team can encourage users by educating and equipping them with knowledge about fitness benefits, suggest different types of exercises, calories intake and burn rate information on Bellabeat application.
