# Week5Assign 第五階段專案任務

## Task2 - Create Database and Table
```sql
SHOW DATABASES;
CREATE DATABASE website;
USE website;
SHOW TABLES;
CREATE TABLE member(
	id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  password VARCHAR(255) NOT NULL,
  follower_count INT NOT NULL DEFAULT 0,
  time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```
![task2-1](week5/screenshot/task2-1.png)
![task2-2](week5/screenshot/task2-2.png)
## Task3 - SQL CRUD
```sql
SELECT * FROM member;
INSERT INTO member(name, email, password) VALUES('test', 'test@test.com', 'test'); 
INSERT INTO member(name, email, password) VALUES('apple', 'apple@mail.com', 'apple'); 
INSERT INTO member(name, email, password) VALUES('bee', 'bee@mail.com', 'bee'); 
INSERT INTO member(name, email, password) VALUES('crown', 'crown@mail.com', 'crown'); 
INSERT INTO member(name, email, password) VALUES('yuki', 'yuki@mail.com', 'yuki');
SELECT * FROM member
ORDER BY time DESC
LIMIT 3 OFFSET 1;
SELECT * FROM member WHERE email = 'test@test.com';
SELECT * FROM member WHERE name LIKE '%es%';
SELECT * FROM member WHERE email = 'test@test.com' AND password = 'test';

SET SQL_SAFE_UPDATES = 0;    
UPDATE member 
SET name = 'test2' 
WHERE email = 'test@test.com';
UPDATE member SET follower_count = '100' WHERE id = 5;
UPDATE member SET follower_count = '500' WHERE id = 3;
SELECT * FROM member;
SET SQL_SAFE_UPDATES = 1; 
```
![task3-1,2](week5/screenshot/task3-1,2.png)
![task3-3,4](week5/screenshot/task3-3,4.png)
![task3-5,6,7](week5/screenshot/task3-5,6,7.png)
![task3-8](week5/screenshot/task3-8.png)

## Task4 - SQL Aggregation Functions
```sql
SELECT COUNT(*) FROM member;
SELECT SUM(follower_count) FROM member;
SELECT AVG(follower_count) FROM member;
SELECT AVG(follower_count) FROM ( SELECT follower_count FROM member ORDER by follower_count DESC LIMIT 2) AS top2; 
```
![task4](week5/screenshot/task4.png)

## Task5 - SQL JOIN
```sql
CREATE TABLE message(
	id INT AUTO_INCREMENT PRIMARY KEY,
	member_id INT NOT NULL,
	content TEXT NOT NULL,
	like_count INT NOT NULL DEFAULT 0,
	time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
	FOREIGN KEY (member_id) REFERENCES member(id)
);
![task5-1](week5/screenshot/task5-1.png)

SELECT * FROM message;
INSERT INTO message(member_id, content, like_count) VALUES (2, 'Hello MySQL!', 100);
INSERT INTO message(member_id, content, like_count) VALUES (5, 'How are you~', 10);
INSERT INTO message(member_id, content, like_count) VALUES (4, 'yummy!!!', 5);
INSERT INTO message(member_id, content, like_count) VALUES (5, 'Just Do It!', 100);
INSERT INTO message(member_id, content, like_count) VALUES (2, 'Hello MySQL!', 100);
INSERT INTO message(member_id, content, like_count) VALUES (2, 'Word Hard, Play Hard!', 99);

SELECT message.id, member.name AS sender, message.content, message.like_count, message.time 
FROM message JOIN member ON message.member_id = member.id;
![task5-2](week5/screenshot/task5-2.png)

SELECT message.id, member.name AS sender, message.content, message.like_count, message.time 
FROM message JOIN member ON message.member_id = member.id
WHERE member.email = 'test@test.com';
![task5-3](week5/screenshot/task5-3.png)

SELECT AVG(message.like_count) AS avg_like FROM message JOIN member ON message.member_id = member.id
WHERE member.email = 'test@test.com';
![task5-4](week5/screenshot/task5-4.png)

SELECT member.email, AVG(message.like_count) AS avg_like FROM  member LEFT JOIN message ON member.id = message.member_id
![task5-5](week5/screenshot/task5-5.png)

GROUP BY member.email;
```
