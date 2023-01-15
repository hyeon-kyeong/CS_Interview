# Join

조인: 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용


<br>

<br>

## Join 종류

----

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN


<br>

<br>

## - INNER JOIN

교집합으로, 기준 테이블과 join 테이블의 중복된 값을 보여줌


```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

<br>

## - LEFT OUTER JOIN

기준테이블값과 조인테이블과 중복된 값
왼쪽 테이블 기준으로 join

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

<br>

## - RIGHT OUTER JOIN

오른쪽 테이블 기준 join

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## - FULL OUTER JOIN

합집합

A와 B 테이블의 모든 데이터가 검색됨

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

<br>

## - CROSS JOIN

모든 경우의 수를 전부 표현해주는 방식

A가 3개, B가 4갴면 총 3*4=12개의 데이터가 검색됨


```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

<br>

## - SELF JOIN

자기자신과 자기자신을 조인

자신이 갖고있는 칼럼을 다양하게 변형시켜 활용할 떄 자주 사용함 

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```
