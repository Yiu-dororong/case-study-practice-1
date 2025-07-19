# case-study-practice-1
This project serves as the first hand-on practice on my data analytics skills. It is based on a given topic and with some guidances from the course I am taking, and also mainly focuses on the skills on R during the analysis process. It aims to show all the procedure and thought process here. If you looks for a completion of work, say, for presentation or summary, I highly recommend to view another files instead.

## Introduction
Imagine I were a junior data analyst in Bellabeat, a high-tech manufacturer of health-focused products, and I were asked to gain insight from smart device data to develop marketing strategy of one of their products. This should be reported to the Bellabeat executive team.

## Background
*The following information are from the pdf provided by the course.*
### Company
Urška Sršen and Sando Mur founded Bellabeat, a high-tech company that manufactures health-focused smart products. Sršen used her background as an artist to develop beautifully designed technology that informs and inspires women around the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.

By 2016, Bellabeat had opened offices around the world and launched multiple products. Bellabeat products became available through a growing number of online retailers in addition to their own e-commerce channel on their website. The company has invested in traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively. Bellabeat invests year-round in Google Search, maintaining active Facebook and Instagram pages, and consistently engages consumers on Twitter. Additionally, Bellabeat runs video ads on Youtube and display ads on the Google Display Network to support campaigns around key marketing dates.

Sršen knows that an analysis of Bellabeat’s available consumer data would reveal more opportunities for growth. She has asked the marketing analytics team to focus on a Bellabeat product and analyze smart device usage data in order to gain insight into how people are already using their smart devices. Then, using this information, she would like high-level recommendations for how these trends can inform Bellabeat marketing strategy.

### Products 
* Bellabeat app: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and
make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
* Leaf: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connectsto the Bellabeat app to track activity, sleep, and stress.
* Time: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
* Spring: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
* Bellabeat membership: Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness based on their lifestyle and goals.

### Characters
* Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer
* Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
* Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’’s mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.


## Roadmap
The data analysis process will be divided into six stages, 
* ask 
* prepare 
* process 
* analyze 
* share
* act

which will be proceeded accordingly.

### Ask
The initial objective presented to me is pretty vague, let make the goal clearer and define the business task.
After communication, Sršen asks you to analyze smart device usage data in order to gain insight into how consumers use non-Bellabeat smart devices.
Therefore, the business task is likely to be "Identify trends in smart device from non-Bellabeat smart devices, and then compare the one from Bellabeat smart devices to see if any adjustment to current marketing strategy".
(For example, if a significant growing trend on smart watch is observed and the company has not developed into smart watch, the compaany may consider invest more on smart watch.)
The stakesholders will mainly be the cofounders, and the marketing analytics team. 

### Prepare
Informed by Sršen, I am suggested to use the dataset from Kaggle, [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit). The dataset originated from zenodo.org, and uploaded by a team RTI International researchers, and it is thought to be a reliable research organisation, so the dataset has a relatively high credibility. However, the data are gathered through distributed survey via Amazon Mechanical Turk, this may create a bias that people not using that platform cannot be observed, while the data is not current compared to the time this report is made. The dataset is downloaded and uploaded to RStudio for further process, backups are also made. More details on data format can be found in [here](https://support.mydatahelps.org/hc/en-us/sections/360008888093-Fitbit-Data-Exports).

#### Insepction 
The dataset contains two sets of data, including two one-month observations of 30 eligible Fitbit users' tracker data. They have a long format that each person may have multiple entries accross different points of time, so it requires some organisations later. Some of the information is missing too, for example, in the weightLogInfo_merged.csv, there are only 11 people's data, which is far from 30. Inside the table, some records are empty too, and these happened in other spreadsheets as well. 

### Process
For this analysis, I choose to use RStudio as it is a all-in-one tool, SQL is also a good option, considering the amount of data, but I will try it on my next practice.
To begin with, let's load the dataset into Rstudio.
```
dailyActivity <- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/dailyActivity_merged.csv")
heartrate_seconds<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/heartrate_seconds_merged.csv")
hourlyCalories<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/hourlyCalories_merged.csv")
hourlyIntensities<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/hourlyIntensities_merged.csv")
hourlySteps<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/hourlySteps_merged.csv")
minuteCaloriesNarrow<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/minuteCaloriesNarrow_merged.csv")
minuteIntensitiesNarrow<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/minuteIntensitiesNarrow_merged.csv")
minuteMETsNarrow<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/minuteMETsNarrow_merged.csv")
minuteSleep<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/minuteSleep_merged.csv")
minuteStepsNarrow<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/minuteStepsNarrow_merged.csv")
weightLogInfo<- read.csv("D://mturkfitbit/Fitabase Data 3.12.16-4.11.16/weightLogInfo_merged.csv")
```
Now, I will briefly look into each data frames, by using ```str```, ```head```, ```summary``` functions, but before that, make sure the ```tidyverse``` packages is applied.
```
library(tidyverse)
head()
str()
summary()
```
I discovered some formatting problems in the dataset,
```
> str(weightLogInfo)
'data.frame':	33 obs. of  8 variables:
 $ Id            : num  1.50e+09 1.93e+09 2.35e+09 2.87e+09 2.87e+09 ...
 $ Date          : chr  "4/5/2016 11:59:59 PM" "4/10/2016 6:33:26 PM" "4/3/2016 11:59:59 PM" "4/6/2016 11:59:59 PM" ...
 $ WeightKg      : num  53.3 129.6 63.4 56.7 57.2 ...
 $ WeightPounds  : num  118 286 140 125 126 ...
 $ Fat           : int  22 NA 10 NA NA NA NA NA NA NA ...
 $ BMI           : num  23 46.2 24.8 21.5 21.6 ...
 $ IsManualReport: chr  "True" "False" "True" "True" ...
 $ LogId         : num  1.46e+12 1.46e+12 1.46e+12 1.46e+12 1.46e+12 ...
```
the data type of ```Date``` is recorded as character, but not date; whereas ```IsManualReport``` column has the same problem, the date type being character rather than logical.
To fix this, the following can be applied,
```
weightLogInfo %>% 
  mutate(weightLogInfo,NewDate = mdy_hms(Date)) %>%
  mutate(weightLogInfo,IsManualReport_logical = as.logical(IsManualReport)) %>%
  str()
```
and the data types will be adjusted in new columns.
```
'data.frame':	33 obs. of  10 variables:
 $ Id                    : num  1.50e+09 1.93e+09 2.35e+09 2.87e+09 2.87e+09 ...
 $ Date                  : chr  "4/5/2016 11:59:59 PM" "4/10/2016 6:33:26 PM" "4/3/2016 11:59:59 PM" "4/6/2016 11:59:59 PM" ...
 $ WeightKg              : num  53.3 129.6 63.4 56.7 57.2 ...
 $ WeightPounds          : num  118 286 140 125 126 ...
 $ Fat                   : int  22 NA 10 NA NA NA NA NA NA NA ...
 $ BMI                   : num  23 46.2 24.8 21.5 21.6 ...
 $ IsManualReport        : chr  "True" "False" "True" "True" ...
 $ LogId                 : num  1.46e+12 1.46e+12 1.46e+12 1.46e+12 1.46e+12 ...
 $ NewDate               : POSIXct, format: "2016-04-05 23:59:59" "2016-04-10 18:33:26" "2016-04-03 23:59:59" "2016-04-06 23:59:59" ...
 $ IsManualReport_logical: logi  TRUE FALSE TRUE TRUE TRUE TRUE ...
```

Considering there are many spreadsheets, it would be great to merge them together. Let's take dailyActivity as the main sheet, and review what columns there are.
```
> str(dailyActivity)
'data.frame':	457 obs. of  15 variables:
 $ Id                      : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ ActivityDate            : chr  "3/25/2016" "3/26/2016" "3/27/2016" "3/28/2016" ...
 $ TotalSteps              : int  11004 17609 12736 13231 12041 10970 12256 12262 11248 10016 ...
 $ TotalDistance           : num  7.11 11.55 8.53 8.93 7.85 ...
 $ TrackerDistance         : num  7.11 11.55 8.53 8.93 7.85 ...
 $ LoggedActivitiesDistance: num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveDistance      : num  2.57 6.92 4.66 3.19 2.16 ...
 $ ModeratelyActiveDistance: num  0.46 0.73 0.16 0.79 1.09 ...
 $ LightActiveDistance     : num  4.07 3.91 3.71 4.95 4.61 ...
 $ SedentaryActiveDistance : num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveMinutes       : int  33 89 56 39 28 30 33 47 40 15 ...
 $ FairlyActiveMinutes     : int  12 17 5 20 28 13 12 21 11 30 ...
 $ LightlyActiveMinutes    : int  205 274 268 224 243 223 239 200 244 314 ...
 $ SedentaryMinutes        : int  804 588 605 1080 763 1174 820 866 636 655 ...
 $ Calories                : int  1819 2154 1944 1932 1886 1820 1889 1868 1843 1850 ...
```
Some information, such ```TotalSteps``` and ```Calories``` are already included, so the corresponding sheets, hourlySteps and hourlyCalories, can be omitted unless more details are needed.
The only extra information are intensity, heartrate, METs, sleeping time and weight log.
However, after some research, Fitbit use heartrate and METs to create some high level data, such as intensity and classification of active minutes. 
I will come back to these data if needed.

Now, lets organise the sheets about sleeping time and weight log.
For the sleeping time one, since it is in a long format that check whether the user is sleeping in every minute, so I run this code to find more metadata

```
## calculate each duration of sleeping session and date of sleep by logId
SleepSessionTime <-
  minuteSleep %>% 
  mutate(minuteSleep, NewDate = mdy_hms(date)) %>%
  group_by(Id,logId) %>% 
  summarise(sleep_sec = max(NewDate) - min(NewDate), sleep_date = min(NewDate)) 
## below is to find average time per sleeping session
   group_by(Id) %>% 
   summarise(mean_sleep_sec = mean(sleep_sec))
```

It turns out that some people have a habit of taking a nap, which may need to switch to calculate sleeping per day instead of per session, and there seems to be inaccurate measurement, such as for ```Id``` 2022484408 and 7007744171, their mean sleeping time is below 3 hours, which does not make sense. I shall discard them when I have to use this data.

On the weightLogInfo table, there are serveral duplicates for some people. They have multiple measurement across the period of time. I will pick the most recent as reference, if needed. Also, since almost all the columns inside can be concluded into BMI. By rewriting the code used before to change the format with some tweaks, a newly cleaned data frame is created.

```
## store in a new data frame
BMIInfo <-
  weightLogInfo %>%
## change of format in advance
  mutate(weightLogInfo,NewDate = mdy_hms(Date)) %>%
  mutate(weightLogInfo,IsManualReport_logical = as.logical(IsManualReport)) %>%
## choose the lastest entry for each iD
  group_by(Id) %>%
  filter(NewDate == max(NewDate))
## optional: can add a line of select() to select the desired columns 
```

Note that by running the ```distinct()``` command, it is found that there are only 11 people's BMI and 23 people's sleeping time, which means that not 30 respondants' data are collected, and, to be clear, in the dailyActivity sheet, there are 35 people. 

Now, let's move on to the dailyActivity sheet. I would like to address that, by definition,
TotalDistance = TrackerDistance + LoggedActivitiesDistance = VeryActiveDistance + ModeratelyActiveDistance + LightActiveDistance + SedentaryActiveDistance
VeryActiveMinutes + FairlyActiveMinutes + LightlyActiveMinutes + SedentaryMinutes should be 1440 (minutes) which equals to a whole day, but the following code clearly shows that some entries do not, so I shall keep this in mind that this may not be a good indicator.

```
dailyActivity <- dailyActivity %>% 
  mutate(dailyActivity,TotalRecordedMinutes = VeryActiveMinutes + FairlyActiveMinutes + LightlyActiveMinutes + SedentaryMinutes) %>%
  mutate(dailyActivity,Date = mdy(ActivityDate))
```



Another run of  ```summary()``` and ```str()``` commands is executed to verify there are no problems before further process.


By a simple plot, we can observe that TotalSteps is positively variated with TotalDistance.
```
ggplot(data = dailyActivity) +
geom_point(mapping = aes(x=TotalSteps, y=TotalDistance))
```

And by a pie chart, we see that higher intensity does not mean making up fewer proportion.
```
library('scales')
  
distance_intensity <- data_frame(
distance_intensity_type = c("LightActive", "ModeratelyActive", "VeryActive"),
all_respondants_distance_by_intensity = c(sum(MasterList$TotalLightActiveDistance), sum(MasterList$TotalModeratelyActiveDistance), sum(MasterList$TotalVeryActiveDistance)),
intensity_percent = round((all_respondants_distance_by_intensity / sum(all_respondants_distance_by_intensity))*100,1),
)

distance_intensity <- distance_intensity %>% 
  arrange(desc(distance_intensity_type)) %>%
  mutate(prop = all_respondants_distance_by_intensity / sum(distance_intensity$all_respondants_distance_by_intensity) ) %>%
  mutate(ypos = (cumsum(prop)- 0.5*prop)) 

ggplot(distance_intensity, aes(x="", y=prop, fill=distance_intensity_type )) +
  geom_bar(stat="identity", width=1) +
  coord_polar("y", start=0) +
  theme_void() +
  labs(title="Proportion of different intensity of distance \n among all respondants")+
  theme(legend.position="none",plot.title = element_text(hjust = 0.5, size = 20))+
  geom_text(aes(y = ypos, label = distance_intensity_type), color = "white", size=5) +
  geom_text(aes(x=1.6,y = ypos, label = percent(intensity_percent,scale = 1,suffix = "%") ), color = "black", size=5) 
  scale_fill_brewer(palette="Set1")
```
In terms of total distance, it is composed by 64% of light active, 10% of moderately active, and 26% of very active. This may imply there are two extremes, very people choose to have a moderately active activity.

I further investigate the relationship between number of steps and calories, it is found that they are positively related, but at a mimimal correlation.
```
#relationship between steps and calories
ggplot(data = MasterList,aes(x=NewTotalDistance, y=TotalCalories)) +
  geom_point()+
  geom_smooth(method="loess")+
  labs(title="TotalSteps vs TotalCalories")+
  theme(plot.title = element_text(hjust = 0.5))
```

 Next, I moved on to find if there is any relationship between BMI and daily distance. Since they are data from two different sheets, I have to merge them first. I also classify respondants' healthiness based on BMI, depsite being considered as a outdated and inaccurate measure. Yet, no clear correlation is found. 
 ```
  MasterList <- left_join(MasterList,BMIInfo)  
    BMIpos <- c(14,22,27,35)
    BMIcategory <- c("Underweight","Normal","Overweight","Obese")
    MidDist <-max((MasterList$AvgSteps)-min(MasterList$AvgSteps)) /2
    
  ggplot(data = MasterList) +
    geom_point(mapping = aes(x=AvgSteps, y=BMI))+
    labs(title="Average Steps vs BMI")+
    theme(plot.title = element_text(hjust = 0.5))+
    ylim(10,50)+
    geom_hline(aes(yintercept = 18.5))+
    geom_hline(aes(yintercept = 25))+
    geom_hline(aes(yintercept = 30))+
    annotate('text', x=MidDist, y=BMIpos, label=BMIcategory, size=4)
  ```

Furthermore, I tried to investigate the correlation sleep time and number of steps.
```
  SleepInfo<-
  SleepSessionTime %>% 
    mutate(sleep_day = date(sleep_date)) %>% 
    group_by(Id) %>% 
    summarise(daily_sleep_time = sum(sleep_sec)/n_distinct(sleep_day))
  
  SleepInfo <- SleepInfo[!(SleepInfo$Id %in% c(1644430081,1844505072,2022484408,7007744171)),]

  MasterList <- left_join(MasterList, SleepInfo)

  ggplot(data = MasterList,aes(x=AvgSteps, y=daily_sleep_time/3600)) +
    geom_point()+
    labs(title="Daily Steps vs Daily Sleeping Time")+
    theme(plot.title = element_text(hjust = 0.5))+
    xlab("Daily Steps")+
    ylab("Daily Sleeping Time (hour)")+
    geom_smooth(method='lm',se = FALSE)
  ```
Due to the limited data points, the trend is not apparent. However, one can observed that when daily steps increase, the daily sleeping time also increases in general.

Last but not least, we would also like to find out the trend of the device usage.

There is no clear trend against the day of usage.
```
dailyActivity %>% 
  mutate(dailyActivity,Day = wday(Date, label = TRUE)) %>% 
  group_by(Day) %>% 
  summarise(median_usage = median(TotalRecordedMinutes), mean_usage = mean(TotalRecordedMinutes))
```
Other schema cannot be used, as this may cause an observer bias. For example, one does not want wear the watch during sports, the time of device usage and active minutes will both decrease, so it is inaccurate to make correlation between them.

```
ggplot(data = dailyActivity, aes(TotalRecordedMinutes))+ 
  stat_ecdf(geom = "step")+
  xlim(0,1440)+
  labs(title = "Cumulative Relative Frequency of Daily Usage")+
  xlab("Cumulative Relative Frequency")+
  ylab("Daily Usage")
```
This plot gives a overview how frequent the device is used. It revealed that only a half of the recorded usage showed that the respondant wears it whole day (24hours). Around one-fourth of the them wear less than 16 hours. It is uncertain whether this is due to "they do not wear them at sleep".
```
dailyActivity <- dailyActivity %>% 
  mutate(SedProp =SedentaryMinutes/TotalRecordedMinutes)
```
This calculated the propation of sedentary minutes over total recorded minutes. I am interest how is the actual usage from the view of activeness.

```
ggplot(data = dailyActivity)+
  geom_point(mapping = aes(x=TotalRecordedMinutes, y=SedProp))+
  labs(title="Total Usage vs Sedentary Proportion")+
  theme(plot.title = element_text(hjust = 0.5))+
  xlim(0,1440)+
  annotate("rect",xmin = 750,xmax = 1440,ymin = 0.5,ymax = 1.0,alpha = 0.2)+
  annotate('text', x=100, y=0.92, label=0.9, size=4)+
  geom_hline(yintercept = 0.9)+
  xlab("Total Usage")+
  ylab("Sedentary Proportion")
```
This plot tries to correlate the sedentary proportion of the usage. One can tell from the graph,
(1) Most people are in the first quadrant (usage more than 12 hours, sedentary proportion greater than 0.5)
(2) A clear stack of points on x=1440, which means wear it full day
(3) A few points is above the line y=0.9, meaning some highly inactive usage are recorded. Especially some records are having 100% sedentary proportion, this may imply the respondant is totally idle or suffer from illness. It is very likely to be not wearing it and leaving it on.

### Share
As some of the findings and insight already mentioned above, I will make a conclusion here.

(1) Usage
Some cases of complete idle, or highly inactive usage are found. 
Not everyone wears it whole day, only a half of them wear them frequently.
Even fewer people wear it during sleeping

(2) Health
BMI is a outdated measurement, and should be avoid.
Very little correlation was found
More steps give more distances and also more calories
Intensity of distance: Moderately Active (10%) < Very Active (26%) < Light Active (64%), which is unexpected to see the most active category being second place

(3) Limitation
Dataset has limited data. More extensive datasets can be used, such as a longer period or accross different products.

### Act
Let's further relate these insight to what can be done.

(1) Design a better device that is more user-friendly that will yield higher usage time, and so provide more accurate evaluation to users

(2) Develop notification system as there are some cases that having high idling time to avoid miscalculation. A further step can be send reminder to user to enourage health management.

(3) Extend wider metrics to measure healthiness. For example, BMI is not that accurate, and the correlation between steps and calories is weak, this may imply there is still a lot of factor contribute to calories. 

