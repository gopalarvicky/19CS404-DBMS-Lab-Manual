# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
```
 Create a new table named orders with the following specifications:
    ord_id as TEXT with a length of 4.
    item_id as TEXT.
    ord_date as DATE.
    ord_qty as INTEGER.
    cost as INTEGER.
    The primary key is a composite key consisting of item_id and ord_date.
    ord_id and item_id should not accept NULL
```



```sql
CREATE TABLE orders (
  ord_id CHAR(4) NOT NULL,
  item_id TEXT NOT NULL,
  ord_date DATE,
  ord_qty INTEGER,
  cost INTEGER,
  PRIMARY KEY (item_id, ord_date)
);
```

**Output:**

![Screenshot 2025-04-29 090102](https://github.com/user-attachments/assets/efd65fcb-1914-4e26-b132-6b00cb51481e)


**Question 2**
---
```
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100

```

```sql
-- insert into Products (ProductID,Name,Category,Price,Stock) values('106','Fitness Tracker','Wearables',null,null),('107','Laptop','Electronics','999.99','50'),
('108','Wireless Earbuds','Accessories',null,'100');
```

**Output:**

![Screenshot 2025-04-29 090113](https://github.com/user-attachments/assets/84a5f46c-674b-499d-97d7-5091a525ed49)


**Question 3**
---
```
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
```

```sql
create table jobs(
  job_id text primary key,
  job_title text default '',
  min_salary integer default 8000,
  max_salary integer default null
 
);
```

**Output:**

![Screenshot 2025-04-29 090359](https://github.com/user-attachments/assets/de6c4d3a-c813-45fd-8486-4bd25b5753cb)

**Question 4**
---
```
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.
```

```sql
alter table employee add department_id INTEGER;
alter table employee add manager_id INTEGER default NULL;

```

**Output:**

![Screenshot 2025-04-29 090134](https://github.com/user-attachments/assets/d627244c-4472-489d-bae9-9b609da93e31)

**Question 5**
---
```
Create a table named Invoices with the following constraints:
  InvoiceID as INTEGER should be the primary key.
  InvoiceDate as DATE.
  Amount as REAL should be greater than 0.
  DueDate as DATE should be greater than the InvoiceDate.
  OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```

```sql
create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate  DATE,
Amount REAL check(Amount>0),
DueDate DATE check(DueDate>InvoiceDate),
OrderID INTEGER,
foreign key (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

![Screenshot 2025-04-29 090447](https://github.com/user-attachments/assets/24a5286f-8426-4572-a3b9-259a41f1da8a)

**Question 6**
---
```
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.
```
```sql
insert into Employee (EmployeeID,Name,Position) values('4','Emily White','Analyst');
```

**Output:**

![Screenshot 2025-04-29 090455](https://github.com/user-attachments/assets/d317778c-ec13-4799-840f-637dbe98df86)

**Question 7**
---
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email
```
```sql
insert into Customers(CustomerID, Name, Address, Email)
select CustomerID, Name, Address, Email
from Old_customers
```

**Output:**

![Screenshot 2025-04-29 090508](https://github.com/user-attachments/assets/a03f156e-57da-4b43-90f6-2c8997d70942)

**Question 8**
---
```
Create a table named Locations with the following columns:

  LocationID as INTEGER
  LocationName as TEXT
  Address as TEXT
```
```sql
create table Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

![Screenshot 2025-04-29 090515](https://github.com/user-attachments/assets/d2dec387-1bd2-4985-a045-95090f5a10c9)

**Question 9**
---
```
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

```
```sql
alter table Student_details add email TEXT not null default 'Invalid';
```

**Output:**

![Screenshot 2025-04-29 090523](https://github.com/user-attachments/assets/7d337494-2650-40fa-9f1f-4bc7b926a131)

**Question 10**
---
```
 Create a new table named item with the following specifications and constraints:
  item_id as TEXT and as primary key.
  item_desc as TEXT.
  rate as INTEGER.
  icom_id as TEXT with a length of 4.
  icom_id is a foreign key referencing com_id in the company table.
  The foreign key should cascade updates and deletes.
  item_desc and rate should not accept NULL.
```
```sql
create table item (
item_id TEXT primary key,
item_desc TEXT,
rate INTEGER,
icom_id TEXT check(length(icom_id)=4),
foreign key (icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE

);
```

**Output:**

![Uploading Screenshot 2025-04-29 090530.png…]()


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
