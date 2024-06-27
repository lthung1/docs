- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API xem chi tiết học liệu tham khảo](#1-api-xem-chi-tiết-học-liệu-tham-khảo)
- [2. API tìm kiếm học liệu tham khảo](#2-api-tìm-kiếm-học-liệu-tham-khảo)
- [3. API đếm học liệu tham khảo](#3-api-đếm-học-liệu-tham-khảo)
- [4. API lấy ra chương của khóa học](#4-api-lấy-ra-chương-của-khóa-học)
- [5. API lấy ra bài giảng của chương](#5-api-lấy-ra-bài-giảng-của-chương)
- [6. API tải học liệu tham khảo](#6-api-tải-học-liệu-tham-khảo)
- [7. API yêu thích học liệu tham khảo](#7-api-yêu-thích-học-liệu-tham-khảo)

# 0. Một số chú thích ban đầu
> Giải thích về học liệu tham khảo
* có hai loại học liệu tham khảo là link do giảng viên tải lên (sẽ lưu lên S3 và lấy bằng field mainKey) và loại học liệu bằng link online (lấy trong field referenceUrl)
* mỗi học liệu chỉ có duy nhất 1 đường link

> cách truyền field sort
- đây là một mảng String truyền vào các tiêu chí sắp xếp
- Truyền tiêu chí sắp xếp trước rồi truyền thứ tự vào sau (VD: ["name,asc"])
- Nếu sắp xếp theo nhiều tiêu chí, truyền tiêu chí nào ưu tiên trước lên đầu (VD: ["name,asc", "date,desc"])
- Sẽ có chú thích về các tiêu chí truyền ("name", "date", ...)
- Thứ tự sắp xếp truyền vào 1 trong 2 giá trị "asc" hoặc "desc"

> các type tài liệu

| type   | description |
|-------------| --------- |
|0| Tất cả |
|1| PDF |
|2| Video |
|3| Âm thanh |

# 1. API xem chi tiết học liệu tham khảo

> use case tương ứng : 917

> curl 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course-unit-reference/2377' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NTg3MzUsImV4cCI6MTcxOTU0NTEzNX0.GaOeAfllwK5tbOFQiE80BBq5sWPW21MFk7qSJhRxc-Q'
```

> request

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| unitId  | y         | int     | id học liệu  |path|

> response 

```json
{
  "success": true,
  "data": {
    "courseId": 3, //id khoá học
    "unitId": 2377, //id học liệu
    "unitName": "Hàm số ", // tên học liệu
    "sequenceId": 1140, // id bài giảng
    "sectionId": 6, // id chương
    "sequenceName": "Bài học về sự tin tưởng", // tên bài giảng
    "sectionName": "Chương 6: các học liệu về video, mp3, text, image", // tên chương
    "title": "Hàm số ", // tên học liệu
    "description": "null", // mô tả học liệu
    "iconType": 1,
    "isFavorite": false, // yêu thích?
    "referenceUrl": null, //link học liệu 
    "mainKey": "https://s3.moooc.xyz/dev-stable/document/reference/3/d237a6b3-7c57-43f3-99b5-01a76c3bd312D%E1%BA%A1ng%206.%20Th%E1%BB%A7%20thu%E1%BA%ADt%20casio%20gi%E1%BA%A3i%20%C4%91%E1%BB%93ng%20bi%E1%BA%BFn%2C%20ngh%E1%BB%8Bch%20bi%E1%BA%BFn.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240627T095740Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240627%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=513bbd0886646b282c18014ac09b850270ca41861d3a2f82da30e6da0bf6f1d3"
    //link học liệu
  },
  "message": "Thực hiện thành công"
}
```

# 2. API tìm kiếm học liệu tham khảo

> use case tương ứng : 919

> curl 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course-unit-reference/get-by-condition' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NjExNDQsImV4cCI6MTcxOTU0NzU0NH0.doHM2KTEhxJWgYuIWtrpk3ig1t1A435NYSxjU3alqG4' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "name,asc"
  ],
  "keyword": "",
  "courseId": 3,
  "sectionId": null,
  "sequenceId": null,
  "type": null,
  "isFavorite": null
}'
```

> request 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | y         | int     | trang số  ||
| size  | y         | int     | size 1 trang  ||
| sort  | y         | string[]     | sắp xếp  |tiêu chí: "name", xem lại mục #0 |
| keyword  | n         | string     | từ khoá tìm kiếm  ||
| courseId  | y         | int     | id khoá học  ||
| sectionId  | n         | int     | id chương  ||
| sequenceId  | n         | int     | id bài giảng  ||
| isFavorite  | n         | boolean     | yêu thích?  ||
| type  | n         | int     | loại tài liệu  |xem lại mục #0|

> response 

```json
// các field tương tự như ở #1 chi tiết học liệu
{
  "success": true,
  "data": {
    "count": 5,
    "total": 5,
    "references": [
      {
        "courseId": 3,
        "unitId": 2377,
        "unitName": "Hàm số ",
        "sequenceId": 1140,
        "sectionId": 6,
        "sequenceName": "Bài học về sự tin tưởng",
        "sectionName": "Chương 6: các học liệu về video, mp3, text, image",
        "title": "Hàm số ",
        "description": "null",
        "iconType": 1,
        "isFavorite": false,
        "referenceUrl": null,
        "mainKey": "https://s3.moooc.xyz/dev-stable/document/reference/3/d237a6b3-7c57-43f3-99b5-01a76c3bd312D%E1%BA%A1ng%206.%20Th%E1%BB%A7%20thu%E1%BA%ADt%20casio%20gi%E1%BA%A3i%20%C4%91%E1%BB%93ng%20bi%E1%BA%BFn%2C%20ngh%E1%BB%8Bch%20bi%E1%BA%BFn.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240627T095722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240627%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2f09a54207e19556b53e213f98391c70c1547a6f1b9ea58fc5199378efffb065"
      },
      {
        "courseId": 3,
        "unitId": 2373,
        "unitName": "Học liệu tham khảo",
        "sequenceId": 1142,
        "sectionId": 13,
        "sequenceName": "Các bài kiểm tra",
        "sectionName": "Chương 13: Các học liệ xAPI, scorm",
        "title": "Học liệu tham khảo",
        "description": "taif",
        "iconType": 5,
        "isFavorite": false,
        "referenceUrl": null,
        "mainKey": "https://s3.moooc.xyz/dev-stable/document/reference/3/2e043f68-3fe0-4254-84b6-b6a1bc07caf8sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240627T095722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240627%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2b26742ee2accb0cacda86c98fe91cf1518c7b07bc882f0dd823f21a65cae3fe"
      },
      {
        "courseId": 3,
        "unitId": 2376,
        "unitName": "Tài liệu ",
        "sequenceId": 1140,
        "sectionId": 6,
        "sequenceName": "Bài học về sự tin tưởng",
        "sectionName": "Chương 6: các học liệu về video, mp3, text, image",
        "title": "Tài liệu ",
        "description": "xxtk",
        "iconType": 1,
        "isFavorite": false,
        "referenceUrl": null,
        "mainKey": null
      },
      {
        "courseId": 3,
        "unitId": 2374,
        "unitName": "Tài liệu tham khảo pdf url",
        "sequenceId": 1142,
        "sectionId": 13,
        "sequenceName": "Các bài kiểm tra",
        "sectionName": "Chương 13: Các học liệ xAPI, scorm",
        "title": "Tài liệu tham khảo pdf url",
        "description": "pdf",
        "iconType": 5,
        "isFavorite": false,
        "referenceUrl": "https://www.antennahouse.com/hubfs/xsl-fo-sample/pdf/basic-link-1.pdf",
        "mainKey": null
      },
      {
        "courseId": 3,
        "unitId": 2375,
        "unitName": "thêm,",
        "sequenceId": 1142,
        "sectionId": 13,
        "sequenceName": "Các bài kiểm tra",
        "sectionName": "Chương 13: Các học liệ xAPI, scorm",
        "title": "thêm,",
        "description": "",
        "iconType": 4,
        "isFavorite": false,
        "referenceUrl": null,
        "mainKey": "https://s3.moooc.xyz/dev-stable/document/reference/3/92907501-630a-411c-b8b4-fbec9206bcf520MB-TESTFILE.ORG.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240627T095722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240627%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=e417d3c33d6869870242801fed1f4d6f09e5059ccd1e415b6ceb7af7f06002c6"
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 3. API đếm học liệu tham khảo

> use case tương ứng : 917, 918, 919

> curl 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course-unit-reference/get-count' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NjExNDQsImV4cCI6MTcxOTU0NzU0NH0.doHM2KTEhxJWgYuIWtrpk3ig1t1A435NYSxjU3alqG4' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "name,asc"
  ],
  "keyword": "",
  "courseId": 3,
  "sectionId": null,
  "sequenceId": null,
  "type": null,
  "isFavorite": null
}'
```

> request 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | y         | int     | trang số  ||
| size  | y         | int     | size 1 trang  ||
| sort  | y         | string[]     | sắp xếp  |tiêu chí: "name", xem lại mục #0 |
| keyword  | n         | string     | từ khoá tìm kiếm  ||
| courseId  | y         | int     | id khoá học  ||
| sectionId  | n         | int     | id chương  ||
| sequenceId  | n         | int     | id bài giảng  ||
| isFavorite  | n         | boolean     | yêu thích?  ||
| type  | n         | int     | loại tài liệu  |xem lại mục #0|

> response 

```json
{
  "success": true,
  "data": {
    "countAll": 5,
    "countFavorite": 0
  },
  "message": "Thực hiện thành công"
}
```

# 4. API lấy ra chương của khóa học

> use case tương ứng : 917, 918, 919 (dùng để lấy ra combobox)

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

# 5. API lấy ra bài giảng của chương

> use case tương ứng : 917, 918, 919 (dùng để lấy ra combobox)

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

# 6. API tải học liệu tham khảo

> use case tương ứng : 918

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course-unit-reference/download-all/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NjExNDQsImV4cCI6MTcxOTU0NzU0NH0.doHM2KTEhxJWgYuIWtrpk3ig1t1A435NYSxjU3alqG4'
```

> request

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id khoá học  |path|

> response : file zip

# 7. API yêu thích học liệu tham khảo

> use case tương ứng : 917

> curl 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/mooc-course-unit/favorite' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NjExNDQsImV4cCI6MTcxOTU0NzU0NH0.doHM2KTEhxJWgYuIWtrpk3ig1t1A435NYSxjU3alqG4' \
  -H 'Content-Type: application/json' \
  -d '{
  "unitId": 2237,
  "isFavorite": true
}'
```

> request 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| unitId  | y         | int     | id học liệu  ||
|  isFavorite | y         | boolean     | yêu thích?  ||
