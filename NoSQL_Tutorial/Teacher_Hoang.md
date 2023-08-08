// Tạo DB
use StudentManagement
// Tạo Bảng và thêm dữ liệu (thì mới bắt đầu có dữ liệu)
db.students.insertOne({name: "Tuan"})

// Câu lệnh tìm kiếm dữ liệu
db.students.find()

// Bỏ 1 collection || drop
db.students.drop()
// xóa thành công trả về true

//thêm || cụ thể là thêm collection students nếu chưa có, sau đó thêm dữ liệu (bản ghi) thông qua insertOne
// id thì mongodb luôn tự tạo
db.students.insertOne({
    name: "Nguyen Thai Tuan", //key: value
    dateOfBirth: new Date('2000-08-07'), //key: value || new Date ('năm-tháng-ngày') - giớ giấc không có mặc định 00:00:00
    email: "thaituan7820@gmail.com",
    address: "822/32 Huong Lo 2, HCM, VietNam"
})

// câu lệnh tìm kiếm, find điều kiện đầu vào mà không có giá trị truyền vào thì là tìm kiếm tất cả || nó giống select * from trong SQL
db.students.find()

// Thêm nhiều bản ghi, hơi khác 1 chút với insertOne là đối tượng {}, insertMany thì truyền 1 mãng ([])
db.students.insertMany([
    {
        name: "Nguyen Van Hoang", //key: value
        dateOfBirth: new Date('2000-08-07'), //key: value || new Date ('năm-tháng-ngày') - giớ giấc không có mặc định 00:00:00
        email: "thaituan7820@gmail.com",
        address: "822/32 Huong Lo 2, HCM, VietNam"
    },
    {
        name: "Thai Thi Thuy Trang", //key: value
        dateOfBirth: new Date('2000-08-07'), //key: value || new Date ('năm-tháng-ngày') - giớ giấc không có mặc định 00:00:00
        email: "thaituan7820@gmail.com",
        address: "822/32 Huong Lo 2, HCM, VietNam"
    }
])


// Validate Schema

// Tạo bảng Course
// Tham số thứ 1 tên bảng, tham số thứ 2 là đối tượng
db.createCollection('courses', {
    validator: {
        // lưu ý các thuộc tính $ là do mongodb cung cấp
        $jsonSchema:{
            bsonType: 'object', //object của object, trong object có thể chứa các kiểu dữ liệu khác nhau string, number, ... ngoài ra còn chứa object
            // binary json (Javascript Object notation)
            title: 'Validate Course object',
            properties: {
                title: {
                    bsonType: 'string',
                    description: 'title must be a string'
                },
                hours: {
                    bsonType: 'int',
                    minimum: 3,
                    maximum: 100,
                    description: 'hours must be between 3 and 100'
                },
                startDate: {
                    // Nếu mà trường nhận vào nhiều hơn 2 giá trị, 
                    // bsonType: ['date', 'string'],
                    bsonType: ['date'],
                    description: 'Incorrect date type'
                },
                price: {
                    bsonType: ['int', 'double'],
                    description: 'price must be a number'
                }
            }
        } 
    }
})

// Chạy đúng thì trả về 1, sai trả về 0

db.courses.find()

db.courses.insertOne({
    title: "Javascript programing language for beginer",
    hours: 50,
    startDate: new Date('2023-02-10')
})

db.courses.insertOne({
    title: "PHP Course",
    hours: 100, // falidate 3 -> 100 nếu vượt quá 100 thì vi phạm validate, thông báo lỗi
    startDate: new Date('2023-08-07'),
    price: 123.2
})

// Tính xem 1 cái collection đó có bao nhiêu bản ghi
db.courses.find().count();

// Giới hạn số bản ghi để có thể in ra (truyền_lượng_bản_ghi)
db.courses.find().limit(1);

// Get detail validation ?

// db.getCollectionInfos({name: "courses"}).length
db.getCollectionInfos({name: "courses"})[0].options.validator["$jsonSchema"].properties


//Có thêm thì cũng sẽ có sửa
// Update Schema Validation
// Update thì không cần phải nhập đầy đủ chỉ cần nhập thông tin nào cần cập nhật
db.runCommand({
    collMod: "courses", // collection Modify
    validator: {
        $jsonSchema: {
            bsonType: 'object',
            properties: {
                hours: {
                    bsonType: 'int',
                    minimum: 3,
                    maximum: 200, //update từ 100 lên 200
                    description: 'hours must be between 3 and 100'
                },
            }
        }
    }
})

// Kiểm tra kiểu dữ liệu trong bảng sau khi cập nhật
db.getCollectionInfos({name: "courses"})[0].options.validator["$jsonSchema"].properties

//data is small 

db.courses.find().count()
// Như đã biết find có thể truyền vào

// Vì truyền vào find bằng 1 thuộc tính nên value hiển thị cũng chỉ 1 thuộc tính
// limit giới hạn số lượng dữ liệu lấy ra. chứ 10 triệu bản ghi lấy ra cùng 1 lúc là chết
db.courses.find({}, {hours: 50}).limit(1);


// Trường id sẽ luôn luôn hiển thị thì set id là 0, lúc này chỉ hiện mỗi hours thui
db.courses.find({}, {hours: 50, _id:0}).limit(1);



// Để hiển thị dữ liệu từ khoảng thời gian này đến khoảng thời gian kia, và vẫn lấy ra đầy đủ thông tin
db.courses.find({
    hours: {
        $gte: 51, //greater than  or equals (lớn hơn hoặc bằng)
        $lte: 200, //letter than  or equals (nhỏ hơn hoặc bằng)
    }
})


// có mẹo trước khi in ra thì nên count trước xem có bao nhiêu bản ghi
db.courses.find({
    hours: {
        $gte: 51, //greater than  or equals (lớn hơn hoặc bằng)
        $lte: 200, //letter than  or equals (nhỏ hơn hoặc bằng)
    }
}, {
    price: 1,
    hours: 1
}).count()



// chỉ lấy cụ thể thông tin cần thiết thui.
// Tham số thứ nhất là điều kiện tìm kiếm, tham số thứ 2 là số trường (dữ liệu) sẽ xuất hiện không lấy hết, nếu để trống thì là lấy hết
db.courses.find({
    hours: {
        $gte: 51, //greater than  or equals (lớn hơn hoặc bằng)
        $lte: 200, //letter than  or equals (nhỏ hơn hoặc bằng)
    }
}, {
    price: 1,
    hours: 1
})

// muốn xem nó loại gì, bao nhiêu loại thì dùng distinct nó sẽ xuất ra có bao nhiêu loại và in ra các loại đó
// distinct không trùng
// ví dụ dưới đây giá có nhiều loại, dùng distinct để lọc ra có bao nhiêu giá trong đây.
db.courses.distinct("price")


// có thể nesting viết ví dụ
/**
    tomatoes: {
        viewer: { rating: 5, numReviews: 5},
        ...
    }
*/
// nesting tomatoes > viewer > lấy value rating
db.movie.find({
    "tomatoes.viewer.ratting": 5 
}, {
    tomatoes: 1
})

db.movie.find({
    "tomatoes.viewer.ratting": {
        $gte: 5 //greater than equals
    } 
}, {
    tomatoes: 1
})

//what is the maximum of "imdb.rating"
db.movies.find({
    "tomatoes.viewer.ratting": {
        $exists:true
    }
}).sort({"imdb.rating": -1}).limit(1)


db.movies.find().sort({"tomatoes.viewer.ratting": -1}).limit(1)
// what is the min of "tomatoes.viewer.ratting"
db.movies.find({
    "tomatoes.viewer.ratting": {
        $exists:true
    }
})
.sort({"tomatoes.viewer.ratting": 1}).limit(1)

// sẽ tìm ra đúng bộ phim 1 trong 2 ông này hoặc là cả 2 cùng làm
db.movies.find({
    directors: {
        $in: ["William K.L. Dickson", "Edswin S.Porter"]
    }
}, {
    title: 1,
    year: 1,
    directors: 1
})


db.movies.find({
    directors: {
        $in: ["William K.L. Dickson", "Edswin S.Porter"]
    }
}, {
    title: 1,
    year: 1,
    directors: 1
}).count();
//  đếm số lượng đó


// tìm ra các bộ phim của 1 đạo diễn: sử dụng $size do mongodb cung cấp

db.movies.find({
    directors: {
        $size: 1
    }
}, {
    title: 1,
    year: 1,
    directors: 1
})

// find by id, tìm kiếm thông tin của đối tượng theo _id, tìm kiếm đối tượng thì truyền vào () phải là đối tượng {} và id phải là kiểu ObjectId
db.movies.find({
    _id: ObjectId("573a1390712sdzfewweff31")
})

// caculated fields
db.movies.find({},{
    title: 1,
    year: 1,
    directors: 1,
    numberOfDirectors: {$size:"$directors"}
})

// Skip, limit dùng để làm phân trang => pagination
// Quy tắc phân trang là trang đầu tiên lấy ra 5 phần tử đầu tiên
// trang thứ 2 lấy ra bỏ qua 5 phần tử đầu tiên và lấy ra 5 phần tử tiếp theo
// trang thứ 3 lấy ra bỏ qua 10 phần tử đầu tiên và lấy ra 5 phần tử tiếp theo
// trang thứ 4 lấy ra bỏ qua 15 phần tử đầu tiên và lấy ra 5 phần tử tiếp theo

//trang đầu tiên 
db.movies.find().skip(0).limit(5)
// Nếu mà dữ liệu nhiều quá thì nên giới hạn 1 số trường để lấy ra thui // 1 đại diện là true á
// Trong MongoDB, 1 được sử dụng để chỉ định rằng trường sẽ được hiển thị trong kết quả tìm kiếm. 
// Giá trị 0 được sử dụng để chỉ định rằng trường sẽ không được hiển thị trong kết quả tìm kiếm. nên {title: 1}
db.movies.find({}, {title: 1}).skip(0).limit(5)
//second page
db.movies.find({}, {title: 1}).skip(5).limit(5)
//third page
db.movies.find({}, {title: 1}).skip(10).limit(5)
//third page
db.movies.find({}, {title: 1}).skip(15).limit(5)


// Hàm Aggregate: tổng hợp, đôi lúc tốt hơn hiều find
// Aggregate, something better than "find"
// PIPELINE: giúp Aggregate làm việc theo kiểu tuần tự
// Ví dụ: việc 1 sửa tìm kiếm, việc 2 cập nhật, việc 3..., các giai đoạn phải xong mới qua giai đoạn mới.

//tham số thứ 1 là 1 mảng,
db.movies.aggregate([
    {
        //state1: lấy ví dụ tìm kiếm
        $match: { 
            _id: ObjectId("573a1390712sdzfewweff31")
            
        }
    }, 
    {
        //state 2
        // Nó được sử dụng để chọn các trường cụ thể từ các bản ghi được sắp xếp và sau đó trả về các bản ghi đã chọn.
        $project: {
            // để không hiển thị id
            _id:0, // 1 khi set 0 là id sẽ không hiện
            title: 1,
            year: 1,
            directors: 1
        }
    },
    {
        //state 3
    }
    // ...
]).toArray().length

// lưu ý là count không đi vớiaggregate, mà bạn muốn đếm thì sẽ có cách khác dùng toArray().length

db.movies.aggregate([
    {
        //state1: lấy ví dụ tìm kiếm email, thay vì dùng find
        $match: { 
            email: 'thaituan7820@gmail.com'
        }
    }, 
])

// ngoài ra còn có thể đếm, trước khi in ra

db.movies.aggregate([
    {
        //state1: lấy ví dụ tìm kiếm email, thay vì dùng find
        $match: { 
            email: 'thaituan7820@gmail.com'
        }
    }, 
]).toArray().length

// sử dụng thêm điều kiện and và or

db.movies.aggregate([
    //stage 1: lấy ví dụ tìm kiếm email, thay vì dùng find
    {
        $match: { 
            // Điều kiện và
            $and: [
                    {
                        "imb.votes": 884
                    },
                    {
                        type: 'movie'
                    },
                    {
                        yeaer: 1917
                    }
                ]
        },
    }, 
    //stage 2:
    {
        $project: {
            title: 1,
            year: 1,
            type: 1
        }
    }
])

// cách này chưa hay || lọc ra các bộ phim
db.movies.aggregate([
    //stage 1: lấy ví dụ tìm kiếm email, thay vì dùng find
    {
        $match: { 
            // Điều kiện và
            $and: [
                    {
                        type: 'movie'
                    },
                    {
                        $or: [
                            {
                                year: 1917
                            },
                            {
                                year: 1997
                            }
                        ]
                    }
                ]
        },
    }, 
    //stage 2:
    {
        $project: {
            title: 1,
            year: 1,
            type: 1
        }
    }
])


//lọc ra những bộ phim 1917, 1997 cách tối ưu hơn
db.movies.aggregate([
    //stage 1: lấy ví dụ tìm kiếm email, thay vì dùng find
    {
        $match: { 
            // Điều kiện và
            $and: [
                    {
                        type: 'movie'
                    },
                    {
                       year: {
                           $in: [1917, 1997]
                       }
                    }
                ]
        },
    }, 
    //stage 2:
    {
        $project: {
            title: 1,
            year: 1,
            type: 1
        }
    }
])

// 2. movies có nhiều comments
db.comments.aggregate([
    {
        $group: {
            _id: "$movie_id", //thêm dấu $ để lấy cái biến movie_id comment
            numberOfComments: {
                $count: {} // chỗ này không có điều kiện nào cả, cứ nhìn thấy là lấy
            }
        }
    },
    {
        $lookup: {
            from: "movies",
            localField: "_id",
            foreignField: "_id",
            as: "detailMovie"
        }
    }
])

db.comments.aggregate([
    {
        $match: {
            // không phân biệt hoa thường || * là có hoặc không
            // biểu thức chính quy
            text: /.*Itaque magni.*/i // text contains ...
            text: /^Nilil asp.*/i //    text start with...    
        }
    }    
])


