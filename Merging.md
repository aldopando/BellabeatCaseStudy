## Checking user consistency across datasets before merging tables.

In order to merge both periods into a whole, we will check if users Id are consistent between both datasets.

**weightLogInfo vs weightLogInfo_secondPeriod**

        SELECT 
          DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.weightLogInfo` 
        
        ORDER BY Id 

---

        SELECT 
          DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.weightLogInfo_secondPeriod` 
        
        ORDER BY Id



![image](https://github.com/user-attachments/assets/f94d8ec2-53b2-4619-b8d0-40741d8ce432)



Whereas there are some users that are present in both datasets (which it comes handy to see the whole picture of their weight evolution), there are more than half users that lack information in one of the two datasets, resulting into incomplete information. 

We will check if there is notable change in the average weight for users who tracked their weight data during the two-month period. 

**weightLogInfo (average weight)**

        SELECT  
          Id,
          ROUND(AVG(WeightKg),0) AS average_weight
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.weightLogInfo` 
        
        GROUP BY Id
        ORDER BY Id
        
----

**weightLogInfo_secondPeriod (average weight)**

        SELECT  
          Id,
          ROUND(AVG(WeightKg),0) AS average_weight
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.weightLogInfo_secondPeriod`  
        
        GROUP BY Id
        ORDER BY Id


![image](https://github.com/user-attachments/assets/3d826a99-4f3f-4c17-b79d-6127b3f760ac)


***We observed that users' weight did not show significant changes throughout the two-month period. Additionally, the data is incomplete. Participants did not track their weight every day and only recorded it occasionally. Therefore, we decided to include all available weight data from both datasets, regardless of whether some users are missing weight information in one of them. Our goal is to use the weight data as an overall indicator of the participants' health status during the survey.***


---


**minuteSleep vs minuteSleep_secondPeriod**

        SELECT  
          DISTINCT Id
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteSleep` 
        
        ORDER BY Id

---
        SELECT  
          DISTINCT Id
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteSleep_secondPeriod` 
        
        ORDER BY Id


![image](https://github.com/user-attachments/assets/e2b8e975-35c7-468f-b6ec-ff268432ba0e)



***We observe that there are three participants who appear in only one of the two dataset, but not in both. Although the combined datasets contain 25 unique participants,, we need each user ID to be present in both datasets. Therefore, when merging the tables, we will exclude these three users, resulting in a final dataset with 22 participants.***

---

**calories, intensities, METs and Steps**

Since we already know that calories, intensities, METs, and steps are consistent across the minute tables in both datasets, we can select one table from each dataset to represent these variables. 

        SELECT 
          DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow` 
        
        ORDER BY Id

---

        SELECT 
          DISTINCT Id 
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteStepsNarrow_secondPeriod` 
        
        ORDER BY Id



![image](https://github.com/user-attachments/assets/11b3cc39-cf1a-4987-8f13-e2713f3773c2)

***We observed that there are three participants who are not present in one of the datasets. However, we need each user ID to be present in both datasets. Therefore, when merging the tables, we will exclude these three users by using the INNER JOIN statement in SQL, resulting in a final dataset with 32 participants.***


---

**heartrate_seconds vs heartrate_seconds_secondPeriod**

        SELECT
          DISTINCT Id
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.heartrate_seconds`
        
        ORDER BY Id

---

        SELECT  
          DISTINCT Id
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.heartrate_seconds_secondPeriod`
         
        ORDER BY Id


![image](https://github.com/user-attachments/assets/277aa88f-284a-493d-a67d-58443d8c5986)

As in the previous cases, there are some users that lack information about hear rate in one of the two datasets. Both tables sum 15 unique users together. However, we wil need that user ID is present in both datasets, therefore we will exclude the participants that lack information in one of the two datasets, resulting in 12 out of 15 participants.


---

# Merging tables.

## Creation of a new dataset to save the merged tables.

We created a new dataset called `data_merged` in our project `analysisbellabeat246` to save the new tables merged.


## weightLogInfo and weightLogInfo_secondPeriod tables.

To merge the rows of the two tables from the datasets, we will perform a UNION ALL operation in our query and save the result as a new table called `weight_data` within our recently created dataset `data_merged`. However, in this new table, we will exclude the `Fat` column (as most of its values are NULL), as well as the `IsManualReport` and `LogId columns`, since they are not relevant to our analysis. Additionally, we will convert the `Date` column from a string to a TIMESTAMP data type. Afterward, we will extract only the date portion from the TIMESTAMP values, as we only need the day the user tracked their weight as a reference point throughout the entire period. The time component is irrelevant for this analysis.

Query.

        SELECT 
          Id,
          DATE(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', Date)) AS Date,
          WeightKg,
          WeightPounds,
          BMI
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.weightLogInfo` 
        
        UNION ALL
        
        SELECT 
          Id,
          DATE(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', Date)) AS Date,
          WeightKg,
          WeightPounds,
          BMI
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.weightLogInfo_secondPeriod` 


Rows.


| weightLogInfo | weightLogInfo_secondPeriod | weight_data |
| --- |  --- |  --- |
| 33 | 67 | 100 |


## minuteSleep and minuteSleep_secondPeriod tables.

To merge the rows of the these tables from the two datasets, we will perform a UNION ALL operation in our query, however we will have to filter only the users who are present in both tables and exclude who do not, and save the result as a new table called `minuteSleep_merged` within our  `data_merged` dataset.  Additionally, we will convert the `date` column from a string to a TIMESTAMP data type.

Query.

        SELECT  
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date) AS activityMinute,
          value,
          logId
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteSleep` 
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteSleep_secondPeriod`)
        
        UNION ALL
                
        SELECT  
            Id,
            PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', date) AS activityMinute,
            value,
            logId
                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteSleep_secondPeriod`
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteSleep`)

Rows.


| minuteSleep | minuteSleep_secondPeriod | minuteSleep_merged |
| --- |  --- |  --- |
| 198,559 | 188,521 | 377,133 |

We can noticed how summing rows of both tables it should have given us a higher result. However we exclude the users' records who are not present in one of the two tables.

---

**Verifying that we only include the users Id that were present in both tables**

        SELECT  
        
          COUNT(DISTINCT(Id)) AS total_users
        
        FROM `analysisbellabeat246.data_merged.minuteSleep_merged` 


| total_users |
| --- |
| 22 |



**hourlyCalories and minuteCaloriesNarrow_secondPeriod tables**

To merge these datasets, we will first aggregate the data of the `minuteCaloriesNarrow_secondPeriod` dataset from minutes to hours. We will also cast the variable `Calories` to an integer data type and save the results as a new table called `hourlyCalories_secondPeriod_cleaned` in the `FitabaseData_20160412_20160512 dataset` dataset.

Query.

        SELECT 
          Id,
          TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR) AS ActivityHour,
          CAST(SUM(Calories) AS INT64) AS Calories
        
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteCaloriesNarrow_secondPeriod` 
        
        GROUP BY Id, ActivityHour

Afterward, we will merge the rows of the these tables from the two datasets, we will perform a UNION ALL operation in our query, however we will have to filter only the users who are present in both tables and exclude who do not, and save the result as a new table called `hourlyCalories_merged` within our `data_merged` dataset.  Additionally, we will convert the `ActivityHour` column from a string to a TIMESTAMP data type. We will also have to filter only the users who are present in both tables and exclude who do not.

Query.

        SELECT 
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour) AS activityHour,
          Calories
              
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories` 
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyCalories_secondPeriod_cleaned`)
                
        UNION ALL
                
        SELECT 
          Id,
          ActivityHour AS activityHour,
          Calories
                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyCalories_secondPeriod_cleaned` 
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`)


Rows.


| hourlyCalories | hourlyCalories_secondPeriod_cleaned | hourlyCalories_merged |
| --- |  --- |  --- |
| 24,084 | 22,093 |  44,755 |



**Verifying that we only include the users Id that were present in both tables**

        SELECT  
        
          COUNT(DISTINCT(Id)) AS total_users
        
        FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`  


| total_users |
| --- |
| 32 |


---


**hourlyIntensities and minuteIntensitiesNarrow_secondPeriod**

To merge these datasets, we will first aggregate the data of the `minuteIntensitiesNarrow_secondPeriod` table from minutes to hours and save the results as a new table called `hourlyIntensities_secondPeriod_cleaned` in the `FitabaseData_20160412_20160512 dataset` dataset.


Query.

        SELECT
          Id,
          TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR) AS ActivityHour,
          SUM(Intensity) AS TotalIntensity,
          ROUND(AVG(Intensity), 1) AS AverageIntensity
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteIntensitiesNarrow_secondPeriod`
        
        GROUP BY Id, ActivityHour


Afterward, we will merge the rows of the these tables from the two datasets, we will perform a UNION ALL operation in our query, however we will have to filter only the users who are present in both tables and exclude who do not, and save the result as a new table called `hourlyIntensities_merged` within our `data_merged` dataset.  Additionally, we will convert the `ActivityHour` column from a string to a TIMESTAMP data type. We will also have to filter only the users who are present in both tables and exclude who do not.

Query.

        SELECT  
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour) AS activityHour,
          TotalIntensity,
          AverageIntensity
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyIntensities_secondPeriod_cleaned`)
                
        UNION ALL
                
        SELECT 
          Id,
          ActivityHour AS activityHour,
          TotalIntensity,
          AverageIntensity
                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyIntensities_secondPeriod_cleaned`
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`)


Rows.


| hourlyIntensities | hourlyIntensities_secondPeriod_cleaned | hourlyIntensities_merged |
| --- |  --- |  --- |
| 24,084 | 22,093 | 44,755 |


**Verifying that we only include the users Id that were present in both tables**

        SELECT
        
          COUNT(DISTINCT(Id)) AS total_users
        
        FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged`   


| total_users |
| --- |
| 32 |


---


**hourlySteps and minuteStepsNarrow_secondPeriod**

To merge these datasets, we will first aggregate the data of the `minuteStepsNarrow_secondPeriod` table from minutes to hours and save the results as a new table called `hourlySteps_secondPeriod_cleaned` in the `FitabaseData_20160412_20160512 dataset` dataset.


Query.


        SELECT
          Id,
          TIMESTAMP_TRUNC(PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute), HOUR) AS ActivityHour,
          SUM(Steps) AS StepTotal,
                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteStepsNarrow_secondPeriod`
                
        GROUP BY Id, ActivityHour



Afterward, we will merge the rows of the these tables from the two datasets, we will perform a UNION ALL operation in our query, however we will have to filter only the users who are present in both tables and exclude who do not. We will save the result as a new table called `hourlySteps_merged` within our `data_merged` dataset.  Additionally, we will convert the `ActivityHour` column from a string to a TIMESTAMP data type.  We will also have to filter only the users who are present in both tables and exclude who do not.


Query.


        SELECT  
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityHour) AS activityHour,
          StepTotal
                
                
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps` 
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod_cleaned`)
                
        UNION ALL 
                
        SELECT 
                
          Id,
          ActivityHour AS activityHour,
          StepTotal
                
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod_cleaned`
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`)



Rows.


| hourlySteps | hourlySteps_secondPeriod_cleaned | hourlySteps_merged |
| --- |  --- |  --- |
| 24,084 | 22,093 | 44,755 |


**Verifying that we only include the users Id that were present in both tables**

        SELECT 
        
          COUNT(DISTINCT(Id)) AS total_users
        
        FROM `analysisbellabeat246.data_merged.hourlySteps_merged`  


| total_users |
| --- |
| 32 |

**minuteMETsNarrow and minuteMETsNarrow_secondPeriod**

To merge the rows of the these tables from the two datasets, we will perform a UNION ALL operation in our query, however we will have to filter only the users who are present in both tables and exclude who do not, and save the result as a new table called `minuteMETs_merged` within our `data_merged` dataset.  Additionally, we will convert the `` column from a string to a TIMESTAMP data type.


Query.

        SELECT 
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute) AS activityMinute,
          METs
        
        FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteMETsNarrow` 
        
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteMETsNarrow_secondPeriod`)
        
        UNION ALL 
        
        SELECT
        
          Id,
          PARSE_TIMESTAMP('%m/%d/%Y%I:%M:%S %p', ActivityMinute) AS activityMinute,
          METs
        
        FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteMETsNarrow_secondPeriod` 
        
        WHERE Id IN (SELECT Id FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteMETsNarrow`)
