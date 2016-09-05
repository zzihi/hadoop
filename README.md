Hadoop Lecture
==================

- 실습 데이터 (영국 교통사고 데이터)

> 사고 이력 : https://github.com/longnym/lecture/raw/master/sample_data/DfTRoadSafety_Accidents.zip

> 사상자 정보 : https://github.com/longnym/lecture/raw/master/sample_data/DfTRoadSafety_Casualties.zip

> 지역 코드 : https://github.com/longnym/lecture/raw/master/sample_data/DfTRoadSafety_District.zip

> 데이터 활용 가이드 : http://github.com/longnym/lecture/raw/master/sample_data/Road-Accident-Safety-Data-Guide.xls

<br>

- MapReduce Application 다운로드

> http://github.com/longnym/lecture/raw/master/build/hadoop_ex01.jar

> http://github.com/longnym/lecture/raw/master/build/hadoop_ex02.jar

> http://github.com/longnym/lecture/raw/master/build/hadoop_ex03.jar

<br>

- Driver Class의 실행 (실습 1)

>hadoop jar hadoop_ex01.jar -D inputPath=/input/acc/Accidents_2005_2015.csv -D outputPath=/output/result01 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Driver Class의 실행 (실습 2)

>hadoop jar hadoop_ex02.jar -D inputPath=/input/acc/Accidents_2005_2015.csv -D outputPath=/output/result02 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Driver Class의 실행 (실습 3)

>hadoop jar hadoop_ex03.jar -D inputPath1=/input/acc/Accidents_2005_2015.csv -D inputPath2=/input/cas/Casualties_2005_2015.csv -D cachePath=/input/dis/District.txt -D tempPath=/output/result03_1 -D outputPath=/output/result03_2 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Yarn Application의 실행

>yarn jar simple-yarn-app-1.1.0.jar com.hortonworks.simpleyarnapp.Client /bin/date 2 hdfs:///test/simple-yarn-app-1.1.0.jar

<br>

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

- PIG Table 생성 (Accidents)

>A = LOAD '/input/acc/Accidents_2005_2015.csv' USING PigStorage(',') AS (
<br>Accident_Index:chararray, Location_Easting_OSGR:chararray, Location_Northing_OSGR:chararray, 
<br>Longitude:chararray, 
<br>Latitude:chararray, 
<br>Police_Force:chararray, 
<br>Accident_Severity:chararray, 
<br>Number_of_Vehicles:chararray, 
<br>Number_of_Casualties:chararray, 
<br>Date_Acc:chararray, 
<br>Day_of_Week:chararray, 
<br>Time:chararray, 
<br>District:chararray, 
<br>Highway:chararray, 
<br>first_Road_Class:chararray, 
<br>first_Road_Number:chararray, 
<br>Road_Type:chararray, 
<br>Speed_limit:chararray, 
<br>Junction_Detail:chararray, 
<br>Junction_Control:chararray, 
<br>second_Road_Class:chararray, 
<br>second_Road_Number:chararray, 
<br>Pedestrian_Crossing_Human_Control:chararray, 
<br>Pedestrian_Crossing_Physical_Facilities:chararray, 
<br>Light_Conditions:chararray, 
<br>Weather_Conditions:chararray, 
<br>Road_Surface_Conditions:chararray, 
<br>Special_Conditions_at_Site:chararray, 
<br>Carriageway_Hazards:chararray, 
<br>Urban_or_Rural_Area:chararray, 
<br>Did_Police_Officer_Attend_Scene_of_Accident:chararray, 
<br>Lower_Super_Ouput_Area_of_Accident_Location:chararray);

<br>

- Hive QL

>set hive.execution.engine=mr
<br>select a.Day_of_Week,c.Sex_of_Casualty, count(1) from accidents a join casualties c on a.accident_index = c.acc_index group by Day_of_Week,Sex_of_Casualty;

<br>

- MySQL 샘플 데이터

> https://github.com/datacharmer/test_db/archive/master.zip

<br>

- Sqoop Import

> sqoop import --driver com.mysql.jdbc.Driver --connect jdbc:mysql://localhost/employees --username root --table employees --target-dir /test/employees

<br>

- Sqoop Export

> sqoop export --driver com.mysql.jdbc.Driver --connect jdbc:mysql://localhost/employees --username root --table employees --export-dir /test/employees
