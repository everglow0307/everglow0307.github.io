---
title:  "MYSQL 그룹별 ROWNUM 생성 방법"
excerpt: "MYSQL ROWNUM"

categories: 
  - mysql
tags:
  - [mysql]

toc: true
toc_sticky: true
 
date: 2022-07-14
---


### :one: MYSQL ROWNUM 생성 기초
MYSQL은 ORACLE과 같은 ROWNUM이 없기 때문에, 다음과 같은 방법으로 rownum을 만든다.

```sql
SELECT
    @ROWNUM:= @ROWNUM + 1,
    t.*
FROM
    test t,(SELECT @ROWNUM:=0) r
```
FROM절에서 변수 ROWNUM값을 초기화하고, SELECT절에서 ROWNUM을 +1한다. ROWNUM초기화할 때 데이터타입이 같아야한다.(위의 예제에서 @ROWNUM: = '' 이렇게 초기화하면 안 됨.)


<br><br>
### :two: MYSQL ROWNUM 그룹별 생성 
응용해서, 그룹별로 ROWNUM을 매기고 싶다면 아래와 같이 사용한다.

```sql
SELECT (
    CASE @VAL WHEN SUBSTRING(ts.write_datetime,3,2)
    THEN @R:=@R+1 
    ELSE @R:=1 END) AS rNum,
    (@VAL:=SUBSTRING(ts.write_datetime,3,2)) temp
FROM
    trouble_shooting ts,(SELECT @VAL:='', @R:=0) t
```
자료형이 다른 변수 @VAL과 @R을 FROM절에서 초기화하고, temp 컬럼에서 @VAL값을 넣어준다. CASE문에서 @VAL값을 비교해서 WHEN절의 조건(SUBSTRING(ts.write_datetime,3,2))을 충족하면 R+1해서 rownum을 매기고, 그외의 경우 1값으로 초기화한다. 

그룹조건에 따라 ROWNUM을 매기고 싶을 때 위와 같이 MYSQL쿼리를 사용한다.








