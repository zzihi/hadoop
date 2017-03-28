- Partitioned Hive Table 생성 (Accidents)

>CREATE EXTERNAL TABLE IF NOT EXISTS ACCIDENTS_P (
<br>Accident_Index STRING,
<br>Location_Easting_OSGR INT,
<br>Location_Northing_OSGR INT,
<br>Longitude DOUBLE,
<br>Latitude DOUBLE,
<br>Police_Force INT,
<br>Accident_Severity INT,
<br>Number_of_Vehicles INT,
<br>Number_of_Casualties INT,
<br>Date_Acc STRING,
<br>Day_of_Week INT,
<br>Time STRING,
<br>District INT,
<br>Highway STRING,
<br>first_Road_Class INT,
<br>first_Road_Number INT,
<br>Road_Type INT,
<br>Speed_limit INT,
<br>Junction_Detail INT,
<br>Junction_Control INT,
<br>second_Road_Class INT,
<br>second_Road_Number INT,
<br>Pedestrian_Crossing_Human_Control INT,
<br>Pedestrian_Crossing_Physical_Facilities INT,
<br>Light_Conditions INT,
<br>Weather_Conditions INT,
<br>Road_Surface_Conditions INT,
<br>Special_Conditions_at_Site INT,
<br>Carriageway_Hazards INT,
<br>Urban_or_Rural_Area INT,
<br>Did_Police_Officer_Attend_Scene_of_Accident INT,
<br>Lower_Super_Ouput_Area_of_Accident_Location STRING
<br>)
<br>PARTITIONED BY (Year_Acc STRING, Month_Acc STRING)
<br>ROW FORMAT DELIMITED FIELDS TERMINATED BY ","
<br>LOCATION '/input/acc';

<br>

- Non-Partitioned Table -> Partitioned Table
> set hive.exec.dynamic.partition.mode=nonstrict;
<br>INSERT OVERWRITE TABLE ACCIDENTS_P PARTITION (Year_Acc, Month_Acc) SELECT *, SUBSTR(Date_Acc, 7) AS Year_Acc, SUBSTR(Date_Acc,4,2) AS Month_Acc FROM ACCIDENTS;
