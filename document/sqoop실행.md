
sqoop 처리
==================
- sqoop Mysql HDFS 생성
>sqoop import --driver com.mysql.jdbc.Driver --connect jdbc:mysql://sl-us-south-1-portal.0.dblayer.com:15823/compose --username admin --password BKAHMJQHQQLPHCYV --table employees --target-dir /user/movios/test/employees
<br>
- HDFS 생성   조회
