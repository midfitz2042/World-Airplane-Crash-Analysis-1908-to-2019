# World-Airplane-Crash-Analysis-1908-to-2019
As part of my capstone project for the #NG30DaysOfLearning program, I analyzed Airplane Crashes around the world from 1908 to 2019.
# Introduction
In June 2022, I participated in a learning program organized by Olarenwaju Oyinbooke titled #NG30DaysOfLearning. This is my Capstone
project.
In this project, we were asked analyzed a dataset containing data of airplane accidents involving civil, commercial and military 
transport worldwide from 1908-09-17 to 2009-06-08:I went a step further and got another dataset that contained crashes from 2009 to 2019.
So I analyzed airplane crashes around the world from 1908 to 2019.
# Problem Statement
From the dataset provided, I would like to look at the trends in airplane crashes over the years, the airliners and operators that were
involved in these crash, the amount of people that died in these crash, the type of planes involved in these crash, the commonest causes
of airplane crash and where these crashes occured.
This analysis can help airliners take better safety precautions, educate pilots,beef up security and prevent future occurence.
# Data Sourcing
Both Datasets for this analysis were gotten from Kaggle
-First Dataset (1908-2009) from Kaggle
-Second Dataset (1908-2019) from Kaggle
# Data Cleaning in Microsft Excel and Power Query
## Microsoft Excel
The datasets were loaded into different excel workbooks, the original files were in .csv format so they were saved as .xlsx

Both datasets were checked to ensure they had the same number of columns and contained similar data types. The columns from the Second
(updated) dataset starting from the date 29-06-2009 to 30-7-2019 were then copied and pasted it into the First dataset after merging the workbooks.

The combined dataset was formatted as a table and was now ready to be cleaned. <br/>
The date column had some part formatted as text and other parts formatted as date data type, so the date column was converted to date data type
of the format "dd-mm-yyyy" using the Excel Text to Column feature.

The remaining columns were filtered to check for anomalies and missing values were replaced with "nil" if they were in a field with the text data type and "0" if they were in fields that contained integers. This was done using the Excel Find and Replace feature.

6 new colums were created to aid analysis namely:
- Country: This was created using the Location column with Text to Column feature and Flash Fill in Excel. Whitespaces were removed from the Country column using the =TRIM() function. It was noticed that the United States only contained names of states, so those states were replaced with "United States". Other typographical error were looked for manually and corrected within this column.
- With_or_without_survivor: Using the formula "=IF([@Aboard]=[@Fatalities],"No Survivors","Survivors")"
- Survivors: Using the formula "=[@Aboard]-[@Fatalities]"
- Total_crash_with_Survivors: Using the function "=COUNTIF(K:K,"Survivors")"
- Total_crash_without_Survivors: Using the function "=COUNTIF(K:K,"No Survivors")"
- Overall_Fatality: Using the formula "=[@Fatalities]+[@Ground]"

3 columns were then deleted namely:
- Flight
- Registration
- cn/in <br/>
This was done to because these columns were not going to be used in our analysis and thus not advisable to import them into Microsoft Power BI.

After combining the first and second datasets and cleaning in Microsoft Excel, the number of columns were 16 and the number of rows were 5522 (including the header row).
## Power Query
Prior to loading the dataset into Power BI, it was transformed in Microsft Power Query <br/>

The Time column appeared as datetime so the data type was changed to "time" format. Values initially labelled as "nil" showed errors and were then replaced with "00:00:00".

A new column for "Cause" was added using Conditional Column feature in Power Query. This was composed of 5 categories namely: Pilot Error, Technical Failure, Weather, Attacked and Others(Those airplane crash where the cause was unknown, or crashed into objects, or crashed into the sea).

The dataset was checked for duplicate rows and then loaded into Power BI for Visualization.
# Attributes of the data
- Date: The date the airplane crash occured
- Time: Local time in 24 hour fprmat
- Location: Location of the accident
- Operator: Airline or Operator of the aircraft
- Flight #: Flight number assigned by the operator
- Route: Complete or partial route flown prior to the accident
- Type: Aircraft type
- Registration: ICAO registration of the aircraft
- cn/in: Construction or serial number / Line or fuselage number
- Aboard: Total aboard (passengers / crew)
- Fatalities: Total fatalities aboard (passengers / crew)
- Ground: Total killed on the ground
- Summary: Brief description of the accident and cause if known <br/>
# Visualization
All the Visualization for this project were done in Microsoft Power BI <br/>
Upon loading the dataset into Power BI, the following measures were created using DAX(Data Analysis Expressions). This was done to optimize performance:
- Total Fatality on Air
- Total Fatality on Ground
- Overall Fatality
- Total Crash
- Total People Aboard
- Total Survivors <br/>

The following columns were also created using DAX:
- NYear: A Year column to be used in the visuals
- NMonth: A Month column to be used in the visuals

Data categorization was used to categorize Country as Place and a Custom Shape Map file was imported into Power BI.
# Analysis
