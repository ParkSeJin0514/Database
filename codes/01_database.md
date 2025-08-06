```sql
CREATE TABLE BTC_3
( ID VARCHAR(10)
, NAME VARCHAR(20)
, ADDR VARCHAR(50) NOT NULL
, PHONE_NUM INTEGER
, CLASS VARCHAR(5) CHECK (CLASS in ('BTC-1', 'BTC-2'))
, PRIMARY KEY(ID)
, UNIQUE KEY(PHONE_NUM)
);
```
```sql
create table member_1
( mem_id CHAR(8) not null comment '사용자 아이디' primary key
, mem_name VARCHAR(10) not null comment '사용자 이름'
, mem_number INTEGER not null comment '사용자 번호',
addr CHAR(2) not null comment '주소'
, phone1 CHAR(3) comment '전화번호 국번'
, phone2 CHAR(13) comment '전화번호'
, height smallint comment '키'
, debut_date DATE comment '데뷔일자'
);
```