## Extra spaces in data

### hourlyCalories_merged

**Id**

We know that each Id value should contain exactly 10 digits. Therefore, to identify rows with extra spaces or unexpected characters, we will detect all rows where the Id does not have exactly 10 characters. To do this, we will create a temporary table that includes a column showing the character count of each Id, after converting it from a numeric to a string data type. Finally, we will filter this temporary table to return only the rows where the character count is different from 10, allowing us to detect any anomalies such as extra spaces or characters.


    WITH id_length AS (
      SELECT 
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`
    )
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10

***we didn't find any extra space across the rows in the column `Id`, all records contain exactly 10 digitis***

---

**activityHour**

The `activityHour` column contains TIMESTAMP values (YYYY-MM-DD HH:MM:SS UTC), which are expected to have exactly 22 characters. To identify any rows with extra spaces or formatting issues, we will count the number of characters in each cell and filter out the rows that do not contain exactly 22 characters.

    WITH activityHour_length AS (
      SELECT 
        LENGTH(CAST(activityHour AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`
    )
    
    SELECT *
    FROM activityHour_length
    WHERE number_of_characters != 22;

***We didn't find any extra space or character across the rows in the column `activityHour`, all records contain exactly 22 characters***

---

### hourlyIntensities_merged

**Id**

    WITH id_length AS (
      SELECT 
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged` 
    )
        
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10

***We didn't find any extra space or characters across the rows in the column `Id`***

---

**activityHour**

    WITH activityHour_length AS (
      SELECT 
        LENGTH(CAST(activityHour AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged`
    )
        
    SELECT *
    FROM activityHour_length
    WHERE number_of_characters != 22;
        

***We didn't find any extra space or character across the rows in the column `activityHour`***

---

### hourlySteps_merged

**Id**

    WITH id_length AS (
    SELECT 
      LENGTH(CAST(Id AS STRING)) AS number_of_characters
    FROM `analysisbellabeat246.data_merged.hourlySteps_merged` 
    )
            
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10

***We didn't find any extra space or characters across the rows in the column `Id`***

---

**activityHour**

    WITH activityHour_length AS (
      SELECT 
        LENGTH(CAST(activityHour AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlySteps_merged` 
    )
        
    SELECT *
    FROM activityHour_length
    WHERE number_of_characters != 22;

***We didn't find any extra space or character across the rows in the column `activityHour`***

---

### minuteMETs_merged

**Id**

    WITH id_length AS (
      SELECT 
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteMETs_merged`  
    )
            
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10

***We didn't find any extra space or characters across the rows in the column `Id`***

---

**activityMinute**

    WITH activityMinute_length AS (
      SELECT 
        LENGTH(CAST(activityMinute AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteMETs_merged` 
    )
            
    SELECT *
    FROM activityMinute_length
    WHERE number_of_characters != 22;

***We didn't find any extra space or character across the rows in the column `activityMinute`***

---


### minuteSleep_merged

**Id**

    WITH id_length AS (
      SELECT 
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteSleep_merged`
    )
            
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10
    

***We didn't find any extra space or characters across the rows in the column `Id`***

---

**activityMinute**

    WITH activityMinute_length AS (
      SELECT 
        LENGTH(CAST(activityMinute AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteSleep_merged`
    )
            
    SELECT *
    FROM activityMinute_length
    WHERE number_of_characters != 22;

***We didn't find any extra space or character across the rows in the column `activityMinute`***

---

**value**

The `value` column contains rows with values indicating the sleep state. 1 = asleep, 2 = restless, 3 = awake. It means all rows across this column have to contain exactly 1 charater. To identify any rows with extra spaces or characters, we will count the number of characters in each cell and filter out the rows that do not contain exactly 1 character.


    WITH value_length AS (
      SELECT 
        LENGTH(CAST(value AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteSleep_merged`
    )
            
    SELECT *
    FROM value_length
    WHERE number_of_characters != 1

***We didn't find any extra space or characters across the rows in the column `value`***

---

**logId**

The `logId` column contains rows with unique log id in Fitbit’s system for the sleep record. This unique log id contains exatly 11 digits. To identify any rows with extra spaces or characters, we will count the number of characters in each cell and filter out the rows that do not contain exactly 11 character.

    WITH logId_length AS (
      SELECT 
        LENGTH(CAST(logId AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.minuteSleep_merged`
    )
            
    SELECT *
    FROM logId_length
    WHERE number_of_characters != 11


***We didn't find any extra space or characters across the rows in the column `logId`***

---

### weight_data

**Id**

    WITH id_length AS (
      SELECT 
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.weight_data`
    )
            
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10

***We didn't find any extra space or characters across the rows in the column `Id`***

---

**Date**

The `activityHour` column contains DATE data type values, which are expected to have exactly 10 characters (YYYY-MM-DD). To identify any rows with extra spaces or formatting issues, we will count the number of characters in each cell and filter out the rows that do not contain exactly 10 characters.

    WITH date_length AS (
      SELECT 
        LENGTH(CAST(Date AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.weight_data`
    )
            
    SELECT *
    FROM date_length
    WHERE number_of_characters != 10;
    
***We didn't find any extra space or characters across the rows in the column `Date`***

---

***We didn't check for extra spaces or characters in the `WeightKg`, `WeightPounds`, and `BMI` columns because these contain FLOAT values***.


## Duplicates in data.

Before using the DISTINCT statement to remove any duplicate in the data, first we need to pinpoint if there are duplicates at all in the merged tables. In order to ensure a table doesn't have duplicates, a user cannot have more than one record with the same time.

Since BigQuery doesn't allow in-place updates or deletions of individual rows in standard tables, we will create a dataset that will storage the cleaned version of the tables that contain only distinct rows. This dataset is named `clean_data`.


## hourlyCalories_merged

We group the data by users and dates so that all the rows with the same combination of user `id` and `activityHour` are put together. Then we use `COUNT()` function to count and display in the column called `duplicate_count` all rows that each group contain. 

Finallly, we use the `HAVING COUNT` statement to filter out the groups of data with the same `id` and `activityHour` that contain more than one row. In other words, duplicates.

**Query**.

    SELECT 
      Id, 
      activityHour,
      COUNT(*) AS duplicate_count
    
    FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`
    
    GROUP BY Id, activityHour
    
    HAVING COUNT(*) > 1


**Preview of the results**.

![image](https://github.com/user-attachments/assets/a0641d6b-8e9e-40bf-a369-76450fa9792c)

***We found 175 records, each one with 2 duplicates***.

---

To remove these the duplicate rows, we will use the DISTINCT statement and create a new table named `hourlyCalories_cleaned` that it only contains the non-duplicate rows.

Query.

    CREATE TABLE clean_data.hourlyCalories_cleaned AS
    
    SELECT 
      DISTINCT *
    
    FROM `analysisbellabeat246.data_merged.hourlyCalories_merged` 


**Verification number of rows**.

| hourlyCalories_merged | hourlyCalories_cleaned |
| --- | --- |
| 44,755 | 44,580 |


***We removed the 175 duplicate rows***



## hourlyIntensities_merged


**Query**.

    SELECT 
      Id, 
      activityHour,
      COUNT(*) AS duplicate_count
    
    FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged`
    
    GROUP BY Id, activityHour
    
    HAVING COUNT(*) > 1


**Preview of the results**.


![image](https://github.com/user-attachments/assets/431f03cd-3e63-41b5-9834-240186fafbf4)


***We found 175 records, each one with 2 duplicates***.

---

To remove these duplicate rows, we will use the DISTINCT statement and create a new table named `hourlyIntensities_cleaned` that it only contains the non-duplicate rows.

**Query**.

    CREATE TABLE clean_data.hourlyIntensities_cleaned AS
    
    SELECT 
      DISTINCT *
    
    FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged` 


**Verification number of rows**.

| hourlyCalories_merged | hourlyCalories_cleaned |
| --- | --- |
| 44,755 | 44,632 |


***We expected to remove the 175 duplicate rows, but instead the query only removed 123 duplicates. We supposed that this query didn't remove all duplicates because even tiny differences in the other columns (TotalIntensity, AverageIntensity) prevent rows from being considered duplicates. These columns contain FLOAT values so that may be the reason***.

---

The goal is to remove duplicates based on the `Ìd` and `activityHour` columns, but still including the other columns, even if they vary. 

We created a temporary table where we grouped the data by `Id` and `activityHour` columns using `PARTITION BY`, then we used the `ROW_NUMBER()` window function to assign a number to each row within a group. Afterward, we filter out only the rows that whose conatined the number "1" as the first row in each group ` WHERE num_row = 1` , removing all duplicates. Then we replaced the table that we had previously created.

**Query**.

    CREATE OR REPLACE TABLE `clean_data.hourlyIntensities_cleaned` AS
    WITH unique_combination AS (
    
      SELECT *,
      ROW_NUMBER() OVER(PARTITION BY Id, activityHour)AS num_row
      FROM `analysisbellabeat246.data_merged.hourlyIntensities_merged`
    )
    
    SELECT 
      Id,
      activityHour,
      TotalIntensity,
      AverageIntensity
    
    FROM unique_combination
    WHERE num_row = 1;


**Verification number of rows**.

| hourlyCalories_merged | hourlyCalories_cleaned |
| --- | --- |
| 44,755 | 44,580 |


***We removed the 175 duplicate rows***



## hourlySteps_merged


**Query**.

    SELECT 
      Id, 
      activityHour,
      COUNT(*) AS duplicate_count
        
    FROM `analysisbellabeat246.data_merged.hourlySteps_merged`
        
    GROUP BY Id, activityHour
    HAVING COUNT(*) > 1


**Preview of the results**.



***We found 175 records, each one with 2 duplicates***.

---

To remove these duplicate rows, we will use the DISTINCT statement and create a new table named `hourlySteps_cleaned` which it will only contain the non-duplicate rows.

Query.

    CREATE TABLE clean_data.hourlySteps_cleaned AS
    
    SELECT 
      DISTINCT *
      
    FROM `analysisbellabeat246.data_merged.hourlySteps_merged`


**Verification number of rows**.

| hourlySteps_merged | hourlySteps_cleaned |
| --- | --- |
| 44,755 | 44,580 |


***We removed the 175 duplicate rows***


## minuteMETs_merged

## weight_data
