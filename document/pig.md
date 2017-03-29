Pig
==================

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
