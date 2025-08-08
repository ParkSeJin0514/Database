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
### 급여 평균이 가장 높은 부서 5개를 출력
```sql
SELECT D.DEPT_NAME, AVG(S.SALARY) AS AVG_SALARY
FROM SALARIES S, DEPARTMENTS D, DEPT_EMP DE
WHERE DE.DEPT_NO = D.DEPT_NO
AND DE.EMP_NO = S.EMP_NO
AND DE.TO_DATE = '9999-01-01' AND S.TO_DATE = '9999-01-01'
GROUP BY D.DEPT_NAME
ORDER BY AVG_SALARY DESC
LIMIT 5;
```
### 직원들의 평균 급여 출력
```sql
SELECT E.EMP_NO, AVG(S.SALARY) AS AVG_SALARY
FROM EMPLOYEES E, SALARIES S, DEPT_EMP DE
WHERE DE.EMP_NO = S.EMP_NO
AND E.EMP_NO = DE.EMP_NO 
AND DE.TO_DATE = '9999-01-01' AND S.TO_DATE = '9999-01-01'
GROUP BY E.EMP_NO
ORDER BY AVG_SALARY DESC
```
### 급여를 많이 받는 매니저를 높은 순으로 출력
```sql
SELECT DM.EMP_NO, AVG(S.SALARY) AS AVG_SALARY
FROM EMPLOYEES E, SALARIES S, DEPT_MANAGER DM, DEPT_EMP DE
WHERE DM.EMP_NO = S.EMP_NO
AND DM.EMP_NO = E.EMP_NO 
AND DE.TO_DATE = '9999-01-01' AND S.TO_DATE = '9999-01-01'
GROUP BY DM.EMP_NO
ORDER BY AVG_SALARY DESC
```
### 급여에 따른 순위와 직원 수 출력 
```sql
SELECT
CASE WHEN S.SALARY >= 100000 THEN '1'
     WHEN S.SALARY >= 80000 THEN '2'
     WHEN S.SALARY >= 65000 THEN '3'
     WHEN S.SALARY >= 45000 THEN '4'
ELSE '5'
END AS 'RANK',
COUNT(*) CNT
FROM SALARIES S
WHERE S.TO_DATE = '9999-01-01'
GROUP BY
CASE WHEN S.SALARY >= 100000 THEN '1'
     WHEN S.SALARY >= 80000 THEN '2'
     WHEN S.SALARY >= 65000 THEN '3'
     WHEN S.SALARY >= 45000 THEN '4'
ELSE '5' END
ORDER BY 1;
```