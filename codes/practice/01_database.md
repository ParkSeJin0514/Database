# 🗄️ 08.06 Database
## 🚀 기본 명령어
### 테이블 생성
```sql
CREATE TABLE BTC_3
(ID VARCHAR(10),
NAME VARCHAR(20),
ADDR VARCHAR(50) NOT NULL,
PHONE_NUM INTEGER,
CLASS VARCHAR(5) CHECK (CLASS in ('BTC-1', 'BTC-2')),
PRIMARY KEY(ID),
UNIQUE KEY(PHONE_NUM));
```
### 생성된 테이블에 코멘트 삽입
```sql
ALTER TABLE member MODIFY column mem_id
CHAR(8) NOT NULL COMMENT '사용자 아이디';
```
### 생성할 때 코멘트 작성
```sql
CREATE TABLE member_1
(mem_id INTEGER AUTO_INCREMENT NOT NULL PRIMARY KEY comment '사용자 아이디',
mem_name VARCHAR(10) NOT NULL comment '사용자 이름',
mem_number INTEGER NOT NULL comment '사용자 번호',
addr CHAR(2) NOT NULL comment '주소',
phone1 CHAR(3) comment '전화번호 국번',
phone2 CHAR(13) comment '전화번호',
height SMALLINT comment '키',
debut_date DATE comment '데뷔일자');
```
### 테이블 데이터 삽입
```sql
INSERT INTO employees VALUES 
(0001, 20220101, '강', '감찬', 'M', 20000101),
(0002, 20220201, '이', '순신', 'M', 20010101),
(0003, 20220301, '유', '관순', 'F', 20020101),
(0004, 20220401, '김', '유신', 'M', 20030101),
(0005, 20220501, '정', '약용', 'M', 20040101),
(0006, 20220601, '윤', '봉길', 'M', 20050101);
```
### PRIMARY KEY 두 개 이상 설정
```sql
CREATE TABLE dept_manager
(emp_no INTEGER comment '사원번호',
dept_no CHAR(4) comment '부서번호',
from_date DATE NOT NULL comment '발령일시',
to_date DATE NOT NULL comment '발령종료일시',
PRIMARY KEY (emp_no, dept_no));
```
### FOREIGN KEY 설정
```sql
CREATE TABLE dept_emp
(emp_no INTEGER comment '사원번호',
dept_no CHAR comment '부서번호',
from_date DATE NOT NULL comment '발령일시',
PRIMARY KEY (emp_no, dept_no),

# 현재 테이블의 emp_no 컬럼을 외래 키로 지정
# 외래 키가 참조하는 대상은 employees 테이블의 emp_no 컬럼
FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
FOREIGN KEY (dept_no) REFERENCES departments(dept_no));
```
### fk_dept_emp 제약조건 추가 후 FOREIGN KEY 설정
```sql
ALTER TABLE dept_emp
ADD CONSTRAINT fk_dept_emp
FOREIGN KEY (emp_no)
REFERENCES EMPLOYEES (emp_no);
```
### 제약조건 삭제
```sql
ALTER TABLE dept_manager
DROP FOREIGN KEY dept_manager_ibfk_2;
```
### BULK 로딩
    
```sql
# 환경 변수 편집 X
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql" -uroot -p aaa < [파일 위치]
  
# 환경 변수 편집 O
mysql -u root -p [데이터베이스] < "[파일 위치]"
```