# 📖 08.06 Database
## 🚀 조건 연산자
### CONCAT
```sql
SELECT concat(stadium_name, ' (', seat_count, '석', ')')
FROM stadium
```
### WHERE
```sql
SELECT player_id, team_id
FROM player
WHERE player_name='레오'
```
### IN
```sql
SELECT dept_no, dept_name
FROM departments
WHERE dept_name IN ('marketing', 'sales');
```
### LIKE
```sql
SELECT emp_no, first_name, last_name
FROM employees
WHERE last_name LIKE '__p%'
```
### BETWEEN
```sql
SELECT emp_no, first_name, last_name, gender, BIRTH_DATE 
FROM employees
WHERE Birth_date BETWEEN '1955-01-01' AND '1960-12-31'
```
### UPDATE
```sql
UPDATE player2 SET TEAM_ID = 'kor'
WHERE team_id = 'K01'
```
## 🚀 함수 연산자
### 종합
```sql
# 사원(employees) 테이블에서 모든 컬럼의 값을 출력하되, First_name, Last_name은 소문자로 하나의 컬럼으로 출력하고 이름의 길이를 출력하는 신규 컬럼을 생성하여 출력

SELECT emp_no, birth_date, LOWER(CONCAT(SUBSTR(first_name, 1,1), SUBSTR(last_name, 1, 1))), first_name, last_name, LENGTH(last_name), gender, hire_date
FROM employees
```
## 🚀 CASE
### Simple CASE Expression
```sql
SELECT emp_no AS '사원번호',
CASE dept_no
	WHEN 'd001' THEN '마케팅'
	WHEN 'd002' THEN '재무'	
	WHEN 'd003' THEN '인사'
	WHEN 'd004' THEN '상품'
	WHEN 'd005' THEN '개발'
	WHEN 'd006' THEN '품질'
	WHEN 'd007' THEN '영업'
	WHEN 'd008' THEN '연구'
	WHEN 'd009' THEN '고객서비스'
ELSE ''
END AS '부서명'
FROM dept_emp
```
### Searched CASE Expression
```sql
SELECT emp_no AS '사원번호',
CASE
	WHEN dept_no = 'd001' THEN '마케팅'
	WHEN dept_no = 'd002' THEN '재무'	
	WHEN dept_no = 'd003' THEN '인사'
	WHEN dept_no = 'd004' THEN '상품'
	WHEN dept_no = 'd005' THEN '개발'
	WHEN dept_no = 'd006' THEN '품질'
	WHEN dept_no = 'd007' THEN '영업'
	WHEN dept_no = 'd008' THEN '연구'
	WHEN dept_no = 'd009' THEN '고객서비스'
ELSE ''
END AS '부서명'
FROM dept_emp
```