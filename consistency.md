
## Checking for consistency between calories, intensity, METs, steps and sleep in minute tables.

### FitabaseData_20160312_20160411 dataset

#### Users Id 

I converted the 'ActivityMinute' as a TIMESTAMP data type in order to accurately pull the oldest and latest time of the period of time when the health metrics of each user wre tracked.

**minuteCaloriesNarrow**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow`
        
        GROUP BY Id
        ORDER BY Id

**minuteIntensitiesNarrow**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteIntensitiesNarrow`
                
        GROUP BY Id
        ORDER BY Id


**minuteMETsNarrow**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteMETsNarrow`
                
        GROUP BY Id
        ORDER BY Id


**minuteStepsNarrow**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow`
                
        GROUP BY Id
        ORDER BY Id


**minuteSleep**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date)) AS oldest_date
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteSleep`
                
        GROUP BY Id
        ORDER BY Id

![image](https://github.com/user-attachments/assets/28454fa0-b571-48fd-9653-cd0f938791bc)

number of users 
**After comparing the user Ids in both tables, we discovered tha `miunteSleep` was tracked in a diferent period of time compared to the rest of minute tables**

## Checking number of users from `FitabaseData_20160312_20160411` vs `FitabaseData_20160412_20160512` datasets

In order to compare the users (Id) for both datasets, we use `hourlySteps` and `hourlySteps_secondPeriod`, each one belongs to a different dataset. Both cointain the data but in different periods of time.

### Total number of users

**hourlySteps**

        SELECT
          COUNT(DISTINCT Id) AS total_users
              
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps` 

**hourlySteps_secondPeriod**

        SELECT
          COUNT(DISTINCT Id) AS total_users
              
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod` 

Results:

| Table | total_users |
| :---: | :---:|
| hourlySteps | 34 |
| hourlySteps_secondPeriod | 33 | 

### Comparing users Ids in both datasets

**hourlySteps**

        SELECT
              DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps` 
        
        ORDER BY ID DESC 

**hourlySteps_secondPeriod**

        SELECT
              DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod` 
        
        ORDER BY Id DESC

Both results were merged in Google Sheets, to identify what Id was different across the datasets. 







## Steps

### Comparing the total number of steps tracked for each user. 
**dailyActivity**

    SELECT
      DISTINCT Id,
      SUM(TotalSteps) AS totalSteps_month
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.dailyActivity`
    
    GROUP BY Id
    ORDER BY Id DESC
    LIMIT 10

| Id	| totalSteps_month |
| :---:| :---:|
|8877689391 |	209005|
|8792009665 |	37139|
|8583815059	| 24364|
|8378563200 |	97623|
|8253242879 |	28679|
|8053475328 |	163288|
|7086361926 |	73247|
|7007744171 |	147124|
|6962181067 |	176956|
|6775888955 |	50031|



**hourlySteps**

    SELECT
      DISTINCT Id,
      SUM(StepTotal) AS totalSteps_month
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`
    
    GROUP BY Id
    ORDER BY Id DESC
    LIMIT 10

|Id	| totalSteps_month|
| :---:| :---:|
|8877689391 |	534197|
|8792009665 |	49762|
|8583815059 |	60581|
|8378563200 |	252872|
|8253242879 |	28393|
|8053475328 |	467018|
|7086361926 |	198157|
|7007744171 |	349504|
|6962181067 |	444551|
|6775888955 |	142721|


**minuteStepsNarrow**

    SELECT
      DISTINCT Id,
      SUM(Steps) AS totalSteps_month
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow`
    
    GROUP BY Id
    ORDER BY Id DESC
    LIMIT 10

|Id	| totalSteps_month |
| :---:| :---:|
|8877689391 |	534197|
|8792009665 |	49762|
|8583815059 |	60581|
|8378563200 |	252872|
|8253242879 |	28393|
|8053475328 |	467018|
|7086361926 |	198157|
|7007744171 |	349504|
|6962181067 |	444551|
|6775888955 |	142721|

*We can notice that the total steps for every user between `hourlySteps` and `minuteStepsNarrow` are the same, nevertheless we can highlight that `dailyActivity` tracked a different number of steps compared to the other tables*

### Comparing the periods of time tracked for each user. 

**dailyActivity**

    SELECT
      DISTINCT Id,
      MAX(ActivityDate) AS latest_date,
      MIN(ActivityDate) AS oldest_date
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.dailyActivity`
    
    GROUP BY Id
    ORDER BY Id DESC


**hourlySteps**

    SELECT
      DISTINCT Id,
      MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
      MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`
    
    GROUP BY Id
    ORDER BY Id DESC


**minuteStepsNarrow** 

    SELECT
      DISTINCT Id,
      MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
      MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow`
    
    GROUP BY Id
    ORDER BY Id DESC


| dailyActivity |  |  | hourlySteps |  |  | minuteStepsNarrow |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Id | latest_date | oldest_date | Id | latest_date | oldest_date | Id | latest_date | oldest_date |
| 8877689391 | 2016-04-12 | 2016-04-01 | 8877689391 | 2016-04-12 08:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8877689391 | 2016-04-12 08:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 8792009665 | 2016-04-12 | 2016-04-01 | 8792009665 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8792009665 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 8583815059 | 2016-04-08 | 2016-04-01 | 8583815059 | 2016-04-08 17:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8583815059 | 2016-04-08 17:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 8378563200 | 2016-04-12 | 2016-04-01 | 8378563200 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8378563200 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 8253242879 | 2016-04-12 | 2016-04-01 | 8253242879 | 2016-04-11 19:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8253242879 | 2016-04-11 19:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 8053475328 | 2016-04-12 | 2016-04-02 | 8053475328 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 8053475328 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 7086361926 | 2016-04-12 | 2016-04-01 | 7086361926 | 2016-04-12 07:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 7086361926 | 2016-04-12 07:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 7007744171 | 2016-04-12 | 2016-04-01 | 7007744171 | 2016-04-12 07:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 7007744171 | 2016-04-12 07:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 6962181067 | 2016-04-12 | 2016-03-30 | 6962181067 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 6962181067 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 6775888955 | 2016-04-09 | 2016-04-01 | 6775888955 | 2016-04-09 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 6775888955 | 2016-04-09 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 6391747486 | 2016-04-09 | 2016-04-01 | 6391747486 | 2016-04-09 02:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 6391747486 | 2016-04-09 02:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 6290855005 | 2016-04-10 | 2016-04-01 | 6290855005 | 2016-04-02 16:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 6290855005 | 2016-04-02 16:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 6117666160 | 2016-04-10 | 2016-04-01 | 6117666160 | 2016-04-09 22:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 6117666160 | 2016-04-09 22:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 5577150313 | 2016-04-11 | 2016-04-01 | 5577150313 | 2016-04-11 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 5577150313 | 2016-04-11 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 5553957443 | 2016-04-12 | 2016-04-01 | 5553957443 | 2016-04-12 07:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 5553957443 | 2016-04-12 07:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4702921684 | 2016-04-12 | 2016-03-29 | 4702921684 | 2016-04-11 21:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4702921684 | 2016-04-11 21:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4558609924 | 2016-04-12 | 2016-04-01 | 4558609924 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4558609924 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4445114986 | 2016-04-12 | 2016-03-29 | 4445114986 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4445114986 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4388161847 | 2016-04-05 | 2016-03-29 | 4319703577 | 2016-04-08 22:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4319703577 | 2016-04-08 22:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4319703577 | 2016-04-09 | 2016-03-29 | 4057192912 | 2016-04-12 05:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4057192912 | 2016-04-12 05:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4057192912 | 2016-04-12 | 2016-03-12 | 4020332650 | 2016-04-12 04:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 4020332650 | 2016-04-12 04:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 4020332650 | 2016-04-12 | 2016-03-12 | 3977333714 | 2016-04-12 02:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 3977333714 | 2016-04-12 02:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 3977333714 | 2016-04-12 | 2016-04-01 | 3372868164 | 2016-04-10 14:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 3372868164 | 2016-04-10 14:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 3372868164 | 2016-04-10 | 2016-04-01 | 2891001357 | 2016-04-05 11:00:00.000000 UTC | 2016-04-05 00:00:00.000000 UTC | 2891001357 | 2016-04-05 11:59:00.000000 UTC | 2016-04-05 00:00:00.000000 UTC |
| 2891001357 | 2016-04-05 | 2016-03-29 | 2873212765 | 2016-04-11 19:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 2873212765 | 2016-04-11 19:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 2873212765 | 2016-04-12 | 2016-04-01 | 2347167796 | 2016-04-12 06:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 2347167796 | 2016-04-12 06:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 2347167796 | 2016-04-12 | 2016-03-29 | 2320127002 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 2320127002 | 2016-04-12 10:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 2320127002 | 2016-04-12 | 2016-04-01 | 2026352035 | 2016-04-12 09:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 2026352035 | 2016-04-12 09:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 2026352035 | 2016-04-12 | 2016-04-01 | 2022484408 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 2022484408 | 2016-04-12 10:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 2022484408 | 2016-04-12 | 2016-04-01 | 1927972279 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1927972279 | 2016-04-12 10:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1927972279 | 2016-04-12 | 2016-04-01 | 1844505072 | 2016-04-12 06:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1844505072 | 2016-04-12 06:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1844505072 | 2016-04-12 | 2016-04-01 | 1644430081 | 2016-04-10 03:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1644430081 | 2016-04-10 03:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1644430081 | 2016-04-10 | 2016-04-01 | 1624580081 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1624580081 | 2016-04-12 10:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1624580081 | 2016-04-12 | 2016-03-25 | 1503960366 | 2016-04-11 23:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1503960366 | 2016-04-11 23:59:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1503960366 | 2016-04-12 | 2016-03-25 |  |  |  |  |  |  |



*We can notice that the periods of time between `hourlySteps` and `minuteStepsNarrow` are the same, nevertheless we can highlight that `dailyActivity` was tracked in a different period of time in every user compared to the other tables*

**`hourlySteps` and `minuteStepsNarrow` are consistent tables, they were tracked during the same periods of time and sum up the same total of steps by user**

**`dailyActivity` sum up a different number of steps because it was tracked in a different period of time by user**


## Checking for consistency between steps, calories and intensity, hourly tables.

### Consistency period of time


**hourlySteps**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`
        
        GROUP BY Id
        ORDER BY Id
        LIMIT 5

**hourlyCalories**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`
        
        GROUP BY Id
        ORDER BY Id
        LIMIT 5


**hourlyIntensities**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`
        
        GROUP BY Id
        ORDER BY Id
        LIMIT 5

Results:

| Steps |  |  | Calories |  |  | Intensities |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Id | latest_date | oldest_date | Id | latest_date | oldest_date | Id | latest_date | oldest_date |
| 1503960366 | 2016-04-11 23:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1503960366 | 2016-04-11 23:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1503960366 | 2016-04-11 23:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1624580081 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1624580081 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1624580081 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1644430081 | 2016-04-10 03:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1644430081 | 2016-04-10 03:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1644430081 | 2016-04-10 03:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1844505072 | 2016-04-12 06:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1844505072 | 2016-04-12 06:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1844505072 | 2016-04-12 06:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |
| 1927972279 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1927972279 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC | 1927972279 | 2016-04-12 10:00:00.000000 UTC | 2016-03-12 00:00:00.000000 UTC |

**We can notice that the three tables tracked the data during the same period of time by user**

### Consistency number of users (Id)

**hourlySteps**

        SELECT
          COUNT(DISTINCT Id) AS total_users
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`

**hourlyCalories**

        SELECT
          COUNT(DISTINCT Id) AS total_users
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`


**hourlyIntensities**

        SELECT
          COUNT(DISTINCT Id) AS total_users
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`


Results:

| Table | total_users |
| :---: | :---:|
| hourlySteps | 34 |
| hourlyCalories | 34 | 
| hourlyIntensities | 34 |

**The number of users is consistent across these tables, nevertheless, it returns a number of 34 participants, which is incorrect because the number of users who participated in the survey is 33**.
