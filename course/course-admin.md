- [1. API xuất bản khoá học màn xây dựng nội dung](#1-api-xuất-bản-khoá-học-màn-xây-dựng-nội-dung)
- [2. API lấy ra danh sách khoá học của giảng viên](#2-api-lấy-ra-danh-sách-khoá-học-của-giảng-viên)

# 1. API xuất bản khoá học màn xây dựng nội dung

* note : API này sẽ xuất bản cả trang nội dung và trang trình bày của khoá học

> request
```json
curl --location --request PUT 'https://be.moooc.xyz/v2/api/mooc-courses/publish' \
--header 'accept: */*' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgyMDI5MTYsImV4cCI6MTcxODI4OTMxNn0.E8ksRD0MhIWWvs50p34KsXeFJxXJwBI6fa6bZCFyQ5Q' \
--data '{
  "courseIds": [
    1234 , 2345
  ]
}'
```

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| courseIds  | y         | arr     | mảng mã khoá học  |


> response

```json
{
  "success": true,
  "data": null,
  "message": "Thực hiện thành công"
}
```

# 2. API lấy ra danh sách khoá học của giảng viên

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course-student-register/get-course-list' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjY3MTMzNCwiaWF0IjoxNzIyNTg0OTM0fQ.9dTj57Ry3GkCB_4PzlcIsbYKLzTKo120K1MqiBAYFGE' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "id,desc", "name,desc"
  ],
  "keyword": "1"
}'
```

> response

```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 357,
        "name": "Khóa học chơi daxua 15ff (Bản sao) (Bản sao)",
        "enterpriseName": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
        "image": null,
        "code": "KH_0fdb46bb7460"
      },
      {
        "id": 356,
        "name": "Khóa học chơi daxua 15ff (Bản sao)",
        "enterpriseName": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
        "image": null,
        "code": "KH_a61f1ad72bf7"
      },
      {
        "id": 348,
        "name": "Khóa học chơi daxua 15ff",
        "enterpriseName": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
        "image": null,
        "code": "GPMN1975"
      },
      {
        "id": 340,
        "name": "test12312312345",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "test12312312345"
      },
      {
        "id": 324,
        "name": "Khoa hoc hungtest113y",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas113h"
      },
      {
        "id": 323,
        "name": "Khoa hoc hungtest113",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas113"
      },
      {
        "id": 321,
        "name": "Khoa hoc hungtest11338",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas11338ww"
      },
      {
        "id": 320,
        "name": "Khoa hoc hungtest11338",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas11338"
      },
      {
        "id": 319,
        "name": "Khoa hoc hungtest1133",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas1133"
      },
      {
        "id": 318,
        "name": "Khoa hoc hungtest11",
        "enterpriseName": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "image": null,
        "code": "323rdas11"
      }
    ],
    "pageable": {
      "pageNumber": 0,
      "pageSize": 10,
      "sort": [
        {
          "direction": "DESC",
          "property": "id",
          "ignoreCase": false,
          "nullHandling": "NATIVE",
          "descending": true,
          "ascending": false
        },
        {
          "direction": "DESC",
          "property": "name",
          "ignoreCase": false,
          "nullHandling": "NATIVE",
          "descending": true,
          "ascending": false
        }
      ],
      "offset": 0,
      "paged": true,
      "unpaged": false
    },
    "totalPages": 15,
    "totalElements": 148,
    "last": false,
    "size": 10,
    "number": 0,
    "sort": [
      {
        "direction": "DESC",
        "property": "id",
        "ignoreCase": false,
        "nullHandling": "NATIVE",
        "descending": true,
        "ascending": false
      },
      {
        "direction": "DESC",
        "property": "name",
        "ignoreCase": false,
        "nullHandling": "NATIVE",
        "descending": true,
        "ascending": false
      }
    ],
    "numberOfElements": 10,
    "first": true,
    "empty": false
  },
  "message": "Thực hiện thành công"
}
```