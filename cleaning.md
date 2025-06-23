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
