# BellabeatCaseStudy
Bellabeat Case Study 

# Phases of data analysis process about Bellabeat Ivy 


## Ask 


**What is the problem you are trying to solve?**  

Identify trends and patterns from overall smart devices usage data in order to draw insights and how they may apply in a Bellabeat product**  	
 
**How can your insights drive business decisions?**

My insights can influence in how to address the new Bellabeat marketing strategy.

  

**Business Task**

*Draw meaningful insights from smart device usage trends and how they can impact on Bellabeat marketing strategy*


## Prepare

**About the data**
These datasets were generated by respondents to a distributed survey via Amazon Mechanical Turk between 03.12.2016-05.12.2016. Thirty eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring.
Prepare Guiding questions
 
 - Where is your data stored?   
 **Data is stored in a collection of datasets on Kaggle**
 **This collection contains several tables across different metrics of personal tracker data**
 **This collection is broken down into two folders,  both with same metrics but each folder contains data in different periods of time**

 - How is the data organized? Is it in long
   or wide format?  
   **The data is organized in two folders, each folder representing a different period of time:**
   
	 - First Folder (11 tables) **2016/03/11 - 2016/04/11** 
		 - `dailyActivity_merged.csv` 
			 - The dataset is in **wide format**.

				-   Each data subject `id` has a row of a combination of multiple attributes such as `TotalSteps, TotalDistance, TrackerDistance, etc`.
				    
				-   Variables are spread across the columns. Columns represent different metrics like steps, distance, active minutes, etc.
				- Each variable has its own column.

		 - `heartrate_seconds_merged.csv`  
			 - The dataset is in **long format**.

				-   Each row is a single observation of the variable `heart rate value`   by a specific user `id` at a specific time `Time`.
				    
				-  The subject user `id` is repeated across multiple rows to represent the value `heart rate`  at different points of time `Time`
				
		- `hourlyCalories_merged.csv`
			- The dataset is in **long format**.
				-  Each row is a single observation of the variable `number of calories burnt`   by a specific user `id` at a specific time `ActivityHour`.
				    
				-  The subject user `id` is repeated across multiple rows to represent a value of `Calories`  at different hours `ActivityHour`.
		
		- `hourlyIntensities_merged.csv`
			- The dataset is in **long format**. It has more than column apparently representing more than one variable. In reality, the second column represents an aggregate function to calculate the **average** of intensity state exhibited during a specific hour by the user. In other words, the column `AverageIntensity` is the statistical summary of the variable `TotalIntensity`.  Therefore, this dataset only contains one variable where each row represents one observation of this variable at a specific time.

		- `hourlySteps_merged.csv` - The dataset is in **long format**.
  
		- `minuteCaloriesNarrow_merged.csv` - The dataset is in **long format**.
     
		- `minuteIntensitiesNarrow_merged.csv` - The dataset is in **long format**.
     			
		- `minuteMETsNarrow_merged.csv` - The dataset is in **long format**.
			
		- `minuteSleep_merged.csv`
			- The dataset is in **wide format**.  Each row represents a unique combination of identifiers (user **id**, **date** and **logId**).
			
		- `minuteStepsNarrow_merged.csv` - The dataset is in **long format**
		
		- `weightLogInfo_merged.csv`
			- The dataset is in **wide format**. Each data subject `id` has a row of a combination of multiple attributes such as `WeightKg, WeightPounds, Fat, BMI, IsManualReport, LogId`

	- Second Folder  (18 tables) **2016/04/11 - 2016/05/11** 
		 - `dailyActivity_merged.csv*` - The dataset is in **wide format**.
			
		 - `dailyCalories_merged.csv` - The dataset is in **long format**.
		
		- `dailyIntensities_merged.csv`
			- The dataset is in **wide format**. In this dataset there is a combination of multiple columns representing attributes for each row. Each column has its own variable.  A single row has atributes such as `SedentaryMinutes, LightlyActiveMinutes, VeryActiveMinutes, ModeratelyActiveDistance, etc.`
		
		- `dailySteps_merged.csv` - The dataset is in **long format**.
			
		- `heartrate_seconds_merged.csv` - The dataset is in **long format**.
			
		- `hourlyCalories_merged.csv` - The dataset is in **long format**.
			
		- `hourlyIntensities_merged.csv` - The dataset is in **long format**.
			
		- `hourlySteps_merged.csv` - The dataset is in **long format**.
			
		- `minuteCaloriesNarrow_merged.csv` - The dataset is in **long format**.
			
		- `minuteCaloriesWide_merged.csv`
			- The dataset is in **wide format**.  *It has multiple columns that contain the same type of data for different time points.*  For example, columns for `"Calories00", "Calories01", "Calories02"... "Calories59"`  
			E.g.
			***Calories05 = calories burned in fifth minute of the hour.***
			
		- `minuteIntensitiesNarrow_merged.csv`
			- The dataset is in **long format**. The same data as "minuteCaloriesWide_merged.csv" but in long format. **The time points (minutes) are spread out through the rows.**
			
		- `minuteIntensitiesWide_merged.csv` - The dataset is in **wide format**.
			
		- `minuteMETsNarrow_merged.csv` - The dataset is in **long format**.
			
		- `minuteSleep_merged.csv` - The dataset is in **wide format**.
			
		- `minuteStepsNarrow_merged.csv` - The dataset is in **long format**.
			
		- `minuteStepsWide_merged.csv` - The dataset is in **wide format**.
			
		- `sleepDay_merged.csv`
			- The dataset is in **wide format**. The number of rows in this dataset can initially suggest a "long" format, especially when it can be observed many repeated IDs or timestamps. But **the format (wide vs. long) is not defined by the number of rows**. it’s defined by **how the variables are organized**
Each row of this dataset is a summary of many variables (`TotalSleepRecords, TotalMinutesAsleep, TotalTimeInBed `) for a specific time `SleepDay`

			
		- `weightLogInfo_merged.csv` - The dataset is in **wide format**.

****
 - Are there issues with bias or credibility in this data? Does your
   data ROCCC?
   
    **Reliability**
	   
	 - ***Uncertainty about bias in the data***: The authors of this dataset doesn't share any information about how participants were chosen for the sample. Therefore, we cannot make sure if the data was collected using random sampling to fairly have a good representation of the population. 
	 - **Small sample**:  This dataset has a sample size of 30 users. Even though it has been statistically proven that 30 is the smallest sample size where an average result of a sample starts to represent the average result of a population, this dataset is at borderline of this minimum number. A larger sample size would have been better to get more accurate and reliable results from analysis,specially in very large market. According to [statista](https://www.statista.com/forecasts/1425172/fitness-tracker-users-by-segment-us), In 2024, there were around 62 million fitness tracker users in the United States (35% women). In the near future, the number of fitness tracker users is forecast to steadily increase, jumping to over 92 million by 2029. 



    **Original**
   
    The dataset is ***third-party data*** , shared by the user *Möbius* on Kaggle. 
    Möbius has attached the link of the original source which it comes from an **open data source**, under a **Creative Commons Attribution 4.0 International license**. meaning anyone can copy, distribute, remix, and build upon the material for any purpose, even commercially, as long as you give credit for the original creators. 
     In other words, you can have accessibility to the **original data source** under a permissive license to give credit to the **original authors** who collect and generate this dataset.
  
    **Comprehensive**
  
    ***Critical Information needed to solve the business task***
    The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products
    
    ***Data contained in FitBit Fitness Tracker  datasets***
    FitBit Fitness Tracker Data contains user's information about their heart rate, sleep monitoring, daily activity by tracking totals for steps, intensity, distance, calories, and logged activities.
    We can make sure that the datasets utilized for this analysis cover most of the important metrics that Bellabeat uses to provide insights about its user's health and wellness.
    We are lacking of specific information about reproductive health data for women, but this is an exclusive feature that Bellabeat offers compared to other brands. 
  
    ***Completeness***
    
     - **Small sample size**: The sample size fall short, using only *thirty people* as sample size of a huge population that every year is growing more and more. 
     - **Short period of time**: The data collection was released during two months 2016/03/12 - 2016/05/12. This period of time might be a limitation to track noticeable changes in user's routine. According to [James Clear](https://jamesclear.com/new-habit#:~:text=On%20average%2C%20it%20takes%20more,to%20form%20a%20new%20habit.), "***On average, it takes more than 2 months before a new behavior becomes automatic — 66 days to be exact.** And how long it takes a new habit to form can vary widely depending on the behavior, the person, and the circumstances. In Lally’s study, it took anywhere from 18 days to 254 days for people to form a new habit.*"
  
  
  
    **Current**
   
    Checking the dataset *FitBit Fitness Tracker Data* in its original source, we notice that the last time updated was May 31, 2016. This data is out of date, which it means that the data is less relevant to the current time this analysis is being performed.
    
    **Cited**
  
    These datasets were created by *Robert, Brinton Furberg, Julia Brinton, Michael Keating and Alexa Ortiz*, published and hosted via Zenodo website, a reliable open repository. 
    The data was collected by a distributed survey via Amazon Mechanical Turk between 03/12/2016-05/12/2016. 
  
     *Citation*
    Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo.
    [https://doi.org/10.5281/zenodo.53894](https://doi.org/10.5281/zenodo.53894)
****
 - How are you addressing licensing, privacy, security, and
   accessibility?
  
 ### Authors
 Furberg, Robert.
 Brinton, Julia.
 Keating, Michael.
 Ortiz, Alexa.
 
 ### Citation
   
   Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo.
  
  ### Rights

**License**

 ![cc-by-4.0 icon](https://zenodo.org/static/icons/licenses/cc-by-icon.svg)  
[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/legalcode)
   
   ****
  
 - How does it help you answer your question?     
 
*FitBit Fitness Tracker Data* contain all critical information (such as heart rate, sleep monitoring, and daily activity) to draw insights, identify patterns and trends into how people how people are using wearable devices. It is cited as well and comes from an original and reliable source. The dataset is structured and organized to start cleaning the data and performing analysis.


****
 -  Are there any problems with the data?
 
**Problems and limitations with the data**:

-   **Small sample size:**  This dataset has a sample size of 30 users. The market of people using wearable devices is huge (80 million just in USA) and growing each year. This can be a limitation to get an accurate result of the sample that fairly represents the entire population.  
-   **Out of date**: The data was generated since 2016, making it more irrelevant due to  the analysis is being conducted in 2025.
-   **Limited period of time:** This period of time might be a limitation to track any change in user's routine, which is essential to identify outliers and have a more complete representation of patterns and tends people have in their wellness and daily activity.
-   **Possible biased sample:** The sample may not be a fair representation of the population. We don't have accessibility to details about how participants were eligible to the survey. 
-   **Lack of demographic data**: Age and gender are not specified, this is essential information because Bellabeat products are targeted to women. 
- **Lack of reproductive health data**: Bellabeat tracks reproductive data such as menstrual cycle, pregnancy and fertility. Nevertheless, this dataset doesn't contain any information about these type of metrics.


 **Possible missing data or inconsistencies: Must be checked during processing.**

Key tasks 
1. Download data and store it appropriately. 
2. Identify how it’s organized. 
3. Sort and filter the data. 
4. Determine the credibility of the data. 

**Deliverable.**
 A description of all data sources used


## Process 

Process Guiding questions 
- What tools are you choosing and why? 
**Cleaning data**.
I decided to process and clean the data using SQL because SQL 
- Have you ensured your data’s integrity? 

**Changelog**
Author: Aldair Pichon Aguila.
 
1. I downloaded the datasets from Kaggle in my local machine. 05/20/2025
2. I renamed the two main folders that contain the datasets to ensure better clarity, consistency and organization of the data following guidelines of naming conventions:
	Fitabase Data 3.12.16-4.11.16  ->   FitabaseData_20160312-20160411
	Fitabase Data 4.12.16-5.12.16  ->  FitabaseData_20160412-20160512
	
05/20/2025
  
3. I created a new project in BigQuery named `analysisbellabeat246` and two datasets for each of the two folders. 05/20/2025
4. When uploading the table `heartrate_seconds_merged.csv` and checking the auto-detect box to automatically set the schema for this table in BigQuery, then it tries to parse the column `"Time"` as TIMESTAMP data type. Due to the original format of `"Time"`  is one that BigQuery cannot recognized as TIMESTAMP, it returns an error.  To fix this problem, rather than BigQuery auto detecting the schema of the table, I manually specified the schema in JSON format and defining the column `"Time"` as STRING instead of TIMESTAMP.
 In order to figure out the name, data type and description of each column I referred to the document [Fitbit Data Dictionary](https://www.fitabase.com/media/2088/fitabase-fitbit-data-dictionary-as-of-4524.pdf). 05/20/2025
 
 
	    [  
			{  
				"description": "Id",  
				"mode": "NULLABLE",  
				"name": "Id",  
				"type": "INTEGER"  
			},  
			{  
				"description": "Time",  
				"mode": "NULLABLE",  
				"name": "Time",  
				"type": "STRING"  
			},  
			{  
				"description": "Value",  
				"mode": "NULLABLE",  
				"name": "Value",  
				"type": "INTEGER"  
			}  
		]

5. I uploaded the rest of tables through manually writing the schema in JSON format for the datasets `FitabaseData_20160312-20160411` and `FitabaseData_20160412-20160512`.
    [Here](SchemaTables.md) you can find the code in JSON format to define the schemma of tables uploaded in BigQuery. Except for the tables `dailyCalories`,  `dailyIntensities`, and `dailySteps`. Their schema created automatically by BigQuery due to it didn't have problems to parse them.
    05/21/2025
 
7. When uploading the tables into the dataset `FitabaseData_20160412-20160512`, I decided to add `_secondPeriod` at the end of each table's name to distinguish these tables from the tables of the `FitabaseData_20160312-20160411` dataset . It will avoid any confusion in the future when merging the tables. This is important because after downloading the datasets from Kaggle I noticed that some table's name repeat across the two folders representing the same information but in different periods of time. 05/21/2025
   
    E.g.
    
    	 `FitabaseData_20160312-20160411 -> heartrate_seconds_merged.csv`
    	 `FitabaseData_20160412-20160512 -> heartrate_seconds_merged.csv`
    	 
    Renamed tables after uploading in BigQuery 
    
    	 `FitabaseData_20160312-20160411 -> heartrate_seconds.csv`
    	 `FitabaseData_20160412-20160512 -> heartrate_seconds_secondPeriod.csv`


8.  Checking for NULL values in each table. In order to figure out how to address possible NULL values in the data, first I need to know if they exist at all and in what columns. I counted the null values for each column in each table of the project. [Here](checkingNulls.md) you can see the queries used and the results in each table.
   05/26/2025

9. Before knowing what tables I'm going to use for the analysis, I decided to to go over some certain tables and determinate if they represent accurate and comnplete information for analysis and make sense with other tables. 

10. Checking for consistency between minute tables in each dataset.  Allegedlly, each minute table contains a specific metric (calories, steps, METs, intensities, and sleep) that was tracked simultaniously at the same time and for the same users (Id) along with the other metrics. Therefore, I decided to compare and see if the tables contain the same users Id and during the same periods of time. For this task, I used SQL along with Google sheets.









    
12. I ensured that minutes and hours tables were consistent between them in each dataset. They allegedlly were tracked during the same peiod of time and add up the same total for each id user.

	
13. I created a subquery in the `heartrate_seconds` table to convert the STRING values of the `"Time"` column to `TIMESTAMP` values using the `PARSE_TIMESTAMP()`function. 

    `enter code here`



 

Key tasks 
10. Check the data for errors. 
11. Choose your tools.
12. Transform the data so you can work with it effectively. 
13. Document the cleaning process.
