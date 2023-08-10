Database -> Tables -> Records
Database -> Collections -> Documents

---

{shows dbs} shows the available databases - hiển thị các cơ sở dữ liệu có sẵn

---

{use 'db_name'} switches to the database 'db_name' if it already exists or creates it if it doesn't
{use 'db_name'} chuyển sang cơ sở dữ liệu 'db_name' nếu nó đã tồn tại hoặc tạo nó nếu không.

---

{db.dropDatabase()} drops the current database
{db.dropDatabase()} xóa cơ sở dữ liệu hiện tại

---

{db.createCollection('collection_name')} creates a new collection named 'collection_name'
{db.createCollection('collection_name')} tạo một bộ sưu tập mới có tên 'collection_name'

---

{show collections} to show all the collections in the current db
{show collections} để hiển thị tất cả các bộ sưu tập trong cơ sở dữ liệu hiện tại

---

{db.createCollection('collection*name', {capped : true, size : 10000, max: 100}, {autoIndexID : false})} will create a collection with some upper limit of size and number of documents in the collection, autoIndexID to false will tell mongoDB to not create the default index on the * id field in this collection.
By default mongoDB creates an index on the \_ id field in a collection.

{db.createCollection('collection*name', {capped : true, size : 10000, max: 100}, {autoIndexID : false})} sẽ tạo một collection (bộ sưu tập) có giới hạn kích thước và số lượng tài liệu nhất định trong collection (bộ sưu tập), autoIndexID thành false sẽ chỉ cho mongoDB không tạo chỉ mục mặc định trên trường * id trong collection (bộ sưu tập) này.
Theo mặc định, mongoDB tạo chỉ mục trên trường \_ id trong một collection (bộ sưu tập).

---

{db.collection_name.drop()} to drop the collection
{db.collection_name.drop()} xóa collection (bộ sưu tập).

---

{db.collection_name.insertOne({key value pairs here})} inserts a document into the collection named 'collection_name'
{db.collection_name.insertOne({key value pairs here})} chèn một tài liệu vào collection (bộ sưu tập) có tên 'collection_name'

---

{db.collection_name.insertMany([{key value pairs here}, {key value pairs here}, {key value pairs here}])} inserts many documents into the collection named 'collection_name'
{db.collection_name.insertMany([{key value pairs here}, {key value pairs here}, {key value pairs here}])} chèn nhiều tài liệu vào collection (bộ sưu tập) có tên 'collection_name'

---

{db.collection_name.find()} lists all the documents of the collection named 'collection_name'
{db.collection_name.find()} liệt kê tất cả các tài liệu của collection (bộ sưu tập) có tên 'collection_name'

---

{db.collection_name.find().sort({key value pairs})} to sort all the listed documents wrt to key value pairs provided.
Ex -
db.students.find().sort({name : 1}) sorts the documents in alphb. order
db.students.find().sort({name : -1}) sorts the documents in reverse alphb. order

{db.collection_name.find().sort({key value pairs})} để sắp xếp tất cả các tài liệu được liệt kê theo thứ tự các cặp giá trị khóa được cung cấp.
Ví dụ:
db.students.find().sort({name: 1}) sắp xếp các tài liệu theo thứ tự bảng chữ cái
db.students.find().sort({name: -1}) sắp xếp các tài liệu theo thứ tự bảng chữ cái ngược lại

---

{db.collection_name.find().limit(x)} limits the documents listed to a number x, i.e., total documents lisited will be x

{db.collection_name.find().limit(x)} giới hạn số lượng tài liệu được liệt kê là x, tức là tổng số tài liệu được liệt kê sẽ là x

---

{db.collection_name.find({query}, {projection})}

-   {query} -> filters the documents wrt the query provided, query is just a document or a collection of key value pairs
-   {projection} -> is used to show only some specific fields of all the documents after filtering, projection is just a document or a collection of key value pairs
    Ex -
    db.students.find({}, {id:false,name:true, gpa:true})
    No filters given, but attributes to be listed are given

{db.collection_name.find({query}, {projection})}

{query} -> lọc các tài liệu theo truy vấn được cung cấp, truy vấn chỉ là một tài liệu hoặc một tập hợp các cặp giá trị khóa
{projection} -> được sử dụng để chỉ hiển thị một số trường cụ thể của tất cả các tài liệu sau khi lọc, projection chỉ là một tài liệu hoặc một tập hợp các cặp giá trị khóa Ví dụ: db.students.find({}, {id:false,name:true, gpa:true}) Không có bộ lọc nào được cung cấp, nhưng các thuộc tính cần được liệt kê được cung cấp
Ex -
db.students.find({}, {id:false,name:true, gpa:true})
Không có bộ lọc nào được cung cấp, nhưng các thuộc tính được liệt kê được cung cấp

---

{db.collection_name.updateOne({filter}, {update})}

-   {query} -> filters the documents to select the document whose data to update
-   {update} -> actually updates the document
    Ex -
    db.students.updateOne({name: "Sam"}, {$ set : {age : 20}})
    Instead of updating an attribute with $ set, an attribute can also be remove using $ unset
    Ex -
    db.students.updateOne({name: "Sam"}, {$ unset : {age : ""}})

{db.collection_name.updateOne({filter}, {update})}

-   {query} -> lọc các tài liệu để chọn tài liệu cần cập nhật dữ liệu
-   {update} -> thực sự cập nhật tài liệu
    Ví dụ -
    db.students.updateOne({name: "Sam"}, {$ set : {age : 20}})
    Thay vì cập nhật một thuộc tính bằng $ set, một thuộc tính cũng có thể được xóa bằng $ unset
    Ví dụ -
    db.students.updateOne({name: "Sam"}, {$ unset : {age : ""}})

---

{db.collection_name.updateMany({query}, {update})}

-   {query} -> same as updateOne()
-   {update} -> same as updateOne()
    Ex -
    db.students.updateMany({}, {$ set : {fulltime: false}})
    Updates everyone's fulltime attribute to false
    Similarly $ unset can be used here

Ex -
db.students.updateMany({fulltime : {$ exists:false}}, {$ set : {fulltime: true}})

{db.collection_name.updateMany({query}, {update})}

-   {query} -> same as updateOne()
-   {update} -> same as updateOne()
    Ex -
    db.students.updateMany({}, {$ set : {fulltime: false}})
    Cập nhật thuộc tính toàn thời gian của mọi người thành false.
    Tương tự $unset có thể được sử dụng ở đây.

Ex -
db.students.updateMany({fulltime : {$ exists:false}}, {$ set : {fulltime: true}})

---

{db.collection_name.deleteOne({query})}

-   {query} -> filters the document to select the document to delete

{db.collection_name.deleteOne({query})}

-   {query} -> lọc tài liệu để chọn tài liệu cần xóa

---

{db.collection_name.deleteMany({query})}

-   {query} -> filters the document to select all the documents to delete

{db.collection_name.deleteMany({query})}

-   {query} -> lọc tài liệu và chọn tất cả tài liệu cần xóa

---

{db.collection_name.find({name : {$ ne : 'NAME'}})}
to find all the documents whose name attribute is not equal to 'NAME'

{db.collection_name.find({name : {$ ne : 'NAME'}})}
để tìm tất cả các tài liệu có thuộc tính tên không bằng 'TÊN' || Lưu ý $ ne là do hàm mongodb cung cấp và nó mãng nghĩa là không bằng.

---

{db.collection_name.find({gpa : {$ lt: value}})}
to find all the documents whose gpa attribute's value is less than 'value'

{db.collection_name.find({gpa : {$ lt: value}})}
để tìm tất cả các tài liệu có thuộc tính gpa có giá trị nhỏ hơn 'giá trị'

---

Comparision Operators -
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

---

{db.collection_name.find({gpa : {$ gte : 3, $ lte : 4}})}
to find all the documents whose gpa attribute's value is between 3 and 4

{db.collection_name.find({gpa : {$ gte : 3, $ lte : 4}})}
để tìm tất cả các tài liệu có thuộc tính gpa có giá trị nằm giữa 3 và 4

---

{db.collection_name.find({name : {$ in : ['value 1', 'value 2', 'value n']}})}
to find all the documents whose name attribute's value is one of 'value 1', 'value 2', 'value n'
$ in -> in
$ nin -> not in

{db.collection_name.find({name : {$ in : ['value 1', 'value 2', 'value n']}})}
để tìm tất cả các tài liệu có thuộc tính name có giá trị là một trong các giá trị 'value 1', 'value 2', 'value n'
$ in -> nằm trong
$ nin -> không nằm trong

---

db.students.find({ $ and : [{fullTime:true}, {age : {$ gte : 18} }] }, {\_ id:false, name:true, age:true})
to find all the documents where the value of fullTime attribute is true and age is less than or equal to 'value'

db.students.find({ $ and : [{fullTime:true}, {age : {$ gte : 18} }] }, {\_ id:false, name:true, age:true})
để tìm tất cả các tài liệu có giá trị của thuộc tính fullTime là true và tuổi nhỏ hơn hoặc bằng 'giá trị'

---

Logical Operators -
$ and
$ or
$ nor

$ not

---

db.collection_name.find({age : {$ not: {$ gte : value}}})
to find all the documents where the value of the age attribute is not greater than or equal to 'value', i.e., is less than 'value'

db.collection_name.find({age : {$ not: {$ gte : value}}})
để tìm tất cả các tài liệu có giá trị của thuộc tính tuổi không lớn hơn hoặc bằng 'giá trị', tức là nhỏ hơn 'giá trị'

giá trị in ra phải nhỏ hơn value đó ý nghĩa value này

Indexes -

{db.collection_name.find({name:'value'}).explain('executionStats')}
to get info about the execution of the query

{db.collection_name.find({name:'value'}).explain('executionStats')}
để biết thông tin về việc thực thi truy vấn

---

{db.collection_name.createIndex({name : 1})}
will return the name of the index created.
Index will be created on the 'name' field

{db.collection_name.createIndex({name : 1})}
sẽ trả về tên của chỉ mục được tạo.
Chỉ mục sẽ được tạo trên trường 'name'

---

{db.collection_name.getIndexes()}
will return all the indexes created for the collection

{db.collection_name.getIndexes()}
sẽ trả về tất cả các chỉ mục được tạo cho collection

---

{db.collection_name.dropIndex("name_of_index")}
to drop the index

{db.collection_name.dropIndex("name_of_index")}
để bỏ chỉ mục

---

Some Examples -
db.students.find({ gpa : {$ gte:5, $ lte:9}, fullTime : { $ exists: true } }, {\_ id:false, name:true, gpa: true})

db.students.find({name : {$ ne : "Sam"}}, {\_ id:false,name:true, gpa:true}).sort({gpa:-1}).limit(3)

Complex ->
db.students.find({ $ and : [{fullTime:true}, {age : {$ gte : 18} }], $ or : [{name : { $ in : ["Sam", "Patric"] } }, {age: { $ gte : 10 } }] }, {\_ id:false, name:true, age:true})

Đầu tiên, mã sử dụng toán tử $and để tìm tất cả các tài liệu có trường fullTime là true và trường age lớn hơn hoặc bằng 18. Sau đó, mã sử dụng toán tử $or để tìm tất cả các tài liệu có trường name bằng Sam hoặc Patric, hoặc trường age lớn hơn hoặc bằng 10. Cuối cùng, mã chỉ định rằng trường \_id không nên được trả về trong kết quả, và chỉ các trường name và age nên được trả về.

Dưới đây là phân tích mã:

db.students.find(): Dòng mã này nói với MongoDB để tìm tất cả các tài liệu trong collection students.

{ $ and : [{fullTime:true}, {age : {$ gte : 18} }], $ or : [{name : { $ in : ["Sam", "Patric"] } }, {age: { $ gte : 10 } }] }: Dòng mã này định nghĩa các tiêu chí tìm kiếm. Toán tử $and được sử dụng để tìm các tài liệu đáp ứng cả hai điều kiện, và toán tử $or được sử dụng để tìm các tài liệu đáp ứng bất kỳ điều kiện nào.

{\_ id:false, name:true, age:true}: Dòng mã này chỉ định các trường nên được trả về trong kết quả. Trường \_id là định danh duy nhất cho mỗi tài liệu, vì vậy nó không được bao gồm trong kết quả. Các trường name và age được bao gồm trong kết quả.

Aggregation, replication, and sharding are three important concepts in MongoDB.

Tập hợp, sao chép và phân đoạn là ba khái niệm quan trọng trong MongoDB.

Aggregation is a way to process data in MongoDB. It allows you to perform complex queries on your data, such as grouping, sorting, and filtering.
Tập hợp là một cách để xử lý dữ liệu trong MongoDB. Nó cho phép bạn thực hiện các truy vấn phức tạp trên dữ liệu của mình, chẳng hạn như nhóm, sắp xếp và lọc.

Replication is a way to ensure that your data is always available. It involves copying your data to multiple servers, so that if one server fails, the others can still access your data.

Sao chép là một cách để đảm bảo rằng dữ liệu của bạn luôn sẵn sàng. Nó liên quan đến việc sao chép dữ liệu của bạn vào nhiều máy chủ để nếu một máy chủ bị lỗi, những máy chủ khác vẫn có thể truy cập dữ liệu của bạn.

Sharding is a way to scale your MongoDB deployment. It involves dividing your data across multiple servers, so that you can handle more traffic.

Sharding là một cách để mở rộng quy mô triển khai MongoDB của bạn. Nó liên quan đến việc chia dữ liệu của bạn trên nhiều máy chủ để bạn có thể xử lý nhiều lưu lượng truy cập hơn.

Aggregation Tích hợp

Aggregation is a powerful tool for processing data in MongoDB. It allows you to perform complex queries on your data, such as grouping, sorting, and filtering.

Tích hợp là một cách để xử lý dữ liệu trong MongoDB. Nó cho phép bạn thực hiện các truy vấn phức tạp đối với dữ liệu của mình, chẳng hạn như nhóm, sắp xếp và lọc.

Aggregation queries are written in a language called aggregation pipeline. The aggregation pipeline is a series of stages that are used to process the data.

Các truy vấn tích hợp được viết bằng ngôn ngữ gọi là tích hợp đường ống. Đường ống tích hợp là một chuỗi các giai đoạn được sử dụng để xử lý dữ liệu.

The aggregation pipeline is a powerful tool, but it can be complex to learn. However, there are many resources available to help you learn about the aggregation pipeline.

Đường ống tích hợp là một công cụ mạnh mẽ, nhưng nó có thể phức tạp để học. Tuy nhiên, có nhiều tài nguyên sẵn có để giúp bạn tìm hiểu về đường ống tích hợp.

Replication Sao chép

Replication is a way to ensure that your data is always available. It involves copying your data to multiple servers, so that if one server fails, the others can still access your data.

Sao chép là một cách để đảm bảo rằng dữ liệu của bạn luôn có sẵn. Nó liên quan đến việc sao chép dữ liệu của bạn sang nhiều máy chủ, để nếu một máy chủ bị lỗi, các máy chủ khác vẫn có thể truy cập dữ liệu của bạn.

MongoDB replication is a built-in feature. It is easy to configure and manage.

Sao chép MongoDB là một tính năng tích hợp. Nó dễ cấu hình và quản lý.

Replication is an important part of any MongoDB deployment. It helps to ensure that your data is always available, even if one of your servers fails.

Sao chép là một phần quan trọng trong bất kỳ triển khai MongoDB nào. Nó giúp đảm bảo rằng dữ liệu của bạn luôn có sẵn, ngay cả khi một trong các máy chủ của bạn bị lỗi.

Sharding Phân mảnh

Sharding is a way to scale your MongoDB deployment. It involves dividing your data across multiple servers, so that you can handle more traffic.

Phân mảnh là một cách để mở rộng quy mô triển khai MongoDB của bạn. Nó liên quan đến việc chia dữ liệu của bạn trên nhiều máy chủ, để bạn có thể xử lý nhiều lưu lượng truy cập hơn.

Sharding is a complex topic, but it can be very beneficial for large MongoDB deployments.

Phân mảnh là một chủ đề phức tạp, nhưng nó có thể rất có lợi cho các triển khai MongoDB lớn.

If you are considering sharding your MongoDB deployment, I recommend that you consult with a MongoDB expert.

Nếu bạn đang xem xét phân mảnh triển khai MongoDB của mình, tôi khuyên bạn nên tham khảo ý kiến ​​chuyên gia MongoDB.

Examples:

Aggregation: Tích hợp

Truy vấn tích hợp để tìm tất cả các tài liệu trong collection products có giá trị của trường price lớn hơn 100:

db.products.aggregate([
{
"$match": {
"price": { "$gt": 100 }
}
}
])

Truy vấn này sẽ trả về một mảng các tài liệu có giá trị của trường price lớn hơn 100.

Dưới đây là một ví dụ khác về truy vấn tích hợp để tìm tổng số tài liệu trong collection products:

db.products.aggregate([
{
"$group": {
"_id": null,
"totalCount": { "$sum": 1 }
}
}
])

Truy vấn này sẽ trả về một tài liệu có trường \_id là null và trường totalCount là tổng số tài liệu trong collection products.

Dưới đây là một ví dụ khác về truy vấn tích hợp để tìm các tài liệu trong collection products được nhóm theo giá trị của trường category và tính tổng giá trị của trường price cho mỗi nhóm:

db.products.aggregate([
{
"$group": {
"_id": {
"category": "$category"
},
"totalPrice": { "$sum": "$price" }
}
}
])

Truy vấn này sẽ trả về một mảng các tài liệu có trường \_id là một đối tượng có trường category và trường totalPrice là tổng giá trị của trường price cho tất cả các tài liệu trong nhóm.

replication

sharding
