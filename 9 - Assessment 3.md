# Section 9: Assessment 3

### Question 1 
#### The students table should have columns for student_id, first_name, last_name, homeroom_number, phone, email, and graduation year.
```SQL
CREATE TABLE students(
	student_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	homeroom_number INTEGER,
	phone VARCHAR(20) NOT NULL UNIQUE,
	email VARCHAR(115) NOT NULL UNIQUE,
	grad_year integer
)
```

### Question 2
#### The teachers table should have columns for teacher_id, first_name, last_name, homeroom_number, department, email, and phone.
```SQL
CREATE TABLE teachers(
	teacher_id SERIAL PRIMARY KEY, 
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	homeroom_number INTEGER,
	department VARCHAR(50) NOT NULL,
	email VARCHAR(50) UNIQUE, 
	phone VARCHAR(50) UNIQUE
)
```

### Question 3 
#### Insert a student named Mark Watney (student_id=1) who has a phone number of 777-555-1234 and doesn't have an email. He graduates in 2035 and has 5 as a homeroom number.
```SQL
ALTER TABLE students
ALTER COLUMN email DROP NOT NULL;

INSERT INTO students(first_name, last_name, homeroom_number, phone, grad_year)
VALUES
('Mark', 'Watney', 5, '777-555-1234', 2035);
```

### Question 4 
#### Insert a teacher names Jonas Salk (teacher_id = 1) who as a homeroom number of 5 and is from the Biology department. His contact info is: jsalk@school.org and a phone number of 777-555-4321.
```SQL
INSERT INTO teachers(first_name, last_name, homeroom_number, department, email, phone)
VALUES
('Jonas', 'Salk', 5, 'Biology', 'jsalk@school.org', '777-555-4321');
```