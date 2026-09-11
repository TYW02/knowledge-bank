---
title: Lab 02 SQL Basics in MariaDB
tags:
  - SQL
  - MariaDB
---
## Creating a User in MariaDB
```SQL
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

## Grant Permissions to DB
```SQL
GRANT ALL PRIVILEGES ON *.* TO 'app_user'@'localhost'
```

> [!Note]
> This gives global administrator permissions


## Creating Database
- Table name: students
- sid int primary key
- name varchar(50)
- grade char(2)
```SQL
CREATE TABLE students (
	sid INT PRIMARY KEY,
	name VARCHAR(50),
	grade CHAR(2)
)
```

### Showing databases available
```SQL
show databases;
```


## Read Operation
```SQL
SELECT * FROM students
```


## Insert Operations
- Add a new student
- (sid = 2001111, name = Lewis, grade = NA)
- (sid = 2002222, name = Valtteri, grade = NULL)
- (sid = 2003333, name = Micheal, grade = NULL)
```SQL
INSERT INTO students (sid, name, grade) VALUES (2001111, 'Lewis', 'NA');
INSERT INTO students (sid, name) VALUES (2002222, 'Valtteri');
INSERT INTO students (sid, name) VALUES (2003333, 'Micheal');
```

### Alternative Command
```SQL
INSERT INTO students (sid, name, grade)
VALUES
(2001111, 'Lewis', 'NA'),
(2002222, 'Valtteri', NULL),
(2003333, 'Micheal', NULL);
```


## Update Operation
- Update the grade of Micheal to 'A+'
- Update grade of Valtteri to 'A-'
```SQL
UPDATE students 
SET grade = 'A+' 
WHERE name = 'Micheal';

UPDATE students
SET grade = 'A-'
WHERE name = 'Valtteri';
```

## Delete Operation
- Delete Valtteri
```SQL
DELETE FROM students WHERE name = 'Valtteri';
```

- Delete table
```SQL
DELETE FROM students;
```

- Delete Database
```SQL
DROP TABLE yuanweiDB;
```
































