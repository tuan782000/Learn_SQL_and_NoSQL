SQL là từ viết tắt của Structured Query Language, là ngôn ngữ truy vấn có cấu trúc, cho phép bạn truy cập và thao tác với các cơ sở dữ liệu để tạo, xóa, sửa đổi, trích xuất dữ liệu.
Main SQL concepts: Database, schema, table, columns & rows, constraints 
Các loại lệnh chính trong SQL (commands)

DQL (data query language): Lệnh truy vấn. 80-90% công việc của DA/BI sẽ thao tác trong nhóm lệnh này. 
DDL (data definition language): Lệnh định nghĩa, xây dựng và quản lý các đối tượng trong databases (tables, views và procedures). 
DCL (data control language): Lệnh thao tác quản lý bảo mật dữ liệu và phân quyền cho các đối tượng người dùng. 
DML (data manipulation language): Lệnh thay đổi các giá trị dữ liệu trong bảng ( INSERT, UPDATE, DELETE)
TCL (transaction control language): 


B. Chú trọng nhóm lệnh truy vấn (DQL)

DEV nên chú trọng
DDL data definition language
	Create
	Drop
	Alter
	Truncate
DML data manipulation language
	Insert
	Update
	Delete
DQL data query language (dùng nhiều)

Câu lệnh truy vấn đầy đủ gồm:
	SELECT: hiển thị kết quả truy vấn
	FROM: lấy data từ tables nào
	WHERE: khai báo các điều kiện
	GROUP BY: gom nhóm theo đối tượng
	ORDER BY: sắp xếp dữ liệu
	HAVING: sắp xếp dữ liệu sau khi gom nhóm

Phép ghép các bảng dữ liệu
	JOIN: mở rộng tables theo chiều ngang
	UNION: mở rộng tables theo chiều dọc

Hàm tính toán có sẵn (built-in functions)
	Scalar functions: nhóm hàm thao tác trên từng dòng và trả về 1 giá trị. 
     Có thể liệt kê các hàm chuyển đổi CONVERTION, DATE & TIME, STRING, …
	Logical functions: Mệnh đề CASE… WHEN, IIF, CHOOSE, ISNULL, …
	Ranking: hàm xếp hạng dữ liệu (RANK, ROW_NUMBER, …)
	Aggregate: hàm tính tổng (MIN, MAX, SUM, AVERAGE, …)

Truy vấn trên bảng phụ
	Subquery: Câu lệnh truy vấn lồng ghép
	CTE (Common table expression): Tạo ra bảng phụ bằng câu lện truy vấn

D. Tư duy logic và hiểu thứ tự thực hiện các lệnh trong SQL
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT



===============================================================================================================
Định nghĩa về dữ liệu và truy vấn thao tác

Lệnh ADD
ADD dùng để thêm một cột mới vào một bảng đã tồn tại.

ALTER TABLE employee ADD last_name varchar2(255); 
// Câu lệnh này sẽ thêm một cột mới có tên last_name vào bảng employee. 
// Cột last_name sẽ là một kiểu varchar2, với độ dài tối đa là 255 ký tự.
ALTER TABLE employee ADD CONSTRAINT emp_det PRIMARY KEY (id, last_name); 
// Câu lệnh này sẽ thêm một ràng buộc khóa chính vào bảng employee. 
// Ràng buộc khóa chính sẽ được đặt trên các cột id và last_name. 
// Điều này có nghĩa là mỗi hàng trong bảng employee phải có một giá trị duy nhất cho cả hai cột id và last_name.


// Nói cách khác, hai câu lệnh sẽ thêm một cột mới có tên last_name vào bảng employee 
và làm cho các cột id và last_name trở thành khóa chính của bảng.


Từ khóa ALTER TABLE được sử dụng để sửa đổi cấu trúc của một bảng. 
Từ khóa ADD được sử dụng để thêm một cột mới vào một bảng. 
Cột last_name sẽ là một kiểu varchar2, với độ dài tối đa là 255 ký tự.


Từ khóa CONSTRAINT được sử dụng để tạo một ràng buộc trên một bảng. 
Ràng buộc PRIMARY KEY được sử dụng để chỉ định rằng một cột hoặc kết hợp các cột là khóa chính của bảng. 
emp_det là tên của ràng buộc, và các cột id và last_name là các cột tạo thành khóa chính.


Lệnh ALTER TABLE

ALTER TABLE được sử dụng để thêm, xóa hoặc cập nhật các cột trong một bảng đã tồn tại trước đó. 
Nó cũng có thể được dùng để xoá bỏ các ràng buộc toàn vẹn trên bảng hiện có.

// Thêm (cột last_name)
ALTER TABLE employee ADD last_name varchar2(255); 

// Xóa (cụ thể xóa cột last_name) 
ALTER TABLE employee DROP COLUMN last_name;


Lệnh ALTER COLUMN

ALTER COLUMN dùng để thay đổi loại dữ liệu của cột.

Ví dụ:
ALTER TABLE employee ALTER COLUMN joining_date datetime;

- Trả về kết quả là một giá trị boolean.
- Trả về TRUE nếu tất cả các giá trị con khớp với điều kiện.
- Thường được dùng với các mệnh đề SELECT, WHERE và HAVING.

SELECT employee_name, joining_date from employee WHERE employee_id = ALL (select employee_id from department_details WHERE department = ‘R&D’);


Lệnh AND

Toán tử AND sẽ:

- Được dùng để kiểm tra 2 hoặc nhiều điều kiện trong các lệnh SELECT, INSERT, UPDATE hoặc DELETE.
- Trả về TRUE khi tất cả các điều kiện trong mệnh đề WHERE được thỏa mãn.

SELECT employee_name, salary from employee WHERE city = ‘California’ AND salary > 2000;

Lệnh ANY

Toán tử ANY sẽ:

Trả về kết quả là một giá trị kiểu boolean.
Trả về TRUE nếu có bất kỳ giá trị con nào khớp với điều kiện.

SELECT employee_id, employee_name from employee 
WHERE employee_id = ANY (select employee_id from department_details WHERE department = ‘HR’ OR department = ‘R&D’);


Lệnh AS (Alias)
AS được dùng để tạo tên tạm thời (gọi là bí danh) cho cột hoặc bảng.

SELECT count(employee_id) AS employees_from_houston from employee WHERE city = 'Houston';



Lệnh ASC
ASC được sử dụng để sắp xếp dữ liệu theo thứ tự tăng dần, sử dụng theo mệnh đề ORDER BY.

SELECT employee_name, joining_date, salary from employee ORDER BY employee_name ASC;


Lệnh BETWEEN
BETWEEN chọn các giá trị trong một phạm vi.

SELECT employee_name, joining_date, department_id from employee WHERE salary  BETWEEN 40000 AND 100000;


Lệnh CASE
Câu lệnh CASE đi qua các điều kiện và trả về một giá trị khi điều kiện đầu tiên được đáp ứng. Nếu:

Điều kiện là đúng, nó sẽ dừng đọc và trả về kết quả. Nếu không có điều kiện nào đúng, nó sẽ trả về giá trị trong mệnh đề ELSE.
Không có phần ELSE và không có điều kiện nào là đúng, nó sẽ trả về NULL.

SELECT order_amount, customer_id, contact_email 
CASE WHEN order_amount > 3000 THEN "Eligible for 40% discount" 
WHEN order_amount between 2000 and 3000 THEN "Eligible for 25% discount" 
ELSE "Eligible for 5% discount" END FROM order_details;


Lệnh CREATE DATABASE
CREATE DATABASE được sử dụng để tạo cơ sở dữ liệu SQL mới.

CREATE DATABASE movies_development;


Lệnh CREATE TABLE
CREATE TABLE được sử dụng để tạo bảng mới với tên bảng và tên cột được chỉ định.

CREATE TABLE movie_info 
(movie_name varchar2(255), 
release_date datetime, 
lead_actor varchar2(255), 
music_director varchar2(255));


Lệnh DEFAULT
DEFAULT được sử dụng để thiết lập một giá trị mặc định cho một cột. 
Được sử dụng với các lệnh CREATE và ALTER TABLE.


CREATE TABLE employee (joining_date SET DEFAULT CURRENT_DATE);


ALTER TABLE product ALTER is_available SET DEFAULT true;


Lệnh DELETE

DELETE được sử dụng để xóa dữ liệu khỏi bảng được chỉ định.

DELETE from employee where employee_id = 345;

Lệnh DESC

DESC được sử dụng để sắp xếp dữ liệu theo thứ tự giảm dần, sử dụng theo mệnh đề ORDER BY.

SELECT employee_name, joining_date, salary from employee ORDER BY employee_name DESC;

Lệnh DROP COLUMN

DROP COLUMN được dùng để xóa cột được chỉ định khỏi bảng được chỉ định.

ALTER TABLE employee DROP COLUMN employee_name;


Lệnh DROP DATABASE
DROP DATABASE dùng để xóa toàn bộ cơ sở dữ liệu.

DROP DATABASE movies_development;


Lệnh DROP DEFAULT
DROP DEFAULT dùng để xóa giá trị mặc định của cột được chỉ định.

ALTER TABLE employee ALTER COLUMN is_available DROP DEFAULT;


Lệnh DROP TABLE
DROP TABLE được dùng để xóa bảng được chỉ định.
DROP TABLE employee;


Lệnh EXISTS
Toán tử EXISTS được sử dụng để:

Kiểm tra sự tồn tại của bất kỳ bản ghi nào trong một truy vấn con.
Trả về giá trị TRUE nếu truy vấn con trả về một hoặc nhiều bản ghi.

SELECT employee_id, contact_number FROM employee 
WHERE EXISTS (SELECT employee_id, department FROM department WHERE employee_id = 345 AND department = 'HR');


Lệnh FROM
FROM được dùng để được sử dụng để liệt kê các bảng và các phép giao cần thiết cho câu lệnh SQL

SELECT * FROM employee; DELETE FROM employee where employee_id = 345;


Lệnh GROUP BY
GROUP BY được dùng để kết hợp với lệnh SELECT để sắp xếp dữ liệu từ nhiều bản ghi đồng nhất vào trong các nhóm.

Hiển thị số lượng nhân viên ở mỗi quốc gia.
SELECT COUNT(employee_id), country from employee GROUP BY country;


Hiển thị xếp hạng trung bình nhân viên của mỗi bộ phận.
SELECT AVG(rating), department from employee GROUP BY department;


Lệnh IN
IN được dùng để chọn nhiều giá trị cùng một lúc trong mệnh đề WHERE thay vì sử dụng điều kiện OR.

SELECT employee_name FROM employee WHERE country IN ('India', 'United Kingdom', 'Singapore', 'Australia');


Lệnh INDEX
INDEX làm cho dữ liệu truy vấn hiệu quả và nhanh hơn, thường được tạo trên các cột được tìm kiếm nhiều nhất.

Tạo INDEX
CREATE INDEX idx_employee ON employee (first_name, last_name);


Tạo INDEX duy nhất trong đó các giá trị không thể được nhân đôi
CREATE UNIQUE INDEX idx_employee ON employee (first_name, last_name);


Xóa INDEX
ALTER TABLE employee DROP INDEX idx_employee;


Lệnh INSERT INTO
INSERT INTO dùng để thêm hàng mới vào bảng.

INSERT INTO employee (employee_id, employee_name, salary, core_skill) VALUES (451, ‘Lee Cooper’, 40000, ‘Java’);


Lệnh IS NULL
IS NULL dùng để kiểm tra các giá trị null.

SELECT employee_id from employee where employee_name IS NULL;



Lệnh IS NOT NULL
IS NOT NULL kiểm tra các giá trị không phải là null.
SELECT employee_id, core_skill from  employee where core_skill IS NOT NULL;


Lệnh LIKE
LIKE xác định xem một chuỗi ký tự có khớp với mẫu đã chỉ định hay không.

SELECT employee_id,  first_name, last_name  where  first_name LIKE ‘%tony’;


Lệnh NOT LIKE
NOT LIKE xác định xem một chuỗi ký tự không khớp với mẫu đã chỉ định.

SELECT employee_id,  first_name, last_name  where  first_name NOT LIKE ‘%tony’;


Lệnh OR
OR được dùng để kiểm tra nhiều điều kiện xem có bản ghi nào trong kết quả trả về đáp ứng được điều kiện hay không.


SELECT * from employee where country = ‘India’ OR country = ‘Australia’;


Lệnh ORDER BY
ORDER BY được sử dụng để sắp xếp dữ liệu theo thứ tự tăng dần (theo mặc định) 
hoặc thứ tự được chỉ định trong truy vấn (tăng dần hoặc giảm dần).


SELECT employee_name, salary from employee ORDER BY salary DESC;



Lệnh ROWNUM
ROWNUM được sử dụng để chỉ định số lượng bản ghi trả vềtheo mệnh đề WHERE.

SELECT * from employee where ROWNUM <= 5; This will return the first five rows in the resultset.


Lệnh SELECT
SELECT là lệnh được dùng để lấy kết quả từ một hoặc nhiều bảng trong cơ sở dữ liệu của SQL Server.

SELECT employee_id from employee; SELECT * from employee;


Lệnh SELECT INTO
SELECT INTO được dùng để tạo bảng từ 1 bảng sẵn có bằng cách sao chép các cột từ bảng ban đầu.

SELECT * INTO new_employee_info FROM employee; 
SELECT employee_name, joining_date, core_skill INTO new_employee_info FROM employee;


Lệnh SELECT TOP
SELECT TOP dùng để chọn số lượng bản ghi được chỉ định từ bảng.

SELECT TOP 5 employee_id from employee where employee_rating = 5;


Lệnh SET
SET dùng để đặt giá trị của một cột thành giá trị được chỉ định trong hoạt động UPDATE.

UPDATE employee SET first_name = ‘Tony’ WHERE employee_id = 345;


Lệnh SOME
SOME dùng để so sánh một giá trị với từng giá trị trong tập dữ liệu. 
SOME trả về TRUE nếu có một giá trị bất kỳ trong tập dữ liệu này thỏa mãn điều kiện. 
SOME và ANY về cơ bản hoàn toàn giống nhau.


SELECT employee_id, employee_name from employee 
WHERE salary > SOME (select salary from employee WHERE department = ‘HR’);



Lệnh TRUNCATE TABLE
TRUNCATE TABLE được sử dụng để xóa hoàn toàn các bản ghi từ một bảng đang tồn tại trong SQL.

TRUNCATE TABLE log_info;


Lệnh UNION
UNION được dùng để kết hợp 2 bộ kết quả từ 2 hoặc nhiều lệnh SELECT. 
Nó sẽ xóa các hàng trùng trong các lệnh SELECT này.

SELECT city from employee UNION SELECT city from office_locations;



Lệnh UNIQUE
UNIQUE được sử dụng để bảo đảm rằng chỉ các giá trị duy nhất được nhập vào trong cột hoặc một tập hợp các cột. 
Nó cho phép nhà phát triển chắc chắn rằng không có các giá trị trùng lặp được nhập vào.

CREATE TABLE employee (employee_id int NOT NULL, UNIQUE(employee_id));

ALTER TABLE employee ADD UNIQUE(employee_id);


Lệnh UPDATE
UPDATE được dùng để cập nhật các bản ghi hiện có trên một bảng trong cơ sở dữ liệu của SQL Server.

UPDATE employee SET first_name = ‘Tony’ WHERE employee_id = 345;

Lệnh VALUES
VALUES được sử dụng với lệnh INSERT để thêm một hàng giá trị mới vào bảng.

INSERT INTO employee (employee_id, employee_name, salary, core_skill) VALUES (451, ‘Lee Cooper’, 40000, ‘Java’);


Lệnh WHERE
WHERE được sử dụng để chỉ định điều kiện khi lấy dữ liệu từ một bảng hoặc nối nhiều bảng với nhau. 
Nếu điều kiện được thỏa mãn thì nó chỉ trả về những giá trị cụ thể trong bảng.


SELECT * from employee WHERE salary > 20000;


Chức năng tổng hợp
Hàm tổng hợp là các lệnh thao tác dữ liệu hoạt động trên các cột số như int và float, 
hữu ích trong việc lọc và sắp xếp dữ liệu ở cấp cơ sở dữ liệu. Một số hàm tổng hợp thường được sử dụng là:


Hàm AVG
AVG trong SQL Server trả về giá trị trung bình của một biểu thức hay giá trị trung bình theo cột được chỉ định 
của các dòng được chọn.

SELECT AVG(marks) from students where subject = ‘English’;



Hàm MIN
MIN trong SQL Server trả về giá trị nhỏ nhất của cột được chỉ định.

SELECT MIN(price) from product WHERE product_category = ‘shoes’;


Hàm MAX
MAX trong SQL Server trả về giá trị lớn nhất của cột được chỉ định.

SELECT MAX(quantity), product_name from inventory;


Hàm COUNT
COUNT trong SQL Server trả về số lượng các giá trị riêng biệt của cột nhất định.

SELECT COUNT(*) from employee; - returns total number of records in the employee table.<br><br>SELECT COUNT(*) from employee where salary > 20000; - returns number of employees whose salary is greater than 20000

Hàm SUM
SUM trong SQL Server trả về tổng các giá trị của cột số được chỉ định.
SELECT SUM(marks) from students where subject = ‘English’;


SQL Joins
SQL joins là phép kết nối dữ liệu từ nhiều bảng lại với nhau, nối 2 bảng, 3 bảng... với nhau. 
Khi bạn cần truy vấn các cột dữ liệu từ nhiều bảng khác nhau để trả về trong cùng một tập kết quả , bạn cần dùng JOIN.



INNER JOIN (Hoặc JOIN)
Trả về tất cả các hàng khi có ít nhất một giá trị ở cả hai bảng.

Cú pháp:

SELECT column1, column2… from table1 INNER JOIN table2 on table1.columnN = table2.columnN;


select c.customer_id, o.order_id, c.customer_phone from customer c INNER JOIN order o on c.customer_id = o.customer_id;



FULL OUTER JOIN (Hoặc OUTER JOIN)
Trả về tất cả các dòng đúng với 1 trong các bảng.

Cú pháp:

SELECT column1, column2… from table1 FULL OUTER JOIN table2 on table1.columnN = table2.columnN;

select c.customer_id, o.order_id, c.customer_phone from customer c FULL OUTER JOIN order o on c.customer_id = o.customer_id;


LEFT OUTER JOIN (Hoặc LEFT JOIN)
Trả lại tất cả các dòng từ bảng bên trái, và các dòng đúng với điều kiện từ bảng bên phải.

Cú pháp:

SELECT column1, column2… from table1 LEFT JOIN table2 on table1.columnN = table2.columnN;


select c.country_id, c.country_name, l.location_name from country c LEFT JOIN locations l on c.country_id = l.country_id;



RIGHT OUTER JOIN (Hoặc RIGHT JOIN)
Trả lại tất cả các hàng từ bảng bên phải, và các dòng thỏa mãn điều kiện từ bảng bên trái.

Cú pháp:

SELECT column1, column2… from table1 RIGHT JOIN table2 on table1.columnN = table2.columnN;


select c.country_id, c.country_name, l.location_name from country c RIGHT JOIN locations l on c.country_id = l.country_id;




