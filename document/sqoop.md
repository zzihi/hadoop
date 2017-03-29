Sqoop
==================

- MySQL 샘플 데이터

> https://github.com/datacharmer/test_db/archive/master.zip
<br>$ mysql -u root -p < employees.sql

<br>

- Sqoop Import

> sqoop import --driver com.mysql.jdbc.Driver --connect jdbc:mysql://localhost/employees --username root --password hadoop --table employees --target-dir /test/employees

<br>

- Sqoop Export

> sqoop export --driver com.mysql.jdbc.Driver --connect jdbc:mysql://localhost/employees --username root --password hadoop --table employees --export-dir /test/employees

<br>

- Sqoop Usage : MySQL -> HDFS -> HIVE

>CREATE EXTERNAL TABLE IF NOT EXISTS EMPLOYEES ( 
<br>emp_no INT,
<br>birth_date DATE,
<br>first_name STRING,
<br>last_name STRING,
<br>gender STRING,
<br>hire_date DATE
<br>) 
<br>ROW FORMAT DELIMITED FIELDS TERMINATED BY "," 
<br>LOCATION '/test/employees';
