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



***Whereas there are some users are present in both datasets (which it comes handy to see the whole picture of their weight evolution), there are other users that lack information in one of the two datasets, resulting into incomplete information. However, for this analysis we will need the whole picture of the weight because we will merge the rest of tables such as calories, steps, etc. and see how weight changed compared with them***
**Hence, we will use INNER JOIN statement in SQL to include only the users who have complete weight data, resulting in only 6 out of 13 particpants**

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



***We observed that there are three participants who are present in either one of the two dataset but not in both. While these datasets sum 25 unique participants together, we need every user ID to be present in both datasets. Therefore, when merging the tables, we will exclude these three users by using the INNER JOIN statement in SQL, resulting in a final dataset with 22 participants.***

---

**calories, intensities, METs and Steps**

We already know that calories, intensities, METs, and steps are consistent between them in minute tables in both datasets. For that reason, we can select one table representing the set of these variables for each dataset. 

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

***We observed that there are three participants who are present in either one of the two dataset but not in both. While these datasets sum 35 unique participants together, we need every user ID to be present in both datasets. Therefore, when merging the tables, we will exclude these three users by using the INNER JOIN statement in SQL, resulting in a final dataset with 32 participants.***


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
