# case-study-practice-1
This project serves as the first hand-on practice on my data analytics skills. It is based on a given topic and guided by the pdf given from the course I am taking, and also mainly focuses on the skills on R during the analysis process.

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
Informed by Sršen, I am suggested to use the dataset from Kaggle, [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit). The dataset originated from zenodo.org, and uploaded by a team RTI International researchers, and it is thought to be a reliable research organisation, so the dataset has a relatively high credibility. However, the data are gathered through distributed survey via Amazon Mechanical Turk, this may create a bias that people not using that platform cannot be observed, whiile the data is not current compared to the time this report is made. The dataset is downloaded and uploaded to RStudio for further process, backups are also made.

#### Insepction 
The dataset contains two sets of data, including two one-month observations of 30 eligible Fitbit users' tracker data. They have a long format that each person may have multiple entries accross different points of time, so it requires some organisations later. Some of the information is missing too, for example, in the weightLogInfo_merged.csv, there are only 11 people's data, which is far from 30. Inside the table, some records are empty too, and these happened in other spreadsheets as well. 

```
install.packages('ggfortify')
```
