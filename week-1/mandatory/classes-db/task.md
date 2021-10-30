# Class Database

## Submission

Below you will find a set of tasks for you to complete to set up a databases of students and mentors.

To submit this homework write the correct commands for each question here:

```sql


```

When you have finished all of the questions - open a pull request with your answers to the `Databases-Homework` repository.

## Task

1. Create a new database called `cyf_classes` (hint: use `createdb` in the terminal)

CREATE DATABASE cyf_classes owner postgres;

2. Create a new table `mentors`, for each mentor we want to save their name, how many years they lived in Glasgow, their address and their favourite programming language.

CREATE TABLE mentors(
id SERIAL PRIMARY KEY,
name VARCHAR(50) NOT NULL,
yearsInGlasgow int,
address VARCHAR(120),
favProgramLanguage VARCHAR(100)
);

3. Insert 5 mentors in the `mentors` table (you can make up the data, it doesn't need to be accurate ;-)).

INSERT INTO mentors (name, yearsinglasgow, address, favprogramlanguage) VALUES ('Maria', 1, 'Barcelona', 'JavaScript');
INSERT INTO mentors (name, yearsinglasgow, address, favprogramlanguage) VALUES ('Jose', 2, 'Barcelona', 'JavaScript');
INSERT INTO mentors (name, yearsinglasgow, address, favprogramlanguage) VALUES ('Andrea', 3, 'Barcelona', 'JavaScript');
INSERT INTO mentors (name, yearsinglasgow, address, favprogramlanguage) VALUES ('Pedro', 4, 'Barcelona', 'JavaScript');
INSERT INTO mentors (name, yearsinglasgow, address, favprogramlanguage) VALUES ('Ines', 5, 'Barcelona', 'JavaScript');

4. Create a new table `students`, for each student we want to save their name, address and if they have graduated from Code Your Future.

CREATE TABLE students(
id SERIAL PRIMARY KEY,
name VARCHAR(50) NOT NULL,
address VARCHAR(120),
graduated BOOL
);

5. Insert 10 students in the `students` table.

INSERT INTO students (name, address, graduated) VALUES ('Juan', 'Catalunya. Barcelona', 'true');
INSERT INTO students (name, address, graduated) VALUES ('Jose', 'Catalunya. Barcelona', 'true');
INSERT INTO students (name, address, graduated) VALUES ('Miria', 'Catalunya. Barcelona', 'true');
INSERT INTO students (name, address, graduated) VALUES ('Aneska', 'Catalunya. Barcelona', 'true');
INSERT INTO students (name, address, graduated) VALUES ('Sandra', 'Catalunya. Barcelona', 'false');
INSERT INTO students (name, address, graduated) VALUES ('Yelitza', 'Madrid. Madrid', 'false');
INSERT INTO students (name, address, graduated) VALUES ('Nuria', 'Valencia. Valencia', 'false');
INSERT INTO students (name, address, graduated) VALUES ('Mario', 'Madrid. Madrid', 'false');
INSERT INTO students (name, address, graduated) VALUES ('Luigi', 'Aragon. Zaragoza', 'true');
INSERT INTO students (name, address, graduated) VALUES ('Carlos', 'Aragon. Zaragoza', 'true');

6. Verify that the data you created for mentors and students are correctly stored in their respective tables (hint: use a `select` SQL statement).

SELECT * FROM mentors;
SELECT * FROM students;

7. Create a new `classes` table to record the following information:

   - A class has a leading mentor
   - A class has a topic (such as Javascript, NodeJS)
   - A class is taught at a specific date and at a specific location

CREATE TABLE classes(
id SERIAL PRIMARY KEY,
leadingmentor VARCHAR(50) NOT NULL,
topic VARCHAR(120) NOT NULL,
date DATE NOT NULL,
location VARCHAR(30) NOT NULL
);

8. Insert a few classes in the `classes` table

INSERT INTO classes (leadingmentor, topic, date, location) VALUES ('Peter Love', 'JavaScript', '2021/05/05', 'USA');
INSERT INTO classes (leadingmentor, topic, date, location) VALUES ('Mary Simm', 'React', '2021/07/05', 'Spain');
INSERT INTO classes (leadingmentor, topic, date, location) VALUES ('Susan Glow', 'Node', '2021/08/05', 'UK');
INSERT INTO classes (leadingmentor, topic, date, location) VALUES ('Juan Love', 'JavaScript', '2021/05/05', 'USA');

9. We now want to store who among the students attends a specific class. How would you store that? Come up with a solution and insert some data if you model this as a new table.

CREATE TABLE classes_attends (
	student_id INT REFERENCES students(id),
	class_id INT REFERENCES classes(id),
	class_date DATE REFERENCES classes(specific_date)
);

INSERT INTO classes_attends (student_id, class_id, class_date) VALUES (1, 3, '2021/08/05');
INSERT INTO classes_attends (student_id, class_id, class_date) VALUES (2, 2, '2021/07/05');
INSERT INTO classes_attends (student_id, class_id, class_date) VALUES (3, 1, '2021/05/05');

10. Answer the following questions using a `select` SQL statement:
    - Retrieve all the mentors who lived more than 5 years in Glasgow
    SELECT * FROM mentors WHERE yearsinglasgow > 5;
    - Retrieve all the mentors whose favourite language is Javascript
    SELECT * FROM mentors WHERE favprogramlanguage = 'JavaScript';
    - Retrieve all the students who are CYF graduates
    SELECT * FROM students WHERE graduated = 'true';
    - Retrieve all the classes taught before June this year
    SELECT * FROM classes WHERE date < '2021-06-01';
    - Retrieve all the students (retrieving student ids only is fine) who attended the Javascript class (or any other class that you have in the `classes` table).
    SELECT student_id, class_id FROM classes_attends WHERE class_id = 1;