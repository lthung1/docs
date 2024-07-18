- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Lọc khóa học](#1-lọc-khóa-học)
- [2. Lọc chuyên ngành](#2-lọc-chuyên-ngành)
- [3. Lọc trường](#3-lọc-trường)

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

# 1. Lọc khóa học

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/open-api/course/get-course-by-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6W10sIm5hbWUiOiJoZ3Z4dW4iLCJpc1N1cGVyVXNlciI6ZmFsc2UsImlkIjo4NCwicG9zaXRpb24iOiJpc19xdGh0IiwiZW1haWwiOiJob2FuZ3Z4QGdtYWlsLmNvbSIsImV4cCI6MTcyMTMyNDU4NiwiaWF0IjoxNzIxMjM4MTg2fQ.iKUWGOntkIcHrrsG9ZxuKYhVwUKQT2o2inb95c9Fkcw' \
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
        "id": 6, // mã khóa học
        "name": "Quản trị mạng", // tên khóa học
        "cost": 3000000, // giá
        "avgStar": 2, // đánh giá trung bình
        "assigners": [ // bỏ qua
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 1, // số học sinh ghi danh
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 6,
          "name": "Quản trị mạng",
          "description": "abc1",
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
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận"
          }
        ],
        "completedPercentage": null, // bỏ qua
        "isRegistered": false, // đã đăng ký khóa học chưa
        "isSaved": false // đã lưu khóa học chưa
      },
      {
        "id": 75,
        "name": "Khoa Hoc 9",
        "cost": 3000000,
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
          },
          {
            "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
            "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
            "slug": "NEU",
            "isSponsor": true
          }
        ],
        "totalStudents": 2,
        "industryName": null,
        "publicDate": null,
        "reviewDescription": {
          "id": 75,
          "name": "Khoa Hoc 9",
          "description": "abc1",
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
            "lastName": "ADMIN"
          },
          {
            "id": 16,
            "email": "anhnt@gmail.com",
            "username": "anhnt@gmail.com",
            "firstName": "Ánh",
            "lastName": "Nguyễn Thuận"
          },
          {
            "id": 18,
            "email": "mailt@gmail.com",
            "username": "mailt@gmail.com",
            "firstName": "",
            "lastName": ""
          },
          {
            "id": 38,
            "email": "vantungdeveloper@gmail.com",
            "username": "vantungdeveloper@gmail.com",
            "firstName": "Nguyễn",
            "lastName": "Văn Tùng"
          },
          {
            "id": 40,
            "email": "hakonaryuuj1@gmail.com",
            "username": "hakonaryuuji@gmail.com",
            "firstName": "Nguyễn",
            "lastName": "Trung Quân"
          },
          {
            "id": 49,
            "email": "quanpd.nkg@gmail.com",
            "username": "quanpd.nkg@gmail.com",
            "firstName": "",
            "lastName": ""
          }
        ],
        "completedPercentage": 0,
        "isRegistered": true,
        "isSaved": false
      },
      {
        "id": 218,
        "name": "khoá học test của MN",
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
          "id": 218,
          "name": "khoá học test của MN",
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
            "lastName": "ADMIN"
          }
        ],
        "completedPercentage": null,
        "isRegistered": false,
        "isSaved": false
      }
    ],
    "total": 27
  },
  "message": "Thực hiện thành công"
}
```

# 2. Lọc chuyên ngành

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/open-api/course/get-industry-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6W10sIm5hbWUiOiJoZ3Z4dW4iLCJpc1N1cGVyVXNlciI6ZmFsc2UsImlkIjo4NCwicG9zaXRpb24iOiJpc19xdGh0IiwiZW1haWwiOiJob2FuZ3Z4QGdtYWlsLmNvbSIsImV4cCI6MTcyMTMyNDU4NiwiaWF0IjoxNzIxMjM4MTg2fQ.iKUWGOntkIcHrrsG9ZxuKYhVwUKQT2o2inb95c9Fkcw' \
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
      "id": 1,
      "code": "7140101",
      "name": "Giáo dục học",
      "count": 67
    },
    {
      "id": 2,
      "code": "7140111",
      "name": "Công nghệ giáo dục",
      "count": 68
    },
    {
      "id": 3,
      "code": "7140114",
      "name": "Quản lý giáo dục",
      "count": 58
    },
    {
      "id": 4,
      "code": "7140199",
      "name": "Kinh tế Giáo dục",
      "count": 33
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 3. Lọc trường

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/open-api/course/get-university-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6W10sIm5hbWUiOiJoZ3Z4dW4iLCJpc1N1cGVyVXNlciI6ZmFsc2UsImlkIjo4NCwicG9zaXRpb24iOiJpc19xdGh0IiwiZW1haWwiOiJob2FuZ3Z4QGdtYWlsLmNvbSIsImV4cCI6MTcyMTMyNDU4NiwiaWF0IjoxNzIxMjM4MTg2fQ.iKUWGOntkIcHrrsG9ZxuKYhVwUKQT2o2inb95c9Fkcw' \
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
      "uuid": "84b44910479d4f5486c8a44f4b37cc10",
      "name": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
      "count": 9,
      "slug": "HANU"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37cc12",
      "name": "ĐẠI HỌC QUỐC GIA HÀ NỘI",
      "count": 4,
      "slug": "VNU"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37cc13",
      "name": "TRƯỜNG ĐẠI HỌC XÂY DỰNG HÀ NỘI",
      "count": 6,
      "slug": "HUCE"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37cc17",
      "name": "TRƯỜNG ĐẠI HỌC KINH TẾ KỸ THUẬT CÔNG NGHIỆP",
      "count": 4,
      "slug": "KTKTCN"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
      "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
      "count": 140,
      "slug": "NEU"
    },
    {
      "uuid": "84b44910479d4f5486c8a44f4b37ccd8",
      "name": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
      "count": 33,
      "slug": "HUST"
    }
  ],
  "message": "Thực hiện thành công"
}
Response headers
```