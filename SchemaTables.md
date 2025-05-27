# Table Schema in JSON format

## FitabaseData_20160312_20160411

**heartrate** 

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "Time",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Value",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Heart rate value"   
    	}  
    ]

----

**hourlyCalories**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Calories",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of estimated calories burned"   
    	}  
    ]


-----

**hourlyIntensities**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "TotalIntensity",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Value calculated by adding all the minute-level intensity values that occurred within the hour"   
    	},
        {  
    		"name": "AverageIntensity",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Value calculated by adding all the minute-level intensity values that occurred within the hour"   
    	}    
    ]

----

**hourlySteps** 

     [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "StepTotal",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of steps taken"   
    	}  
    ]


**minuteCaloriesNarrow** 

    [  
    	{  	
        "name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Calories",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Total number of estimated calories burned"   
    	}  
    ]

----

**minuteIntensitiesNarrow** 

      [  
      	{  	
      		"name": "Id",  
      		"type": "INTEGER",  
      		"mode": "NULLABLE",
      		"description": "Id"   
      		 
      	},  
      	{  
      		"name": "ActivityMinute",  
      		"type": "STRING",  
      		"mode": "NULLABLE",
      		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
      	},  
      	{  
      		"name": "Intensity",  
      		"type": "INTEGER",  
      		"mode": "NULLABLE",
      		"description": "Intensity value. 0 = Sedentary, 1 = Light, 2 = Moderate, 3 = Very Active"   
      	}   
      ]

-----

**minuteMETsNarrow** 

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "METs",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "MET value for the given minute. Important: All MET values exported from Fitabase are multiplied by 10. Please divide by 10 to get accurate MET values"   
    	}   
    ]

   
**minuteSleep**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "date",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "value",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Value indicating the sleep state. 1 = asleep, 2 = restless, 3 = awake"   
    	},
      	
      {  
    		"name": "logId",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "The unique log id in Fitbit’s system for the sleep record"   
    	}    
    ]

----

**minuteStepsNarrow** 

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Steps",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of steps taken"   
    	}   
    ]

-----

**weightLogInfo**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "Date",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and time at which weight was recorded in mm/dd/yy hh:mm:ss format"  
    	},  
    	{  
    		"name": "WeightKg",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Weight recorded in kilograms"   
    	},
      	
      {  
    		"name": "WeightPounds",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Weight in pounds"   
    	},
       
      {  
    		"name": "Fat",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Body fat percentage recorded"   
    	},
    
      {  
    		"name": "BMI",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Measure of body mass index based on the height and weight in the participant’s Fitbit.com profile"   
    	},
    
      {  
    		"name": "IsManualReport",  
    		"type": "BOOLEAN",  
    		"mode": "NULLABLE",
    		"description": "If the data for this weigh in was done manually (TRUE), or if data was measured and synched directly to Fitbit.com from a connected scale (FALSE)"   
    	},
    
      {  
    		"name": "LogId",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "The unique log id in Fitbit’s systems"   
    	}    
    ]

----


## FitabaseData_20160412_20160512

**heartrate_secondPeriod**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "Time",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Value",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Heart rate value"   
    	}  
    ]

----

**hourlyCalories_secondPeriod**

    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Calories",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of estimated calories burned"   
    	}  
    ]

----

**hourlyIntensities_secondPeriod**

    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "TotalIntensity",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Value calculated by adding all the minute-level intensity values that occurred within the hour"   
    	},
        {  
    		"name": "AverageIntensity",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Value calculated by adding all the minute-level intensity values that occurred within the hour"   
    	}    
    ]

-----    
    
**hourlySteps_secondPeriod**
    
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityHour",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "StepTotal",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of steps taken"   
    	}  
    ]
    
----

**minuteCaloriesNarrow_secondPeriod** 

    [  
    	{  	
        		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Calories",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Total number of estimated calories burned"   
    	}  
    ]
    
----
    
**minuteIntensitiesNarrow_secondPeriod**
					    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Intensity",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Intensity value. 0 = Sedentary, 1 = Light, 2 = Moderate, 3 = Very Active"   
    	}   
    ]

-----

**minuteMETsNarrow_secondPeriod**
			
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "METs",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "MET value for the given minute. Important: All MET values exported from Fitabase are multiplied by 10. Please divide by 10 to get accurate MET values"   
    	}   
    ]

----   

**minuteSleep_secondPeriod** 
			
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "date",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "value",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Value indicating the sleep state. 1 = asleep, 2 = restless, 3 = awake"   
    	},
      	
      {  
    		"name": "logId",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "The unique log id in Fitbit’s system for the sleep record"   
    	}    
    ]

----

**minuteStepsNarrow_secondPeriod** 
			
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "ActivityMinute",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and hour value in mm/dd/yyyy hh:mm:ss format"  
    	},  
    	{  
    		"name": "Steps",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of steps taken"   
    	}   
    ]

-----

**sleepDay_secondPeriod**
			 
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "SleepDay",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date on which the sleep event started. (in mm/dd/yyyy hh:mm:ss format)"  
    	},  
    	{  
    		"name": "TotalSleepRecords",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Number of recorded sleep records for that day"   
    	},
      	
      {  
    		"name": "TotalMinutesAsleep",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total number of minutes classified as being “asleep” sum total of light, deep, and REM sleep)"   
    	},
    
      {  
    		"name": "TotalTimeInBed",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Total minutes spent in bed, including awake, light, deep, and REM sleep, during a defined sleep record"   
    	}     
    ]

-----

**weightLogInfo_secondPeriod**
    
    [  
    	{  	
    		"name": "Id",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Id"   
    		 
    	},  
    	{  
    		"name": "Date",  
    		"type": "STRING",  
    		"mode": "NULLABLE",
    		"description": "Date and time at which weight was recorded in mm/dd/yy hh:mm:ss format"  
    	},  
    	{  
    		"name": "WeightKg",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Weight recorded in kilograms"   
    	},
      	
      {  
    		"name": "WeightPounds",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Weight in pounds"   
    	},
       
      {  
    		"name": "Fat",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "Body fat percentage recorded"   
    	},
    
      {  
    		"name": "BMI",  
    		"type": "FLOAT",  
    		"mode": "NULLABLE",
    		"description": "Measure of body mass index based on the height and weight in the participant’s Fitbit.com profile"   
    	},
    
      {  
    		"name": "IsManualReport",  
    		"type": "BOOLEAN",  
    		"mode": "NULLABLE",
    		"description": "If the data for this weigh in was done manually (TRUE), or if data was measured and synched directly to Fitbit.com from a connected scale (FALSE)"   
    	},
    
      {  
    		"name": "LogId",  
    		"type": "INTEGER",  
    		"mode": "NULLABLE",
    		"description": "The unique log id in Fitbit’s systems"   
    	}    
    ]

-----
