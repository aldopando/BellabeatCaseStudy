## Extra spaces in data

### hourlyCalories_merged

**Id**
We know that each Id value should contain exactly 10 digits. Therefore, to identify rows with extra spaces or unexpected characters, we will detect all rows where the Id does not have exactly 10 characters. To do this, we will create a temporary table that includes a column showing the character count of each Id, after converting it from a numeric to a string data type. Finally, we will filter this temporary table to return only the rows where the character count is different from 10, allowing us to detect any anomalies such as extra spaces or characters.


    WITH id_length AS (
      SELECT 
        Id,
        LENGTH(CAST(Id AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`
    )
    SELECT *
    FROM id_length
    WHERE number_of_characters != 10


**activityHour**

The `activityHour` column contains TIMESTAMP values, which are expected to have exactly 22 characters. To identify any rows with extra spaces or formatting issues, we will count the number of characters in each cell and filter out the rows that do not contain exactly 22 characters.

    WITH activityHour_length AS (
      SELECT 
        LENGTH(CAST(activityHour AS STRING)) AS number_of_characters
      FROM `analysisbellabeat246.data_merged.hourlyCalories_merged`
    )
    
    SELECT *
    FROM activityHour_length
    WHERE number_of_characters != 22;





