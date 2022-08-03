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

![moving work book](https://user-images.githubusercontent.com/107150730/182656098-b6a97d7b-2702-4414-8a92-5b3bc148d54f.jpg)

![copied excel](https://user-images.githubusercontent.com/107150730/182656739-549d12ab-d17b-460d-b3b1-18eb91379153.jpg)

The combined dataset was formatted as a table and was now ready to be cleaned. <br/>
The date column had some part formatted as text and other parts formatted as date data type, so the date column was converted to date data type
of the format "dd-mm-yyyy" using the Excel Text to Column feature.

![converting text to date](https://user-images.githubusercontent.com/107150730/182657318-b5b24806-eea0-4cb0-b508-218889d9ca02.jpg)

The remaining columns were filtered to check for anomalies and missing values were replaced with "nil" if they were in a field with the text data type and "0" if they were in fields that contained integers. This was done using the Excel Find and Replace feature.

![find and replace](https://user-images.githubusercontent.com/107150730/182657918-af6f1bbf-ed44-43d1-a9a7-218a062a7515.jpg)

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

![count of columns excel](https://user-images.githubusercontent.com/107150730/182658314-cedd972d-9200-48ee-953b-e210a67a1ed7.jpg)

## Power Query
Prior to loading the dataset into Power BI, it was transformed in Microsft Power Query <br/>

The Time column appeared as datetime so the data type was changed to "time" format. Values initially labelled as "nil" showed errors and were then replaced with "00:00:00".

![image](https://user-images.githubusercontent.com/107150730/182659278-5fded114-4784-4732-a12d-1346d3d3640c.png)

A new column for "Cause" was added using Conditional Column feature in Power Query. This was composed of 5 categories namely: Pilot Error, Technical Failure, Weather, Attacked and Others(Those airplane crash where the cause was unknown, or crashed into objects, or crashed into the sea).

![image](https://user-images.githubusercontent.com/107150730/182659932-d6d1339c-a267-488b-8684-0578fd26e288.png)

The following from Country column were replaced to enhance compatibility with the shape map visual:
- "United States" was replaced with "United States of America"
- "USSR" was replaced with "Russia"
- "Tanzania" was replaced with "United Republic of Tanzania"
- "Zaire" and "Democratic Republic of Congo" were replaced with "Democratic Republic of the Congo"

"Test" and "Testing" in the Route column were replaced with "Test flight" to ensure uniformity

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
- Total Survivors
- Fatality Rate <br/>

![image](https://user-images.githubusercontent.com/107150730/182662661-35953be4-fc23-4141-9ee7-383c4e7cd6a1.png)

The following columns were also created using DAX:
- NYear: A Year column to be used in the visuals
- NMonth: A Month column to be used in the visuals

![image](https://user-images.githubusercontent.com/107150730/182663117-e49354dc-a562-43cc-97be-8d0a9e433e3b.png)

Data categorization was used to categorize Country as Place and a Custom Shape Map file was imported into Power BI.

![image](https://user-images.githubusercontent.com/107150730/182663491-8f75cfcc-7d6f-4d40-b608-ffc4035850b1.png)

![image](https://user-images.githubusercontent.com/107150730/182663779-c41b0ae9-940c-4606-926d-c2046e62339c.png)

# Analysis
## Key Indices
From September 17,1908 to July 30,2019, there was a total of 5,521 crashes out of which there were no survivors in 3,687 of the crashes. There was a total of 153,837 people aboard the flights. The Fatality Rate was 73% with 112,332 people losing their lives. The Overall Fatality including ground victims amounted to 118,189 and the Total amount of suvivors was 41,505.

![image](https://user-images.githubusercontent.com/107150730/182669875-0a2242d4-4a11-4362-bafb-048d2eeac10b.png)

## Time Trend
### By Year
Since the first airplane crash in 1908, there was a gradual increase in air accidents. The year 1972 was the deadliest year in aviation history and had the most crash with 104 crashes claiming 2967 lives. It is followed closely by 1968 and 1989 with 96 and 95 crashes respectively. However there has been a staggering 90% decrease in airplane crash over the last 3 decades, a result of technology, adherence to safety regulations, improvement in air traffic control and better pilot training.

![image](https://user-images.githubusercontent.com/107150730/182670403-7f8dbb9d-5ab7-474f-a610-4c1f4114566c.png)

However the year 2001 accounts for the most fatalities on ground(2,891) which is largely due to the terror attack where two Boeing-767s were hijacked by terrorists and crashed into the World Trade Center, New York, USA claiming 2,750 lives.

![image](https://user-images.githubusercontent.com/107150730/182685070-e48642cc-fcab-44b6-a7d1-c767fa9af34c.png)

### By Month
The trend of crash by month shows the highest peak in December(537 crashes) followed by January(512 crashes) and August(506 crashes) and higher number of crashes taking place in the second half of the year. These peaks are partly due to the bad weather towards the end and beginning of the year.

![image](https://user-images.githubusercontent.com/107150730/182684230-62eeb478-ba43-4dce-97c8-1610da29dc96.png)

The trend of crash by month is also similar to that of fatality on air by month showing most peaks in the second half of the year; This corresponds to the time in which most people travel either due to the holidays or vacations. The deadliest months being December (10,908 fatalities) followed closely by August and September with 10,563 and 10,533 fatalities respectively.

![image](https://user-images.githubusercontent.com/107150730/182684634-bc9101c1-7ceb-41a2-ba04-ddcf67e325ae.png)

## Operator
Founded in 1923, Aeroflot, the flag carrier and largest airline of Russia (and formerly the Soviet Union), had the highest number of fatal crashes(179), with a total of 7,156 passengers dying in Aeroflot crashes. Most of the crash occurred during the soviet era and majority of the planes that crashed were old soviet models. This is followed closely by the US-Military with a total crash of . This is partly due to the harsh conditions in which these aircrafts operate and the limits they are pushed to during combat operations, and rescue missions.

![image](https://user-images.githubusercontent.com/107150730/182695979-6b418e62-69d4-4937-899c-143e42f2e873.png)

However, the Operator with the most fatalities involving ground victims is American Airlines with 2889 fatalities on ground. Part of this can be accounted for by the September 11, 2001 attack when two Boeing-767 belonging to American Airlines and United Airlines respectively were hijacked and crashed into the World Trade Center leading to a combined death toll of 2750.

![image](https://user-images.githubusercontent.com/107150730/182696917-9f18e356-c8ef-4e30-9dd0-75d91570b543.png)

## Type
The Douglas DC-3 is a propeller-driven airliner, which had a lasting effect on the airline industry in the 1930s to 1940s and World War II. It was born into a nascent airline industry when travelling by air was riskier. It accounted for 335 crashes and 4824 fatalities.

![image](https://user-images.githubusercontent.com/107150730/182698088-05c49dd8-d935-4ec7-a537-d2c63a4e7681.png)

However, the Boeing 767-223ER and Boeing B-767-222 account for the most fatalities on ground due to the 2001 terror attack on the World Trade Center, New York, USA claiming 2750 lives.
## Location
The United States accounts for 1407 crashes. This could be partly attributed to the weather and also the large air transport network within the US due to the large distance between cities. <br/>
Russia accounts for 260 Crashes. This is largely due to the mountainous terrain and harsh weather. <br/>
Brazil holds the spot for the 3rd country with the highest crash(194). This is partly due to lack of adherence  to safety regulations. It is followed closely by Colombia and Canada with 157 and 153 crashes respectively.

![image](https://user-images.githubusercontent.com/107150730/182698585-1cb4898e-6e3e-4906-95a2-425f2046109d.png)

What was to be one of the worst disasters in aviation history occurred as a result of a series of unfortunate events, starting with an explosion at Gran Canaria airport in Spain. This resulted in a number of flights being diverted to Tenerife Airport. As a result of dense fog, the absence of ground radar, and miscommunication, two Boeing 747s belonging to Pan American Airways and KLM collided with each other, claiming the lives of all 583 passengers on board in both the flights of which only 61 passengers from the Pan Amercan flight survived.

![image](https://user-images.githubusercontent.com/107150730/182699283-046b83d2-c274-4584-8522-882f0f1a620e.png)

Training Route accounted for the highest amount of crash(86)

![image](https://user-images.githubusercontent.com/107150730/182700907-f3c8c78b-108b-4665-b3dd-9a9fc556ae93.png)

## Cause
Pilot Error accounted for 37.69% (1179) of Airplane crash followed closely by Weather and Technical Failure accounting for 29.76%(931) and 28.01%(876) respectively. Other causes of airplane crash not included in the charts include those that the causes were unknown, those that crashed into objects, those that crashed over the sea and those that vanished.

![image](https://user-images.githubusercontent.com/107150730/182702051-8797da71-5290-4ec0-96e9-016ed0ce3bc7.png)


