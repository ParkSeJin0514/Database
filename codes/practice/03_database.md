# 📖 08.06 Database
## 🚀 JOIN
### INNER JOIN
```sql
SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a INNER JOIN team b
ON a.team_id = b.team_id
```
### LEFT OUTER JOIN
```sql
SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a LEFT OUTER JOIN team b
ON a.team_id = b.team_id
```
### RIGHT OUTER JOIN
```sql
SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a RIGHT OUTER JOIN team b
ON a.team_id = b.team_id
```
### UNION
```sql
SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a LEFT OUTER JOIN team b
ON a.team_id = b.team_id

UNION

SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a LEFT OUTER JOIN team b
ON a.team_id = b.team_id
```
### CROSS JOIN
```sql
SELECT a.player_id, a.player_name, a.team_id, b.stadium_id, b.team_name
FROM player a, team b
```
### 3 TABLE JOIN
```sql
SELECT E.EMP_NO, E.BIRTH_DATE, E.GENDER, DE.DEPT_NO, D.DEPT_NAME
FROM EMPLOYEES E, DEPT_EMP DE, DEPARTMENTS D
WHERE E.EMP_NO = DE.EMP_NO
AND DE.DEPT_NO = D.DEPT_NO
AND E.LAST_NAME = 'WEGERLE'
AND E.FIRST_NAME = 'SHIRISH';
```
## 🔥 TEST
### 1999년 입사한 사원 출력
```sql
SELECT *
FROM employees
WHERE HIRE_DATE BETWEEN '1999-01-01' AND '1999-12-31'
```
### 1998년에 입사한 남자 출력
```sql
SELECT gender, count(*)
FROM employees
WHERE HIRE_DATE BETWEEN '1998-01-01' AND '1998-12-31'
GROUP BY gender
HAVING gender = 'M'
```
### 업무별 직원수 출력
```sql
SELECT d.dept_name, de.dept_no, COUNT(*) 
FROM DEPT_EMP DE, DEPARTMENTS D
WHERE D.DEPT_NO = DE.DEPT_NO
GROUP BY d.dept_name, de.dept_no
```
### 남여 직원수 출력
```sql
SELECT gender, count(*)
FROM employees
GROUP BY gender
```
### 개발부에서 급여를 가장 많이 받는 직원 5명 출력
```sql
SELECT E.EMP_NO, D.DEPT_NO, S.SALARY
FROM EMPLOYEES E, DEPARTMENTS D, DEPT_EMP DE, SALARIES S
WHERE E.EMP_NO = DE.EMP_NO
AND D.DEPT_NO = DE.DEPT_NO
AND S.EMP_NO = E.EMP_NO 
AND D.dept_no = 'd005'
ORDER BY S.SALARY DESC
LIMIT 5
```
### 남여 직원수를 구하고 M은 '남', F는 '여'로 출력
```sql
SELECT
CASE WHEN gender = 'M' THEN '남'
WHEN gender = 'F' THEN '여'
END AS 성별,
count(*) 직원수
FROM employees
GROUP BY gender
```