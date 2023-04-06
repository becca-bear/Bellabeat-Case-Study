# Bellabeat-Fitness-App-Case-Study

This project is a data analysis of the usage patterns and trends of the Bellabeat fitness tracker app. 

#

This case study will be following the six steps of the data analysis process:



### [Ask](#1-ask)
### [Prepare](#2-prepare)
### [Process](#3-process)
### [Analyze](#4-analyze)
### [Share](#5-share)
### [Act](#6-act)



# Scenario

Bellabeat is a high-tech manufacturer of health-focused products for women. They have the potential to become a larger player in the global smart device market, but to do so, they need to unlock new growth opportunities. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart device fitness data could help the company achieve this goal. As a junior data analyst working on the marketing analyst team, I was asked to focus on one of Bellabeat's products and analyze smart device data to gain insights into how consumers are using their smart devices. My findings will help guide marketing strategy for the company.




# Ask

### Business Task: The goal of this analysis is to guide the marketing strategy for the company and help Bellabeat unlock new growth opportunities in the global smart device market. The ultimate business task is to increase sales and market share for Bellabeat's products.

### Bellabeat Products

> 1. **Bellabeat app:** The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
> 2. **Leaf:** Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
> 3. **Time:** This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
> 4. **Spring:** This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
> 5. **Bellabeat membership:** Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness based on their lifestyle and goals.

### The Stakeholders:

> - **Urška Sršen:** Bellabeat’s cofounder and Chief Creative Officer. 
> - **Sando Mur:**  Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team.
> - **Bellabeat marketing analytics team:** A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy.


This analysis will be based on these questions:

1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat marketing strategy?



# Prepare

### Data Source: https://www.kaggle.com/datasets/arashnic/fitbit

 * A total of 30 users consented to the submission of personal tracker data.
* The data set was generated by respondents to a distributed survey via Amazon Mechanical Turk. 
Link: https://zenodo.org/record/53894#.ZCr07-zMJ-W
* The data is not comprehensive as it lacks additional information, such as age, gender, ethnicity which could improve the accuracy of any analysis.
* The data is not current as it was obtained seven years ago.
* The data has been cited.




This analysis will be conducted using R Studio, which offers a wide range of packages and data visualization tools for effectively exploring the data.

Data was cleaned in Google Sheets prior to starting this analysis. 



# Process



To begin, I will import the files into R Studio and create data frames with concise names:


```
daily_activity <- read_csv("dailyActivity_merged.csv")
weight_info <- read_csv("weightLogInfo_merged.csv")
daily_sleep <- read_csv("sleepDay_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
heart_rate_sec <- read.csv("heartrate_seconds_merged.csv")
minute_METs <- read.csv("minuteMETsNarrow_merged.csv")
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
```

 
 
I need to make sure that all data was imported accurately, which can be done by using the head() and glimpse() functions.

```
head(daily_activity)
```
![Screen Shot 2023-04-03 at 3 25 55 PM](https://user-images.githubusercontent.com/66655353/229650637-07755b81-af4a-45d3-93a4-369ab533b8e6.png)


```
glimpse(daily_activity)
```
![Screen Shot 2023-04-03 at 4 03 50 PM](https://user-images.githubusercontent.com/66655353/229650698-5f871562-b66e-4bce-885b-db7058aa0ba6.png)





Next, I will check the number of participants in each data set by using the ```n_distinct()``` function.

```
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_sleep$Id)
n_distinct(weight_info$Id)
```


I find that there are 33 participants in the daily_activity, daily_calories and daily_intensities data sets, 24 in the daily_sleep and only 8 in the weight_info data sets. The difference in the weights_info data set can cause the data to not be sufficient.






# Analyze


Let's check the min, max, mean, median and any outliers:



```
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes, Calories) %>%
  summary()


daily_activity %>%
  select(VeryActiveMinutes, FairlyActiveMinutes, LightlyActiveMinutes) %>%
  summary()


daily_calories %>%
  select(Calories) %>%
  summary()

daily_sleep %>%
  select(TotalSleepRecords, TotalMinutesAsleep, TotalTimeInBed) %>%
  summary()
  
  
  weight_info %>%
  select(WeightKg, BMI) %>%
  summary() 
  ```
  
  
  
![Screen Shot 2023-04-04 at 11 55 22 AM](https://user-images.githubusercontent.com/66655353/229848992-8fe4c016-f988-4457-bcd7-75c0e82ac7e2.png)

![Screen Shot 2023-04-04 at 11 51 40 AM](https://user-images.githubusercontent.com/66655353/229848170-52112bcd-8d37-4db7-990a-f5bd95b42e35.png)

![Screen Shot 2023-04-04 at 11 56 57 AM](https://user-images.githubusercontent.com/66655353/229849369-0ead3cfe-f754-47eb-bdb8-37d65c2821de.png)

![Screen Shot 2023-04-04 at 11 57 39 AM](https://user-images.githubusercontent.com/66655353/229849537-7457ebf9-1a67-4b95-812f-f7799df73c19.png)

![Screen Shot 2023-04-04 at 11 58 11 AM](https://user-images.githubusercontent.com/66655353/229850134-39702577-8ace-4e97-b1aa-8590fb258be3.png)



Based on this summary, some interesting findings were uncovered:

  - Average of 7638 steps per day, which is below the generally recommended 10,000.
  - The average sedentary time among participants was 991 minutes or 16 hours, indicating a need for reduction.
  - Majority of particpants are lightly active with the average being 192.8 minutes per day.
  - Participants slept an average of 7 hours.
 
 
 

Let's see if there is a relationship between the total Calories burned vs the Total Steps:


```
ggplot(data=daily_activity, aes(x=TotalSteps, y=Calories)) + 
  geom_point() + geom_smooth() + labs(title="Total Steps vs. Calories")
  ```



![Screen Shot 2023-04-04 at 1 30 59 PM](https://user-images.githubusercontent.com/66655353/229871629-f8b92a0e-7f24-4578-b436-439438519765.png)

An obvious correlation shown, the more steps we take the more calories we burn.







Let's see the relationship between Very Active Minutes and Calories:

```
ggplot(data=daily_activity, aes(x=VeryActiveMinutes, y=Calories)) + 
  geom_point() + geom_smooth() + labs(title="Very Active Minutes vs. Calories")
 ```





![Screen Shot 2023-04-04 at 2 09 24 PM](https://user-images.githubusercontent.com/66655353/229880611-1c62c49c-3559-4864-88b6-bca99c889cd7.png)


As expected we see another correlation between Very Active Minutes vs Calories. Very active people will burn more calories.




```
ggplot(data=daily_sleep, aes(x=TotalMinutesAsleep, y=TotalTimeInBed)) + 
  geom_point()+ labs(title="Total Minutes Asleep vs. Total Time in Bed")
 ```

![Screen Shot 2023-04-04 at 5 35 25 PM](https://user-images.githubusercontent.com/66655353/229928092-19c4e533-4142-4853-b4ac-0e69034d6097.png)


Given the relationship between Total Minutes Asleep and Total Time in Bed, participants may benefit from considering strategies such as developing consistent sleep routines and creating a favorable sleep environment, and exploring the use of sleep notifications.



Next I am going to merge two tables that contain the Id and Date column.

```
merged_data <- merge(daily_sleep, daily_activity, by=c('Id', 'Date'))
head(merged_data)
 ```

![Screen Shot 2023-04-04 at 7 26 38 PM](https://user-images.githubusercontent.com/66655353/229944154-5a852b7e-8823-46c3-af5a-7300199bea02.png)




```
ggplot(data=merged_data, aes(x=TotalMinutesAsleep, y=SedentaryMinutes)) + 
  geom_point(color='blue') + geom_smooth() +
  labs(title="Minutes Asleep vs. Sedentary Minutes")
 ```

![Screen Shot 2023-04-04 at 7 33 42 PM](https://user-images.githubusercontent.com/66655353/229944971-b8e313a0-562a-4607-ab1d-250a55a3bca6.png)


- There appears to be a negative relationship between the Total Minutes Asleep and the Sedentary Minutes.

- Bellabeat app can suggest reducing sedentary time to users who aim to enhance their sleep quality.




# Share


The following visuals were created using Python.



![dailyactiveminutes](https://user-images.githubusercontent.com/66655353/230202695-0fee8de9-d943-4a9f-94ee-e6befebc054f.png)



The pie chart displays the proportion of active minutes in four categories, namely very active, fairly active, lightly active, and sedentary. It is evident from the chart that the majority of users spent 81.3% of their daily activity being sedentary, whereas only 1.74% of their time was spent being very active.

![corrmax_bellbeat](https://user-images.githubusercontent.com/66655353/230435476-61bd5585-1c5f-429b-ac78-3da6cd76328b.png)

This correlation matrix displays all of the categories from the daily_activity dataset. Correlation coefficients measure the strength and direction of the linear relationship between two variables, with values ranging from -1 (negative correlation) to 1 (positive correlation), with 0 indicating no correlation. An interesting find here is the Logged Activities Distance has a negative relationship with all of the other variables. This means the number of times users logged in their activity did not make a difference on how active they are or motivate them to become more active.







# Act
