Hive
==================

- Hive Table 생성 (Accidents)

>CREATE EXTERNAL TABLE IF NOT EXISTS ACCIDENTS (
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
<br>ROW FORMAT DELIMITED FIELDS TERMINATED BY ","
<br>LOCATION '/input/acc';

<br>

- Hive Table 생성 (Casualties)

>CREATE EXTERNAL TABLE IF NOT EXISTS CASUALTIES (
<br>Acc_Index STRING,
<br>Vehicle_Reference INT,
<br>Casualty_Reference INT,
<br>Casualty_Class INT,
<br>Sex_of_Casualty INT,
<br>Age_Band_of_Casualty INT,
<br>Casualty_Severity INT,
<br>Pedestrian_Location INT,
<br>Pedestrian_Movement INT,
<br>Car_Passenger INT,
<br>Bus_or_Coach_Passenger INT,
<br>Pedestrian_Road_Maintenance_Worker INT,
<br>Casualty_Type INT,
<br>Casualty_Home_Area_Type INT
<br>)
<br>ROW FORMAT DELIMITED FIELDS TERMINATED BY "," 
<br>LOCATION '/input/cas';

<br>

- Hive QL

>set hive.execution.engine=mr;
<br>set hive.auto.convert.join=false;
<br>select a.Day_of_Week,c.Sex_of_Casualty, count(1) from accidents a join casualties c on a.accident_index = c.acc_index group by Day_of_Week,Sex_of_Casualty;

<br>

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
<br>LOCATION '/input/acc_p';

<br>

- Non-Partitioned Table -> Partitioned Table

> set hive.exec.dynamic.partition.mode=nonstrict;
<br>INSERT OVERWRITE TABLE ACCIDENTS_P PARTITION (Year_Acc, Month_Acc) SELECT *, SUBSTR(Date_Acc, 7) AS Year_Acc, SUBSTR(Date_Acc,4,2) AS Month_Acc FROM ACCIDENTS;

<br>
