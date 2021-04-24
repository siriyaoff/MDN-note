# 1. DB란?
## SQL의 개요
table : 정보를 효율적으로 보관하기 위해 만들어놓은 공간  
database : table을 모아놓은 것  
SQL(Structured Query Language)
- database 하부 언어
- 여러 개의 table에서 원하는 정보를 읽고 쓰기 위해 사용

DBMS(Databse Management System)
- database 관리, data의 추가, 변경, 삭제, 검색 등의 기능 수행<br>e.g. Oracle, MySQL, Teradata ...
- DBMS의 특성
	- Real time processing
	- Continuous evolution
	- Concurrent sharing : 다수의 사용자가 동시에 접근, 이용이 가능
	- Contents reference : data의 참조는 data값에 따라 사용자의 요구에 맞는 것만 선택됨

DB의 구성
- table : spreadsheet와 비슷
- schema : DB의 논리적 구조(= table에 data가 저장되는 방식)
- column : table을 구성하는 각각의 정보(분류 기준) e.g. 고객 ID, 이름, 번호 ...
	- 각 열마다 data 형식이 지정됨
	- 세밀하게 분류될 수록 원하는 정보를 찾기 효율적임
- row : table의 data(= record)
- primary key : 각 row를 고유하게 하는 column e.g. 고객 ID
	- table 생성시 반드시 필요

## SQL이란?
관계형 DB 모델의 규칙에 의해 정의됨<br>=> 관계형 DB 언어라고도 함  
- DB에서 data를 읽거나 쓰고 수정하기 위한, 분명한 용도로 만들어짐<br>=> 몇 개의 단어로 이루어지고, 배우기 쉬움
- ANSI, ISO에서 SQL 표준안을 발표했지만 DBMS를 제공하는 회사들은 자신만의 SQL 사용

SQL
- DDL(Data Definition Language) : table, schema를 정의하는 언어<br>e.g. CREATE(table 생성), DROP(table 삭제), ALTER(table 재정의)
- DML(Data Manipulation Language) : data의 검색, 수정을 위한 언어<br>e.g. INSERT, DELETE, UPDATE, SELECT
- DCL(Data Control Language) : DB 사용자의 권한 제어를 위한 언어<br>e.g. GRANT(table에 권한 부여), REVOKE(부여한 권한 취소/회수)

SQL의 활용
- SQL은 big data에서 자료를 읽고 쓰기 위해 사용됨
- business insight ↑


# 2. SQL의 기초
기본 문법 : `SELECT [col] FROM [Table] WHERE [Condition];`

## 데이터 가져오기
`SELECT [c1], [c2] FROM [T1];`
- comma를 이용해 여러 열을 선택 가능(여러 개일 경우 순서대로 출력됨)
- SQL syntax는 case-insensitive(data는 sensitive!)
- SQL은 공백, carriage return을 무시함(`;`으로 쿼리문의 끝 인식)
- keyword는 열이름으로 사용할 수 없음

e.g.  
```
SELECT ID, STAFF_NM, BIRTH_DT FROM CLERK;

SELECT * FROM CLERK;
```

## 데이터 정렬하기
`SELECT [c1], [c2] FROM [T1] ORDER BY [col name/index] (ASC/DESC);`
- 열 위치로 정렬할 경우 SELECT 뒤에서 선택된 열들만 선택 가능(index가 저 list에서의 index임)<br>e.g. `SELECT EMP, GENDER, NM FROM CLERK ORDER BY 1, 2, 3;`
- 열 이름으로 기준을 선택할 경우 SELECT에서 선택하지 않은 열도 기준으로 사용 가능
- `ASC`, `DESC`를 기준 뒤에 붙여 정렬 방식 설정 가능<br>e.g. `SELECT EMP, GENDER, NM FROM CLERK ORDER BY 1 ASC, 2 DESC;`
- `ORDER BY`는 항상 문장 마지막에 위치


# `SELECT`문에 추가적으로 필요한 키워드
## `DISTINCT`
`SELECT DISTINCT [c1], [c2], DISTINCT [c3] FROM [T1];`
- `DISTINCT`가 적용된 열의 중복된 값을 제거하고 출력(`DISTINCT`가 여러 열에 적용된다면 각 열들의 data의 조합 중 중복 제거 후 출력)
- `DISTINCT` ↔ `ALL`
- `COUNT`같은 집계 함수나 하부 쿼리에서 많이 사용<br>e.g. `SELECT COUNT(DISTINCT position) FROM EMP;`
- 범주형 변수(↔ 연속형 변수)
	- Nominal variable(명목 변수) : e.g. 거주지 : 주택, 아파트 ...
	- Ordinal variable(순서 변수) : e.g. 학점 : A, B, C, D, F

## `ALIAS`
`SELECT [c1] AS [a1], [c2] "a2", [c3] FROM [T1];`
- double quotes를 사용할 경우 한글, 공백, 특수문자 사용 가능 cf. `AS`를 사용하면 영어로 한 단어만 가능(공백 x)
- `AS`, `""`를 섞어서 사용 가능
- `AS`가 가독성 ↑ => 가능하면 `AS`를 쓰는게 나음
- 한 번 alias를 선언하면 해당 쿼리문 내에서 어디든 사용 가능

# `WHERE`조건절을 활용한 데이터 조건 주기
`SELECT`에서 산술연산자 사용 가능  
e.g. `SELECT [c1]*0.1 AS [a1] FROM [T1];`

`SELECT [c1] FROM [T1] WHERE [Condition];`
- 비교 연산자 : 웬만한 것은 C랑 비슷
	- 같지 않다 : `<>`, `!=`, `^=`
	- n∈[a, b] : `n BETWEEN a AND B`, `a<=n<=b`, `a<=n AND n<=b`
	- `IS NULL`, `IS NOT NULL`
- `[Condition]`에 괄호도 사용 가능
- `NULL`은 정렬 시 가장 큰 값으로 분류됨, 연산 시 계산식 전체가 NULL로 바뀜

## NULL의 처리(Missing value imputation)
1. `COALESCE(p1, p2, ... , pn)` : `p1`, `p2`, ... , `pn` 중 `NULL`이 아닌 가장 빠른 값 리턴
2. `ZEROIFNULL([c1])` : `NULL`이면 `0` 리턴
3. `NVL2([c1], p1, p2)` : 해당 열이 `NULL`이면 `p2`, 아니면 `p1` 리턴

=> `ZEROIFNULL`, `NVL2`는 DBMS에 따라 지원 여부 다름


# 논리 연산자를 활용한 데이터 조건 주기
## 논리 연산자 AND, OR 알아보기
`OR`이 `AND`보다 우선순위 높음!

## 논리 연산자 IN, NOT IN 알아보기
`[c1] IN (v1, v2)` ⇔ `[c1]=v1 OR [c1]=v2`  
`[c1] NOT IN (v1, v2)` ⇔ `[c1]^=v1 AND [c1]^=v2`
- `IN`은 동치인 `OR`조건문보다 연산속도 ↑
- `IN` 안에 다른 `SELECT` 사용 가능(sub-query)

※ 날짜 형식은 `200000101`과 같이 입력


# 텍스트 마이닝을 활용한 데이터 조건 주기
Text filtering : `(NOT) LIKE`, wild card 이용
- wild card `%` : 모든 문자(=`*`)
- wild card `_` : 한 문자(=`?`)<br>e.g. `SELECT [c1] FROM [T1] WHERE [c1] LIKE '가나_라마바%하`;

## 필드 결합하기(concatenate)
`||` 또는 `+` 이용  
e.g.  
```
SELECT CITY || '(' || COUNTRY || ')' AS ADDR
FROM CUSTOMERS;

SELECT CITY + '(' + COUNTRY + ')' AS ADDR
FROM CUSTOMERS;
```

## 공백 제거(trim)
`TRIM`, `LTRIM`, `RTRIM` 이용  
e.g.  
```
SELECT CITY + '(' + TRIM(COUNTRY) + ')' AS ADDR
FROM CUSTOMERS;
```


# 기본 함수 배우기
## 문자/숫자/날짜 함수 배워보기
### 문자 함수
|Function|Explanation|
|:---|:---|
|`LOWER([c1])`|lowercase|
|`UPPER([c1])`|uppercase|
|`LENGTH([c1])`|len|
|`SUBSTR([c1], s, n)`|`[c1]`의 s번째부터 n개 리턴|
|`RTRIM([c1])`|trim right|
|`LTRIM([c1])`|trim left|
|`TRIM([c1])`|trim both side|
|`REPLACE([c1], [str1], [str2])`|`[c1]`에서 `[str1]`을 찾아 `[str2]`로 바꿈|
|`COALESCE(p1, p2, ... , pn)`|`p1`, `p2`, ... , `pn` 중 `NULL`이 아닌 가장 빠른 값 리턴|
|`INITCAP([c1])`|`[c1]`의 각 단어의 첫 글자를 대문자로, 나머지는 소문자로 바꿈|

### 숫자 함수
|Function|Explanation|
|:---|:---|
|`ROUND([c1], d)`|`[c1]`을 반올림해 소수점 `d`자리까지 나타냄|
|`TRUNC([c1], d)`|`[c1]`을 버림해 소수점 `d`자리까지 나타냄|
|`MOD(m, n)`|`m%n` 리턴|
|`ABS(p)`|`abs(p)` 리턴|
|`SIGN(p)`|`p`가 양수면 `1`, 음수면 `-1`, 0이면 `0` 리턴|
|`SQRT(p)`|`sqrt(p)` 리턴|
|`COS(p)`|`cos(p)` 리턴|
|`SIN(p)`|`sin(p)` 리턴|
|`PI(p)`|`rad(p)` 리턴|
|`TAN(p)`|`tan(p)` 리턴|

### 날짜 함수
|Function|Explanation|
|:---|:---|
|`ADD_MONTHS([c1], m)`|`[c1]`에 `m`개월을 더한 날짜 리턴|
|`SYSDATE`|현재 system의 날짜 리턴|
|`LAST_DAY([date])`|`[date]`에 해당하는 월의 마지막 날짜 리턴|
|`MONTH_BETWEEN([date1], [date2])`|`[date1]`, `[date2]` 사이의 개월 수 리턴(정확히 떨어지지 않을 경우 소수점 이용)|


# 함수 활용하기
## 숫자 데이터 요약하기
### 집계 함수
|Function|Explanation|
|:---|:---|
|`COUNT(p)`|`COUNT(*)` : `NULL`을 포함한 전체 행의 수 리턴<br>`COUNT([c1])` : `NULL`을 제외한 `[c1]`의 행의 수 리턴<br>`COUNT(DISTINCT [c1])` : 중복을 제외한 `[c1]`의 행의 수 리턴|
|`SUM([c1])`|`[c1]`의 sum 리턴|
|`AVG([c1])`|`[c1]`의 avg 리턴|
|`MAX([c1])`|`[c1]`의 max 리턴|
|`MIN([c1])`|`[c1]`의 min 리턴|
|`STDENV([c1])`|`[c1]`의 표준편차 리턴|
|`VARIANCE([c1])`|`[c1]`의 분산 리턴|

※ `AVG`를 사용할 때, [c1]에 `NULL`이 포함되어있을 수 있는 경우, `AVG([c1])`만 쓰면 계산이 잘못됨  
(`NULL`은 아예 계산에서 제외됨)  
=> `AVG(COALESCE([c1], 0))`을 사용해야 함!

## 조건문 이해하기
```
SELECT [c1], 
	CASE WHEN [Condition] THEN [result]
		WHEN [Condition] THEN [result]
		ELSE [result]
	END AS [a1]
FROM [T1];
```
- `CASE WHEN`의 조건이 equal만 있을 경우 `DECODE` 사용 가능

e.g.  
```
SELECT [c1], 
	DECODE([c2], v1, [result],--[c1]=v1일 경우 [result]
		v2, [result], 
		v3, [result], [default]) [a1]
FROM [T1];
```
- alias를 함수 뒤에 바로 붙임
- `CASE WHEN`을 다른 함수(SUM 등) 안에 파라미터로 집어넣을 수도 있음


# 데이터의 그룹화, 필터링
## 데이터의 그룹화
`GROUP BY` 이용  
```
SELECT [c1], [c2], [집계 함수1], [집계 함수2]
FROM [T1]
WHERE [Condition]
GROUP BY [c1], [c2];
```
- `GROUP BY`에서 열 이름 말고 index로도 호출 가능
- 집계 함수(Aggregate function)제외한 `SELECT`문의 모든 열은 그룹화 대상임 => `GROUP BY`에 있어야 함
- `WHERE`<br>`GROUP BY`<br>`ORDER BY` 순서로 작성
- 그룹화될 열에 `NULL`값이 포함될 경우, `NULL`도 하나의 그룹으로 인식됨

e.g.  
CARD_FLG, LOAN_FLG가 `0`, `1`의 값을 가질 때  
```
SELECT CARD_FLG, LOAN_FLG, COUNT(*) AS CNT
FROM PRC_201312
GROUP BY 1, 2;
```
=>  

|CARD_FLG|LOAN_FLG|CNT|
|:---|:---|:---|
|0|0|3|
|1|0|2|
|1|1|4|

※ 없는 경우의 수는 생략됨(위에서 `(0, 1)`의 case처럼)

## 그룹화된 데이터의 필터링
```
SELECT [c1], [집계 함수1]
FROM [T1]
WHERE [Condition]
GROUP BY [c1]
HAVING [집계 함수 조건];
```
- `HAVING`은 `WHERE`과 비슷하게 조건을 적용시켜 필터링하지만, `HAVING`은 그룹화된 데이터에 대해 적용됨
- `WHERE` - 각각의 데이터에 대한 filtering<br>`GROUP BY`<br>`HAVING` - 그룹화된 데이터에 대한 filtering<br>`ORDER BY` 순서로 작성
- `WHERE`에 의해 제외된 행들은 그룹화되지 않음


# 테이블 합치기
## 열 합치기
### 내부 조인
![sql-inner-join](https://github.com/siriyaoff/MDN-note/blob/master/images/sql-inner-join.png?raw=true)
- `FROM`/`WHERE`, `INNER JOIN` 2개의 방법이 있음
- 두 table 모두에 key가 존재해야 함

#### `FROM`/`WHERE` 사용
```
SELECT [A1].[c1], [A2].[c2], [A3].[c3]
FROM [T1] (AS) [A1], [T2] (AS) [A2], [T3] (AS) [A3]
WHERE [A1].KEY1=[A2].KEY1
	AND [A2].KEY2=[A3].KEY2;
```

#### `INNER JOIN` 사용
```
SELECT [A1].[c1], [A2].[c2], [A3].[c3]
FROM [T1] (AS) [A1]
	INNER JOIN [T2] (AS) [A2] ON [A1].KEY1=[A2].KEY1
	INNER JOIN [T3] (AS) [A3] ON [A2].KEY2=[A3].KEY2;
```

※ table에 alias를 정의할 때 `AS`가 지원되지 않는 DBMS(e.g. Oracle) 존재  
=> `AS` 생략하고 space 뒤에 바로 alias 적으면 됨  
join 조건을 지정하지 않은 채 합치면 table들의 곱집합(출력되는 열들의 모든 조합)가 출력됨  
e.g. T1이 8rows, T2가 9rows => 72 rows 출력됨

`하나의 key에 T1, T2 모두 2개의 data가 있으면?`  
출력되는 table에는 2개의 행이냐 4개의 행이냐

### 외부 조인
```
SELECT [A1].[c1], [A2].[c2], [A3].[c3]
FROM [T1] (AS) [A1]
	LEFT (OUTER) JOIN [T2] [A2] ON [A1].KEY1=[A2].KEY1
	LEFT JOIN [T3] [A3] ON [A2].KEY2=[A3].KEY2;
```

|left join|right join|full join|
|:---|:---|:---|
|![sql-left-join](https://github.com/siriyaoff/MDN-note/blob/master/images/sql-left-join.png?raw=true)|![sql-right-join](https://github.com/siriyaoff/MDN-note/blob/master/images/sql-right-join.png?raw=true)|![sql-full-join](https://github.com/siriyaoff/MDN-note/blob/master/images/sql-full-join.png?raw=true)|

- Left / Right / Full join이 있음
- 기준이 되는 table(`[T1]`)에 있는 data는 join되는 table(`[T2]`)에 같은 key 값이 없어도 출력됨<br>(T2에서 가져오는 열은 `NULL`로 출력됨)
- full join은 한 쪽만 가지는 key 모두 출력(비는 값은 `NULL`)

Example  
`Table_A`

|ID|DA|
|:---|:---|
|1|a|
|2|b|
|3|c|

`Table_B`

|ID|DB|
|:---|:---|
|1|aa|
|2|bb|
|4|dd|

#### Left join
```
SELECT TA.ID, TA.DA, TB.DB
FROM Table_A TA
	LEFT JOIN Table_B TB ON TA.ID=TB.ID;
```
results

|ID|DA|DB|
|:---|:---|:---|
|1|a|aa|
|2|b|bb|
|3|c|`NULL`|

#### Right join
```
SELECT TA.ID, TA.DA, TB.DB
FROM Table_A TA
	RIGHT JOIN Table_B TB ON TA.ID=TB.ID;
```
results

|ID|DA|DB|
|:---|:---|:---|
|1|a|aa|
|2|b|bb|
|4|`NULL`|dd|

#### Full join
```
SELECT TA.ID, TA.DA, TB.DB
FROM Table_A TA
	FULL JOIN Table_B TB ON TA.ID=TB.ID;
```
results

|ID|DA|DB|
|:---|:---|:---|
|1|a|aa|
|2|b|bb|
|3|c|`NULL`|
|4|`NULL`|dd|

- `LEFT`를 `RIGHT`, `FULL`로 바꿔서 다른 조인도 구현 가능(`FULL JOIN`은 지원하지 않는 DBMS도 존재)
- `OUTER`는 생략 가능
- `FROM [T1] [A1] LEFT JOIN (SELECT [c1], [c2] FROM [T2]) [A2]` 이렇게 table의 일부만 가져올 수도 있음(하위 쿼리)

※ `*=`, `=*`는 `LEFT/RIGHT JOIN`과 다름!!  
```
FROM T1 A1, T2 A2
WHERE A1.KEY1*=A2.KEY2
```
이렇게 `WHERE`에 OUTER JOIN 조건만 있으면 결과가 같지만,  
다른 조건들이 더 있을 경우 OUTER JOIN을 사용하면 OUTER JOIN이 일어난 후에 `WHERE`의 조건을 체크하고,  
`*=`연산자를 사용한 경우 OUTER JOIN 전에 `WHERE`의 다른 조건들이 체크되어 다른 결과가 출력될 수 있음

## 행 합치기
```
SELECT [c1], [c2] FROM [T1] WHERE [Condition]
UNION
SELECT [c3], [c4] FROM [T2] WHERE [Condition]
UNION
...
SELECT ...
ORDER BY 1;
```
- 각 `SELECT`문의 열의 숫자, data type은 각각 동일해야 함
- `UNION`만 사용하면 중복되는 값은 한 번만 표시<br>(`UNION ALL`을 사용하면 중복되는 값 모두 출력)
- `ORDER BY`를 마지막에 적으면 union된 table이 정렬되어 출력됨
- 출력되는 table의 열 이름은 첫 번째 `SELECT`문장의 열 이름으로 결정됨


# 하위 쿼리
## 하위 쿼리의 이해
- table이 들어갈 자리에 `SELECT`를 이용한 쿼리문을 넣는 것

### `FROM`에서의 하위 쿼리
- `FROM`에서 하위 쿼리를 사용할 때는 꼭 alias를 부여해야 함!<br>(다른 부분에서 호출하기 때문에 alias가 없으면 호출할 수가 없음)

```
SELECT [c1], [c2]
FROM (SELECT *
	FROM [T1]
	WHERE [Condition]) [A1]
WHERE [Condition];

SELECT [A1].[c1], [A2].[c2]
FROM [T1] [A1] LEFT JOIN
	(SELECT [c3], [c4]
	FROM [T2]
	WHERE [Condition]) [A2]
ON [A1].KEY=[A2].KEY;
```

### `WHERE`에서의 하위 쿼리
```
SELECT [c1], [c2]
FROM [T1]
WHERE [c3] IN (SELECT [c4]
		FROM [T2]
		WHERE [Condition]);
```
- 보통 `IN`과 함께 쓰임(python의 in과 비슷한 듯)
- 전체에서의 특정 목록과 일치하는 것들만 뽑아낼 때 사용
- 하위 쿼리의 예상 결과가 단일 행일 경우 `IN` 대신 `=` 사용 가능


# 데이터 및 테이블 조작
## 데이터 조작
### 데이터 삽입
```
INSERT INTO [T1]([c1], [c3])
VALUES([val1], [val3]);

INSERT INTO [T1]([c1], [c2], [c3])
SELECT [c1], [c2], [c3] FROM [T2] WHERE [Condition];
```
- 특정 열을 선택하여 넣을 때는 `INSERT`에 열 명시해야 함<br>모든 열을 넣을 때는 `INSERT`에 열 명시하지 않아도 됨
- `INSERT`에 열 순서가 바뀌어도 대입되는 값아 매치만 되면 table에 제대로 들어감<br>e.g. (c1, c3, c2), (v1, v3, v2)로 매치해서 넣어도 알아서 1, 2, 3 순서대로 된 table에 넣어짐

### 데이터 삭제
```
DELETE FROM [T1]
WHERE [Condition];
```
- `WHERE` 빼면 모든 행을 삭제함
- SQL에서는 실행취소가 불가능

### 데이터 수정
```
UPDATE [T1]
SET [c1]=[v1]
WHERE [Condition];
```
- `WHERE` 안쓰면 [c1]의 모든 행이 바뀜

## 테이블 조작
### 테이블 생성
```
CREATE TABLE [T1]
{
	[col name1] [data format(size)] [option],
	[col name2] [data format(size)] [option],
	...
};

CREATE TABLE [T2] AS
	SELECT [c1], [c2] FROM [T3];
```

#### data types
**문자형**

|data types|description|
|:---|:---|
|`CHAR(n)`<br>(= `CHARACTER(n)`)|길이 `n`(최대 4KB)으로 고정된 string<br>(남으면 공백으로 채움)|
|`NCHAR(n)`<br>(= `NATIONAL VARYING(n)`)|`CHAR(n)`과 비슷하지만 더 다양한 언어 지원|
|`VARCHAR(n)`<br>(= `CHARACTER VARYING(n)`)|최대 길이가 `n`인 string<br>`n`보다 작은 문자열이 들어오면 공간 자체를 줄임|
|`NVARCHAR(n)`|최대 길이가 `n`인 `NCHAR`<br>`VARCHAR`과 마찬가지로 공간이 남으면 줄임|

**숫자형**

|data types|description|
|:---|:---|
|`BIT`|단일 비트|
|`NUMERIC(p, s)`<br>(= `DECIMAL(p, s)`)|`p` : 전체 digits, `s` : 소수점 이하 자리수<br>e.g. 7891.324 : p=7, s=3|
|`FLOAT`|실수 값|
|`INT`<br>(= `INTEGER`)|int|

**날짜 및 시간**

|data types|description|
|:---|:---|
|`DATE`|날짜<br>e.g. 2021-04-23|
|`TIME`|시간<br>e.g. 23:39:40|
|`TIMESTAMP`|DATE+TIME<br>e.g. 2021-04-23 23:39:40|


#### options
|options|description|
|:---|:---|
|`NOT NULL`|`NULL`이 허용되지 않음|
|`DEFAULT [default]`|해당 열에 값이 지정되지 않으면 자동으로 `[default]`가 저장됨|
|`PRIMARY KEY`|해당 열이 기본키로 설정됨<br>기본키는 `NULL`일 수 없고 모든 값들이 unique해야 하며 수정 불가|
|`REFERENCES [T1]([c1])`|T1의 c1을 가리키는 외래키(foreign key)를 정의할 때 사용<br>외래키는 가리키는 열에 존재하는 값만 가질 수 있음<br>data의 참조 무결성(reference integrity)을 위해 사용|

### 테이블 변경 및 삭제
#### 열 추가
```
ALTER TABLE [T1]
ADD ([c1] [data type(size)]);
```

#### 열 data type 변경
```
ALTER TABLE [T1]
MODIFY ([c1] [data type(size)]);
```

#### 테이블 이름 변경
```
RENAME [T1] TO [T1'];
```

#### 테이블 삭제
```
DROP TABLE [T1];
```
