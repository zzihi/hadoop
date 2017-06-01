
sqoop 처리
==================
- sqoop Mysql HDFS 생성
>sqoop import --driver com.mysql.jdbc.Driver --connect jdbc:mysql://sl-us-south-1-portal.0.dblayer.com:15823/compose --username admin --password BKAHMJQHQQLPHCYV --table employees --target-dir /user/movios2/test/employees
<br>
- HDFS 생성 FILE 조회
>hadoop fs -ls /user/movios2/test/employees
