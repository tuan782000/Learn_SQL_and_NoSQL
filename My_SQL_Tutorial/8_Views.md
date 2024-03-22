```sql

-- Tạo bảng employees

CREATE TABLE employees (
    id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);

-- Thêm dữ liệu

INSERT INTO employees (id, first_name, last_name, department, salary)
VALUES
    (1, 'John', 'Doe', 'IT', 50000.00),
    (2, 'Jane', 'Smith', 'HR', 60000.00),
    (3, 'Alice', 'Johnson', 'Finance', 70000.00);

-- Create a view
CREATE VIEW employee_names AS
SELECT id, CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;

-- view này nhiệm vụ là lấy ra bảng ghi kèm id và full_name từ bảng employees
-- full_name là sự kết hợp nối chuỗi giữa 3 tham số

-- Query the view
SELECT * FROM employee_names; -- sử dụng view mình đã tạo ra

-- Update the view (recreate it)
-- Create a view if didn't exists already, or replace it with this new one.
-- Tạo ra 1 view hoặc cập nhật lại view nó nếu đã tồn tại.

CREATE OR REPLACE VIEW employee_names AS
SELECT id, CONCAT(first_name, ' ', last_name) AS full_name
FROM employees
WHERE department = 'IT';

SELECT * FROM employee_names;

-- Delete the view
DROP VIEW employee_names; -- xóa view đó đi
```