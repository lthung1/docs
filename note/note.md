- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API lấy ra danh sách ghi chú](#1-api-lấy-ra-danh-sách-ghi-chú)
- [2. API tìm kiếm ghi chú](#2-api-tìm-kiếm-ghi-chú)
- [3. API lấy ra chương của khóa học](#3-api-lấy-ra-chương-của-khóa-học)
- [4. API lấy ra bài giảng của chương](#4-api-lấy-ra-bài-giảng-của-chương)
- [5. API lấy ra học liệu của bài giảng](#5-api-lấy-ra-học-liệu-của-bài-giảng)
- [6. API tạo mới ghi chú](#6-api-tạo-mới-ghi-chú)
- [7. API ghim, bỏ ghim ghi chú](#7-api-ghim-bỏ-ghim-ghi-chú)
- [8. API xóa ghi chú](#8-api-xóa-ghi-chú)
- [9. API cập nhật ghi chú](#9-api-cập-nhật-ghi-chú)
- [10. API xem danh sách ghi chú](#10-api-xem-danh-sách-ghi-chú)
- [11. API xem lịch sử ghi chú](#11-api-xem-lịch-sử-ghi-chú)

# 0. Một số chú thích ban đầu
# 1. API lấy ra danh sách ghi chú

> use case tương ứng : 906

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/get-by-id/42' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbImdoYURTSEdKSEpTREEiXSwiaWF0IjoxNzE4Nzg0MzYxLCJleHAiOjE3MTg3ODc5NjF9.PREZ_GX6ssIYOKuJkakEQmVzJShzJh2uC0tJAcBTxkY'
```

> input :

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id ghi chú  |path|

> output :

```json
{
  "success": true,
  "data": {
    "id": 42,
    "unitId": 1874,
    "courseId": 129,
    "studentUserId": 4,
    "title": "ghi chus cho van ban",
    "content": "chu gi",
    "isOfWholeUnit": false,
    "isPinned": false,
    "documentPosition": null,
    "markerText": null,
    "markerTextStart": null,
    "markerTextEnd": null,
    "videoPositionStart": 0,
    "videoPositionEnd": 0,
    "createdDate": "2024-06-05T11:20:14Z",
    "updatedDate": null,
    "attachments": [
      {
        "id": 68,
        "mainKey": "student-unit-note/e49628a7-2ab1-4dba-ace2-344a0340973d956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm (1).docx",
        "fileName": "956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm (1).docx",
        "attachmentType": "word"
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

> explain output :

* isOfWholeUnit (boolean): ghi chú có phải của toàn bộ học liệu không
* isPinned (boolean): ghi chú có đang được ghim không
* documentPosition (string): vị trí của học liệu (ví dụ: trang thứ mấy của học liệu)
* markerText(string): nội dung ghi chú của học liệu text
* markerTextStart (int): vị trí kí tự bắt đầu của vùng được ghi chú so với học liệu.
* markerTextEnd (int): vị trí kí tự kết thúc của vùng được ghi chú so với học liệu.
* videoPositionStart (int): Vị trí thời gian bắt đầu của học liệu video (tính bằng giây)
* videoPositionEnd (int): Vị trí thời gian kết thúc của học liệu video (tính bằng giây)

# 2. API tìm kiếm ghi chú

> use case tương ứng : 907

> curl: 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/get-by-conditions' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbImdoYURTSEdKSEpTREEiXSwiaWF0IjoxNzE4Nzg0MzYxLCJleHAiOjE3MTg3ODc5NjF9.PREZ_GX6ssIYOKuJkakEQmVzJShzJh2uC0tJAcBTxkY' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "",
  "courseId": 129,
  "unitId": 1874,
  "sectionId": 284,
  "sequenceId": 317,
  "sortByName": "asc",
  "sortByCreateDate": "desc",
  "createdFromDate": "",
  "page": 1,
  "size": 10,
  "createdToDate": ""
}'
```

> input :

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| keyword  | n         | string     | từ khóa tìm kiếm  ||
| courseId  | n         | int     | id khóa học  ||
| unitId  | n         | int     | id học liệu  ||
| sectionId  | n         | int     | id chương  ||
| sequenceId  | n         | int     | id bài giảng  ||
| sortByName  | n         | string     |sắp xếp theo tên |asc/desc|
| sortByCreateDate  | n | string|sắp xếp theo ngày|asc/desc|
| createdFromDate  | n | date|ngày tạo từ||
| createdToDate  | n | date|ngày tạo đến||
| page  | n | int|trang số||
| size  | n | int|số lượng 1 trang||

> output :

```json
{
  "success": true,
  "data": {
    "count": 4,
    "total": 4,
    "notes": [
      {
        "id": 76,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "",
        "content": "",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "i và loài mèo dẫn tới việc nó thường được khắc họa trong các truyền thuyết và thần thoại tại nhiều nền văn hoá, gồm truyền thuyết và thần thoại Ai Cập cổ, Trung Quốc cổ, Na Uy cổ, và vị Vua xứ Wales thời Trung Cổ Hywel Dda (người Tử tế) đã thông qua bộ luật bảo vệ động vật đầu tiên trên thế giới bằng cách coi hành động giết hại hay làm tổn hại tới mèo là vi phạm pháp luật, với những hình phạt nặng nề cho những kẻ vi phạm. Tuy nhiên, mèo thỉnh thoảng bị coi là ma quỷ và có 9 mạng, ví dụ như nó không mang lại may mắn hay thường đi liền với những ",
        "markerTextStart": 1222,
        "markerTextEnd": 1772,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T07:08:58Z",
        "updatedDate": null,
        "attachments": []
      },
      {
        "id": 70,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "",
        "content": "",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "",
        "markerTextStart": 0,
        "markerTextEnd": 0,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T04:05:23Z",
        "updatedDate": null,
        "attachments": []
      },
      {
        "id": 42,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "ghi chus cho van ban",
        "content": "chu gi",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": null,
        "markerTextStart": null,
        "markerTextEnd": null,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-05T11:20:14Z",
        "updatedDate": null,
        "attachments": [
          {
            "id": 68,
            "mainKey": "https://s3.moooc.xyz/dev-stable/student-unit-note/e49628a7-2ab1-4dba-ace2-344a0340973d956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm%20%281%29.docx?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240619T090051Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240619%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=34eb6d82bcf255f99547caab4a12159ce8ff7563f76e2b835d53f49225fffa8c",
            "fileName": "956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm (1).docx",
            "attachmentType": "word"
          }
        ]
      },
      {
        "id": 75,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "vùng chọn",
        "content": "chọn vùng",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "",
        "markerTextStart": 0,
        "markerTextEnd": 0,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T07:02:07Z",
        "updatedDate": null,
        "attachments": []
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

> explain output :

* isOfWholeUnit (boolean): ghi chú có phải của toàn bộ học liệu không
* isPinned (boolean): ghi chú có đang được ghim không
* documentPosition (string): vị trí của học liệu (ví dụ: trang thứ mấy của học liệu)
* markerText(string): nội dung ghi chú của học liệu text
* markerTextStart (int): vị trí kí tự bắt đầu của vùng được ghi chú so với học liệu.
* markerTextEnd (int): vị trí kí tự kết thúc của vùng được ghi chú so với học liệu.
* videoPositionStart (int): Vị trí thời gian bắt đầu của học liệu video (tính bằng giây)
* videoPositionEnd (int): Vị trí thời gian kết thúc của học liệu video (tính bằng giây)

# 3. API lấy ra chương của khóa học

> use case tương ứng : 907 (dùng để lấy ra combobox)

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course-section/get-section-by-courseId/129' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA'
```

> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id khóa học  |path|

> output :

```json
[
  {
    "name": "Vui lòng nhập tên chương",
    "id": 284
  },
  {
    "name": "Vui lòng nhập tên chương",
    "id": 286
  }
]
```

# 4. API lấy ra bài giảng của chương

> use case tương ứng : 907 (dùng để lấy ra combobox)

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course-sequence/get-sequence-by-section/284' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA'
```

> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id chương  |path|

> output :

```json
[
  {
    "name": "Vui lòng nhập tên bài giảng",
    "id": 317
  },
  {
    "name": "Vui lòng nhập tên bài giảng",
    "id": 318
  }
]
```

# 5. API lấy ra học liệu của bài giảng

> use case tương ứng : 907 (dùng để lấy ra combobox)

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-course-unit/get-by-sequence/317' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA'
```

> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id bài giảng  |path|

> output :

```json
{
  "success": true,
  "data": [
    {
      "id": 451,
      "name": "Tên học liệu",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": 1,
      "isDeleted": true,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1863,
      "name": "pdf",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": "a",
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1871,
      "name": "video ne",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1874,
      "name": "van ban",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1875,
      "name": "audio ne",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1879,
      "name": "scorm ne",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1880,
      "name": "xapi nay",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": false,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    },
    {
      "id": 1881,
      "name": "Bai thi",
      "courseSequenceId": null,
      "courseSequenceName": null,
      "courseSectionId": null,
      "courseSectionName": null,
      "description": null,
      "availableStatus": null,
      "scheduleType": null,
      "scheduleStartDate": null,
      "scheduleEndDate": null,
      "emailNotificationAll": null,
      "emailNotificationLearner": null,
      "isHide": null,
      "timeCompletedCondition": null,
      "orderNumber": null,
      "isDeleted": true,
      "startedDate": null,
      "publishedDate": null,
      "imagePath": null
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 6. API tạo mới ghi chú

> use case tương ứng : 908

> Lưu ý : 
* Hiện chỉ có tạo ghi chú cho toàn bộ học liệu, không có chọn vùng
* Khi tạo, luôn truyền field 'isOfWholeUnit' với value là 'true'
* Các field documentPosition, markerText, markerTextStart, markerTextEnd, videoPositionStart, videoPositionEnd không truyền lên (hoặc truyền lên 'null')

> curl :

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/create' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA' \
  -H 'Content-Type: multipart/form-data' \
  -F 'isPinned=false' \
  -F 'attachments=@images.jpg;type=image/jpeg' \
  -F 'attachments=@Anime-Jujutsu-Kaisen-yuta-okkotsu.jpg;type=image/jpeg' \
  -F 'courseId=129' \
  -F 'title=Thêm mới ghi chú' \
  -F 'content=Học liệu này cần chỉnh sửa' \
  -F 'isOfWholeUnit=true' \
  -F 'unitId=1874'
```
> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| courseId  | y         | int     | id khóa học  ||
| unitId  | y         | int     | id học liệu  ||
| title  | y         | string     | tên ghi chú  ||
| content  | y         | string     | nội dung ghi chú  ||
| isOfWholeUnit  | y    | boolean | toàn bộ học liệu?|truyền 'true'|
| isPinned  | y    | boolean | ghim?||
| attachments  | n    | file | file đính kèm|có thể truyền nhiều|

# 7. API ghim, bỏ ghim ghi chú

> use case tương ứng : 906

> curl :

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/update-pinned' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 52,
  "isPinned": true
}'
```
> input :

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id ghi chú  ||
| isPinned  | y         | boolean     | có ghim hay không?  ||

# 8. API xóa ghi chú

> use case tương ứng : 906

> curl :

```json
curl -X 'DELETE' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/delete' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA' \
  -H 'Content-Type: application/json' \
  -d '{
  "ids": [
    11, 12, 13
  ]
}'
```

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| ids  | y         | int[]     | id các ghi chú  ||


# 9. API cập nhật ghi chú

> use case tương ứng : 908

> curl :

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/update' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA' \
  -H 'Content-Type: multipart/form-data' \
  -F 'isPinned=false' \
  -F 'deleteAttachmentIds=79,80' \
  -F 'attachments=@Anime-Jujutsu-Kaisen-yuta-okkotsu.jpg;type=image/jpeg' \
  -F 'attachments=@images.jpg;type=image/jpeg' \
  -F 'title=Sửa lại ghi chú' \
  -F 'content=Ghi chú cần sửa lại' \
  -F 'isOfWholeUnit=true' \
  -F 'id=117'
```

> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id ghi chú  ||
| title  | y         | string     | tên ghi chú  ||
| content  | y         | string     | nội dung ghi chú  ||
| isOfWholeUnit  | n    | boolean | toàn bộ học liệu?|có thể cập nhật hoặc không|
| isPinned  | y    | boolean | ghim?||
| attachments  | n    | file | file đính kèm|có thể truyền nhiều|
| deleteAttachmentIds  | n    | string | các id file muốn xóa|ngăn cách nhau bằng dấu phảy|

# 10. API xem danh sách ghi chú

> use case tương ứng : 909

> curl : 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/get-by-unit?unitId=1874' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA'
```

> input :

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id ghi chú  ||
| keyword  | y         | string     | từ khóa tìm kiếm  ||

> output : 

```json
{
  "success": true,
  "data": {
    "count": 5,
    "total": 5,
    "notes": [
      {
        "id": 117,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "Sửa lại ghi chú",
        "content": "Ghi chú cần sửa lại",
        "isOfWholeUnit": true,
        "isPinned": false,
        "documentPosition": null,
        "markerText": null,
        "markerTextStart": null,
        "markerTextEnd": null,
        "videoPositionStart": null,
        "videoPositionEnd": null,
        "createdDate": "2024-06-19T09:40:37Z",
        "updatedDate": "2024-06-19T10:02:13Z",
        "attachments": [
          {
            "id": 81,
            "mainKey": "https://s3.moooc.xyz/dev-stable/student-unit-note/51a9ecfb-7820-43c3-b4f4-a3c15a267e8eAnime-Jujutsu-Kaisen-yuta-okkotsu.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240619T102132Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240619%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=ffe6439e2f63f7c1bd9e71f1e8318a2a5e9030d28fc0b56ae07e9a0b58948269",
            "fileName": "Anime-Jujutsu-Kaisen-yuta-okkotsu.jpg",
            "attachmentType": "image"
          },
          {
            "id": 82,
            "mainKey": "https://s3.moooc.xyz/dev-stable/student-unit-note/01684ba1-b943-4e99-8f21-b219722459b1images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240619T102132Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240619%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=87e1327963915eb2734019fae1486a6ccd2948c9910477a4e9008e1adf5e2605",
            "fileName": "images.jpg",
            "attachmentType": "image"
          }
        ]
      },
      {
        "id": 76,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "",
        "content": "",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "i và loài mèo dẫn tới việc nó thường được khắc họa trong các truyền thuyết và thần thoại tại nhiều nền văn hoá, gồm truyền thuyết và thần thoại Ai Cập cổ, Trung Quốc cổ, Na Uy cổ, và vị Vua xứ Wales thời Trung Cổ Hywel Dda (người Tử tế) đã thông qua bộ luật bảo vệ động vật đầu tiên trên thế giới bằng cách coi hành động giết hại hay làm tổn hại tới mèo là vi phạm pháp luật, với những hình phạt nặng nề cho những kẻ vi phạm. Tuy nhiên, mèo thỉnh thoảng bị coi là ma quỷ và có 9 mạng, ví dụ như nó không mang lại may mắn hay thường đi liền với những ",
        "markerTextStart": 1222,
        "markerTextEnd": 1772,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T07:08:58Z",
        "updatedDate": null,
        "attachments": []
      },
      {
        "id": 75,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "vùng chọn",
        "content": "chọn vùng",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "",
        "markerTextStart": 0,
        "markerTextEnd": 0,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T07:02:07Z",
        "updatedDate": null,
        "attachments": []
      },
      {
        "id": 70,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "",
        "content": "",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": "",
        "markerTextStart": 0,
        "markerTextEnd": 0,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-06T04:05:23Z",
        "updatedDate": null,
        "attachments": []
      },
      {
        "id": 42,
        "unitId": 1874,
        "sequenceId": 317,
        "sectionId": 284,
        "unitName": "van ban",
        "sequenceName": "Vui lòng nhập tên bài giảng",
        "sectionName": "Vui lòng nhập tên chương",
        "studentUserId": 4,
        "title": "ghi chus cho van ban",
        "content": "chu gi",
        "isOfWholeUnit": false,
        "isPinned": false,
        "documentPosition": null,
        "markerText": null,
        "markerTextStart": null,
        "markerTextEnd": null,
        "videoPositionStart": 0,
        "videoPositionEnd": 0,
        "createdDate": "2024-06-05T11:20:14Z",
        "updatedDate": null,
        "attachments": [
          {
            "id": 68,
            "mainKey": "https://s3.moooc.xyz/dev-stable/student-unit-note/e49628a7-2ab1-4dba-ace2-344a0340973d956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm%20%281%29.docx?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240619T102132Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240619%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7e46ff837f9bee3e547ebd9503e28a10e36285229158f7bcba9371a1fe5338f7",
            "fileName": "956059b4-4960-47a8-bb3b-0bd332cf600dca569e6d-ad76-4f24-815a-be6b4755d3b8antoanpm (1).docx",
            "attachmentType": "word"
          }
        ]
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```
> explain output :

* isOfWholeUnit (boolean): ghi chú có phải của toàn bộ học liệu không
* isPinned (boolean): ghi chú có đang được ghim không
* documentPosition (string): vị trí của học liệu (ví dụ: trang thứ mấy của học liệu)
* markerText(string): nội dung ghi chú của học liệu text
* markerTextStart (int): vị trí kí tự bắt đầu của vùng được ghi chú so với học liệu.
* markerTextEnd (int): vị trí kí tự kết thúc của vùng được ghi chú so với học liệu.
* videoPositionStart (int): Vị trí thời gian bắt đầu của học liệu video (tính bằng giây)
* videoPositionEnd (int): Vị trí thời gian kết thúc của học liệu video (tính bằng giây)

# 11. API xem lịch sử ghi chú

> use case tương ứng : 906

> curl :

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/mooc-student-note/history/get-by-conditions' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTg3NjcwNDAsImV4cCI6MTcxODg1MzQ0MH0.IP5qnuFPhrmQ80jJj7OUFlnv4uj9dm9n2_Qx51syIyA' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "",
  "courseId": 242,
  "unitId": null,
  "sectionId": null,
  "sequenceId": null,
  "sortByName": "asc",
  "sortByCreateDate": "desc",
  "createdFromDate": "",
  "page": 1,
  "size": 10,
  "createdToDate": ""
}'
```

> input : 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| keyword  | n         | string     | từ khóa tìm kiếm  ||
| courseId  | n         | int     | id khóa học  ||
| unitId  | n         | int     | id học liệu  ||
| sectionId  | n         | int     | id chương  ||
| sequenceId  | n         | int     | id bài giảng  ||
| sortByName  | n         | string     |sắp xếp theo tên |asc/desc|
| sortByCreateDate  | n | string|sắp xếp theo ngày|asc/desc|
| createdFromDate  | n | date|ngày tạo từ||
| createdToDate  | n | date|ngày tạo đến||
| page  | n | int|trang số||
| size  | n | int|số lượng 1 trang||

> output :

```json
{
  "success": true,
  "data": {
    "count": 10,
    "total": 15,
    "notes": [
      {
        "id": 224,
        "courseId": 242,
        "unitId": 2248,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "tieu de ne",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 85,
        "title": "a nam nê cue ",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:20:57Z"
      },
      {
        "id": 219,
        "courseId": 242,
        "unitId": 2248,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "tieu de ne",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 85,
        "title": "a nam nê cue ",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:20:14Z"
      },
      {
        "id": 217,
        "courseId": 242,
        "unitId": 2248,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "tieu de ne",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 85,
        "title": "a nam nê cue ",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:19:50Z"
      },
      {
        "id": 253,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 114,
        "title": "em tung tesst",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-17T04:09:07Z"
      },
      {
        "id": 225,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 83,
        "title": "em tùng test",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:22:13Z"
      },
      {
        "id": 218,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 83,
        "title": "em tùng test",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:20:12Z"
      },
      {
        "id": 215,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 83,
        "title": "em tùng test",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:19:15Z"
      },
      {
        "id": 227,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 82,
        "title": "ghi chu video",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:22:38Z"
      },
      {
        "id": 226,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 82,
        "title": "ghi chu video",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:22:31Z"
      },
      {
        "id": 222,
        "courseId": 242,
        "unitId": 2247,
        "sequenceId": 1128,
        "sectionId": 822,
        "unitName": "ok chua",
        "sequenceName": "Bài giảng 1",
        "sectionName": "Chương 1",
        "noteId": 82,
        "title": "ghi chu video",
        "active": "Chỉnh sửa",
        "createdDate": "2024-06-14T09:20:54Z"
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```
