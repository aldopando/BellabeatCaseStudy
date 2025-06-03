
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


We merged the results of the five tables obtained from BigQuery SQL into Google Sheets, then we created a pivot table to dispaly if users Id are consistent across the tables.
![image](https://github.com/user-attachments/assets/e3357b87-7761-448b-8d31-62fe53f9a02a)


***We discovered that minuteSleep table lack of users Id, only containing 23 users, meanwhile the rest of the tables remain consistent between them, nevertheless they add up 34 users, when they should sum up 33 users based on the data collection***
***Therefore, minuteSleep table is going to be used individually for the analysis****

Then knowing that the rest of the tables (`minuteCaloriesNarrow`,`minuteIntensitiesNarrow`, `minuteMETsNarrow`, and `minuteStepsNarrow`) contain the same users id, we compared if these tables have the same periods of time when the health data of each user were tracked. 
We created a pivot table and used the function `XLOOKUP()` to compare the beginning of period of time by each user id across the four tables.

![image](https://github.com/user-attachments/assets/6f16ca9f-1682-4ad4-bafb-c664180ba9d2)


***We discovered that 33 participants started to track their data at the same time, except for one user. We figured out that this different user is the same across the four tables***

Afterwards, we created a pivot table grouping the users by the latest date when they finished tracking their data, due to users finished their interval in different times. Then we counted how many times the same user with same latest date repeated across the four tables 

![image](https://github.com/user-attachments/assets/d46e4ddd-3f65-4134-a0cd-f41846d29eec)


***The results were that the latest date each user finished their time frame were consistent across the four tables***
**After comparing the users and their period of time in the minute tables, we can ensure that `minuteCaloriesNarrow`,`minuteIntensitiesNarrow`, `minuteMETsNarrow`, and `minuteStepsNarrow` are consistent between them. Therefore,we can merge them to create a single table to compare the correlation between the variables. 



### FitabaseData_20160412_20160512 dataset

Knowing that the minutes tables in the second dataset are basically the same as in the first but in a different period of time, I performed the same steps as above. 

#### Users Id 

**minuteCaloriesNarrow_secondPeriod**

                SELECT
                    DISTINCT Id,
                    MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
                    MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
                FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteCaloriesNarrow_secondPeriod`         
                        
                GROUP BY Id
                ORDER BY Id



**minuteIntensitiesNarrow_secondPeriod**

                SELECT
                    DISTINCT Id,
                    MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
                    MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
                FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteIntensitiesNarrow_secondPeriod`         
                        
                GROUP BY Id
                ORDER BY Id


**minuteMETsNarrow_secondPeriod**

                SELECT
                    DISTINCT Id,
                    MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
                    MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
                FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteMETsNarrow_secondPeriod`         
                        
                GROUP BY Id
                ORDER BY Id


**minuteStepsNarrow_secondPeriod**

                SELECT
                    DISTINCT Id,
                    MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
                    MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                
                FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteStepsNarrow_secondPeriod`         
                        
                GROUP BY Id
                ORDER BY Id

**minuteSleep_secondPeriod**
           
                SELECT
                    DISTINCT Id,
                    MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date)) AS latest_date,
                    MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date)) AS oldest_date
                
                FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteSleep_secondPeriod`         
                        
                GROUP BY Id
                ORDER BY Id


We merged the results of the five tables obtained from BigQuery SQL into Google Sheets, then we created a pivot table to count how many times a unique user Id repeated across the five tables.

![image](https://github.com/user-attachments/assets/301496c1-58ac-4f36-8522-3e7e1e2e4ce0)

***We discovered that minuteSleep table lack of users Id, only containing 24 users, meanwhile the rest of the tables remain consistent between them, adding up 33 users each one which is correct, knowing that 33 users participate in the survey***
***minuteSleep_secondPeriod table is going to be used individually for the analysis****

Now we created a pivot tables to compare the consistency of the time period of time by each user across the tables that until now remain consistent. 

In the first pivot table we count how many times users with a specific oldest date appear across the tables. 


![image](https://github.com/user-attachments/assets/b9a229a0-b360-4dbc-9787-655a74cd9d51)

***The results shown that all the users across the four tables started to track their data at the same date***


In the second pivot table we filter the tables (calories, intensities, METs, and Steps). Then we grouped the users by the date when they finished to track their data, and we check if each combination (user-lastest date) repeated across the four tables by counting if this combination appear or not in each table.


![image](https://github.com/user-attachments/assets/58c05481-0ca3-47c7-86ff-53a9b18f2ca5)

**We counclude that the tables`minuteCaloriesNarrow_secondPeriod`,`minuteIntensitiesNarrow_secondPeriod`, `minuteMETsNarrow_secondPeriod`, and `minuteStepsNarrow_secondPeriod` are consistent between them containing the same users Id tracking their data during the same periods of time**




## Checking for consistency in hour tables (calories, intensity, and steps).

In order to check for the consistency between these tables, we performed the same steps as in the minute tables.

### FitabaseData_20160312_20160411 dataset


**hourlyCalories**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`      
                                
        GROUP BY Id
        ORDER BY Id


**hourlyIntensities**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`     
                                
        GROUP BY Id
        ORDER BY Id


**hourlySteps**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`      
                                
        GROUP BY Id
        ORDER BY Id


Consistency in users:


![image](https://github.com/user-attachments/assets/9fc3afd3-b4fa-4935-9b43-6a7866608970)


Consistency in period of time:


![image](https://github.com/user-attachments/assets/49376dc9-5839-4d3b-b240-6157eeea0a1d)


![image](https://github.com/user-attachments/assets/8dcefebe-8b9e-4734-af7e-435bde8ea7af)


**The tables `hourlyCalories`, `hourlyIntensities`, and `hourlySteps` contain the same users Id and each user tracked their data during the same peiod of time across the tables, therefore these tables are consistent between them**




### FitabaseData_20160412_20160512 dataset


**hourlyCalories_secondPeriod**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyCalories_secondPeriod`      
                                
        GROUP BY Id
        ORDER BY Id

**hourlyIntensities_secondPeriod**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyIntensities_secondPeriod`      
                                
        GROUP BY Id
        ORDER BY Id
        

**hourlySteps_secondPeriod**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod`      
                                
        GROUP BY Id
        ORDER BY Id



Users: 

![image](https://github.com/user-attachments/assets/b1cab425-25a3-4c60-82bb-219345872b53)


Period of time: 

![image](https://github.com/user-attachments/assets/7a1ed078-ff4b-4d3b-9eda-42c56c4a1356)



![image](https://github.com/user-attachments/assets/a40a7e3e-98f0-4ed2-a94b-aba181444dfc)


**The tables `hourlyCalories_secondPeriod`, `hourlyIntensities_secondPeriod`, and `hourlySteps_secondPeriod` contain the same users Id and each user tracked their data during the same peiod of time across the tables, therefore these tables are consistent between them**




## Checking for consistency minutes VS. hourly tables.

Now that we know minute tables are consistent between them as well as hourly tables, we can select a single metric to check for their consistency 

### FitabaseData_20160312_20160411 dataset 

***Period of Time***

**hourlyCalories**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour)) AS oldest_date
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`     
                                        
        GROUP BY Id
        ORDER BY Id
        LIMIT 5


**minuteCaloriesNarrow**

        SELECT
          DISTINCT Id,
          MAX(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS latest_date,
          MIN(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute)) AS oldest_date
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow`     
                                        
        GROUP BY Id
        ORDER BY Id
        LIMIT 5


![image](https://github.com/user-attachments/assets/c3d94f2b-646d-44c9-a055-4ece8eba1d06)


![image](https://github.com/user-attachments/assets/89a2a169-60fa-47a2-b9c5-39396ae7ddf8)


***Total  hourlyCalories vs Total minuteCaloriesNarrow***

**hourlyCalories**

        SELECT
          DISTINCT Id,
          SUM(Calories) AS total_hourlyCalories
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`     
                                        
        GROUP BY Id
        ORDER BY Id

**minuteCaloriesNarrow**

        SELECT
          DISTINCT Id,
          ROUND(SUM(Calories), 0) AS total_minutesCalories
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow`     
                                        
        GROUP BY Id
        ORDER BY Id


![image](https://github.com/user-attachments/assets/b340e2dc-c0fb-4371-b080-36c208281383)



***Total  hourlyIntensities vs Total minuteIntensitiesNarrow***

**hourlyIntensities**

        SELECT
          DISTINCT Id,
          SUM(TotalIntensity) AS total_hourlyIntensities
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`     
                                        
        GROUP BY Id
        ORDER BY Id

**minuteIntensitiesNarrow**

        SELECT
          DISTINCT Id,
          SUM(Intensity) AS total_minutesIntensities
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteIntensitiesNarrow`     
                                        
        GROUP BY Id
        ORDER BY Id



![image](https://github.com/user-attachments/assets/1c1bd1c9-cb6f-4ae2-bbb7-4e2c87ef2a22)




***Total  hourlySteps vs Total minuteStepsNarrow***

**hourlySteps**

        SELECT
          DISTINCT Id,
          SUM(StepTotal) AS total_hourlySteps
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`     
                                        
        GROUP BY Id
        ORDER BY Id


**minuteStepsNarrow**

        SELECT
          DISTINCT Id,
          SUM(Steps) AS total_minuteSteps
                                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow`     
                                        
        GROUP BY Id
        ORDER BY Id


![image](https://github.com/user-attachments/assets/3d997cc7-82e1-4f4b-bec4-4f45525bf5d1)



### FitabaseData_20160412_20160512 dataset

***Period of Time***

![image](https://github.com/user-attachments/assets/3f7b08ba-a277-4775-9b08-41dac0cf554b)



***Total hourlyCalories_secondPeriod vs Total minuteCaloriesNarrow_secondPeriod***


**hourlyCalories_secondPeriod**

        SELECT
            DISTINCT Id,
            SUM(Calories) AS total_hourlyCalories
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyCalories_secondPeriod` 
        
        GROUP BY Id
        ORDER BY Id


**minuteCaloriesNarrow_secondPeriod**


        SELECT
            DISTINCT Id,
            ROUND(SUM(Calories), 0) AS total_minutesCalories
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteCaloriesNarrow_secondPeriod` 
        
        GROUP BY Id
        ORDER BY Id


![image](https://github.com/user-attachments/assets/d9d7bb35-20e1-4c2d-bf66-76736797d787)



***Total hourlyIntensities_secondPeriod vs Total minuteIntensitiesNarrow_secondPeriod***


**hourlyIntensities_secondPeriod**

        SELECT
            DISTINCT Id,
            SUM(TotalIntensity) AS total_hourlyIntensities
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyIntensities_secondPeriod` 
        
        GROUP BY Id
        ORDER BY Id


**minuteIntensitiesNarrow_secondPeriod**

        SELECT
          DISTINCT Id,
          SUM(Intensity) AS total_minutesIntensities
                                        
          FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteIntensitiesNarrow_secondPeriod`     
                                                
        GROUP BY Id
        ORDER BY Id
        


![image](https://github.com/user-attachments/assets/4a185fe6-d9fe-4d80-a28e-13c3444eca4f)





***Total hourlySteps_secondPeriod vs Total minuteStepsNarrow_secondPeriod***

**Total hourlySteps_secondPeriod**

        SELECT
          DISTINCT Id,
          SUM(StepTotal) AS total_hourlySteps
                                        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod`     
                                                
        GROUP BY Id
        ORDER BY Id

**minuteStepsNarrow_secondPeriod**


        SELECT
          DISTINCT Id,
          SUM(Steps) AS total_minuteSteps
                                        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteStepsNarrow_secondPeriod`     
                                                
        GROUP BY Id
        ORDER BY Id


![image](https://github.com/user-attachments/assets/a7707ad6-4c03-4830-a05b-b54adca64920)





















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
