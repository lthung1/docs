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
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjQyMTgyMiwiaWF0IjoxNzIyMzM1NDIyfQ.itCePC5J-hikx9dtB2DT72dc6T5adspAXZvpjq8lJII' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "name,asc", "id,desc"
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
        "name": "123213123123123123",
        "id": 261
      },
      {
        "name": "132132131",
        "id": 257
      },
      {
        "name": "1asdasdsa",
        "id": 166
      },
      {
        "name": "aaaaaaa",
        "id": 145
      },
      {
        "name": "aaaaaaaaaa",
        "id": 185
      },
      {
        "name": "abccxz",
        "id": 152
      },
      {
        "name": "cecececececececeeccde ",
        "id": 165
      },
      {
        "name": "Certificate 1",
        "id": 292
      },
      {
        "name": "cho nó chácw",
        "id": 163
      },
      {
        "name": "cstunggggggggggggggg",
        "id": 187
      }
    ],
    "pageable": {
      "pageNumber": 0,
      "pageSize": 10,
      "sort": [
        {
          "direction": "ASC",
          "property": "name",
          "ignoreCase": false,
          "nullHandling": "NATIVE",
          "descending": false,
          "ascending": true
        },
        {
          "direction": "DESC",
          "property": "id",
          "ignoreCase": false,
          "nullHandling": "NATIVE",
          "descending": true,
          "ascending": false
        }
      ],
      "offset": 0,
      "unpaged": false,
      "paged": true
    },
    "totalPages": 15,
    "totalElements": 146,
    "last": false,
    "size": 10,
    "number": 0,
    "sort": [
      {
        "direction": "ASC",
        "property": "name",
        "ignoreCase": false,
        "nullHandling": "NATIVE",
        "descending": false,
        "ascending": true
      },
      {
        "direction": "DESC",
        "property": "id",
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