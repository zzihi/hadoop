Hadoop Lecture
==================

- 실습 데이터 (영국 교통 사고 이력)

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2005.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2006.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2007.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2008.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2009.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2010.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2011.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2012.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2013.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2014.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Accidents_2015.zip

<br>

- 실습 데이터 (영국 교통 사고 사상자 정보)

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2005.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2006.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2007.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2008.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2009.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2010.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2011.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2012.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2013.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2014.zip

> http://data.dft.gov.uk/road-accidents-safety-data/DfTRoadSafety_Casualties_2015.zip

<br>

- 실습 데이터 (지역 코드)

> https://github.com/longnym/mapreduce/raw/master/District.csv

<br>

- 실습 데이터 정의서

> http://data.dft.gov.uk/road-accidents-safety-data/Road-Accident-Safety-Data-Guide.xls

<br>

- MapReduce Application 다운로드

> wget https://github.com/longnym/mapreduce/raw/master/hadoop_ex01/hadoop_ex01.jar

> wget https://github.com/longnym/mapreduce/raw/master/hadoop_ex02/hadoop_ex02.jar

> wget https://github.com/longnym/mapreduce/raw/master/hadoop_ex03/hadoop_ex03.jar

<br>

- Driver Class의 실행 (실습 1)

>hadoop jar hadoop_ex01.jar -D inputPath=/input/acc/Accidents0514.csv -D outputPath=/output/result01 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Driver Class의 실행 (실습 2)

>hadoop jar hadoop_ex02.jar -D inputPath=/input/acc/Accidents0514.csv -D outputPath=/output/result02 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Driver Class의 실행 (실습 3)

>hadoop jar hadoop_ex03.jar -D inputPath1=/input/acc/Accidents0514.csv -D inputPath2=/input/cas/Casualties0514.csv -D cachePath=/input/dis/District.csv -D tempPath=/output/result03_1 -D outputPath=/output/result03_2 -D numReduceTasks=3 skill.coach.TestDriver

<br>

- Yarn Application의 실행

>yarn jar simple-yarn-app-1.1.0.jar com.hortonworks.simpleyarnapp.Client /bin/date 2 hdfs:///test/simple-yarn-app-1.1.0.jar

<br>

- Hive Table 생성 (Accidents)

>CREATE EXTERNAL TABLE IF NOT EXISTS ACCIDENTS (
<br>Accident_Index           STRING,
<br>Location_Easting_OSGR    STRING,
<br>Location_Northing_OSGR   STRING,
<br>Longitude                STRING,
<br>Latitude                 STRING,
<br>Police_Force             STRING,
<br>Accident_Severity        STRING,
<br>Number_of_Vehicles       STRING,
<br>Number_of_Casualties     STRING,
<br>Date_Acc                 STRING,
<br>Day_of_Week              STRING,
<br>Time                     STRING,
<br>District                 STRING,
<br>Highway                  STRING,
<br>first_Road_Class           STRING,
<br>first_Road_Number          STRING,
<br>Road_Type                STRING,
<br>Speed_limit              STRING,
<br>Junction_Detail          STRING,
<br>Junction_Control         STRING,
<br>second_Road_Class           STRING,
<br>second_Road_Number          STRING,
<br>Pedestrian_Crossing_Human_Control            STRING,
<br>Pedestrian_Crossing_Physical_Facilities      STRING,
<br>Light_Conditions                             STRING,
<br>Weather_Conditions                           STRING,
<br>Road_Surface_Conditions                      STRING,
<br>Special_Conditions_at_Site                   STRING,
<br>Carriageway_Hazards                          STRING,
<br>Urban_or_Rural_Area                          STRING,
<br>Did_Police_Officer_Attend_Scene_of_Accident  STRING,
<br>Lower_Super_Ouput_Area_of_Accident_Location  STRING
<br>)
<br>ROW FORMAT DELIMITED FIELDS TERMINATED BY ","
<br>LOCATION '/input/acc';

<br>

- PIG Table 생성 (Accidents)

>A = LOAD '/input/acc/Accidents0514.csv' USING PigStorage(',') AS (
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
