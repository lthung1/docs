- [1. API xuất bản khoá học màn xây dựng nội dung](#1-api-xuất-bản-khoá-học-màn-xây-dựng-nội-dung)

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