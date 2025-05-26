# Checking for NULL values

## FitabaseData_20160312-20160411

**heartrate_seconds**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(Time IS NULL) AS time_nulls,
      COUNTIF(Value IS NULL) AS value_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.heartrate_seconds`

Results:
| id_nulls	| time_nulls	| value_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 


**hourlyCalories**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
      COUNTIF(Calories IS NULL) AS calories_nulls
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyCalories`

| id_nulls	|  activtyHour_nulls	| calories_nulls |
| :---: | :---: | :---: |
| 0	| 0 | 0 |


**hourlyIntensities**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
      COUNTIF(TotalIntensity IS NULL) AS totalIntensity_nulls,
      COUNTIF(AverageIntensity IS NULL) AS averageIntensity_nulls
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlyIntensities`


Results:

| id_nulls | activtyHour_nulls | totalIntensity_nulls | averageIntensity_nulls |
| :---: | :---: | :---: | :---: |
| 0	| 0	| 0	| 0 |


**hourlySteps**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
      COUNTIF(StepTotal IS NULL) AS stepTotal_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.hourlySteps`


Results:

| id_nulls | activtyHour_nulls |	stepTotal_nulls |
| :---: | :---: | :---: |
| 0	| 0	| 0 |

**minuteCaloriesNarrow**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Calories IS NULL) AS calories_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteCaloriesNarrow`


Results: 
| id_nulls |	activtyMinute_nulls |	calories_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |


**minuteIntensitiesNarrow**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Intensity IS NULL) AS intensity_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteIntensitiesNarrow`


Results: 
| id_nulls |	activtyMinute_nulls |	intensity_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |


**minuteMETsNarrow**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(METs IS NULL) AS METs_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteMETsNarrow`


Results: 

| id_nulls |	activtyMinute_nulls |	METs_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |


**minuteSleep**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(date IS NULL) AS date_nulls,
      COUNTIF(value IS NULL) AS value_nulls,
      COUNTIF(logId IS NULL) AS logId_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteSleep`

Results: 

| id_nulls |	date_nulls |	value_nulls |	logId_nulls |
| :---: | :---: | :---: | :---: |
| 0 |	0 |	0 |	0 |

**minuteStepsNarrow**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Steps IS NULL) AS Steps_nulls
    
    
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.minuteStepsNarrow`

Results:

| id_nulls |	activtyMinute_nulls |	Steps_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |

**weightLogInfo**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(Date IS NULL) AS date_nulls,
      COUNTIF(WeightKg IS NULL) AS weightKg_nulls,
      COUNTIF(WeightPounds IS NULL) AS weightPounds_nulls,
      COUNTIF(Fat IS NULL) AS fat_nulls,
      COUNTIF(BMI IS NULL) AS BMI_nulls,
      COUNTIF(IsManualReport IS NULL) AS isManualReport_nulls,
      COUNTIF(LogId IS NULL) AS logId_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160312_20160411.weightLogInfo`

Results:

| id_nulls | date_nulls | weightKg_nulls | weightPounds_nulls | fat_nulls | BMI_nulls | isManualReport_nulls | logId_nulls |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 0 | 0 | 31 | 0 | 0 | 0 |



## FitabaseData_20160412-20160512


**dailyCalories_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityDay IS NULL) AS activityDay_nulls,
      COUNTIF(Calories IS NULL) AS calories_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.dailyCalories_secondPeriod` 

Results:

| id_nulls |	activityDay_nulls |	calories_nulls |
| :---: | :---: | :---: |
| 0	| 0	| 0 |


**dailySteps_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityDay IS NULL) AS activityDay_nulls,
      COUNTIF(StepTotal IS NULL) AS stepTotal_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.dailySteps_secondPeriod` 


 Results:

| id_nulls |	activityDay_nulls |	stepTotal_nulls |
| :---: | :---: | :---: |
| 0	| 0	| 0 |   


**heartrate_seconds_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(Time IS NULL) AS time_nulls,
      COUNTIF(Value IS NULL) AS value_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.heartrate_seconds_secondPeriod`

Results:
| id_nulls	| time_nulls	| value_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 


**hourlyCalories_secondPeriod**

    SELECT 
        COUNTIF(Id IS NULL) AS id_nulls,
        COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
        COUNTIF(Calories IS NULL) AS calories_nulls
        
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyCalories_secondPeriod` 

Results:

| id_nulls |	activtyHour_nulls |	calories_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 


**hourlyIntensities_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
      COUNTIF(TotalIntensity IS NULL) AS totalIntensity_nulls,
      COUNTIF(AverageIntensity IS NULL) AS averageIntensity_nulls
      
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlyIntensities_secondPeriod`

Results:

| id_nulls |	activtyHour_nulls |	totalIntensity_nulls |	averageIntensity_nulls |
| :---: | :---: | :---: | :---: |
| 0 | 0	| 0 | 0 |


**hourlySteps_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityHour IS NULL) AS activtyHour_nulls,
      COUNTIF(StepTotal IS NULL) AS stepTotal_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.hourlySteps_secondPeriod`

Results: 

| id_nulls |	activtyHour_nulls |	stepTotal_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 


**minuteCaloriesNarrow_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Calories IS NULL) AS calories_nulls
      
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteCaloriesNarrow_secondPeriod`

Results: 

| id_nulls |	activtyMinute_nulls |	calories_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 


**minuteIntensitiesNarrow_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Intensity IS NULL) AS intensity_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteIntensitiesNarrow_secondPeriod`

Results: 

| id_nulls |	activtyMinute_nulls |	intensity_nulls |
| :---: | :---: | :---: |
| 0 | 0	| 0 | 



**minuteMETsNarrow_secondPeriod**

    SELECT 
          COUNTIF(Id IS NULL) AS id_nulls,
          COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
          COUNTIF(METs IS NULL) AS METs_nulls
          
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteMETsNarrow_secondPeriod`


Results: 

| id_nulls |	activtyMinute_nulls |	METs_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |


**minuteSleep_secondPeriod**


    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(date IS NULL) AS date_nulls,
      COUNTIF(value IS NULL) AS value_nulls,
      COUNTIF(logId IS NULL) AS logId_nulls
      
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteSleep_secondPeriod`
    

Results: 

| id_nulls |	date_nulls |	value_nulls |	logId_nulls |
| :---: | :---: | :---: | :---: |
| 0 |	0 |	0 |	0 |


**minuteStepsNarrow_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(ActivityMinute IS NULL) AS activtyMinute_nulls,
      COUNTIF(Steps IS NULL) AS Steps_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.minuteStepsNarrow_secondPeriod`

Results:

| id_nulls |	activtyMinute_nulls |	Steps_nulls |
| :---: | :---: | :---: |
| 0	 | 0 |	0 |


**sleepDay_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(SleepDay IS NULL) AS sleepDay_nulls,
      COUNTIF(TotalSleepRecords IS NULL) AS totalSleepRecords_nulls,
      COUNTIF(TotalMinutesAsleep IS NULL) AS totalMinutesAsleep_nulls,
      COUNTIF(TotalTimeInBed IS NULL) AS totalTimeInBed_nulls
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.sleepDay_secondPeriod` 

| id_nulls |	sleepDay_nulls |	totalSleepRecords_nulls |	totalMinutesAsleep_nulls |	totalTimeInBed_nulls |
| :---: | :---: | :---: | :---: | :---: |
| 0	 | 0 |	0 | 0 | 0 |


**weightLogInfo_secondPeriod**

    SELECT 
      COUNTIF(Id IS NULL) AS id_nulls,
      COUNTIF(Date IS NULL) AS date_nulls,
      COUNTIF(WeightKg IS NULL) AS weightKg_nulls,
      COUNTIF(WeightPounds IS NULL) AS weightPounds_nulls,
      COUNTIF(Fat IS NULL) AS fat_nulls,
      COUNTIF(BMI IS NULL) AS BMI_nulls,
      COUNTIF(IsManualReport IS NULL) AS isManualReport_nulls,
      COUNTIF(LogId IS NULL) AS logId_nulls
      
    
    FROM `analysisbellabeat246.FitabaseData_20160412_20160512.weightLogInfo_secondPeriod`


Results:

| id_nulls | date_nulls | weightKg_nulls | weightPounds_nulls | fat_nulls | BMI_nulls | isManualReport_nulls | logId_nulls |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 0 | 0 | 65 | 0 | 0 | 0 |
  
