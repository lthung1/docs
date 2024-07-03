- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API lấy ra danh sách khoá học của tôi](#1-api-lấy-ra-danh-sách-khoá-học-của-tôi)
- [2. API tìm kiếm lịch](#2-api-tìm-kiếm-lịch)
- [3. API cài đặt lịch](#3-api-cài-đặt-lịch)
- [4. API lấy thông tin cài đặt lịch](#4-api-lấy-thông-tin-cài-đặt-lịch)
# 0. Một số chú thích ban đầu
<h2>Phần xem bài tập, kiểm tra, thi</h2>

>type loại lịch

| Type   | Chú thích |
|-------------| --------- |
|0| Lịch học |
|1| Lịch bài tập |
|2| Lịch kiểm tra |
|3| Lịch thi |
|#N/A| Lịch học thêm |

<hr/>

<h2>Phần cài đặt cấu hình lịch</h2>

> type định dạng ngày

| Type   | Chú thích |
|-------------| --------- |
|1| dd/mm/yyyy |
|2| yyyy/mm/dd |
|3| mm/dd/yyyy |

> type định dạng giờ

| Type   | Chú thích |
|-------------| --------- |
|1| 24 giờ |
|2| 12 giờ |

> Type định dạng đại lượng thời gian

| Type   | Chú thích |
|-------------| --------- |
|1| phút |
|2| giờ |
|3| giây |
|4| tuần |
|5| tháng |

> Type lựa chọn "Thời gian thông báo" => selectedOption

| Type   | Chú thích |
|-------------| --------- |
|1| Trước 01 tuần |
|2| Trước 01 ngày |
|3| Trước 01 giờ |
|4| Tuỳ chọn |

# 1. API lấy ra danh sách khoá học của tôi

>use case tương ứng : UC920

> curl 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/my-registration/get-all-my-course?page=1&size=10' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NTg3MzUsImV4cCI6MTcxOTU0NTEzNX0.GaOeAfllwK5tbOFQiE80BBq5sWPW21MFk7qSJhRxc-Q'
```
> request

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | n         | int     | trang số  |mặc định là 1|
| size  | n         | int     | size 1 trang  |mặc định là số rất lớn|

> response 

```json
{
  "success": true,
  "data": [
    {
      "name": "Kĩ năng sống1",
      "id": 96
    },
    {
      "name": "testCCQuanNgheo (Bản sao)",
      "id": 106
    },
    {
      "name": "hihihihihihihihih",
      "id": 109
    },
    {
      "name": "zoozoozooozoooz1234",
      "id": 114
    },
    {
      "name": "Zo it thoi",
      "id": 115
    },
    {
      "name": "testChinhBan",
      "id": 188
    },
    {
      "name": "zxczxczxczxc",
      "id": 189
    },
    {
      "name": "khoá học 1112",
      "id": 193
    },
    {
      "name": "Khóa học",
      "id": 205
    },
    {
      "name": "Khoa hoc Test 0001",
      "id": 242
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 2. API tìm kiếm lịch

> use case tương ứng : 920 -> 927

> curl 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/study/schedule-search' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NTg3MzUsImV4cCI6MTcxOTU0NTEzNX0.GaOeAfllwK5tbOFQiE80BBq5sWPW21MFk7qSJhRxc-Q' \
  -H 'Content-Type: application/json' \
  -d '{
  "courseId": 3,
  "scheduleTypes": [
    
  ],
  "keyword": "",
  "dateFrom": "2024-01-01T08:22:45.282Z",
  "dateTo": "2024-12-27T08:22:45.282Z"
}'
```

> request

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| courseId  | y         | int     | id khoá học  |0. tất cả|
| scheduleTypes  | n    | int[]     | loại lịch  |xem lại mục #0 ,lấy tất cả khi không truyền lên|
| keyword  | n    | string     | từ khoá  ||
| dateFrom  | y    | date     | ngày bắt đầu  ||
| dateTo  | y    | date     | ngày kết thúc  ||

> response 

```json
{
  "success": true,
  "data": [
    {
      "id": 2357, // unitId
      "blockId": 898,
      "courseId": 3,
      "start": "2024-06-08T00:00:00Z",
      "end": "2024-08-03T00:00:00Z",
      "title": "Hóa học vô cơ",
      "type": 1
    },
    {
      "id": 2358, 
      "blockId": 899,
      "courseId": 3,
      "start": "2024-06-07T00:00:00Z",
      "end": "2024-08-10T00:00:00Z",
      "title": "Hóa học hữu cơ",
      "type": 2
    },
    {
      "id": 2359,
      "blockId": 900,
      "courseId": 3,
      "start": "2024-06-28T00:00:00Z",
      "end": "2024-08-03T00:00:00Z",
      "title": "Bài tập điện phân",
      "type": 3
    },
    {
      "id": 2360,
      "blockId": 901,
      "courseId": 3,
      "start": "2024-06-08T00:00:00Z",
      "end": "2024-07-11T00:00:00Z",
      "title": "Giao động điều hòa ",
      "type": 1
    },
    {
      "id": 2361,
      "blockId": 902,
      "courseId": 3,
      "start": "2024-06-12T00:00:00Z",
      "end": "2024-07-28T00:00:00Z",
      "title": "Phản ứng hạt nhân",
      "type": 2
    },
    {
      "id": 2362,
      "blockId": 903,
      "courseId": 3,
      "start": "2024-06-05T00:00:00Z",
      "end": "2024-08-11T00:00:00Z",
      "title": "Sóng ánh sáng",
      "type": 3
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 3. API cài đặt lịch

> use case tương ứng : 920

> curl 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/study/schedule-config/config' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk5NzMzODIsImV4cCI6MTcyMDA1OTc4Mn0.itSfyAWQpdFQOCCxra7-VSvpltuT19PNrybr3IbkObQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "dateForm": 1,
  "timeForm": 3,
  "notifyStudy": true,
  "notifyTest": true,
  "notifyExercise": true,
  "notifyExam": true,
  "notifyLearnMore": false,
  "timeLimitBefore": null,
  "timeTypeBefore": null,
  "selectedOption": 4
}'
}'
```

> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| dateForm  | y         | int     | định dạng ngày  ||
| timeForm  | y    | int     | định dạng giờ  ||
| notifyStudy  | y    | boolean     | thông báo lịch học  ||
| notifyTest  | y    | boolean     | thông báo lịch kiểm tra  ||
| notifyExercise  | y    | boolean     | thông báo lịch bài tập  ||
| notifyExam  | y    | boolean     | thông báo lịch thi  ||
| notifyLearnMore  | y    | boolean     | thông báo lịch học thêm ||
| timeLimitBefore  | y    | int | số đại lượng thời gian nhận thông báo trước ||
| timeTypeBefore  | y    | int | đại lượng thời gian nhận thông báo trước ||
| selectedOption  | y    | int | lưu trữ lựa chọn mục "Thời gian thông báo" | xem lại mục #0|

(xem lại mục #0 để xem hằng số)

# 4. API lấy thông tin cài đặt lịch

> use case tương ứng : 920

> curl 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course/structure/study/schedule-config' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTkzOTA2NjYsImV4cCI6MTcxOTQ3NzA2Nn0.oQpuWZjAlodGj0FiEMdMSdyOaXfOpxhGlhVjFpoltZY'
```

> response

```json
{
  "success": true,
  "data": {
    "id": 2,
    "userId": 4,
    "dateForm": 1,
    "timeForm": 3,
    "notifyStudy": true,
    "notifyExercise": true,
    "notifyTest": true,
    "notifyExam": true,
    "notifyLearnMore": false,
    "timeLimitBefore": null,
    "timeTypeBefore": null,
    "selectedOption": 4 // xem lại mục #0
  },
  "message": "Thực hiện thành công"
}

//xem lại mục #0
```