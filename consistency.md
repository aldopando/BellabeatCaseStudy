
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

Now that we know minute tables are consistent between them as well as hourly tables, we can select one minute table and one hourly table to compare the period of time between them.

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

In order to compare the time between hourlyCalories and minuteCalories, we need to truncate the data type TIMESTAMP in the column 'ActivityMinute' in the `minuteCaloriesNarrow` table to hours. In this way, we can agreggate the data by hoursrather than minutes and still conserving the TIMESTAMP format.

**minuteCaloriesNarrow**

        SELECT
          DISTINCT Id,
          MAX(TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR)) AS latest_date,
          MIN(TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR)) AS oldest_date
                                        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow`     
                                                
        GROUP BY Id
        ORDER BY Id

We saved the results in Google Sheets and created a pivot table to compare the oldest and latest date of every user between hourlyCalories and minutesCalories.

**Oldest date**

![image](https://github.com/user-attachments/assets/372126b6-4b24-45ea-ae01-f35b03732706)



**Latest Day**

![image](https://github.com/user-attachments/assets/a4dbf2f8-37f5-44c9-87f8-094d275b70c2)


***We can notice that 33 users started to track their data at the same time in both tables and the extra user is the same in both tables which started to tracked their data in a different time but it's consistent between both tables***
***Every user finished to track their data at the same time in both tables.***

**We can then conclude, that the period of time by each user is consistent between hourly tables and minute tables**

---

In order to ensure minute tables and hourly tables are consistent between them, we need to compare if each variable (calories,intensities, and steps) tables add up the same total in their respective hourly table and minute table in the whole period.

***Total hourlyCalories vs Total minuteCaloriesNarrow***

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

***We can notice that the total calories by each user in the `hourlyCalories` table add up a different value compared to the the total calories in the `minuteCaloriesNarrow` table.***

---

**Figuring out the reasons of inconsistency between total of calories add up by hourlyCalories and minuteCalories**

We coverted the minutes in the minuteCalories table to hours manually in order to detect if the result added up different totals by user compared to the orignal hourlyCalories table.
We created a subquery where we aggregated the data from minutes to hours using the `TIMESTAMP_TRUNC()` function, and then we pulled only the total added up by each unique user from the table generated by the subquery. 


        SELECT
          DISTINCT Id, 
          SUM(hourlyCalories) AS totalCalories
        
        FROM (
            SELECT
              Id, 
              TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR) AS ActivityHour,
              SUM(Calories) AS hourlyCalories
        
            FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow` 
        
            GROUP BY Id, ActivityHour
            ORDER BY Id, ActivityHour
          )
        
        GROUP BY Id 
        ORDER BY Id 


Afterwards, we saved the results in Google sheets and compared them with the results previously saved of the tables `hourlyCalories` and `minuteCaloriesNarrow` 

![image](https://github.com/user-attachments/assets/17dd0995-9976-4bd0-b631-950f99f99ed7)



***We can noticed how converting the minuteCalories table to hourlyCalories add up almost the same total by user without rounding any decimal from the minuteCaloriesNarrow table***

Now we are going to figure out if rounding the decimals we star to stray away from the target value.


**Roundig the totals** 
In order to convert each value per hour into an integer, we used two functions in SQL to accomplish that; `ROUND()` and `CAST()` 

        SELECT
          DISTINCT Id, 
          SUM(hourlyCalories) AS rounded_totalCalories
        
        
        FROM (
            SELECT
              Id, 
              TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR) AS ActivityHour,
              CAST(SUM(Calories) AS INT64) AS hourlyCalories
            # ROUND(SUM(Calories), 0) AS hourlyCalories
        
            FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow` 
        
            GROUP BY Id, ActivityHour
            ORDER BY Id, ActivityHour
          )
        
        GROUP BY Id 
        ORDER BY Id 


![image](https://github.com/user-attachments/assets/199dac13-bede-4fa7-bae7-b26290c50173)

***We can observe that when we round the values per hour we start to stray away from the target value and now the results of rounding values is the same as the results gotten in the `hourlyCalories` table***

***It makes sense that if we want to use integer values to represent the number of calories per hour by each user, we will stray away from the values generated by using decimals***

**Therefore, we discovered that the `hourlyCalories` table was generated by rounding the calories that each user burn per hour**
**The tables `minuteCaloriesNarrow` and `hourlyCalories` add up different values because the total of calories burnt by each user was calculated by using the full decimals in the minuteCalories table and the hourlyCalories table was calculated using rounded values**

**For the sake of using integer values to represent how many calories each user burnt per hour, we are going to stick with the hourlyCalories table even though decimals are rounded**

***Total hourlyIntensities vs Total minuteIntensitiesNarrow***

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


***We can notice that the total intensity in the whole month by user in both tables is the same, therefore, the tables are consistent between them***


***Total hourlySteps vs Total minuteStepsNarrow***

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


***We can notice that the total steps in the whole month by user in both tables is the same, therefore, the tables are consistent between them***

---

### FitabaseData_20160412_20160512 dataset

Now that we know minute tables are consistent between them, as well as hourly tables inthe second period, we can select one minute table and one hourly table to compare the period of time between them.


***Period of Time***

To compare the time periods between the `hourlyCalories_secondPeriod` and `minuteCaloriesNarrow_secondPeriod` tables, we first need to aggregate the data in `minuteCaloriesNarrow_secondPeriod` from minutes to hours using the `TIMESTAMP_TRUNC()` function, as done in the first dataset.

**minuteCaloriesNarrow_secondPeriod**

        SELECT
          DISTINCT Id,
          MAX(TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR)) AS latest_date,
          MIN(TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR)) AS oldest_date
                                                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteCaloriesNarrow_secondPeriod`     
                                                        
        GROUP BY Id
        ORDER BY Id
        
**Comparison of oldest date**

![image](https://github.com/user-attachments/assets/8e2bf219-6c89-4678-848c-1ab4a3e7d454)


**Comparison of latest date**


![image](https://github.com/user-attachments/assets/ef872f20-f363-4c6f-ae42-6daaae3a5ef8)

***We noticed that the latest date on which the users `2022484408`, `4445114986`, `8378563200`, and `8877689391` finished tracking their data is inconsistent between the `hourlyCalories_secondPeriod` and `minuteCaloriesNarrow_secondPeriod ` tables. We observe that each has a different date when they finished their period between both tables. This is unusual, as the hourlyCalories table is supposedly built based on the minuteCalories data.
To confirm whether this inconsistency in the time period affects other variables, we will compare the total steps and intensity levels in the minute and hourly tables by summing the values each user tracked throughout the entire month***.


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



***After comparing the total steps and intensity levels between the minute and hourly tables, we found that the totals differ for the same users who had inconsistent latest dates across the two tables***.


**To address this inconsistency, we decided to not use the hourly tables from the second dataset, instead we will stick with the minute tables and based on them building the hourly tables by ourselves, as well as the daily tables to ensure we are using the same time period and with the same values**.













