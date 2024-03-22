#Lưu ý: MySQL có 1 chút khác biệt với SQL server về cú pháp.

1. DATABASES

1.1 Tạo Database:
Cú pháp:
Create Database ten_Database;
Ví dụ:
Create Database myDB;

1.2 Sử dụng Database:
Tạo xong thì sử dụng
Cú pháp:
Use ten_Database;
Ví dụ:
Use myDB;

1.3 Xóa Database:
Xóa DB:
Cú pháp:
Drop Database ten_Database;
Ví dụ:
Drop Database myDB;

1.4 Alter Database: Thay đổi, giống như là edit thông tin hoặc cấu hình lại...

Người mới bắt đầu sẽ có 2 cái thương sử dụng:

-   Cái đầu tiên chỉ được đọc DB đó
    ALTER DATABASE myDB READ ONLY = 1; // chuyển từ chế độ có thể sửa xóa, thành không thể xóa sửa nhung vẫn truy cập đọc xem dữ liệu bình thường

    Để khôi phục lại thì chế độ có thể xóa sửa.
    ALTER DATABASE myDB READ ONLY = 0; // Để trở lại bình thường hủy chế độ đọc

-   Cái thứ hai là bật mã hóa

    2.TABLES

    2.1 Tạo Table:
    Cú pháp:
    Create TABLE ten_Table(
    ở đây sẽ là khai báo các trường dữ liệu mà Table này sẽ sở hữu
    tên_trường kiểu_dữ_liệu(thí dụ INT, VARCHAR, BOOLEAN, DECIMAL, DATE ),
    INT: kiểu số,
    VARCHAR: kiểu chuỗi, => VARCHAR(50), 50 ở đây là số ký tự chứa tôi đa là 50
    DECIMAL (5, 2), tham số thứ 1 là lượng chữ số tối đa xuất hiện, tham số thứ 2 là số thập phân sẽ xuất hiện
    DATE, không điền tự lấy mặc định chính xác giờ mà tạo ra nó
    ...
    );
    Ví dụ:
    Create TABLE employees(
    employee_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hourly_pay Decimal(5,2),
    hire_date Date,
    );

    2.2 Chọn sử dụng Table:
    Cú pháp:
    Select _ from ten_table;
    Ví dụ:
    Select _ from employees;

    2.3 Thay đổi tên của Table:
    Cú pháp:
    Rename Table tên_hiện_tại_của_Table to tên_mới_của_Table;
    Ví dụ
    Rename Table employees to workers;

chúng ta cũng có thể đổi ngược lại

Rename Table workers to employees;

2.4 Loại bỏ, xóa Table:
Cú pháp:
Drop TABLE ten_Table;
Ví dụ:
Drop TABLE employees;

2.5 Alter Table: Thay đổi, thêm trường dữ liệu mới mà bảng đó đã tồn tại thì dùng Alter để chỉnh sửa...
2.5.1 Bổ sung trường dữ liệu (trường chưa tồn tại trong table)
Cú pháp:
Alter TABLE ten_Table
Add ten_trường_muốn_thêm kiểu_dữ_liệu;
Ví dụ:
Alter TABLE employees
Add phone_number VARCHAR(15);

2.5.2 Thay đổi cái trường dữ liệu (trường này đã tồn tại trong table)
Cú pháp:
Alter TABLE ten*Table
Rename Column tên_trường_muốn*đổi to tên_mới;

Ví dụ: (Đây là muốn đổi trường phone_number thành email)
Alter TABLE employees
Rename Column phone_number TO email;

2.5.3 Thay đổi kiểu dữ liệu cho cái column (cột).
Vấn đề: phone_number chuyển thành email cái kiểu dữ liệu của column không còn khớp
Giải quyết:

Cú pháp:
Alter TABLE ten*Table
Modify Column ten_column kiểu_dữ_liệu_thay*đổi;

Ví dụ:
Alter TABLE employees
Modify Column email Varchar(100);

2.5.4: Muốn thay đổi vị trí đứng của 1 column
Vấn đề: cột email mới thêm muốn nó đứng sau cột last_name thì làm sao?
Giải quyết:

Cú pháp:
Alter TABLE ten*Table
Modify tên_column kiểu_dữ_liệu;
After tên_column_muốn*đứng_sau;

// có thể thay thế After thành Before nếu như muốn đứng trước cột đó

Ví dụ:
Alter TABLE employees
Modify email Varchar(100);
After last_name;

Ngoài ra muốn đôn nó lên đứng đầu luôn
Alter TABLE ten_Table
Modify tên_column kiểu_dữ_liệu;
First;

2.6 Muốn xóa một cột trong Table thì làm sao?

Cú pháp:
Alter TABLE ten_Table
Drop column tên_cột_muốn_xóa;
Ví dụ:
Alter TABLE employees
Drop column email;

3.INSERT ROWS
3.1 Thêm dữ liệu cho trường

Cú pháp:
Insert into tên_table
Values (
điền các giá trị tương ứng với các cột, trùng kiểu dữ liệu.
);
Ví dụ:
Insert into employees
Values (
1,
"Eugene",
"Krabs",
25.50,
"2023-01-02"
);

3.2 Thêm 1 lúc nhiều trường dữ liệu
Cú pháp:
Insert into tên_table
Values
(
điền các giá trị tương ứng với các cột, trùng kiểu dữ liệu.
),
(
điền các giá trị tương ứng với các cột, trùng kiểu dữ liệu.
)
,... nếu muốn nhiều hơn nữa cách nhau bởi dấu "," và bọc dữ liệu thêm vào trong ngoặc tròn
;

Ví dụ:
Insert into employees
Values
(
2,
"Squidward",
"Tentacles",
15.00,
"2023-01-03"
),
(
3,
"Spongebob",
"Squarepants",
12.50,
"2023-01-04"
),
(
4,
"Patrick",
"Star",
12.50,
"2023-01-05"
),
(
5,
"Sandy",
"Cheeks",
17.25,
"2023-01-06"
)
;

// Nếu mà cố tình điền không đủ thông tin trường yêu cầu thì nó sẽ báo lỗi.
Ví dụ:
//Lỗi
(
6,
"Sheldon",
"Cheeks"
)

Nhưng vẫn có cách cho việc thêm thiếu dữ liệu

// Vẫn chấp nhận được vì đã bổ sung (employee_id, first_name, last_name), điều này thông báo rằng các các trường bị thiếu có thể được đặt là null, còn các trường xuất hiện trong dấu ngoặc bắt buộc phải có.

Insert into employees (employee_id, first_name, last_name)
Values
(
6,
"Sheldon",
"Cheeks"
);

4.SELECT

4.1 Để đọc hết toàn bộ dữ liệu trong 1 bảng
Cú pháp:
Select _ from tên_table
Ví dụ:
Select _ from employees

4.2 Để mà lấy ra các thông tin cụ thể hơn:

Cú pháp:
Select tên_trường, tên_trường,...
From tên_table

Ví dụ
Select first_name, last_name
From employees

4.3 Tìm kiếm chính xác 1 đối tượng nào đó

Cú pháp:
Select \*
From tên_table
Where tên_trường = giá_trị_của_trường;

Ví dụ:
Select \*
From employees
Where employee_id = 1;

=> Tìm ra employee có id là 1

Select \*
From employees
Where first_name = "Spongebob";

=> Tìm ra employee có first_name là Spongebob

Select \*
From employees
Where hourly_pay >= 15;

=> Tìm ra employee có hourly_pay là lớn hơn hoặc bằng 15.

Select \*
From employees
where hire_date <= "2023-01-03"

=> Tìm ra employee có hire_date nhỏ hơn hoặc bằng 2023-01-03

Select \*
From employees
Where employee_id != 1;

=> tìm ra tất cả employee nhưng ngoại trừ thằng nào có employee_id = 1

// Đối với các trường có giá trị là null thì không dùng = thay vào đó là is

Select \*
From employees
where hire_date is null;

Ngược lại không in ra các trường có chứa giá trị null

Select \*
From employees
Where hire_date is not null;

5.UPDATE & DELETE

5.1 Cập nhật và xóa dữ liệu 1 bảng

Bạn có để ý chúng ta có employee_id số 6 có null ở cột hourly_pay và hire_date, và giờ sẽ thực hành với nó

Cú pháp:

Update tên*bảng
Set tên_column = giá_trị_mới
where Điều_kiện*để*tìm_thấy_cột*đó

Ví dụ:

Update employees
SET hourly_pay = 10.25
Where employee_id = 6

5.2 Có thể cập nhật một lúc nhiều trường

Update employees
SET hourly_pay = 10.25,
hire_date = "2023-01-07"
Where employee_id = 6

5.3 Đặc biệt nếu thiếu where chuyện gì sẽ xảy ra
SET hourly_pay = 10.25,
hire_date = "2023-01-07"

=> Các nhân viên khác có cột này đều bị xét chung 1 giá trị này, thí dụ có 6 thì cả 6 người ở các vị trí cột lần lượt là hourly_pay = 10.25 và hire_date = "2023-01-07"

Đừng bao giờ quên where khi mà cập nhật và xóa nha!!!

Muốn set Null cho 1 trường

Update employees
SET hire_date = null
Where employee_id = 6

5.4 Delete 1 dữ liệu có trong bảng

Delete from employees
where employee_id = 6;

Nếu thiếu where thì sẽ xóa hết tất cả dữ liệu. Nên cẩn thận

6.AUTOCOMMIT, COMMIT, ROLLBACK

AUTOCOMMIT: là chế độ mặc định của MySQL, khi được bật, nó sẽ tự động xác nhận mỗi giao dịch sau khi hoàn thành. Điều này có nghĩa là các thay đổi đối với dữ liệu sẽ được lưu trữ ngay lập tức, ngay cả khi bạn chưa hoàn thành toàn bộ giao dịch.

COMMIT: được sử dụng để xác nhận các thay đổi đối với dữ liệu và lưu trữ chúng vào cơ sở dữ liệu.

ROLLBACK: được sử dụng để hủy bỏ các thay đổi đối với dữ liệu và đưa cơ sở dữ liệu về trạng thái trước khi giao dịch bắt đầu.

Ví dụ:
Tôi sử dụng Delete mà không dùng where

Delete from employees

SET AUTOCOMMIT = OFF
Giúp các truy vấn không tự động lưu

Sau khi tắt thì phải tự lưu thủ công từng giao dịch,

COMMIT (tạo 1 điểm lưu)

Vô tình xóa không dùng where dẫn đến xóa hết
Delete from employees

Dùng Rollback để quay lại được lúc chưa xóa

7.CURRENT_DATE() & CURRENT_TIME()

Tạo 1 table mẫu

Create Table test (
my_date DATE,
my_time TIME,
my_date_time DATETIME
)

//kiểm tra bảng có tồn tại hay chưa
Select \* from test;

// Thêm dữ liệu vào

Insert into test
Values(CurrentDate(),CurrentTime(), Now());

Select \* from test;

Giải thích:
Những hàm sau đây đều được viết sẵn, chỉ việc sử dụng
CurrentDate: Lấy ra năm tháng ngày hiện tại
CurrentTime: Lấy ra giờ phút giây hiện tại
Now: Lấy ra năm tháng ngày giờ phút giây

// Ngoài ra thực hiện + - cho Date

Bớt đi 1 ngày
Insert into test
Values(CurrentDate() - 1, Null, Null);

Tăng thêm 1 ngày
Insert into test
Values(CurrentDate() + 1, Null, Null);

// Demo xong xóa
Drop table Test

8.UNIQUE: Duy nhất

constraints: những ràng buộc, hạn chế.

Unique constraint: Ràng buộc duy nhất xác định một cột hoặc một nhóm cột trong một bảng mà các giá trị của nó phải là duy nhất.

Create Table products (
product_id Int Unique,
product_name Varchar(50) Unique,
price Decimal(4,2)
)

//Giả sử như bạn tạo table mà bạn quên unique thì bạn vẫn có thể bổ sung thông qua Alter

ALTER TABLE products
Add constraint
Unique (product_id, product_name);

// Thêm dữ liệu thành công
Insert into products
Values
(100, "Hamburger", 3.99),
(101, "fires", 1.98),
(102, "soda", 1.00),
(103, "ice cream", 1.49);

// Thêm dữ liệu thất bại
Insert into products
Values
(100, "Hamburger", 3.99),
(101, "fires", 1.98),
(102, "soda", 1.00),
(101, "fires", 1.98), <== Điểm sai, trùng lập product_id, product_name
(101, "Bakery", 1.98), <== Điểm sai, trùng lập id
(104, "fires", 1.98), <== Điểm sai, trùng lập product_name
(103, "ice cream", 1.49);

Lý do thêm thất bại: Dữ liệu thêm vào bị trùng product_id và product_name, 2 trường này phải là unique không được phép thêm vào các thông tin đã tồn tại.

9.NOT NULL: Không được để trống

Not null constraint: Ràng buộc không null xác định rằng một cột không được phép chứa giá trị NULL.

TH1: cập nhât not null cho price
// giả sử chưa có table products thì ta sẽ dùng này

Create table products(
product_id int,
product_name varchar(25),
price decimal(4,2) Not null
)

TH2: cập nhât not null cho price
// Đã có table products thì dùng Alter để cập nhật

Alter table products
Modify price Decimal(4,2) Not null;

// Sau khi tạo xong các quy định và ràng buộc thì tiếp theo thêm dữ liệu
Insert into products
Values (104, "cookie", null);

==> báo lỗi vì price vi phàm ràng buộc, cụ thể là null

Sửa lại
Insert into products
Values (104, "cookie", 0);

10.CHECK

Check constraint: Ràng buộc kiểm tra xác định một điều kiện mà các giá trị của một cột hoặc một nhóm cột phải đáp ứng.

Ví dụ: Tôi sống hoa kỳ, tùy thuộc vào mỗi bang mà bạn sống sẽ có mức lương theo giờ tối thiểu mà người lao động sẽ được trả
Hãy đặt mức lương theo trả theo giờ bằng mức lương tôi thiểu ở khu vực đó.
Gợi ý: sử dụng constraint check để ràng buộc kiểm tra

Th1: Table chưa có
Create TABLE employees(
employee_id INT,
first_name VARCHAR(50),
last_name VARCHAR(50),
hourly_pay Decimal(5,2),
hire_date Date,

                // Kiểm tra cột lương theo giờ
        constraint chk_Check (hourly_pay >= 10)
    );

Th2: Table này đã tồn tại dùng alter để cập nhật
Alter table employees
Add constraint chk_hourly_pay Check (hourly_pay >= 10)

Insert into employees
Values (6, "Sheldon", "Plankton", 5.00, "2023-01-07")

// Sẽ bị vi phạm cái check vì hourly_pay >= 10 dữ liệu đưa vào chỉ 5.00 cho nên báo lỗi

// Không muốn sử dụng check nữa thì làm sao?

Loại bỏ nó

Alter table employees
Drop check chk_hourly_pay;

// như vậy đã tháo được constraint checking

11.DEFAULT

// Bình thường nếu lúc ban đầu khai báo table mà không có mặc định (default) cho price là 0 thì bắt buộc khi insert phải thêm 0 cho trường dữ liệu đó.

Select \* from products;

Insert into products
Values (104, "straw", 0.00 ),
(105, "napkin", 0.00 ),
(106, "fork", 0.00),
(107, "spoon", 0.00);

Chúng ta có thể khai báo default trong lúc tạo bảng

Có 2 cách:

Cách 1: lúc tạo table thì thêm vào

Create table products (
product_id int,
product_name varchar(25),
price decimal(4,2) default 0
)

Cách 2: dùng alter để cập nhật

Alter table products
Alter price set Default 0

Câu lệnh ALTER TABLE products ALTER price SET DEFAULT 0 sẽ thay đổi giá trị mặc định của cột price trong bảng products thành 0. Điều này có nghĩa là nếu bạn thêm một hàng mới vào bảng products mà không chỉ định giá trị cho cột price, thì giá trị 0 sẽ được sử dụng.

Câu lệnh này có thể hữu ích nếu bạn muốn đảm bảo rằng tất cả các hàng trong bảng products đều có giá trị cho cột price.

Sau khi set default có thể tự bỏ trống trường price

Insert into products
Values (104, "straw" ),
(105, "napkin", 3.50), // nếu có giá trị thì sẽ lấy giá trị không lấy default value
(106, "fork"),
(107, "spoon");

Mặc định cột price sẽ tự thêm 0.00 vào nếu không được truyền dữ liệu

tương tự cho trường hợp này

Insert into products(product_id, product_name)
Values (104, "straw" ),
(105, "napkin"),
(106, "fork"),
(107, "spoon");

vì price set mặc định rồi không truyền nó vẫn ghi 0.00

Một ví dụ khác Default

Create table transactions(
transaction_id int,
amount decimal(5,2),
transaction_date DateTime Default Now()
)

// mặc dù có 3 trường nhưng vì transaction_date đã được set default value nên là không cần nhập vẫn cho
Insert into transactions (transaction_id, amount)
Values (1, 4.99),
(2, 5.99),
(3, 9.99);

// xóa
Drop table transactions

12.PRIMARY KEYS

Một primary key là một ràng buộc được áp dụng cho một cột hoặc một nhóm cột trong một bảng.
Nó xác định một cột hoặc một nhóm cột duy nhất trong một bảng.
Mỗi hàng trong bảng phải có giá trị duy nhất cho khóa chính.

Ràng buộc khóa chính là một ràng buộc quan trọng để đảm bảo tính toàn vẹn dữ liệu của cơ sở dữ liệu.
Nó giúp ngăn chặn các lỗi dữ liệu như nhập hai hàng có cùng giá trị cho khóa chính.

Create table transactions(
transaction_id int primary key,
amount decimal(5,2),
);

Nếu như bảng này đã tồn tại nhưng chưa có primary key thì sử dụng alter để cập nhật

Alter table translations
Add Constraint
Primary key(translation_id);

Nếu set thêm primary key cho amount sẽ báo lỗi

Nên nhớ mỗi một table chỉ nên có 1 primary key thui

Một bảng chỉ nên có một primary key.
Tuy nhiên, primary key có thể là một cột hoặc một nhóm cột.
Nếu primary key là một nhóm cột, thì các cột trong nhóm phải là duy nhất và không thể có giá trị null.

Ví dụ, nếu bạn có một bảng students, bạn có thể đặt cả cột id và cột name làm primary key.
Điều này có nghĩa là mỗi hàng trong bảng students phải có một giá trị duy nhất cho cả cột id và cột name.

Việc sử dụng một nhóm cột làm primary key có thể hữu ích nếu bạn muốn đảm bảo rằng dữ liệu của bạn là duy nhất và nhất quán.
Ví dụ, nếu bạn có một bảng products, bạn có thể đặt cả cột product_id và cột product_name làm primary key.
Điều này có nghĩa là mỗi sản phẩm trong bảng products phải có một ID và tên sản phẩm duy nhất.

Tuy nhiên, bạn cũng cần lưu ý rằng việc sử dụng một nhóm cột làm primary key có thể làm chậm quá trình truy vấn dữ liệu.
Vì vậy, bạn chỉ nên sử dụng một nhóm cột làm primary key nếu thực sự cần thiết.

Insert into translations
Values (1001, 4.99), // ok
(1002, 5.99), // ok
(1002, 6.99), // sai vì primary key không được trùng nhau
(null, 6.99), // sai vì primary key không được phép null
(1003, 7.99); // ok

// Dựa vào id có thể tìm kiếm ra các giá trị ở amount
Select amount
from transactions
where transaction_id = 1003;

select \* from transactions

Drop table transactions

13.AUTO_INCREMENT (tự động tăng)

Create table transactions (
translation_id int primary key auto_increment,
amount decimal(5,2),
);

Select \* from transactions;

// Lý do không điền nội dung id là vì có id là primary key, và set mặc định tự động tăng
Insert into transactions (amount)
Values (4.99),
(5.99),
(3.50);

Nếu mà muốn bắt đầu ở một số nào không phải số 0 thì sử dụng lệnh Alter dể cập nhật lại Auto_increment
Hoặc nếu chưa có thì cũng dùng lệnh alter để set lại auto_increment

Alter table transactions
Auto_increment = 1000;

14.FOREIGN KEYS

Foreign key là một cột hoặc một nhóm cột trong một bảng mà các giá trị của nó phải khớp với các giá trị của primary key trong một bảng khác.
Foreign key được sử dụng để duy trì tính toàn vẹn của dữ liệu trong cơ sở dữ liệu.

Hiểu đơn giản nó là khóa chính của table này, nhưng là khóa ngoại của table khác.
Nó là cầu nối giữa hai bảng

Lợi ích của việc tạo khóa ngoại, ngăn việc phá hủy 1 trong 2 table đang được kết nối.
Ngoài ra nó còn thể dùng để Join table.

ví dụ: Tạo ra 1 table mới customers

Create table Customers (
customer_id int primary key auto_increment,
first_name varchar(50),
last_name varchar(50),
)

// Chúng ta có customer_id là khóa chính tự động tăng

Select \* from customers

// Nhập thông tin khách hàng vào

Insert into customers (first_name, last_name)
values ("Fred", "Fish"),
("Larry", "Lobster"),
("Buble", "Bass");

// Muốn nối FK thì tạm thời xóa
Drop table transactions;

//Tạo lại table transactions

Create table transactions(
transaction_id int primary key auto_increment,
amount decimal(5,2),

    customer_id int,
    Foreign Key(customer_id) References customers(customer_id)

);

// FK customer_id nối với table customers thông qua customer_id

select \* from transactions;

// Muốn bỏ khóa ngoại thì dùng Alter để cập nhập lại bảng transactions

Alter Table transactions
Drop Foreign key transactions_ibfk_1;

// Bạn có thể đặt biệt danh riêng cho khóa ngoại

Alter Table transactions
Add Constraint fk_customer_id // không có cũng ổn, nhưng nên đặt tên phân biệt và tên này cũng nên là duy nhất
foreign key(customer_id) References customers(customer_id)

// chỉnh sửa lại 1 số dữ liệu transactions

ALTER TABLE transactions
Auto_increment = 1000;

Select \* from transactions;

Insert into transactions (amount, customer_id)
Values (4.99, 3),
(2.89, 2),
(3.38, 3),
(4.99, 1);

// Một khi dữ liệu đã được nối bằng khóa ngoại sẽ không thể xóa được, trừ khi cập nhật lại table bỏ khóa ngoại đi lúc đó mới bắt đầu xóa được dữ liệu.

15.JOINS

joins là một mệnh đề được sử dụng để kết hợp các hàng từ hai hoặc nhiều bảng (table) dựa trên một cột có liên quan giữa chúng,
chẳng hạn như khóa ngoại

Đây là 1 ví dụ:
Có 2 bảng translations và customers, có phần giao nhau và phần giao nhau là điểm chung của 2 tables

Bổ sung thêm dữ liệu vào translations và customers

Insert into transactions (amount, customer_id)
Values (1.00, Null);
// Cố tình để FK là null

tưởng tượng 1 khách hàng vào thanh toán bằng tiền mặt, họ là khách vãng lai nên sẽ không có id buộc phải để null

Insert into customers (first_name, last_name)
Values ("Poppy", "Puff"),

// khác hàng này mới tạo, và họ cũng chưa bao giờ mua hàng. customer_id của này chưa kết fk bên table transactions

Bây giờ xem dữ liệu chung giữa hai tables

Để xem được ghép 2 table này lại với nhau bằng join

Inner joins

Select \*
From translations inner join customers
on translations.customer_id = customers.customer_id

Và cái này được gọi inner join

Inner join chỉ lấy ra các phần chung của 2 tables, Các phần chưa được kết nôi hay null thì sẽ không được lấy ra

Ngoài ra chúng ta có thể quy định các thông tin nào sẽ được lấy ra

Select translation_id, amount, first_name, last_name
From translations inner join customers
on translations.customer_id = customers.customer_id

Left joins
ví dụ: transactions và customers (Quy định transactions nằm trái, customers nằm phải)

Left join hiển thị mọi thứ bảng bên trái, ở đây là toàn bộ thông tin của translations
Tuy nhiên đối với table được đem join vào là customers nếu có customer_id phù hợp trùng nhau. Sẽ lấy các dữ liệu khớp hiên thị lên, đối với các trường hợp không có customer_id từ table customer khớp với table transactions vẫn sẽ hiển thị lên nhưng sẽ là để giá trị là null

Select \*
From translations left join customers
on translations.customer_id = customers.customer_id

Right joins
ví dụ: transactions và customers (Quy định transactions nằm trái, customers nằm phải)

Select \*
From translations right join customers
on translations.customer_id = customers.customer_id

// Hiển thị toàn bộ bảng phía bên phải, nếu có kết quả phù hợp nào, chúng tôi sẽ kéo vào bất kỳ hàng phù hợp nào từ bên trái,
chúng tôi sẽ hiển thị tất cả các khách hàng, với các khách hàng mới tạo hoặc chưa mua gì vẫn được hiển thị. Nhưng các khách hàng này ở table translations chưa có thông tin gì nên sẽ để là null hết

16.FUNCTIONS

Hàm trong MySQL là một đoạn mã có thể được sử dụng để thực hiện một nhiệm vụ cụ thể.
Các hàm có thể được sử dụng để thao tác dữ liệu, tính toán các giá trị hoặc thực hiện các hành động khác.

Có hai loại hàm trong MySQL:

Hàm hệ thống: Các hàm hệ thống là các hàm được cung cấp bởi MySQL
và có thể được sử dụng mà không cần phải định nghĩa chúng.
Một số hàm hệ thống phổ biến bao gồm COUNT(), SUM() và AVG().

Hàm định nghĩa người dùng: Các hàm định nghĩa người dùng là các hàm được tạo bởi người dùng
và có thể được sử dụng trong các truy vấn SQL.
Các hàm định nghĩa người dùng có thể được sử dụng để thực hiện bất kỳ nhiệm vụ nào
có thể được thực hiện bởi các hàm hệ thống, cũng như các nhiệm vụ khác mà các hàm hệ thống không thể thực hiện.

CREATE FUNCTION function_name ([parameter_1 [, parameter_n]])
RETURNS data_type
BEGIN
-- body of the function
END;

function_name là tên của hàm. parameter_1, parameter_2, v.v. là các tham số của hàm.
data_type là kiểu dữ liệu của giá trị trả về của hàm.
body of the function là phần thân của hàm, chứa các lệnh thực hiện nhiệm vụ của hàm.

Sau khi tạo một hàm, bạn có thể sử dụng nó trong các truy vấn SQL bằng cách sử dụng cú pháp sau:

SELECT function_name ([parameter_1 [, parameter_n]]) FROM table_name;

Ví dụ, sau đây là một hàm định nghĩa người dùng trả về tổng của hai số:

CREATE FUNCTION sum_two_numbers (a INT, b INT)
RETURNS INT
BEGIN
RETURN a + b;
END;

Bạn có thể sử dụng hàm này trong một truy vấn SQL như sau:

SELECT sum_two_numbers (10, 20) FROM table_name;

Truy vấn này sẽ trả về giá trị 30.

Quay lại bài chính

Muốn đếm xem có bao nhiêu giao dịch diễn ra trong 1 ngày nhất định.
Để làm điều đó, chúng ta có thể sử dụng hàm đếm. Count()
Công dụng của count là đếm số lượng truy vấn count(truyền*vào*đây_cột_cần đếm)
Tôi có thể đặt một cột rồi đếm xem có bao nhiêu hàng trong cột đó

trong ví dụ này sẽ đếm amount của transactions, cụ thể là có bao nhiêu hàng trong cột amount

// Cái này là đếm được rồi
Select Count(amount)
from transactions

// Này đếm cụ thể vào ngày
Select Count(amount)
from transactions
where transactions_date = "2023-01-01"

Cụ thể đếm cột amount từ bảng transactions vào ngày 2023-01-01

Tips: muốn đặt lại tên tạm thời cho cột cũng có thể sử dụng cột alias
// count(amount) sẽ được đặt lại tên cột là Today's transaction
Select count(amount) as "Today's transaction"
From transactions;

Tìm ra giá trị tối đa của cột amount bằng cách sử dụng hàm MAX
trong dấu ngoặc đơn truyền amount vào giống như vầy MAX(amount)

Select Max(amount) as maximum
From transactions;

ngược lại tìm giá trị nhỏ nhất MIN() trong cột amount

Select MIN(amount) as minimum
From transactions;

Tính trung bình là AVG cột amount

Select AVG(amount) as average
From transactions;

Tính tổng của cột amount bằng hàm SUM

Select SUM(amount) as sum
From transactions;

Sang Table employees bây giờ table không có cột full_name.
Muốn tạo ra cột full_name bằng các kết hợp cột first_name và last_name
Kết hợp bằng cách sử dụng hàm CONCAT()

Select CONCAT(first_name, last_name) AS full_name
from employees;

// Nếu như kết hợp như vậy first_name, last_name sẽ dính lại nên phải
thêm khoảng trắng như sau

Select CONCAT(first_name," ",last_name) AS full_name
from employees;

17.AND, OR, NOT, BETWEEN, IN

// Còn nhiều nữa mà tự nghiên cứu thêm

// Toán tử logic

Thêm cột job và nó đứng sau cột hourly_pay;

Alter table employees
Add Column job varchar(25) after hourly_pay;

// Cập nhật job cụ thể cho nhân viên

Update employees
Set job = "manager"
Where employee_id = 1;

Update employees
Set job = "cashier"
Where employee_id = 2;

Update employees
Set job = "cook"
Where employee_id = 3;

Update employees
Set job = "cook"
Where employee_id = 4;

Update employees
Set job = "asst. manager"
Where employee_id = 5;

Update employees
Set job = "asst. janitor"
Where employee_id = 6;

// Tìm nhân viên có số ngày làm việc bắt đầu trước ngày 2023-01-05
// Những người này đã làm lâu
Select \*
From employees
Where hire_date < "2023-01-05"

// Bây giờ tìm ra những người cook làm trước ngày 2023-01-05

// Nó sẽ tìm ra người thỏa mãn cả hai tiêu chí này cùng lúc
Select \*
From employees
Where hire_date < "2023-01-05" and job = "cook";

// Tìm ra các người có công việc là cook

Select \*
From employees
Where job = "cook";

// Tìm ra những người công việc là cook và cashier

Select \*
From employees
Where job = "cook" or job = "cashier";

// tìm ra các nhân viên có công việc không phải là manager
Select \*
From employees
Where not job = "manager"

// tìm ra các nhân viên có công việc không phải là manager và không phải là asst. manager

Select \*
From employees
Where Not job = "manager" and Not job = "asst. manager"

Tìm ra các nhân viên có ngày vào làm từ khoảng A đến khoảng B

Select \*
From employees
Where hire_date Between "2023-01-04" AND "2023-01-07";

Tìm ra các nhân viên có công việc cook, cashier, janitor

Select \*
From employees
Where job in ("cook","cashier","janitor");

18.WILD CARDS

wild card character % _
ký tự đại diện % _

used to subtitle one or more characters in a string
được sử dụng để đặt phụ đề cho một hoặc nhiều ký tự trong một chuỗi

//Tìm các first_name bắt đầu chữ S

Select \*
From employees
Where first_name Like "S%";

S% bắt đầu sau chữ S là các ký tự khác nhau và trước S không có ký tự nào.

%S bắt đầu sau chữ S phải không có ký tự nào và trước S là các ký tự thoải mái.

Có thể ứng dụng vào date, cụ thể hire_date

Select \* from employees
Where hire_date Like "2023%"

sau 2023% là bất kỳ ký tự nào ví dụ
2023-01-04 hợp lệ

01-04-2023 không hợp lệ

// Tìm các last_name có đuôi là r
Select \* from employees
Where last_name Like "%r";

// Tìm các first_name có đầu là sp

Select \* from employees
WHere first_name Like "sp%"

Đối với underscore \_

// Điền từ còn thiếu vào \_, bất kỳ từ nào
Select \* from employees
WHere first_name Like "\_ook"

// có thể dùng _ 2 _ hoặc nhiều hơn
Select \* from employees
WHere first*name Like "\_ook*"

// có thể dùng cho year month date

Select \* from employees
Where hire_date like "\_**\_-01-**"

Select \* from employees
Where hire_date like "\_**\_-**-02"

// các job có ký tự bắt đầu là ngẫu nhiên từ tiếp theo phải là a và thoải mái các ký tự về sau.

Select \* from employees
Where job like "\_a%"

19.ORDER BY
// Sắp xếp kết quả truy vấn theo thứ tự tăng dần hoặc giảm dần, dựa trên những cột mà chúng tôi liệt kê đây là một ví dụ
// Tôi có một danh sách sinh viên như này, yêu cầu liệt kê các nhân viên theo thứ tự bảng chữ cái dựa trên cột last_name

// Nó sẽ sắp xếp theo thứ tự tăng dần của bảng chữ cái a -> z (Mặc định ASC, nhưng vì là mặc định không cần điền)
Select \* from employees
Order by last_name;

// Muốn nó sắp xếp theo kiểu z -> a thêm từ khóa ở cuối trường OrderBy
Select \* from employees
Order by last_name DESC;

Lưu ý mỗi cột đó bị ảnh hưởng thui nha

Qua table Transactions test thử

// Thử cột Amount
Select \* from transactions
Order by amount ASC, customer_id DESC;

Nó sẽ ưu tiên xếp theo thứ tựn tăng dần của amount, sau đó xếp giảm dần của customer_id

20.LIMIT

Limit clause is used to limit the number of records.
Useful if you're working with a lot of data.
Can be used to display a large data on pages (pagination).

Cụm từ LIMIT được sử dụng để giới hạn số lượng bản ghi.
Nó rất hữu ích nếu bạn đang làm việc với nhiều dữ liệu.
Có thể được sử dụng để hiển thị dữ liệu lớn trên các trang (phân trang).

// Giới hạn 1 bản ghi
Select \* from customers
Limit 1;

Hoặc

// Giới hạn 1 bản ghi
Select \* from customers
Limit 5;

Select \* from customers
Order By last_name Limit 1;

Chọn ra tất cả các customers, và Sắp xếp theo a -> z, và lấy ra 1 bản ghi.

Select \* from customers
Order By last_name DESC Limit 1;

Chọn ra tất cả các customers, và Sắp xếp theo z -> a, và lấy ra 1 bản ghi.

Select \* from customers
Limit 1, 1;

số đầu tiên là số lượng bản ghi bỏ qua. số thứ 2 là lượng bản ghi lấy ra.

Câu lệnh SQL SELECT \* FROM customers LIMIT 1, 1; sẽ trả về hàng đầu tiên trong bảng customers.
Cụm từ LIMIT được sử dụng để giới hạn số lượng hàng được trả về.
Trong trường hợp này, 1 trước , là số lượng hàng bị bỏ qua, và 1 sau , là số lượng hàng được trả về.
Vì vậy, câu lệnh SQL này sẽ bỏ qua 0 hàng đầu tiên trong bảng customers và trả về hàng đầu tiên.

Select \* from customers
Limit 10, 10;

// Bỏ qua 10 người, sau đó là lấy ra 10 người tiếp theo

Select \* from customers
Limit 50, 10;
// Bỏ qua 50 người, sau đó là lấy ra 10 người tiếp theo

21.UNIONS

// Union combines the results of two or more Select statements
// Union kết hợp kết quả của hai hoặc nhiều câu lệnh Select

Select first_name, last_name from employees
Union
Select first_name, last_name from customers;

// trường hợp trung cả first_name và last_name thì nó sẽ gộp lại
Có cách thêm all vào

Select first_name, last_name from employees
Union ALL
Select first_name, last_name from customers;

==

SELECT _ FROM income UNION SELECT _ FROM expenses;
sẽ trả về tất cả các hàng từ bảng income và bảng expenses.
Cụm từ UNION được sử dụng để hợp nhất hai tập hợp dữ liệu.
Trong trường hợp này, hai tập hợp dữ liệu là tất cả các hàng trong bảng income và tất cả các hàng trong bảng expenses.

Câu lệnh SQL này sẽ trả về tất cả các hàng từ hai bảng, kể cả các hàng trùng lặp.
Nếu bạn muốn loại bỏ các hàng trùng lặp, bạn có thể sử dụng cụm từ DISTINCT.

Ví dụ, nếu bảng income chứa các hàng sau:

| id  | amount |
| --- | ------ |
| 1   | 100    |
| 2   | 200    |
| 3   | 300    |

và bảng expenses chứa các hàng sau:

| id  | amount |
| --- | ------ |
| 4   | 400    |
| 5   | 500    |
| 6   | 600    |

thì câu lệnh SQL SELECT _ FROM income UNION SELECT _ FROM expenses; sẽ trả về các hàng sau:

| id  | amount |
| --- | ------ |
| 1   | 100    |
| 2   | 200    |
| 3   | 300    |
| 4   | 400    |
| 5   | 500    |
| 6   | 600    |

UNION ALL cũng được sử dụng để hợp nhất hai tập hợp dữ liệu. Tuy nhiên, UNION ALL sẽ trả về tất cả các hàng từ hai tập hợp dữ liệu, bao gồm cả các hàng trùng lặp. Trong khi đó, UNION sẽ chỉ trả về các hàng duy nhất từ hai tập hợp dữ liệu.

SELECT _ FROM income
UNION ALL
SELECT _ FROM expenses;

Ví dụ, nếu bảng income chứa các hàng sau:

| id  | amount |
| --- | ------ |
| 1   | 100    |
| 2   | 200    |
| 3   | 300    |
| 4   | 400    |

và bảng expenses chứa các hàng sau:

| id  | amount |
| --- | ------ |
| 4   | 400    |
| 5   | 500    |
| 6   | 600    |

thì câu lệnh SQL SELECT _ FROM income UNION ALL SELECT _ FROM expenses; sẽ trả về các hàng sau:

| id  | amount |
| --- | ------ |
| 1   | 100    |
| 2   | 200    |
| 3   | 300    |
| 4   | 400    |
| 4   | 400    |
| 5   | 500    |
| 6   | 600    |

22.SELF JOINS

join another copy of a table to itself
used to compare rows of the same table
helps to display a heirarchy of data

Ghép một bản sao khác của bảng vào chính nó
Được sử dụng để so sánh các hàng của cùng một bảng
Giúp hiển thị hệ thống phân cấp dữ liệu

Alter table customers
Add referral_id int;

Select \* from customers;

Update customers
set referral_id = 1
where customer_id = 2;

Update customers
set referral_id = 2
where customer_id = 3;

Update customers
set referral_id = 2
where customer_id = 4;

Select \*
from customers as a
Inner JOIN customers as b
on a.referral_id = b.customer_id

Hoặc không lấy thông tin ra hết thì giới hạn lại

Select a.customer_id, a.first_name, a.last_name,
b.first_name, b.last_name
From customers as a
Inner join customers as b
On a.referral_id = b.customer_id;

Kết hợp bảng b first_name và last_name thành reference_by

Select a.customer_id, a.first_name, a.last_name,
Concat(b.first_name, " ", b.last_name) as "reference_by"
From customers as a
Inner join customers as b
On a.referral_id = b.customer_id;

Có thể dùng left-Join.
Select a.customer_id, a.first_name, a.last_name,
Concat(b.first_name, " ", b.last_name) as "reference_by"
From customers as a
Left join customers as b
On a.referral_id = b.customer_id;

Ví dụ 2:

Select \* from employees;

Trong bảng employees
có Mr krabs là manager
Ms Sandy là asst manager
Thêm 1 cột supervisor_id
Nhân viên sẽ báo cáo lại Sandy và sandy báo cáo lại krabs

Alter table employees
Add supervisor_id

// tại vì cái cột supervisor_id mới được thêm vào chưa có dữ liệu nên bắt buộc phải cập nhật
Update employees
Set supervisor_id = 5 // bị quản lý bởi người trợ lý gián đốc
Where employee_id = 2;

// supervisor_id kho phải unique nên được quyền trùng

Update employees
Set supervisor_id = 5 // bị quản lý bởi người trợ lý gián đốc
Where employee_id = 3;

Update employees
Set supervisor_id = 5 // bị quản lý bởi người trợ lý gián đốc
Where employee_id = 4;

Update employees
Set supervisor_id = 5 // bị quản lý bởi người trợ lý gián đốc
Where employee_id = 6;

Update employees
Set supervisor_id = 1 // trợ lý gián đốc
Where employee_id = 5;

// Sau khi có dữ liệu xong, dùng inner Join để join lại 2 bảng để giải quyết

Select \*
from employees as a
Inner Join employee as b
On a.suppervisor_id = b.employee_id;

//
Select a.first_name, a.last_name,
Concat(b.first_name, " " ,b.last_name) As "reports to"
From employees as a
Inner Join employee as b
On a.suppervisor_id = b.employee_id;

// Kết quả in ra
first_name last_name reports to

Nếu bạn muốn hiện ra tất cả nhân viên của mình thậm chí cả giám đốc thậm chí họ không báo cáo bất kỳ ai
Bạn có thể sử dụng left join

Select a.first_name, a.last_name,
Concat(b.first_name, " " ,b.last_name) As "reports to"
From employees as a
Left Join employee as b
On a.suppervisor_id = b.employee_id;

// giám đốc sẽ không báo váo với ai nhưng vẫn sẽ hiển thị lên và để null

23.VIEWS

A virtual table based on the results-set of an SQL statement
The fields in a view are filleds from one or more real tables in the database
They are not real tables, but can be interacted with as if they were

Một bảng ảo dựa trên kết quả của một câu lệnh SQL
Các trường trong một view được lấy từ một hoặc nhiều bảng thực trong cơ sở dữ liệu
Chúng không phải là bảng thực, nhưng có thể được tương tác như thể chúng là

Views trong MySQL là một đối tượng cơ sở dữ liệu ảo chứa các dữ liệu được chọn từ một hoặc nhiều bảng cơ sở dữ liệu.
Views không phải là đối tượng cơ sở dữ liệu vật lý, nhưng chúng có thể được truy vấn và cập nhật như các bảng thực.

Views được sử dụng để tổ chức dữ liệu, tạo các báo cáo tùy chỉnh, và bảo vệ dữ liệu khỏi những người không có quyền truy cập.


Select * from employees;

Create view employee_attendance as
Select first_name, last_name
From employees;


Select * from employee_attendance
Order by last_name ASC;

// xóa bỏ view

Drop view employee_attendance;

Select * from customers;

Alter Table customers
Add column email varchar(50);

Update customers
Set email = "FFish@gmail.com";
where customer_id = 1;


Update customers
Set email = "LLobster@gmail.com";
where customer_id = 2;


Update customers
Set email = "BBass@gmail.com";
where customer_id = 3;


Update customers
Set email = "PPuff@gmail.com";
where customer_id = 4;


Create View customer_emails as 
Select email
from customers;


Select *
from customer_emails;


Select * from customers

Insert Into customers
Values (5, "Pearl", "Krabs", Null, "PKrabs@gmail.com")

Select * from customer_emails;



24.INDEXES

Index (Btree data structure)
Indexes are used to find values within a specific column more quickly
MySQL normally searches sequentially through a column
the longer the column, the more expensive the operation is
Update takes more time, Select takes less time

Index (cấu trúc dữ liệu Btree)
Index được sử dụng để tìm các giá trị trong một cột cụ thể nhanh hơn.
MySQL thường tìm kiếm tuần tự qua một cột.
Càng dài cột, thao tác càng tốn kém.
Cập nhật mất nhiều thời gian hơn, Chọn mất ít thời gian hơn.


Show INDEXES From customers;

Tạo
Create Index last_name_idx
On customers(last_name);

Kiểm tra tạo thành công hay chưa
Show indexes from customers


Tạo
Create Index last_name_first_name_idx
On customers(last_name, first_name);

Kiểm tra kết quả
Show indexes from customers

// xóa đi index đã tạo
Alter table customers
Drop Index last_name_idx;

Show indexes from customers;

Select * from customers
Where last_name = "Puff" And first_name = "Poppy"



25.SUBQUERIES

-- SubQuery: Truy vấn con
-- a query within another query: Một truy vấn bên trong một truy vấn khác.
-- query (subquery): truy vấn (subquery: truy vấn con)

Có nghĩa 1 câu truy vấn được nằm trong 1 câu truy vấn 


Bài toán:

Ông giám đốc krabs, ông ấy cần chúng tôi so sánh tiền lương theo giờ của mỗi nhân viên với tiền lương trung bình theo giờ của 
bảng nhân viên của chúng tôi, có thể ông krabs sẽ giảm lương cho mọi người chứ không phải tăng lương nhưng ông ấy cần so sánh
tiền lương theo giờ của mọi nhân viên với mức trung bình.

Hướng giải quyết:
Cần ít nhất 2 câu truy vấn.
Truy vấn thứ 1:
Tìm mức lương trung bình theo giờ và sau đó hiển thị tên và họ của mỗi nhân viên, 
Truy vấn thứ 2:
sau đó hiện mức lương trung bình.

// Bắt đầu với câu truy vấn số 2:
Select AVG(hourly_pay) from employees; 

// Chúng ta có thể đem truy vấn này đặt bên trong 1 truy vấn khác

Select first_name, last_name, hourly_pay, (Select AVG(hourly_pay) from employees) as avg_pay
From employees;

first_name      last_name       hourly_pay     avg_pay
Eugene          Krabs           25.50         15.458333
Squidward       Tentacles       15.00         15.458333
Spongebob       Squarepants     12.50         15.458333
Patrick         Star            12.50         15.458333
Sandy           Cheeks          17.25         15.458333
Sheldon         Plankton        10.00         15.458333


//Tìm ra người có mức lương cao hơn so với mức lương trung bình
Select first_name, last_name, hourly_pay, 
From employees
Where hourly_pay > (Select AVG(hourly_pay) from employees);


Bài 2: Làm việc với 2 table customers và transactions

Tìm ra các khách hàng đã từng mua hàng và tìm ra các khách hàng chưa từng mua hàng

Select * from transactions;

// lấy ra customer_id của table transactions với điều kiện customer_id không được null
// Nó cũng sẽ lấy ra luôn các customer_id bị trùng. ở table transactions
Select customer_id from transactions where customer_id is not null 

// Gộp các id này lại
Select Distinct customer_id from transactions where customer_id is not null;

// Lấy ra các khác hàng đã đặt hàng trước đây

SELECT first_name, last_name 
FROM customers
WHERE customer_id in
(
    SELECT DISTINCT customer_id 
    FROM transactions 
    WHERE customer_id IS NOT NULL;
)

// Lấy ra các khác hàng chưa bao giờ đặt hàng trước đây

SELECT first_name, last_name 
FROM customers
WHERE customer_id NOT IN
(
    SELECT DISTINCT customer_id 
    FROM transactions 
    WHERE customer_id IS NOT NULL;
)

// Chúng ta có thể giảm giá cho những khách hàng chưa mua để thuyết phục họ mua hàng




Tổng hợp lại

SELECT first_name, last_name, hourly_pay, 
       (SELECT AVG(hourly_pay) FROM employees) AS avg_pay
FROM employees;

SELECT first_name, last_name
FROM customers
WHERE customer_id IN (SELECT DISTINCT customer_id
FROM transactions WHERE customer_id IS NOT NULL);



26.GROUP BY

GROUP BY = aggregate all rows by a specific column
           often used with aggregate functions
           ex: SUM(), MAX(), MIN(), AVG(), COUNT()

GROUP BY = nhóm tất cả các hàng theo một cột cụ thể
           thường được sử dụng với các hàm tổng hợp
           ví dụ: SUM(), MAX(), MIN(), AVG(), COUNT()

-----

GROUP BY: Nhóm
aggregate: tổng hợp
rows: hàng
column: cột
specific: cụ thể
often: thường xuyên
used with: được sử dụng với
aggregate functions: hàm tổng hợp

-----

SUM(): hàm tổng
MAX(): hàm giá trị lớn nhất
MIN(): hàm giá trị nhỏ nhất
AVG(): hàm giá trị trung bình
COUNT(): hàm đếm số lượng

-----

DROP TABLE IF EXISTS transactions;

CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY AUTO_INCREMENT,
    amount DECIMAL(5, 2),
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) 
    REFERENCES customers(customer_id)
);

INSERT INTO transactions
VALUES 	(1000, 4.99, 3, "2023-01-01"),
		(1001, 2.89, 2, "2023-01-01"),
		(1002, 3.38, 3, "2023-01-02"),
		(1003, 4.99, 1, "2023-01-02"),
		(1004, 1.00, NULL, "2023-01-03"),
		(1005, 2.49, 4, "2023-01-03"),
		(1006, 5.48, NULL, "2023-01-03");
        
SELECT * FROM transactions;
------------------------------------------------------------


Bài tập 1: Bây giờ ông Krabs là chủ muốn biết một ngày business của ổng kiếm được bao nhiêu tiền mỗi ngày,
           tổng tất cả số tiền chúng tôi có mỗi ngày là bao nhiêu 
           Ba ngày khác nhau chẳng hạn 2023-01-01, 2023-01-02 hoặc 2023-01-03
           Tổng số tiền mỗi ngày đó là bao nhiêu

- Cách giải quyết dùng Group By

-- EXAMPLE 1 --
// Tính tổng của ngày hôm đó
SELECT SUM(amount), order_date
FROM transactions 
GROUP BY order_date;

// Tìm số tiền nhỏ nhất của ngày hôm đó
SELECT MIN(amount), order_date
FROM transactions 
GROUP BY order_date;

// Tìm số tiền lớn nhất của ngày hôm đó
SELECT MAX(amount), order_date
FROM transactions 
GROUP BY order_date;

// Tính trung bình của ngày hôm đó
SELECT AVG(amount), order_date
FROM transactions 
GROUP BY order_date;

// Đếm số đơn của ngày hôm đó
SELECT COUNT(amount), order_date
FROM transactions 
GROUP BY order_date;

-- EXAMPLE 2 --
// Nhóm id của khách hàng, có bao nhiêu khách hàng đã chi tiêu tổng cộng


Select SUM (amount), customer_id
From transactions
GROUP BY customer_id


SELECT COUNT(amount), customer_id
FROM transactions 
GROUP BY customer_id
HAVING COUNT(amount) > 1 AND customer_id IS NOT NULL;

SELECT COUNT(amount), customer_id: Lệnh này chọn các cột COUNT(amount) và customer_id từ bảng transactions. Cột COUNT(amount) sẽ chứa số lượng giao dịch của mỗi khách hàng. Cột customer_id sẽ chứa ID khách hàng cho mỗi giao dịch.

FROM transactions: Lệnh này chỉ định rằng dữ liệu cần được truy xuất từ bảng transactions.

GROUP BY customer_id: Lệnh này nhóm các hàng trong bảng transactions theo cột customer_id.

HAVING COUNT(amount) > 1 AND customer_id IS NOT NULL: Lệnh này lọc kết quả để chỉ bao gồm các nhóm có số lượng hàng lớn hơn 1 và cột customer_id không phải là NULL.




27.ROLLUP

-- ROLLUP, extension of the Group by clause
-- produce another row and shows the GRAND TOTAL (super-aggregate value)

-- ROLLUP, phần mở rộng của mệnh đề GROUP BY
-- tạo thêm một hàng và hiển thị TỔNG CỘNG (siêu tổng hợp giá trị )

// Có tổng tiền cho mỗi ngày
Select SUM (amount), order_date
From transactions
Group by order_date;


// Để có thể tính tổng cho gộp lại cho các ngày

Select SUM (amount), order_date
From transactions
Group by order_date WITH ROLLUP;


// Đếm số lần gia dịch
Select COUNT (transaction_id), order_date
From transactions
Group by order_date


// Để có thể tính tổng số lần giao dịch
Select COUNT (transaction_id), order_date
From transactions
Group by order_date WITH ROLLUP;


Select COUNT (transaction_id) as "# of orders", customer_id
From transactions
GROUP BY customer_id WITH ROLLUP;


Select SUM (hourly_pay) as "hourly pay", employee_id
from employees
GROUP BY employee_id WITH ROLLUP;


// Siêu tổng hợp:

SELECT SUM(amount) AS "daily_sales", order_date
FROM transactions
GROUP BY order_date WITH ROLLUP;

SELECT COUNT(transaction_id) AS "# of orders", order_date
FROM transactions
GROUP BY order_date WITH ROLLUP;

SELECT COUNT(transaction_id) AS "# of orders", customer_id
FROM transactions
GROUP BY customer_id WITH ROLLUP;

SELECT SUM(hourly_pay) AS "hourly_pay", employee_id
FROM employees
GROUP BY employee_id WITH ROLLUP;



28.ON DELETE

-- ON DELETE SET NULL = When a FK is deleted, replace FK with Null
-- ON DELETE SET NULL = When a FK is deleted, delete row

-- ON DELETE SET NULL = Khi một FK bị xóa, thay thế FK bằng Null
-- ON DELETE SET NULL = Khi một FK bị xóa, xóa hàng

ON DELETE SET NULL: Khi một khóa ngoại (FK) bị xóa, giá trị của FK trong bảng con sẽ được thay thế bằng NULL. Điều này cho phép bảng con vẫn có thể tồn tại ngay cả khi khóa chính của bảng cha bị xóa.
ON DELETE CASCADE: Khi một khóa ngoại (FK) bị xóa, tất cả các hàng trong bảng con có giá trị FK đó cũng sẽ bị xóa. Điều này đảm bảo rằng không có hàng nào trong bảng con có giá trị FK không hợp lệ.




ALTER TABLE transactions
ADD CONSTRAINT fk_customer_id 
FOREIGN KEY (customer_id) REFERENCES customers(customer_id) 
ON DELETE SET NULL;

ALTER TABLE transactions 
ADD CONSTRAINT fk_customer_id 
FOREIGN KEY (customer_id) REFERENCES customers(customer_id) 
ON DELETE CASCADE;



29.STORED PROCEDURES

Stored procedure = is prepared SQL code that you can save
                    great if there is  a query that you can write often



---- Example 1 ----
// tạo PROCEDURE lấy ra khách hàng
DELIMITER $$
CREATE PROCEDURE get_customers()
BEGIN
 SELECT * FROM customers;
END $$
DELIMITER ;

// dùng
CALL get_customers();

DROP PROCEDURE get_customers;

---- Example 2 ----
// tạo PROCEDURE tìm người dùng bằng id
DELIMITER $$
CREATE PROCEDURE find_customer(IN id INT)  
BEGIN  
 SELECT *
 FROM customers
 WHERE customer_id = id;
END $$
DELIMITER ; 

---- Example 3 ----
// tạo PROCEDURE giúp tìm kiếm theo f_name l_name
DELIMITER $$
CREATE PROCEDURE find_customer(IN f_name VARCHAR(50),
                               IN l_name VARCHAR(50))  
BEGIN  
 SELECT *
 FROM customers
 WHERE first_name = f_name AND last_name = l_name;
END $$
DELIMITER ;

// dùng gọi hàm (truyền đối số tương ứng vào)
CALL find_customer("Larry","Lobster");


30.TRIGGERS

Trigger = when an event happens, do something
          ex. (Insert, Update, Delete)
          check data, handle errors, auditing tables


// Bổ sung cột salary
ALTER TABLE employees
ADD COLUMN salary DECIMAL(10,2) AFTER hourly_pay;
Select * from employees

// Update dữ liệu cho salary

// 1 tuần làm việc 40 tiếng
// 1 năm có 52 tuần
// 40 x 52 = 2080

công thức lương 1 năm. (x là số lương 1 giờ) * số tiếng
x * 2080 

ví dụ 10 $
10 * 2080 = 20800$
25 * 2080 = 52000$

UPDATE employees 
SET salary = hourly_pay * 2080
Select * from employees

// cách tính lương này hơi chuối. Chính vì vậy phải áp dụng Trigger


Trigger

BEFORE: trước khi. (Trước khi tạo, sửa, xóa)


CREATE TRIGGER before_hourly_pay_update
BEFORE UPDATE ON employees 
FOR EACH ROW
SET NEW.salary = (NEW.hourly_pay * 2080);


// làm sao biết trigger tạo ra thành công hay chưa

Có 2 cách: 1 kiểm tra thủ công 2 kiểm tra bằng lệnh

1. Thủ công mở bảng ra và tìm kiếm từ khóa trigger
2. Câu lệnh: SHOW TRIGGERS

// cách hoạt động của trigger này là theo dõi cột hourly_pay, khi cột này cập nhật triggers sẽ kích hoạt.
// Nếu dùng cách truyền thống mình sẽ phải viết câu lệnh update cho salary nữa.


Thí dụ ông chủ muốn tăng 1$ cho mỗi nhân viên

SET hourly_pay = hourly_pay + 1;

// Khi cặp nhật salary sẽ cũng được tính toán lại nhờ trigger kích hoạt


Delete from employees
where employeeId = 6




// Trước khi hàm Insert chạy sẽ có trigger kích hoạt

// Tạo table expenses
CREATE TABLE expenses(
    expense_id INT PRIMARY KEY,
    expense_name VARCHAR(50),
    expense_total DECIMAL(10,2)
)

INSERT INTO expenses
VALUES (1, "salaries", 0),
       (2, "supplies", 0),
       (3, "taxes", 0);


Update expense
SET expense_total = (SELECT SUM(salary)From employees)
where expense_name = "salaries"
Select * from expenses;


CREATE TRIGGER before_hourly_pay_insert
BEFORE INSERT ON employees 
FOR EACH ROW
SET NEW.salary = (NEW.hourly_pay * 2080);


CREATE TRIGGER after_salary_delete
AFTER DELETE ON employees 
FOR EACH ROW
UPDATE expenses
SET expense_total = expense_total - OLD.salary
WHERE expense_name = "salaries";

CREATE TRIGGER after_salary_insert
AFTER INSERT ON employees 
FOR EACH ROW
UPDATE expenses
SET expense_total = expense_total + NEW.salary
WHERE expense_name = "salaries";

CREATE TRIGGER after_salary_update
AFTER UPDATE ON employees 
FOR EACH ROW
UPDATE expenses
SET expense_total = expense_total + (NEW.salary - OLD.salary)
WHERE expense_name = "salaries";