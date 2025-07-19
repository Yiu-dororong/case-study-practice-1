# Case Study Practice 1 (ft. R) 
This project serves as the first hand-on practice on my data analytics skills. It is based on a given topic and with some guidances from the course I am taking, and also mainly focuses on the skills on R during the analysis process. It aims to show all the procedure and thought process here. If you looks for a completion of work, say, for presentation or summary, I highly recommend to view another files instead.

## Introduction
Imagine I were a junior data analyst in Bellabeat, a high-tech manufacturer of health-focused products, and I were asked to gain insight from smart device data to produce high-level recommendations for marketing strategy of one of their products. 

## Background
*Some of the key information are excerpt from the guidance given by the course.*

### Products 
There are several products that are available for choice, which are Bellabeat app, Leaf, Time, Spring and Bellabeat membership. As I was suggested to use Fitbit (smartwatch) to perform the analysis, I am leaned to choose accessory type products, like the followings:

* Leaf: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
* Time: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.

and I believe *Time* is the closest match, and so *Time* would be my choice.

### Stakeholders
* Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer
* Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
* Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’’s mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.


## Roadmap
The data analysis process will be divided into six stages, 
* Ask 
* Prepare 
* Process 
* Analyze 
* Share
* Act

which will be proceeded accordingly.

### Ask
The initial objective presented to me is pretty vague, let make the goal clearer and define the business task.

After communication, I was asked to analyze smart device usage data in order to gain insight into how consumers use non-Bellabeat smart devices.
Therefore, the business task is likely to be "Identify trends in smart device usage from non-Bellabeat smart devices, and look for any discoveies that can help improve the current marketing strategy of *Time*".

### Prepare
Informed by Sršen, I am suggested to use the dataset from Kaggle, [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit). The dataset originated from [zenodo.org](https://zenodo.org/records/53894#.YMoUpnVKiP9), and uploaded by a team RTI International researchers, and RTI International is thought to be a reliable research organisation, so the dataset has a relatively high credibility. However, the data are gathered through distributed survey via Amazon Mechanical Turk, this may create a bias that people not using that platform cannot be observed. Meanwhile, the data is not current compared to the time this report is made. The dataset is downloaded and uploaded to RStudio for further process, backups are also made. More details on data format can be found in [here](https://support.mydatahelps.org/hc/en-us/sections/360008888093-Fitbit-Data-Exports).

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
Now, I will briefly look into each data frames, by using ```str```, ```head```, ```summary``` functions, but before that, make sure the ```tidyverse``` packages are all loaded in.
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

Considering there are many spreadsheets, it would be great to merge them together. Let's treat dailyActivity as the major sheet, and review what columns there are.
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

However, after some research, Fitbit use heartrate and METs to create some high level data, such as intensity and classification of active minutes, I will come back to these data if needed.

Now, lets organise the sheets about sleeping time and weight log.
For the sleeping time one, since it is in a long format that check whether the user is sleeping in every minute, so I run this code to find more metadata

```
## Calculate each duration of sleeping session and date of sleep by logId
SleepSessionTime <-
  minuteSleep %>% 
  mutate(minuteSleep, NewDate = mdy_hms(date)) %>%
  group_by(Id,logId) %>% 
  summarise(sleep_sec = max(NewDate) - min(NewDate), sleep_date = min(NewDate)) 
## Optional: Find average time per sleeping session
   group_by(Id) %>% 
   summarise(mean_sleep_sec = mean(sleep_sec))
```

It turns out that some people have a habit of taking a nap, which may need to switch to calculate sleeping per day instead of per session, and there seems to be inaccurate measurement, such as for ```Id``` 2022484408 and 7007744171, their mean sleeping time is below 3 hours, the same goes for 1644430081 and 1844505072, having a exceptional high sleeping hours, which does not seem to accurate measurement. I shall discard them when I have to use this data.

On the ```weightLogInfo``` table, there are serveral duplicates for some people, because they have multiple measurement across the period of time. I will pick the most recent as reference. Also, since almost all the columns inside can be concluded into BMI. By rewriting the code used before to change the format with some tweaks, a newly cleaned data frame is created.

```
## Store in a new data frame
BMIInfo <-
  weightLogInfo %>%
## Change of format 
  mutate(weightLogInfo,NewDate = mdy_hms(Date)) %>%
  mutate(weightLogInfo,IsManualReport_logical = as.logical(IsManualReport)) %>%
## Choose the lastest entry for each iD
  group_by(Id) %>%
  filter(NewDate == max(NewDate))
## Optional: can add a line of select() to select the desired columns 
```

Note that by running the ```distinct()``` command, it is found that there are only 11 people's BMI and 23 people's sleeping time, which means that not all respondants' data are collected, and, to be clear, in the ```dailyActivity``` sheet, there are 35 people. 

Now, let's move on to the ```dailyActivity``` sheet. I would like to address that, by definition,
TotalDistance = TrackerDistance + LoggedActivitiesDistance = VeryActiveDistance + ModeratelyActiveDistance + LightActiveDistance + SedentaryActiveDistance
VeryActiveMinutes + FairlyActiveMinutes + LightlyActiveMinutes + SedentaryMinutes should be 1440 (minutes) which equals to a whole day, but the following code clearly shows that some entries do not, so I shall keep this in mind that this may not be a good indicator. On the other hand, this is good metric to view their daily usage.

```
## Insert new columns for total recorded minutes per day.
dailyActivity <- dailyActivity %>% 
  mutate(dailyActivity,TotalRecordedMinutes = VeryActiveMinutes + FairlyActiveMinutes + LightlyActiveMinutes + SedentaryMinutes) %>%
  mutate(dailyActivity,Date = mdy(ActivityDate))
```

Another run of  ```summary()``` and ```str()``` commands is executed to verify there are no problems before further process.


### Analyze

By a simple plot, we can observe that TotalSteps is positively variated with TotalDistance.
```
ggplot(data = dailyActivity) +
geom_point(mapping = aes(x=TotalSteps, y=TotalDistance))
```
<img width="661" height="682" alt="totalsteps vs totaldist" src="https://github.com/user-attachments/assets/6e73f8a3-1085-4d6d-81f0-6747b5333c8d" />

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
<img width="661" height="687" alt="pie chart" src="https://github.com/user-attachments/assets/9b9ad5fe-1049-4817-b5ca-a091ed5205e9" />

In terms of total distance, it is composed by 64% of light active, 10% of moderately active, and 26% of very active. This may imply there are two extremes, very people choose to have a moderately active activity.

I further investigate the relationship between number of steps and calories, it is found that they are positively related, but at a mimimal correlation.
```
#Relationship between steps and calories
ggplot(data = MasterList,aes(x=NewTotalDistance, y=TotalCalories)) +
  geom_point()+
  geom_smooth(method="loess")+
  labs(title="TotalSteps vs TotalCalories")+
  theme(plot.title = element_text(hjust = 0.5))
```
<img width="661" height="687" alt="smooth" src="https://github.com/user-attachments/assets/059edf4d-d58b-4c13-91c0-320a3a2713e2" />


 Next, I moved on to find if there is any relationship between BMI and daily distance. Since they are data from two different sheets, I have to merge them first by creating a new sheet called ```MasterList```. I also classify respondants' healthiness based on BMI, depsite being considered as a outdated and inaccurate measure. Yet, no clear correlation is found. 
 ```
## Create a new master list and further refine the data
MasterList <- dailyActivity %>% 
 group_by(Id) %>% 
 summarise(AvgSteps=mean(TotalSteps),NewTotalDistance=sum(TotalDistance), TotalVeryActiveDistance = sum(VeryActiveDistance), TotalModeratelyActiveDistance = sum(ModeratelyActiveDistance), TotalLightActiveDistance = sum(LightActiveDistance), TotalCalories=sum(Calories) )

## Combining with BMI 
MasterList <- left_join(MasterList,BMIInfo)  
    BMIpos <- c(14,22,27,35)
    BMIcategory <- c("Underweight","Normal","Overweight","Obese")
    MidDist <-max((MasterList$AvgSteps)-min(MasterList$AvgSteps)) /2

## Plot with BMI against Average Steps, with BMI classifications
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

<img width="661" height="687" alt="steps vs bmi" src="https://github.com/user-attachments/assets/7dac3ee7-c01e-45e8-9327-3eb706825805" />


Furthermore, I tried to investigate the correlation sleep time and number of steps. Keeping in mind that some outliers mentioned before should be remove.
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

<img width="661" height="687" alt="steps vs sleep" src="https://github.com/user-attachments/assets/1f5c5ad6-cdb1-4bf2-bb99-b02cb6c759bc" />


Due to the limited data points, the trend is not apparent. However, one can observed that when daily steps increase, the daily sleeping time also increases in general.

Last but not least, we would also like to find out the trend of the device usage.

There is no clear trend against the day of usage.
```
dailyActivity %>% 
  mutate(dailyActivity,Day = wday(Date, label = TRUE)) %>% 
  group_by(Day) %>% 
  summarise(median_usage = median(TotalRecordedMinutes), mean_usage = mean(TotalRecordedMinutes))
```
(It automatically give Chinese, but it is Sunday to Saturday for observations 1 to 7)
```
# A tibble: 7 × 3
  Day   median_usage mean_usage
  <ord>        <dbl>      <dbl>
1 週日          1440      1204.
2 週一          1440      1234.
3 週二          1026      1007.
4 週三          1440      1233.
5 週四          1440      1254.
6 週五          1440      1271.
7 週六          1440      1198.
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

<img width="661" height="687" alt="cum fr" src="https://github.com/user-attachments/assets/8485cb03-454c-4eaf-95a7-7e98e5f51b3d" />

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

<img width="661" height="687" alt="sen prop" src="https://github.com/user-attachments/assets/5ea19f27-570f-4dd7-bbd3-71ccd3842a7b" />


This plot tries to correlate the sedentary proportion of the usage. One can tell from the graph,

(1) Most people are in the first quadrant (usage more than 12 hours, sedentary proportion greater than 0.5)

(2) A clear stack of points on x=1440, which means wear it full day

(3) A few points is above the line y=0.9, meaning some highly inactive usage are recorded. Especially some records are having 100% sedentary proportion, this may imply the respondant is totally idle or suffer from illness. It is very likely to be not wearing it and leaving it on.

### Share
As some of the findings and insight already mentioned above, I will make a brief conclusion here.

(1) **Usage**

Some cases of complete idle, or highly inactive usage are found. 
Not everyone wears it whole day, only a half of them wear them frequently.
Even fewer people wear it during sleeping

(2) **Health**

BMI is a outdated measurement, and should be avoid.
Very little correlation was found
More steps give more distances and also more calories
Intensity of distance: Moderately Active (10%) < Very Active (26%) < Light Active (64%), which is unexpected to see the most active category being second place

(3) **Limitation**

Dataset has limited data. More extensive datasets can be used, such as a longer period or accross different products to give a more comprehensive analysis.

### Act
Let's further relate these insight to what can be done.

(1) Design a better device that is more user-friendly that will yield higher usage time, and so provide more accurate evaluation to users

(2) Develop notification system as there are some cases that having high idling time to avoid miscalculation. A further step can be send reminder to user to enourage health management.

(3) Extend wider metrics to measure healthiness. For example, BMI is not that accurate, and the correlation between steps and calories is weak, this may imply there is still a lot of factor contribute to calories. 

