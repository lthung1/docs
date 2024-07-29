- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Tìm kiếm thông báo](#1-tìm-kiếm-thông-báo)
- [2. Đếm số thông báo chưa xem](#2-đếm-số-thông-báo-chưa-xem)
- [3. Cập nhật thông báo thành đã xem, chưa xem](#3-cập-nhật-thông-báo-thành-đã-xem-chưa-xem)
- [4. Đánh dấu đã xem tất cả thông báo](#4-đánh-dấu-đã-xem-tất-cả-thông-báo)
- [5. Xóa thông báo](#5-xóa-thông-báo)
- [6. Xóa tất cả thông báo](#6-xóa-tất-cả-thông-báo)


# 0. Một số chú thích ban đầu

# 1. Tìm kiếm thông báo

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/search-notification' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "keyword": "hehe",
  "isViewed": true,
  "createdFrom": "2024-07-18T00:24:44.667Z",
  "createdTo": "2024-07-18T00:24:44.667Z",
  "createdSort": "asc"
}'
```

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | n         | int     | trang  |
| size  | n         | int     | cỡ  |
| keyword  | n         | string     | từ khóa  |
| isViewed  | n         | boolean     | đã xem chưa?  |
| createdFrom  | n         | date     | ngày gửi từ  |
| createdTo  | n         | date     | ngày gửi đến|
| createdSort  | n         | string     | sắp xếp|

> output

```json
{
  "content": [
    {
      "id": 108,
      "created": "2024-07-17T08:12:48Z",
      "message": "<p>Phục ma ngự trù tử</p>",
      "isViewed": false,
      "senderName": "Hệ thống",
      "title": "Thông báo hệ thôgns",
      "sentDate": "2024-07-17T09:04:55Z",
      "attachments": []
    },
    {
      "id": 107,
      "created": "2024-07-17T07:11:40Z",
      "message": "<p>Gửi thông báo</p>",
      "isViewed": true,
      "senderName": "Hệ thống",
      "title": "dsfsadgfsadfgsdf",
      "sentDate": "2024-07-17T08:21:43Z",
      "attachments": []
    },
    {
      "id": 106,
      "created": "2024-07-17T06:44:30Z",
      "message": "<p>Thông báo gửi tới một số đối tượng</p>",
      "isViewed": false,
      "senderName": "Hệ thống",
      "title": "thêm thông báo",
      "sentDate": "2024-07-17T07:28:41Z",
      "attachments": []
    },
    {
      "id": 105,
      "created": "2024-07-17T06:31:07Z",
      "message": "<p>đây là nội dung thông báo</p>",
      "isViewed": false,
      "senderName": "Hệ thống",
      "title": "Thêm mới thông báo",
      "sentDate": "2024-07-17T06:42:00Z",
      "attachments": []
    }
  ],
  "pageable": {
    "pageNumber": 0,
    "pageSize": 10,
    "sort": [
      {
        "direction": "DESC",
        "property": "created",
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
  "totalElements": 4,
  "totalPages": 1,
  "last": true,
  "size": 10,
  "number": 0,
  "sort": [
    {
      "direction": "DESC",
      "property": "created",
      "ignoreCase": false,
      "nullHandling": "NATIVE",
      "descending": true,
      "ascending": false
    }
  ],
  "numberOfElements": 4,
  "first": true,
  "empty": false
}
```

# 2. Đếm số thông báo chưa xem

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/count-unviewed' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```

> output

```json
{
  "success": true,
  "data": 3,
  "message": "Thực hiện thành công"
}
```

# 3. Cập nhật thông báo thành đã xem, chưa xem

> curl

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/edit-notification-viewed/1?isViewed=true' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjMxMzg1MiwiaWF0IjoxNzIyMjI3NDUyfQ.4tuCcK-idl3w1xk74S1F0Q-F-Gvx4M_rliUqL1HXlQY'
```

* truyền vào notificationId, isViewed(đã xem chưa)

# 4. Đánh dấu đã xem tất cả thông báo

> curl

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/edit-all-notifications-viewed' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```

# 5. Xóa thông báo

> curl

```json
curl -X 'DELETE' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/delete-notification/105' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```

* truyền vào notificationId

# 6. Xóa tất cả thông báo

> curl

```json
curl -X 'DELETE' \
  'https://be.moooc.xyz/v2/api/mooc-notifications/delete-all-notifications' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJjYXNjYWNhY3NjMTIzMjEiXSwibmFtZSI6ImVkeCIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjEzNDY4NzQsImlhdCI6MTcyMTI2MDQ3NH0.ducr8ImAxh4crJlNzH8I8Eiv4_CmL0bnPn0wi0WuzqQ'
```