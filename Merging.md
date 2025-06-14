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

**Hence, we will use OUTER JOIN statement in SQL to include all the users' weight data**

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



***We observe that there are three participants who appear in only one of the two dataset, but not in both. Although the combined datasets contain 25 unique participants,, we need each user ID to be present in both datasets. Therefore, when merging the tables, we will exclude these three users by using the INNER JOIN statement in SQL, resulting in a final dataset with 22 participants.***

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
