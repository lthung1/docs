- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Lọc khóa học đã lưu](#1-lọc-khóa-học-đã-lưu)
- [2. Lọc trường có khóa học đã lưu](#2-lọc-trường-có-khóa-học-đã-lưu)
- [3. Lọc chuyên ngành có khóa học đã lưu](#3-lọc-chuyên-ngành-có-khóa-học-đã-lưu)
- [4. Lưu khóa học](#4-lưu-khóa-học)
- [5. Bỏ lưu khóa học](#5-bỏ-lưu-khóa-học)

# 0. Một số chú thích ban đầu
> giải thích payload bộ lọc chung

* giải thích

```json
{
  "keyword": "string", // từ khóa tìm kiếm
  "industryGroup": 0, // bỏ qua
  "universities": [ // uuid của trường
    "string"
  ],
  "industries": [ // mã chuyên ngành
    0
  ],
  "stars": [ // bộ lọc sao 
    0        // lọc trở lên, truyền số dương. Lọc trở xuống, số âm
  ],         // VD: Từ 4 sao (4), Dưới 2 sao (-2)
  "isFreeOptions": [
    0        // 0. miễn phí  - 1. trả phí
  ],
  "minCost": 0, // giá nhỏ nhất
  "maxCost": 0, // giá lớn nhất
  "courseScheduleType": [ // lịch trình học
    true       // Theo giảng viên (true), theo lịch trình (false)
  ],
  "courseType": [ // loại khóa học
    0         // Tự do ghi danh (3)
  ],          // Thẻ ghi danh (1)
  "sortByName": "asc", // asc hoặc desc
  "sortByCreatedAt": "desc", // asc hoặc desc
  "page": 1,
  "size": 1,
  "minStar": 0, // bỏ qua
  "maxStar": 0 // bỏ qua
}
```

* ví dụ

```json
{
  "keyword": "học",
  "universities": [
    "uuid1", "uuid2"
  ],
  "industries": [
    1, 2
  ],
  "stars": [
    4, -2
  ],
  "isFreeOptions": [
    0, 1
  ],
  "minCost": 1,
  "maxCost": 100,
  "courseScheduleType": [
    true, false
  ],
  "courseType": [
    1, 3
  ],
  "sortByName": "asc",
  "sortByCreatedAt": "desc",
  "page": 1,
  "size": 10
}
```

> Theo nghiệp vụ, khi ghi danh khóa học, nếu khóa học đó đã lưu thì sẽ xóa lưu đi. Trong trường hợp test lưu khóa học với api, nếu khóa học đó mà người đăng nhập đã đăng ký, cần call api xóa lưu để data về đúng nghiệp vụ

# 1. Lọc khóa học đã lưu

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/my-interest/search-saved-courses' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "string",
  "industryGroup": 0,
  "universities": [
    "string"
  ],
  "industries": [
    0
  ],
  "stars": [
    0
  ],
  "isFreeOptions": [
    0
  ],
  "minCost": 0,
  "maxCost": 0,
  "courseScheduleType": [
    true
  ],
  "courseType": [
    0
  ],
  "sortByName": "string",
  "sortByCreatedAt": "string",
  "page": 1,
  "size": 1,
  "minStar": 0,
  "maxStar": 0
}'
```

> output

```json
{
  "success": true,
  "data": {
    "courses": [
      {
        "id": 229, // mã khóa học
        "name": "khoahoctest10", // tên khóa học
        "cost": 0, // giá
        "avgStar": null, // đánh giá trung bình
        "assigners": [ // bỏ qua
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0, // tổng số học sinh ghi danh
        "industryName": null, // bỏ qua
        "publicDate": "2024-05-30T09:37:39.879782Z", // bỏ qua
        "reviewDescription": { // bỏ qua
          "id": 229,
          "name": "khoahoctest10",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null, // ảnh khóa học
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7", // mã trường
        "slug": "NEU", // tên tắt trường
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN", // tên trường
        "completedTime": 0, // tổng số giờ
        "teachers": [ // giảng viên
          {
            "id": 4,
            "email": "edx@example.com",
            "username": "edx",
            "firstName": "",
            "lastName": "ADMIN",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$+Tfknk9TPpqsZRXME7j+C8McOYJU0HqeA7YsSPlzcJM=",
            "passwordRetryCount": 1,
            "isSuperUser": true,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T04:04:17.020139Z",
            "lastLogin": "2024-07-17T08:26:07.875931Z"
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 212,
        "name": "Khoa họic âsa",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 212,
          "name": "Khoa họic âsa",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 1,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:53:10.050Z",
            "lastLogin": null
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 210,
        "name": "Khoa hoc temp",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37cc12",
            "name": "ĐẠI HỌC QUỐC GIA HÀ NỘI",
            "slug": "VNU",
            "isSponsor": false
          },
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 210,
          "name": "Khoa hoc temp",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 1,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:53:10.050Z",
            "lastLogin": null
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 1,
        "name": "Lập trình hướng đối tượng",
        "cost": 0,
        "avgStar": 2.5,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 1,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 1,
          "name": "Lập trình hướng đối tượng",
          "description": "cscscscscsc",
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 215,
        "name": "Khoa hoc 11111",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 215,
          "name": "Khoa hoc 11111",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 18,
            "email": "mailt@gmail.com",
            "username": "mailt@gmail.com",
            "firstName": "",
            "lastName": "",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 0,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:54:14.821Z",
            "lastLogin": "2024-03-08T04:16:09.357701Z"
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 216,
        "name": "Khoá học test Duyệt",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 216,
          "name": "Khoá học test Duyệt",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 1,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:53:10.050Z",
            "lastLogin": null
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 128,
        "name": "Khoa Hoc 5666666666666 (Bản sao) (Bản sao)",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd8",
            "name": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
            "slug": "HUST",
            "isSponsor": false
          },
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 128,
          "name": "Khoa Hoc 5666666666666 (Bản sao) (Bản sao)",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 1,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:53:10.050Z",
            "lastLogin": null
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 105,
        "name": "QuanIsRich",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 105,
          "name": "QuanIsRich",
          "description": "test2",
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$3LvHwMnv5+rGJipASsjG1rEhPrC3TgTBUwJOPdVNW8o=",
            "passwordRetryCount": 1,
            "isSuperUser": false,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T09:53:10.050Z",
            "lastLogin": null
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 226,
        "name": "khoahoctest7",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 226,
          "name": "khoahoctest7",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 4,
            "email": "edx@example.com",
            "username": "edx",
            "firstName": "",
            "lastName": "ADMIN",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$+Tfknk9TPpqsZRXME7j+C8McOYJU0HqeA7YsSPlzcJM=",
            "passwordRetryCount": 1,
            "isSuperUser": true,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T04:04:17.020139Z",
            "lastLogin": "2024-07-17T08:26:07.875931Z"
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      },
      {
        "id": 225,
        "name": "khoahoctest6",
        "cost": 0,
        "avgStar": null,
        "assigners": [
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 0,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 225,
          "name": "khoahoctest6",
          "description": null,
          "slug": null,
          "universityName": null,
          "completedTime": 0
        },
        "thumbnailUrl": null,
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "slug": "NEU",
        "universityName": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "completedTime": 0,
        "teachers": [
          {
            "id": 4,
            "email": "edx@example.com",
            "username": "edx",
            "firstName": "",
            "lastName": "ADMIN",
            "isActive": true,
            "password": "pbkdf2_sha256$600000$HXwHPI8v2YsLojbYHuILJC$+Tfknk9TPpqsZRXME7j+C8McOYJU0HqeA7YsSPlzcJM=",
            "passwordRetryCount": 1,
            "isSuperUser": true,
            "isDeleted": false,
            "isStaff": true,
            "dateJoined": "2024-03-01T04:04:17.020139Z",
            "lastLogin": "2024-07-17T08:26:07.875931Z"
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": true
      }
    ],
    "total": 13
  },
  "message": "Thực hiện thành công"
}
```
# 2. Lọc trường có khóa học đã lưu

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/my-interest/get-saved-enterprises' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "string",
  "industryGroup": 0,
  "universities": [
    "string"
  ],
  "industries": [
    0
  ],
  "stars": [
    0
  ],
  "isFreeOptions": [
    0
  ],
  "minCost": 0,
  "maxCost": 0,
  "courseScheduleType": [
    true
  ],
  "courseType": [
    0
  ],
  "sortByName": "string",
  "sortByCreatedAt": "string",
  "page": 1,
  "size": 1,
  "minStar": 0,
  "maxStar": 0
}'
```

> output

```json
{
  "success": true,
  "data": [
    {
      "uuid": "84b44910479d4f5486c8a44f4b37cc12",
      "name": "ĐẠI HỌC QUỐC GIA HÀ NỘI",
      "count": 1,
      "slug": "VNU"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
      "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
      "count": 13,
      "slug": "NEU"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37ccd8",
      "name": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
      "count": 1,
      "slug": "HUST"
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 3. Lọc chuyên ngành có khóa học đã lưu

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/my-interest/get-saved-industries' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "string",
  "industryGroup": 0,
  "universities": [
    "string"
  ],
  "industries": [
    0
  ],
  "stars": [
    0
  ],
  "isFreeOptions": [
    0
  ],
  "minCost": 0,
  "maxCost": 0,
  "courseScheduleType": [
    true
  ],
  "courseType": [
    0
  ],
  "sortByName": "string",
  "sortByCreatedAt": "string",
  "page": 1,
  "size": 1,
  "minStar": 0,
  "maxStar": 0
}'
```

> output

```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "code": "7140101",
        "name": "Giáo dục học",
        "count": 9
      },
      {
        "id": 2,
        "code": "7140111",
        "name": "Công nghệ giáo dục",
        "count": 3
      },
      {
        "id": 3,
        "code": "7140114",
        "name": "Quản lý giáo dục",
        "count": 1
      },
      {
        "id": 7,
        "code": "7140203",
        "name": "Giáo dục Đặc biệt",
        "count": 1
      },
      {
        "id": 13,
        "code": "7140209",
        "name": "Sư phạm Toán học",
        "count": 1
      }
    ],
    "pageable": {
      "pageNumber": 0,
      "pageSize": 10,
      "sort": [],
      "offset": 0,
      "paged": true,
      "unpaged": false
    },
    "totalElements": 5,
    "totalPages": 1,
    "last": true,
    "size": 10,
    "number": 0,
    "sort": [],
    "numberOfElements": 5,
    "first": true,
    "empty": false
  },
  "message": "Thực hiện thành công"
}
```

# 4. Lưu khóa học

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course/my-interest/create-saved-course/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```

* truyền vào courseId

# 5. Bỏ lưu khóa học

> curl

```json
curl -X 'DELETE' \
  'https://be.moooc.xyz/v2/api/course/my-interest/delete-saved-course/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```

* truyền vào courseId