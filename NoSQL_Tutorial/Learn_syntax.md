- Tạo DB: 
	Cú pháp: use database_name
	Ví dụ: use school (Nếu chưa có thì tự động tạo, nếu tồn tại rồi thì sử dụng)
cú pháp kiểm tra danh sách db
show dbs

- Tạo collection trong DB

Cú pháp: 
  db.createCollection("name_collection")

ví dụ: 
  db.createCollection("students")

- Xóa collection trong db

Cú pháp: 
  db.dropDatabase()


Thêm bản ghi vào collection

Cú pháp: 
  db.name_collection.insertOne({key:"value"})

Ví dụ: 
  db.students.insertOne({name: "Spongebob", age: 30, gpa:3.2}) 

Tìm kiếm tất cả bản ghi trong 1 collection

cú pháp:  

  db.ten_collection.find() // nếu trong find không truyền gì vào hết sẽ tìm kiếm tất cả

ví dụ:  

  db.students.find()

Thêm một lúc nhiều bản ghi vào collection, tiêu chí thêm lúc nhiều bản thì truyền vào mảng

cú pháp: 

  db.ten_collection.insertMany([{},{},{}]) // {} mỗi cặp đối tượng mình sẽ truyền key và value vào

ví dụ: 

  db.students.insertMany([
	{name: "Patricl", age: 38, gpa:1.5},
	{name: "Sandy", age: 27, gpa:4.0},
	{name: "Gary", age: 18, gpa:2.5}
       ])
kết quả: trả về có true là thông báo thành công.

kiểm tra: 

  db.students.find()


Data type trong mongoDB

ví dụ: 

   db.students.insertOne({
				name: "Larry", 	 // kiểu chuỗi string
				age: 32, 	 // kiểu số number
				gpa: 2.8, 	 // kiểu số number không phân biệt số nguyên hay thực trong js
				fullTime: false, // Kiểu boolean
				registerDate: new Date(), // Nếu để trống mặc định lấy ngày hiện tại, vẫn có thể set được ngày cho nó new Date("<YYYY-mm-dd>") || new Date("<YYYY-mm-ddTHH:MM:ss>") || new Date("<YYYY-mm-ddTHH:MM:ssZ>") || new Date(<integer>)
				gradutionDate: null, // kiểu dữ liệu null
				courses: ['Biology','Chemistry','Calculus'], // kiểu array
			    	address: {
						street:"123 Fake St.", 
						city: "Bottom", 
						Zip: 123456
					  } 					// kiểu đối tượng
			    })


kết quả: trả về có true là thông báo thành công.

Nhận xét, bạn có thể thấy việc insert các thông tin có cả các trường mới mà các trường cũ không có. Điều này hoàn toàn hợp lệ. Điều này sql sẽ không làm được.


- sorting and limiting: sắp xếp và giới hạn.

Thông thường ta hay tìm kiếm tất cả bằng 

db.students.find()

Nhưng giờ yêu cầu phải sắp xếp theo chuẩn hay thứ tự nào đó thì ta sẽ dùng sort

Ví dụ sắp xếp điểm GPA từ cao xuống thấp

db.students.find().sort({gpa:-1})

Ví dụ sắp xếp điểm GPA từ thấp tăng lên cao
db.students.find().sort({gpa: 1})

Ví dụ sắp tên cũng tương tự

db.students.find().sort({name: 1}) // từ a -> z

db.students.find().sort({name: 1}) // từ z -> a
...


limit 

db.students.find().limit(1) // lấy ra dữ liệu nhưng giới hạn chỉ 1

db.students.find().limit(3) // lấy ra dữ liệu nhưng giới hạn chỉ 3


Sự kết hợp sort và limit

db.students.find().sort({gpa:-1}).limit(1) // ai là người có điểm trung bình cao nhất.

db.students.find().sort({gpa:1}).limit(1) // ai là người có điểm trung bình thấp nhất.


- find: tìm cụ thể 1 ai đó
cú pháp: db.students.find({query}, {projection}) 	Vậy query là: {key: value}  .Vậy projection là:  

ví dụ:  
	db.students.find({gpa: 4.0})
	db.students.find({fullTime: false})
	db.students.find({name: "Spongebob"})

// truyền nhiều vào find

	db.students.find({gpa: 4.0, fullTime: true})

// truyền hai tham số vào hàm find, tham số thứ nhất tìm dữ liệu dựa vào đặc điểm, tham số thứ quy định dữ liệu nào được xuất hiện
	
	db.students.find({}, {name: true}) // này vô tính cũng hiện ra id của students đó, cũng có cách để ẩn đi id

	
// cách ẩn đi các thông tin không nên nhìn thấy 

	db.students.find({}, {_id: false, name:true}) // các cái trương nào được true thì sẽ hiển thị, nào false sẽ ẩn đi

	db.students.find({}, {_id: false, name:true, gpa:true}) // các cái trương nào được true thì sẽ hiển thị, nào false sẽ ẩn đi




- Update một đối tượng cụ thể

	db.students.updateOne(filter, update)   

	Tham số thứ 1 là đặc điểm nhận dạng
	Tham số thứ 2 giá trị dùng để thay thế
	$set là 1 function có sẵn trong mongoDB, giúp chỉnh sửa dữ liệu

	db.students.updateOne({name: "Spongebob"}, {$set: {fullTime:true}})
	// Giải thích muốn update data nào trường name và name đó có giá trị là Spongebob
	// $set: sẽ là nơi chỉ đị value của trong đối tượng thuộc trường yêu cầu chỉnh sửa và thay đổi value đi
		=> như trong ví dụ ông Spongebob có fullTime từa false sang true.


// Để mà sửa dữ liệu 1 cách chính xác không bị sai. Ta nên sử dụng id truyền cho tham số đầu tiên. Để việc tìm kiếm
// truy xất đến phần tử muốn sửa đổi dữ liệu và tiến hành sửa


// Ngoài $set ta sẽ có một trường đối nghịch lại $unset

Đặc điểm của $set là: nếu giá của id đó có tồn tại nhưng không có trường cần chỉnh sửa, nó sẽ tự động thêm vào

Đặc điểm của $unset là trái ngược sự thêm vào của $set. Việc $unset là sẽ xóa được chỉnh định

Ví dụ: tb.students.updateOne({_id: ObjectId("64d09e8315b6eda752740bae")}, {$unset:{fullTime: ""}) 

// Ở đây xóa phần tử đó thì chỉ cần để trường đó là một cái chuỗi rỗng, $unset sẽ tự hiểu và đem xóa trường đó đi


- Update Many

db.students.updateMany({}, {$set: {fullTime: false}})

câu query này sẽ chỉ định tất cả dự liệu, có lẫn không có trường fullTime đều sẽ được update 
lại thành fullTime: false

kết quả là: true và  matchedCount: 5, modifiedCount: 4, thể hiện sự thành công

kiểm tra lại tất cả đều được cập nhật


// Thử loại bỏ trường fullTime ở 1 vài đối tượng bằng $unset


// chiều vào id tham số thứ 1, tham số thứ 2 là dùng $unset loại bỏ đối tượng {fullTime:""}
db.students.updateOne({ _id: ObjectId("64d0ac798ad7a0f8f5a734f5")},{$unset:{fullTime:""}})
db.students.updateOne({ _id: ObjectId("64d0a3b215b6eda752740bb1")},{$unset:{fullTime:""}})
// sau khi update thì sẽ xóa dòng fullTime:"" của 2 cái id này


Bây giờ bài toán là sẽ làm sao cập nhật các giá trị nào mà không có fullTime:"" thì cập nhật thành co fullTime

// tham số thứ 1 fullTime:{$exists: false} cái này là điều kiện check xem trong data có data nào không có fullTime
// tham số thứ 2 sử dụng $set để cập nhật cho các data đó là fullTime:true

db.collection_name.updateMany({truyền_vào_điều_kiện}, {sử dụng $set:{trường_cập_nhật}})

db.students.updateMany({fullTime:{$exists: false}}, {$set:{fullTime:true}})

// sau khi xong thì kiểm tra lại db.students.find() 


- Delete

Tại vì thực hiện tính năng xóa dữ liệu nên.
Trước khi xóa nhớ xuất file ra json để lưu lại xí import vào lại
- vào mongodb compass 
  chọn export data 
  chọn export query result 
  chọn all fileds
  Nhấn next
  Chọn JSON

riêng delete chỉ truyền vào 1 tham số, tham số này chứa 1 hay nhiều dữ liệu thông tin của đối tượng cần xóa.
Càng đầy đủ xóa càng chính xác. 

Cú pháp: db.collection_names.deleteOne({thông_tin_đối_tượng_xóa})

ví dụ: db.students.deleteOne({name:"Larry"})


Cú pháp xóa nhiều: db.collection_names.deleteMany({fullTime: false})
- xóa nhiều data, cụ thể là các thông tin có fullTime: false trong đối tượng đó là sẽ xóa hết


xóa tất cả các trường mà không có tồn tại ngày registerDate
db.students.deleteMany({registerDate: {$exists:false}})

Ý nghĩa của câu lệnh trên là: nếu cái trường nào không tồn tại registerDate: ... là xóa


- comparison operators
Toán tử so sánh

ne -> not equal
lt -> less than
lte -> less than equals to
gt -> greater than
gte -> greater than equals to

$eq: bằng
$ne: không bằng
$gt: lớn hơn
$gte: lớn hơn hoặc bằng
$lt: nhỏ hơn
$lte: nhỏ hơn hoặc bằng
$in: nằm trong
$nin: không nằm trong
$all: tất cả
$elemMatch: tìm thấy một phần tử
$size: kích thước
$mod: chia cho và lấy phần dư
$exists: tồn tại
$type: kiểm tra loại
$nin: không nằm trong

- ví dụ:
         Tìm tất cả các bản ghi ngoại trừ bản ghi có name là Spongebob
	 $ne là ne -> not equal
	 db.students.find({name:{$ne:"Spongebob"}})

	 Tìm tất cả các bản ghi có age ít hơn 20
	 lt -> less than to (nhỏ hơn)
	 db.students.find({age:{$lt: 20}})


	 Tìm tất cả các bản ghi có age ít hơn hoặc bằng 27
	 lte -> less than equals to (nhỏ hơn hoặc bằng)
	 db.students.find({age:{$lte: 27}})

	 Tìm tất cả các bản ghi có age lớn hơn 27
	 gt -> greater than (lớn hơn)
	 db.students.find({age:{$gt: 27}})
	
	
	 Tìm tất cả các bản ghi có age lớn hơn hoặc bằng 27
	 gte -> greater than equal (lớn hơn)
	 db.students.find({age:{$gte: 27}})


	 Tìm tất cả các bản ghi có gpa lớn hơn hoặc bằng 2.5
	 db.students.find({gpa:{$gte: 2.5}})

	 Tìm tất cả các bản ghi có gpa lớn hơn 3.0
	 db.students.find({gpa:{$gt: 3.0}})

	 
	 Tìm tất cả các bản ghi có gpa nhỏ hơn 2.0
	 db.students.find({gpa:{$lt: 2.0}})

	 Tìm tất cả các bản ghi có gpa nhỏ hơn hoặc bằng 2.0
	 db.students.find({gpa:{$lte: 2.0}})

	
	 Tìm trong bản ghi có name là 3 giá trị "Spongebob", "Patrick", "Sandy" thì hiển thị
	 db.students.find({name: {$in:["Spongebob", "Patrick", "Sandy"]}})
	 // $in -> nằm trong


	 db.students.find({name: {$nin:["Spongebob", "Patrick", "Sandy"]}})
	 // $nin: không nằm trong

2 Điều kiện
	Tìm tất cả các bản ghi có gpa nhỏ hơn hoặc bằng 4.0 và lớn hơn hoặc bằng 3.0
	db.students.find({gpa:{$gte: 3.0, $lte: 4.0}})



- logical operators

$and Joins query clauses with a logical AND returns all documents that match the conditions of both clauses.
     Kết nối các mệnh đề truy vấn bằng AND logic trả về tất cả các tài liệu khớp với điều kiện của cả hai mệnh đề.

$not  Inverts the effect of a query expression and returns documents that do not match the query expression.
      Đảo ngược hiệu ứng của một biểu thức truy vấn và trả về các tài liệu không khớp với biểu thức truy vấn.


$nor  Joins query clauses with a logical NOR returns all documents that fail to match both clauses.
      Kết nối các mệnh đề truy vấn bằng NOR logic trả về tất cả các tài liệu không khớp với cả hai mệnh đề.

$or   Joins query clauses with a logical OR returns all documents that match the conditions of either clause.
      Kết nối các mệnh đề truy vấn bằng OR logic trả về tất cả các tài liệu khớp với điều kiện của bất kỳ mệnh đề nào.

// tìm ra sinh viên có fullTime: true đồng thời độ tuổi nhỏ hơn hoặc bằng 22
   phải thỏa mãn 2 điều kiện
   db.students.find({$and: [{fullTime: true},{age:{$lte: 22}}]})

// tìm ra sinh viên có fullTime: true hoặc nhỏ hơn hoặc bằng 22
   chỉ cần thỏa 1 trong 2 điều kiện
   db.students.find({$or: [{fullTime: true}, {age:{$lte: 22}}]})

// bây giờ tìm ra tất cả sinh viên, nhưng những đứa 22 tuổi thì không lấy. Dùng logic $nor
   chỉ cần $nor để loại ra các filed chứa thông tin đó
   db.students.find({$nor: [{age:{$lte: 22}}]})

   cũng có thể thêm nhiều điều kiện.
   lấy ra các trường fields nhưng đảm bảo là không có 2 vế (gpa lớn hơn hoặc bằng 3.0) và (age nhỏ hơn hoặc bằng 22)
   db.students.find({$nor: [{gpa: {$gte: 3.0}}, {age:{$lte: 22}}]})

// toán tử $not là sẽ đảo ngược điều kiện, ví dụ ở trong là yêu cầu lớn hơn hoặc bằng 30 nhưng khi dùng $not
// kết quả sẽ đảo ngược nó lấy các những người có age nhỏ hơn 30
   db.students.find({age: {$not: {$gte:30}}})

để ý thấy kết quả age là null hoặc nhỏ hơn 30 đều được in ra
[
  {
    _id: ObjectId("64d0a3b215b6eda752740bb0"),
    name: 'Sandy',
    age: null,
    gpa: 4,
    fullTime: true
  },
  {
    _id: ObjectId("64d0a3b215b6eda752740bb1"),
    name: 'Gary',
    age: 18,
    gpa: 2.5,
    fullTime: true
  }
]

- indexes

Indexes support the efficient execution of queries in MongoDB. 
Without indexes, MongoDB must perform a collection scan, i.e. 
scan every document in a collection, to select those documents that match the query statement. 
If an appropriate index exists for a query, 
MongoDB can use the index to limit the number of documents it must inspect.

Chỉ mục hỗ trợ việc thực thi truy vấn hiệu quả trong MongoDB. 
Nếu không có chỉ mục, MongoDB phải thực hiện quét tập hợp, 
tức là quét từng tài liệu trong tập hợp, để chọn các tài liệu khớp với câu lệnh truy vấn. 
Nếu có chỉ mục phù hợp cho truy vấn, MongoDB có thể sử dụng chỉ mục để hạn chế số lượng tài liệu cần kiểm tra.

Thí dụ: bây giờ tìm trong collection students xem có ai trong đó tên là larry không, trong này có 5 trường

 db.students.find({name: "Larry"}).explain("executionStats")

kết quả: 

{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'school.students',
    indexFilterSet: false,
    parsedQuery: { name: { '$eq': 'Larry' } },
    queryHash: '64908032',
    planCacheKey: '64908032',
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    winningPlan: {
      stage: 'COLLSCAN',
      filter: { name: { '$eq': 'Larry' } },
      direction: 'forward'
    },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 1,
    executionTimeMillis: 2,
    totalKeysExamined: 0,
    totalDocsExamined: 5,
    executionStages: {
      stage: 'COLLSCAN',
      filter: { name: { '$eq': 'Larry' } },
      nReturned: 1,
      executionTimeMillisEstimate: 0,
      works: 6,
      advanced: 1,
      needTime: 4,				
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1,
      direction: 'forward',
      docsExamined: 5  	//Tìm kiếm theo kiểu tuyến tính // Tốn 5 lần truy vấn, vì trong collection có 5 trường
						       // Hãy tưởng tượng có 1 triệu bản ghi thì nó sẽ lâu hơn nhiều
						      // chính vì vậy cần tạo indexes để tìm kiếm cho nhánh
    }
  },
  command: { find: 'students', filter: { name: 'Larry' }, '$db': 'school' },
  serverInfo: {
    host: 'tuan',
    port: 27017,
    version: '6.0.8',
    gitVersion: '3d84c0dd4e5d99be0d69003652313e7eaf4cdd74'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 104857600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 104857600,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600
  },
  ok: 1
}


dùng indexes
 db.students.createIndex({name: 1})

 db.students.find({name:"Larry"}).explain("executionStats")
 // .explain("executionStats"): cái này là xem chi tiết hiệu xuất của câu query


Kiểm tra có bao nhiêu indexes đang tồn tại
db.students.getIndexes()

xóa bỏ indexes đã tạo ra
db.students.dropIndex("ten_index_đó")
db.students.dropIndex("name_1")



Câu lệnh db.students.createIndex({name: 1}) sẽ tạo một chỉ mục cho trường name trong collection students. 
Chỉ mục này sẽ sắp xếp các tài liệu trong collection theo thứ tự bảng chữ cái theo trường name. 
Điều này sẽ giúp MongoDB tìm kiếm các tài liệu khớp với truy vấn theo trường name nhanh hơn nhiều 
so với việc quét từng tài liệu trong collection.

Ví dụ: nếu bạn có câu lệnh truy vấn db.students.find({name: "John Doe"}), 
MongoDB sẽ có thể tìm thấy tài liệu mà không cần quét toàn bộ collection. 
Thay vào đó, MongoDB có thể chỉ cần tìm tài liệu đầu tiên trong collection khớp với trường name là "John Doe".

Chỉ mục là một công cụ quan trọng để tăng tốc độ truy vấn trong MongoDB. 
Nếu bạn đang gặp phải các truy vấn chậm, bạn nên xem xét việc tạo chỉ mục 
cho các trường được sử dụng trong các truy vấn đó.


- collections
 Các collections trong DB school cơ bản
- Students
- Teachers
- Courses

Trong SQL có các bảng, trong NoSQL collection cũng tương tự như là các cái bảng trong SQL

Để kiếm tra DB có bao nhiều collections thì: gõ lệnh Show collections

// Cách tạo 1 collections

cú pháp: db.createCollection("tên_của_collections")
ví dụ: db.createCollection("teachers")

Ngoài ra cú pháp này có thể nhận vào 2 tham số. Tham số thứ nhất là tên, 
tham số thứ 2 là tùy biến các setting cho collections đó.

// trong ví dụ này truyền tới 3 tham số và tham số thứ 3 set Indexed id là không tự động tăng
// Nếu không truyền tham số thứ 3 autoIndexed mặc định là true
db.createCollection("teachers",{capped: true, size: 1000000, max: 100},{autoIndexed: false})


// có tạo bảng, sẽ có xóa bảng.
db.tên_bảng.drop()

cú pháp: db.tên_collection.drop()

Ví dụ:  db.courses.drop()

	db.teachers.drop()

















