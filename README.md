** Database PostgreSQL  **

Microsoft Windows [Version 10.0.26100.4202]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Minfy.ALURURAKESHREDD>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE USER u_admin WITH PASSWORD 'your_secure_password';
CREATE ROLE
postgres=# CREATE DATABASE u_db OWNER u_admin;
CREATE DATABASE
postgres=# GRANT ALL PRIVILEGES ON DATABASE u_db TO u_admin;
GRANT
postgres=# \q

C:\Users\Minfy.ALURURAKESHREDD>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
CREATE TABLE
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
ERROR:  relation "students" already exists
university_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE
university_db=> ALTER TABLE students DROP COLUMN enrollment_date;
ALTER TABLE
university_db=> ALTER TABLE students ALTER COLUMN email TYPE VARCHAR(150);
ALTER TABLE
university_db=> ALTER TABLE students RENAME COLUMN date_of_birth TO dob;
ALTER TABLE
university_db=> ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE
university_db=> ALTER TABLE students RENAME TO learners;
ALTER TABLE
university_db=> ALTER TABLE learners RENAME TO students;
ALTER TABLE
university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     dob DATE
university_db(> );INSERT INTO students (student_id, first_name, last_name, email, dob)
CREATE TABLE
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> SELECT * FROM students WHERE student_id = 1
university_db->
university_db-> SELECT * FROM students WHERE student_id = 1
university_db-> SELECT * FROM students WHERE student_id = 1;
ERROR:  syntax error at or near "SELECT"
LINE 2: SELECT * FROM students WHERE student_id = 1
        ^
university_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=> SELECT first_name, last_name FROM students WHERE last_name = 'Smith';
 first_name | last_name
------------+-----------
 Alice      | Smith
(1 row)


university_db=>
university_db=> SELECT * FROM students WHERE dob >= '2003-01-01'; -- Students born in or after 2003
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, dob) VALUES (4, 'Diana', 'Prince', '2001-11-01');
INSERT 0 1
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Diana      | Prince    |                           | 2001-11-01
(4 rows)


university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Diana      | Prince    |                           | 2001-11-01
(4 rows)


university_db=> SELECT first_name, last_name, email FROM students;
 first_name | last_name |           email
------------+-----------+---------------------------
 Alice      | Smith     | alice.smith@example.com
 Bob        | Johnson   | bob.johnson@example.com
 Charlie    | Brown     | charlie.brown@example.com
 Diana      | Prince    |
(4 rows)


university_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=> UPDATE students
university_db-> SET email = 'alices@example.net'
university_db-> WHERE student_id = 1;
UPDATE 1
university_db=> UPDATE students
university_db-> SET first_name = 'Robert', email = 'robert.j@example.com'
university_db-> WHERE student_id = 2;
UPDATE 1
university_db=> SELECT * FROM students WHERE student_id IN (1,2);
 student_id | first_name | last_name |        email         |    dob
------------+------------+-----------+----------------------+------------
          1 | Alice      | Smith     | alices@example.net   | 2003-05-15
          2 | Robert     | Johnson   | robert.j@example.com | 2002-08-22
(2 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (99, 'Temp', 'User', 'temp@example.com', '2000-01-01');
INSERT 0 1
university_db=> SELECT * FROM students WHERE student_id = 99;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
         99 | Temp       | User      | temp@example.com | 2000-01-01
(1 row)


university_db=> DELETE FROM students WHERE student_id = 99;
DELETE 1
university_db=> SELECT * FROM students WHERE student_id = 99;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> SELECT * FROM students ORDER BY last_name ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22
          4 | Diana      | Prince    |                           | 2001-11-01
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
(4 rows)


university_db=> SELECT * FROM students ORDER BY dob DESC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22
          4 | Diana      | Prince    |                           | 2001-11-01
(4 rows)


university_db=> SELECT * FROM students ORDER BY last_name, first_name;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22
          4 | Diana      | Prince    |                           | 2001-11-01
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
(4 rows)


university_db=> SELECT * FROM students ORDER BY dob DESC LIMIT 3;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22
(3 rows)


university_db=> SELECT * FROM students ORDER BY student_id LIMIT 2 OFFSET 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Diana      | Prince    |                           | 2001-11-01
(2 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (5, 'Eve', 'Smith', 'eve.smith@example.com', '2004-07-01');
INSERT 0 1
university_db=> SELECT last_name FROM students;
 last_name
-----------
 Brown
 Prince
 Smith
 Johnson
 Smith
(5 rows)


university_db=> SELECT DISTINCT last_name FROM students ORDER BY last_name;
 last_name
-----------
 Brown
 Johnson
 Prince
 Smith
(4 rows)


university_db=> SELECT DISTINCT last_name, first_name FROM students;
 last_name | first_name
-----------+------------
 Prince    | Diana
 Smith     | Eve
 Smith     | Alice
 Johnson   | Robert
 Brown     | Charlie
(5 rows)


university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50) NOT NULL, -- first_name cannot be NULL
university_db(>     last_name VARCHAR(50) NOT NULL,
university_db(>     email VARCHAR(100) UNIQUE,      -- email must be unique (and can be NULL by default for UNIQUE)
university_db(>     dob DATE,
university_db(>     enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped'))
university_db(> );
CREATE TABLE
university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(>     student_id SERIAL PRIMARY KEY,  -- student_id is now PK, auto-incrementing, NOT NULL
university_db(>     first_name VARCHAR(50) NOT NULL,
university_db(>     last_name VARCHAR(50) NOT NULL,
university_db(>     email VARCHAR(100) UNIQUE,      -- Email should be unique; can be NULL unless NOT NULL is added
university_db(>     dob DATE,
university_db(>     enrollment_status VARCHAR(20) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped', 'pending'))
university_db(> );
CREATE TABLE
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
INSERT 0 1
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
(3 rows)


university_db=> CREATE TABLE courses (
university_db(>     course_id SERIAL PRIMRY KEY,
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
university_db(> );
ERROR:  syntax error at or near "PRIMRY"
LINE 2:     course_id SERIAL PRIMRY KEY,
                             ^
university_db=> \q

C:\Users\Minfy.ALURURAKESHREDD>psql -U university_admin -d university_db
Password for user university_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: fe_sendauth: no password supplied

C:\Users\Minfy.ALURURAKESHREDD>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> CREATE TABLE enrollments (
university_db(>     enrollment_id SERIAL PRIMARY KEY,
university_db(>     student_id INTEGER NOT NULL,
university_db(>     course_id INTEGER NOT NULL,
university_db(>     enrollment_date DATE DEFAULT CURRENT_DATE, -- Sets default if not specified
university_db(>     grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)), -- W for withdraw, NULL if not graded
university_db(>
university_db(>     -- Foreign Key constraint for student_id
university_db(>     CONSTRAINT fk_student
university_db(>         FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE, -- If a student is deleted, their enrollments are also deleted.
university_db(>                            -- Other options: ON DELETE RESTRICT, ON DELETE SET NULL, ON DELETE SET DEFAULT
university_db(>
university_db(>     -- Foreign Key constraint for course_id
university_db(>     CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT, -- (Default if not specified) Prevent deleting a course if students are enrolled.
university_db(>
university_db(>     -- Ensure a student cannot enroll in the same course multiple times (if semester isn't a factor)
university_db(>     UNIQUE (student_id, course_id)
university_db(> );
ERROR:  relation "courses" does not exist
university_db=> CREATE TABLE courses (
university_db(>     course_id SERIAL PRIMRY KEY,
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
university_db(> );
ERROR:  syntax error at or near "PRIMRY"
LINE 2:     course_id SERIAL PRIMRY KEY,
                             ^
university_db=> CREATE TABLE students (
university_db(>     student_id SERIAL PRIMARY KEY,  -- student_id is now PK, auto-incrementing, NOT NULL
university_db(>     first_name VARCHAR(50) NOT NULL,
university_db(>     last_name VARCHAR(50) NOT NULL,
university_db(>     email VARCHAR(100) UNIQUE,      -- Email should be unique; can be NULL unless NOT NULL is added
university_db(>     dob DATE,
university_db(>     enrollment_status VARCHAR(20) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped', 'pending'))
university_db(> );
ERROR:  relation "students" already exists
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(alice.smith@example.com) already exists.
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(robert.j@example.com) already exists.
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(charlie.brown@example.com) already exists.
university_db=>
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
(3 rows)


university_db=> CREATE TABLE courses (
university_db(>     course_id SERIAL PRIMRY KEY,
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
university_db(> );
ERROR:  syntax error at or near "PRIMRY"
LINE 2:     course_id SERIAL PRIMRY KEY,
                             ^
university_db=> CREATE TABLE courses (
university_db(>     course_id SERIAL PRIMARY KEY,  -- Fixed the typo here
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10)
university_db(> );
CREATE TABLE
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
university_db=> CREATE TABLE enrollments (
university_db(>     enrollment_id SERIAL PRIMARY KEY,
university_db(>     student_id INTEGER NOT NULL,
university_db(>     course_id INTEGER NOT NULL,
university_db(>     enrollment_date DATE DEFAULT CURRENT_DATE, -- Sets default if not specified
university_db(>     grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)), -- W for withdraw, NULL if not graded
university_db(>
university_db(>     -- Foreign Key constraint for student_id
university_db(>     CONSTRAINT fk_student
university_db(>         FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE, -- If a student is deleted, their enrollments are also deleted.
university_db(>                            -- Other options: ON DELETE RESTRICT, ON DELETE SET NULL, ON DELETE SET DEFAULT
university_db(>
university_db(>     -- Foreign Key constraint for course_id
university_db(>     CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT, -- (Default if not specified) Prevent deleting a course if students are enrolled.
university_db(>
university_db(>     -- Ensure a student cannot enroll in the same course multiple times (if semester isn't a factor)
university_db(>     UNIQUE (student_id, course_id)
university_db(> );
CREATE TABLE
university_db=> );
ERROR:  syntax error at or near ")"
LINE 1: );
        ^
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (2, 1, 'B');
INSERT 0 1
