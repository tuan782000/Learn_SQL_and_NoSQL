# Database?

A database is structured collection of data that is organized so that can be easily accessed, managed, and updated. It's typically stored and managed using specualized software called a database management system DBMS.

Một cơ sở dữ liệu là một bộ sưu tập dữ liệu được cấu trúc và được tổ chức sao cho có thể truy cập, quản lý và cập nhật dễ dàng. Thông thường, nó được lưu trữ và quản lý bằng phần mềm chuyên dụng gọi là hệ thống quản lý cơ sở dữ liệu (Database Management System - DBMS).

DBMS

DBMS stands for "Database Management System". It's software that allows users to interact with database. DBMSs are designed to manage large volumes of data efficiently and provides mechanisms for storing, retrieving, updating and managing that data.

DBMS viết tắt của "Database Management System". Đó là phần mềm cho phép người dùng tương tác với cơ sở dữ liệu. DBMS được thiết kế để quản lý các lượng dữ liệu lớn một cách hiệu quả và cung cấp các cơ chế để lưu trữ, truy xuất, cập nhật và quản lý dữ liệu đó.

Database?

A database is a structured collection of data that is organized so that it can easily accessed, managed, and updated. It is typically stored and managed using specialized software called a database management system (DBMS).

Một cơ sở dữ liệu là một bộ sưu tập dữ liệu được cấu trúc và được tổ chức sao cho nó có thể được truy cập, quản lý và cập nhật một cách dễ dàng. Thông thường, nó được lưu trữ và quản lý bằng phần mềm chuyên dụng gọi là hệ thống quản lý cơ sở dữ liệu (Database Management System - DBMS).

# Create Database

Tạo 1 Database

```sql
CREATE DATABASE TEN_DU_AN;

--ex:

CREATE DATABASE ECOMMERCE; -- tạo ra database tên là ECOMMERCE
CREATE DATABASE COMPUTER; -- tạo ra database tên là COMPUTER
```

# Showing Databases

Sau khi tạo database thì mình có thể dùng lệnh show để show ra toàn bộ database trên máy

```sql
SHOW DATABASES;
```

# Drop/Delete Database

Loại bỏ đi 1 Database

```sql
DROP DATABASE TEN_DU_AN;

--ex:
DROP DATABASE ECOMMERCE;
DROP DATABASE COMPUTER;
```

# Use Database

Sử dụng Database, để có thể tao tác các bảng bên trong Database này.

```sql
USE TEN_DU_AN;

--ex:
USE ECOMMERCE;
USE COMPUTER;
```

Tổng hợp lại

```sql
CREATE DATABASE PC DEFAULT CHARACTER SET = 'utf8mb4';
```

# TABLE

Chia ra là hàng và cột

Mỗi cột là mỗi thuộc tính của Table

Mỗi hàng chứa dữ liệu

# DATA TYPES? Kiểu dữ liệu

```sql
CREATE TABLE GAMES (
    name VARCHAR(50)
    ratings INT
)
```

Tạo ra 1 bảng GAMES - có 2 thuộc tính - name và ratings

name có kiểu dữ liệu chữ và tối đa 50 ký tự

ratings kiểu dữ liệu số

# Table info

Display a list of all tables in a database

Hiển thị 1 danh sách chứa tât cả tables trong database

```SQL
SHOW TABLES;
```

Display the columns (fields) of table (TABLE NAME)

Hiển thị cột (trường) của bảng (TABLE NAME)

```sql
SHOW COLUMN NAME;

--ex:
SHOW COLUMN FROM GAMES;
```

Display/Describe the structure of a table

Hiển thị/Mô tả cấu trúc của một bảng.

```sql
DESC NAME;

--ex:
DESC GAMES;
```

```sql
CREATE TABLE GAMES (
    name VARCHAR(50) DEFAULT "Anonymous",
    release_year INT DEFAULT 2024,
    ratings INT
)
```

Nếu mà lúc tạo ra dữ liệu mà không điền thì dựa vào "DEFAULT" giá trị mặc định mà tự động điền vào.

```sql
DROP TABLE GAMES
```

CHAR(size)

đoạn chuỗi ngắn

```SQL
CHAR(10)
```

VARCHAR(size)

```Sql
VARCHAR(255)
```

DECIMAL

DECIMAL(p, s)

p là tổng số chữ số (bao gồm cả các số nguyên và thập phân).
s là số chữ số sau dấu thập phân.

```sql
Price DECIMAL(10, 2)
```

DATE

YYYY-MM-DD

TIME

HH:MM:SS

DATETIME

YYYY-MM-DD HH:MM:SS

```sql
CREATE TABLE Movies (
    title VARCHAR(50),
    release_year INT,
    ratings DECIMAL,
    comment CHAR(10),
    commnet_date DATE DEFAULT "2022-04-02",
    commnet_time TIME DEFAULT "14-10-23",
)
```

Sau khi tạo bảng xong insert dữ liệu vào bảng

```sql
INSERT INTO ten_bang(field_01, field_02)
VALUES ('value1', 'value2')

--ex:

INSERT INTO games(name, ratings)
VALUES ('GTA5', 5)

--ex: Multiple values insert

INSERT INTO games(name, ratings)
VALUES ('GTA5', 5)
       ('BATMAN', 7)
       ('ARK', 6)
```

Câu lệnh Select

```sql
SELECT Ten_thuoc_tinh FROM TEN_BANG;

--ex:
SELECT ratings FROM games; -- chọn cột ratings từ bảng games show ra các dòng dữ liệu từ bảng games này

--ex: select multiple properties

SELECT name,ratings FROM games; --
```

Tổng hợp

```sql
CREATE TABLE Movies (
    title VARCHAR(50),
    release_year INT,
    ratings DECIMAL,
    comment CHAR(10),
    commnet_date DATE DEFAULT "2022-04-02",
    commnet_time TIME DEFAULT "14-10-23",
)

INSERT INTO Movies (title, release_year, ratings, comment, commnet_date, commnet_time)
VALUES ('MAI', 2024, 8, 'OK', "2024-04-02", "14-10-23")
       ('Kungfu panda 4', 2024, 6, 'PO', "2024-04-02", "14-10-23")

SELECT title FROM Movies -- xem dữ liệu 1 trường trong bảng Movies
SELECT ratings, comment FROM Movies -- xem dữ liệu 2 trường trong bảng Movies
SELECT * FROM Movies -- xem toàn bộ dữ liệu trong bảng Movies
```

# Primary key - khóa chính

Đặc điểm: không được phép trùng - dữ liệu nhập vào cũng không được trùng -

```sql
CREATE TABLE MOVIES (
    id INT PRIMARY KEY,
    title VARCHAR(50),
    genre VARCHAR(50),
    director VARCHAR(50),
    cast_count INT,
    languages INT,
    release_year INT,
    imdb_ratings DOUBLE,
    duration INT,
)

INSERT INTO MOVIES (id, title, genre, director, cast_count, languages, release_year, imdb_ratings, duration)
VALUES (1, 'The Witcher', 'Horror', 'Timur', 5, 5, 5, 5.0, 120),
       (2, 'The Witcher 2', 'Horror', 'Timur', 5, 5, 5, 5.0, 120),
       (3, 'The Witcher 2', 'Horror', 'Timur', 5, 5, 5, 5.0, 120),
```

# WHERE

Dùng để lọc các bảng ghi.

Ngoài ra ta có thể áp dụng where để SELECT, UPDATE và DELETE những trường nào thỏa mãn điều kiện / yêu cầu của where

```sql
SELECT * FROM games WHERE ratings = 5;
-- Lấy ra những dữ liệu trong bảng games thỏa điều kiện ratings = 5


SELECT name FROM games WHERE ratings = 5; -- lấy ra trường name từ bảng games thỏa mãn điều kiện ratings = 5
```

# ALIAS

chỉnh sửa tạm thời tên cột id thành 1 tên game_id tạm thời

```sql
SELECT id AS game_id FROM GAMES;


SELECT id AS movie_id FROM MOVIES;
SELECT title AS movie_title FROM MOVIES;
```

# Update Data

```sql
UPDATE table_name
SET column1 = value_1, column2 = value_2,...
WHERE condition;
```

# Delete Data

```sql
DELETE FROM table_name
WHERE condition

DELETE FROM table_name -- xóa toàn bộ dữ liệu trong bảng
```

# SUBSTRING() Function

```sql
SUBSTRING(string, start_position, length)

-- string: chuỗi cần cắt
-- start_position: vị trí bắt đầu cắt
-- length: số lượng sẽ cắt đi

--ex:
SELECT SUBSTRING('Hello World', 1, 5) AS SubstringResult;

-- kết quả là: Hello
```

# REPLACE() - thay thế

```SQL
REPLACE(original_string, old_substring, new_substring)
```

original_string là "chuỗi gốc" mà bạn muốn thực hiện thay thế.

old_substring là "chuỗi con" mà bạn muốn thay thế.

new_substring là "chuỗi con" mới bạn muốn thay thế vào vị trí của "chuỗi con cũ".

```sql
SELECT REPLACE('Hello World', 'World', 'Universe') AS ReplacedString;

```

# REVERSE()

REVERSE(string_expression)

string_expression là chuỗi mà bạn muốn đảo ngược.

```sql
SELECT REVERSE('Hello') AS ReversedString;

-- olleH
```

# CHAR_LENGTH()

Trả về số lượng từ xuất hiện trong chuỗi đó

```sql
SELECT CHAR_LENGTH(string)

SELECT CHAR_LENGTH('Hello World') AS LengthOfString;
-- 11
```
