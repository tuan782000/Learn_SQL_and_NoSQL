-- -----------------
-- SHOW DATABASES;
-- Hiển thị toàn bộ Database
-- -----------------

-- -----------------
-- CREATE DATABASE MACHINES;
-- Khởi tạo 1 datasbe
-- -----------------

-- -----------------
-- DROP DATABASE MACHINES;
-- Hủy bỏ 1 database
-- -----------------

-- -----------------
-- CREATE DATABASE MACHINES;
-- USE MACHINES
-- Tạo và sử dụng database
-- -----------------

-- -----------------
-- USE GAMES;
-- SELECT DATABASE()
-- Sử dụng database và chọn database
-- -----------------

-- -----------------
-- CREATE DATABASE PC;
-- USE PC;
-- CREATE TABLE GAMES (
--     name VARCHAR(50),
--     ratings INT
-- );


-- Tạo database PC và sử dụng database PC tạo Table có tên GAMES và mô tả nó 2 thuộc tính name và ratings
-- -----------------

-- -----------------
-- SHOW TABLES;
-- SHOW COLUMNS FROM GAMES;
-- DESC GAMES;

-- Hiển thị toàn bộ các trường trong database
-- -----------------

-- -----------------
-- CREATE TABLE GAMES (
--     name VARCHAR(50) DEFAULT 'Anonymous',
--     release_year INT DEFAULT 2024,
--     ratings INT NOT NULL
-- );

-- DESC GAMES;

Tạo bảng và đặt giá trị mặc định
-- -----------------

-- -----------------
-- DROP TABLE GAMES;
-- SHOW TABLES;

-- Xóa bảng GAMES
-- -----------------

-- CREATE TABLE Movies (
--   name VARCHAR(50),
--   release_year INT,
--   ratings DECIMAL,
--   comment CHAR(10),
--   comment_date DATE DEFAULT "2025-04-02",
--   comment_time TIME DEFAULT "14:10:42"
-- );

-- Tạo bảng Movies chứa các thông tin

-- -----------------

Tạo bảng GAMES có các trường name, release_year, ratings. 
Sau đó Show cái bảng ta. 
Thêm dữ liệu bảng vừa mới tạo ra



-- CREATE TABLE GAMES (
--     name VARCHAR(50) ,
--     release_year INT,
--     ratings INT
-- );

-- DESC GAMES;

-- INSERT INTO GAMES(name, release_year, ratings)
-- VALUES
-- ('GTA 6', 2015, 6),
-- ('GTA 5', 2013, 9),
-- ('Batman: Arkham Knight', 2015, 7),
-- ('AKR 2', 2017, 2);


-- -----------------

-- -----------------
-- SELECT 2 + 2
-- SELECT 2 - 2
-- SELECT 2 * 2

Chỉ lấy dữ liệu name ra từ bảng GAMES

-- SELECT name FROM GAMES;

Chỉ lấy dữ liệu ratings từ bảng GAMES

-- SELECT ratings FROM GAMES;

Chỉ lấy dữ liệu ratings từ bảng GAMES

-- SELECT release_year FROM GAMES;

Chỉ lấy dữ liệu name và ratings từ bảng GAMES

-- SELECT name, ratings FROM GAMES;

Lấy toàn bộ dữ liệu từ bảng GAMES

-- SELECT * FROM GAMES;
-- -----------------


Chủ đề PRIMARY KEY

-- -----------------
-- CREATE TABLE MOVIES (
--     id INT PRIMARY KEY, -- 👈 Primary Key / Unique
--     title VARCHAR(50),
--     genre VARCHAR(50),
--     director VARCHAR(50),
--     cast_count INT,
--     languages INT,
--     release_year INT,
--     imdb_ratings DOUBLE,
--     duration INT
-- );

-- INSERT INTO MOVIES(
--     id,
--     title,
--     genre,
--     director,
--     cast_count,
--     languages,
--     release_year,
--     imdb_ratings,
--     duration
-- )
-- VALUES
--  (1, 'The Wither', 'Horror', 'Timur', 5,5,5,5.0,120),
-- ❌ (1,'Extraction','Action','Sam Hargrave',5,5,5,5.0,120)
--  (2, 'Extraction', 'Action', 'Sam Hargrave', 5,5,5,5.0,120);

-- SELECT * FROM MOVIES;
-- -----------------

-- -----------------

Lấy toàn bộ dữ liệu từ table Movies

-- SELECT * FROM MOVIES;

Lấy toàn bộ dữ liệu từ MOVIES với điều kiện genre = 'Action'

-- SELECT * FROM MOVIES WHERE genre = 'Action';

Lấy dữ liệu title từ bảng MOVIES điều kiện genre = 'Action'

-- SELECT title FROM MOVIES WHERE genre = 'Action';

Lấy dữ liệu title và genre từ table MOVIES điều kiện genre = 'Action'

-- SELECT title, genre FROM MOVIES WHERE genre = 'Action';

Lấy dữ liệu title từ bảng MOVIES điều kiện imdb_ratings = 5.0

-- SELECT title FROM MOVIES WHERE imdb_ratings = 5.0;
-- -----------------

-- -----------------

Alias: đặt tên giả.

nó sẽ đặt 1 tên giả cho cột đó

-- SELECT id AS movie_id FROM MOVIES;
-- SELECT title AS movie_name FROM MOVIES;
-- SELECT imdb_ratings AS movie_rating FROM MOVIES;
-- SELECT cast_count AS casts from MOVIES;
-- -----------------

-- -----------------
1. Tạo bảng USERS

-- CREATE TABLE USERS(
--     id INT PRIMARY KEY,
--     name VARCHAR(50),
--     age INT,
--     email VARCHAR(50),
--     password VARCHAR(50)
-- );

2. Thêm dữ liệu vào cho bảng USERS

-- INSERT INTO USERS(id, name, age, email, password)
-- VALUES
-- (1, 'John', 25, 'U3Qc2@example.com', 'password123'),
-- (2, 'Jane', 30, 'qGqQh@example.com', 'password456'),
-- (3, 'Bob', 35, 'I3l0h@example.com', 'password789');

3. Lấy ra toàn bộ dữ liệu USERS

-- SELECT * FROM USERS;

4. Cập nhật bảng USERS với điều kiện cụ thể

-- UPDATE USERS
-- SET age = 30
-- WHERE id = 1

5. Chọn tất cả dữ liệu từ USERS

-- SELECT * FROM USERS;

6. Cập nhật bảng USERS đi đến cột password và kiểm tra điều kiện id = 1 sẽ set lại giá trị mới cho nó

-- UPDATE USERS
-- SET password = "newpassword"
-- WHERE id = 1

-- SELECT * FROM USERS;
-- -----------------


-- -----------------

SELECT * FROM USERS;
DELETE FROM USERS
WHERE id = 1

SELECT * FROM USERS;

DELETE FROM USERS;

SELECT * FROM USERS;