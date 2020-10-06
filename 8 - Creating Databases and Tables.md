# Section 8: Creating Databases and Tables

### Constraints
#### Column Constraints
- NOT NULL
    - Ensures that a column cannot have a NULL value
- UNIQUE
    - Ensures that all values in a column are different
- PRIMARY Key
    - Uniquely identifies each row in a database table
- FOREIGN Key
    - Constrains data based on columns in other tables
- CHECK
    - Ensures that all values in a column satisfy certain conditions
- EXCLUSION
    - Ensures that if any two rows are compared on the specified column, not all of these comparisons will return TRUE

#### Table Constraints
- CHECK
    - To check a condition when inserting or updating data
- REFERENCES
    - To constrain the value stored in the column that must exist in a column in another table
- UNIQUE(column_list)
    - To force the values stored in the columns listed to be unique
- PRIMARY KEY(column_list)
    - To define the primary key that consists of multiple columns

### CREATE
```SQL
CREATE TABLE account(
	user_id SERIAL PRIMARY KEY,
	username VARCHAR(50) UNIQUE NOT NULL, 
	password VARCHAR(50) NOT NULL,
	email VARCHAR(250) UNIQUE NOT NULL,
	created_on TIMESTAMP NOT NULL,
	last_login TIMESTAMP
)

CREATE TABLE job(
	job_id SERIAL PRIMARY KEY,
	job_name VARCHAR(200) UNIQUE NOT NULL
)

CREATE TABLE account_job(
	user_id INTEGER REFERENCES account(user_id),
	job_id INTEGER REFERENCES job(job_id),
	hire_date TIMESTAMP
)

CREATE TABLE information(
	info_id SERIAL PRIMARY KEY,
	title VARCHAR(50) NOT NULL,
	person VARCHAR(50) NOT NULL UNIQUE
)
```

### INSERT
```SQL
INSERT INTO account(username, password, email, created_on)
VALUES
('Jose', 'password', 'jose@gmail.com', CURRENT_TIMESTAMP);

INSERT INTO job(job_name)
VALUES
('Doctor');

INSERT INTO job(job_name)
VALUE
('Cowboy');

INSERT INTO account_job(user_id, job_id, hire_date)
VALUES
(1, 1, CURRENT_TIMESTAMP);
```

### UPDATE
```SQL
UPDATE account
SET last_login = CURRENT_TIMESTAMP;

UPDATE account
SET last_login = created_on;

UPDATE account_job
SET hire_date = account.created_on
FROM account
WHERE account_job.user_id = account.user_id;

UPDATE account
SET last_login = CURRENT_TIMESTAMP
RETURNING email, created_on, last_login;
```

### DELETE
```SQL
DELETE FROM job
WHERE job_name = 'Cowboy'
RETURNING job_id, job_name;
```

### ALTER
```SQL
ALTER TABLE information
RENAME TO new_info;

ALTER TABLE new_info
RENAME COLUMN person to people;

ALTER TABLE new_info
ALTER COLUMN people DROP NOT NULL;
```

### DROP
```SQL
ALTER TABLE new_info
DROP COLUMN people;
```

### CHECK
```SQL
CREATE TABLE employees(
	emp_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	birthdate DATE CHECK (birthdate > '1900-01-01'),
	hire_date DATE CHECK (hire_date > birthdate),
	salary INTEGER CHECK (salary > 0)
)
```