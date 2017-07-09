스쿱은 대량의 데이터를 아파치 하둡과 RDBMS 사이에서 전송하기 위해 디자인 된 툴이다. 

- 2012년 3월 아파치 톱레벨 프로젝트로 지정

- 현재 1.4.6이 최신 버전(2017.03.10)

- 스쿱2의 최신버전은 1.99.7, 스쿱1과 호환된지 않음, 아직 정식 릴리즈 되지 않음




<주요 기능>

- import: DB -> HDFS 로 데이터를 가져온다. 

- export: HDFS -> DB 로 데이터를 가져온다. 




<import - DB의 데이터를 HDFS로 이동 시킴>

[query 옵션을 이용하는 경우]

- DB의 데이터를 쿼리로 조회하여 target-dir 위치로 복사

sqoop import \

  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \

  --username scott \

  --password tiger \

  --query 'select * from sample_table WHERE $CONDITIONS' \

  --split-by column3 \

  --target-dir hdfs://localhost/user/hadoop/




[table, columns, where 옵션을 이용하는 경우 와 큐이름을 지정하는 경우]

sqoop import \

  -Dmapred.job.queue.name=queue \

  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \

  --username scott \

  --password tiger \

  --table sample_table \

  --columns column1 \

  --where column3=\"eu\" \

  --target-dir hdfs://localhost/user/hadoop/






<export - HDFS의 데이터를 DB로 이동 시킴>

[insert 하기]

- HDFS의 데이터를 DB에 insert 함, export-dir 위치의 데이터를 table 에 입력

sqoop export 

  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \

  --username scott \

  --password tiger \

  --table sample_table \

  --export-dir hdfs://localhost/user/hadoop/ \



[insert 하기 - 칼럼의 이름을 지정하여 입력]
sqoop export 
  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \
  --username scott \
  --password tiger \
  --table sample_table \
  --export-dir hdfs://localhost/user/hadoop/ \
  --columns column1,column2,column3


[update 하기]
- update 는 upudate-key 를 지정하여 처리할 수 있다. 
- columns 를 지정하지 않으면 update-key에 지정한 컬럼을 제외한 모든 칼럼을 update 한다.
- --update-mode는 updateonly, allowinsert 가 있다. 기본값은 updateonly 이다. 
- allowinsert 는 현재는 oracle 만 지원한다. 다른 DB는 프로시저를 이용하여 처리하여야 한다. 
sqoop export 
  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \
  --username scott \
  --password tiger \
  --table sample_table \
  --export-dir hdfs://localhost/user/hadoop/ \
  --columns column1,column2,column3 \
  --update-key column3 \
  --num-mappers 1


[프로시저 call 하기]
sqoop export 
  --connect jdbc:mysql://loclhost:7777/db?zeroDateTimeBehavior=convertToNull \
  --username scott \
  --password tiger \
  --call custom_proc \
  --export-dir hdfs://localhost/user/hadoop/ \
  --num-mappers 1 


출처: http://118k.tistory.com/454 [개발자로 살아남기]
