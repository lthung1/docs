- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API bắt đầu làm bài kiểm tra](#1-api-bắt-đầu-làm-bài-kiểm-tra)
- [2. API khóa học để bạn bắt đầu](#2-api-khóa-học-để-bạn-bắt-đầu)
- [3. API tìm kiếm khóa học của tôi](#3-api-tìm-kiếm-khóa-học-của-tôi)
- [4. API xem chi tiết khóa học](#4-api-xem-chi-tiết-khóa-học)
- [5. API xem chi tiết học liệu](#5-api-xem-chi-tiết-học-liệu)

# 0. Một số chú thích ban đầu
* Đây là các thay đổi của api
* Anh/chị thay đổi xong api nào thì báo giúp em trong group [API] để em báo tester test lại ạ ^^. Em xin cảm ơn

# 1. API bắt đầu làm bài kiểm tra

> Ngày cập nhật: 08/08/2024

> Nội dung thay đổi

* thay đổi endponint (thêm <b>-v2</b> vào cuối endpoint)
* endpoint cũ: https://be.moooc.xyz/v2/api/course/structure/exam
* endponit mới: https://be.moooc.xyz/v2/api/course/structure/exam-v2

> Vị trí cập nhật trong folder docs: ../exam/exam.md (mục 1)

# 2. API khóa học để bạn bắt đầu

> Ngày cập nhật: 08/08/2024

> màn hình: trang chủ

> Nội dung thay đổi
* thay đổi endpoint: (cập nhật sau)
* các field trong response trả về sẽ được giữ nguyên

# 3. API tìm kiếm khóa học của tôi

> Ngày cập nhật: 08/08/2024

> design figma: (UC888, 560-4)

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=63-57758&t=Z0Idpb4wzz0ift5X-0
```

> Nội dung thay đổi: trong design có nút <b>Đánh giá khóa học</b>, căn cứ vào field trả về để hiện lên nút đó

* Trước đó: hiện lên căn cứ vào 2 field <i>isCommented</i> và <i>learningStatus</i>

* Bây giờ: căn cứ vào field <i>isAbleToComment</i> (true => hiện lên), (false => disable)

> minh họa

* api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/my-registration/filter-my-courses' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzIxMjI3NywiaWF0IjoxNzIzMTI1ODc3fQ.2jUENGvR_oUGNE99b4xTDEMxP0VptELruCjb-M1MrCk' \
  -H 'Content-Type: application/json' \
  -d '{
  
}'
```

* response

```json
{
  "success": true,
  "data": {
    "courses": [
      {
        "id": 3,
        "name": "Xác suất thống kê",
        "publicDate": null,
        "learningStatus": 1,
        "enterpriseLogo": "https://s3.moooc.xyz/dev-stable/university/logo/ec7db244-5df3-4939-943a-5d046bbb42dcphoto_6069021705780707393_y.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240808T140529Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240808%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=db63ee131887ce67f6a5b46f5b172cccfb2b7a33050e37ae9247887641dca572",
        "image": null,
        "teachers": [
          "Ánh Nguyễn Thuận",
          "Khoa Hoá Học"
        ],
        "completedPercentage": 24,
        "isCommented": false,
        "isAbleToComment": true  // Xác định hiện lên nút comment
      },
      {
        "id": 13,
        "name": "Kế hoạch Kỹ năng mềm",
        "publicDate": null,
        "learningStatus": 3,
        "enterpriseLogo": "https://s3.moooc.xyz/dev-stable/university/logo/ef6f54ce-536d-434c-804d-33a46aef998et%E1%BA%A3i%20xu%E1%BB%91ng.jfif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240808T140529Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240808%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=197a2738353a81b4e24683d2773ba5d5d5d60e4f0e5de6205856f4bbeccbe5b8",
        "image": null,
        "teachers": [
          "Ánh Nguyễn Thuận"
        ],
        "completedPercentage": 0,
        "isCommented": true,
        "isAbleToComment": false  // Xác định hiện lên nút comment
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 4. API xem chi tiết khóa học

> Ngày cập nhật: 08/08/2024

> design figma: (UC887)

> Nội dung thay đổi: trong design có nút <b>Viết nhận xét</b>, căn cứ vào field trả về để hiện lên nút đó

* Trước đó: hiện lên căn cứ vào 2 field <i>isCommented</i> và <i>learningStatus</i>

* Bây giờ: căn cứ vào field <i>isAbleToComment</i> (true => hiện lên), (false => disable)

> minh họa

* api 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/open-api/course/1' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzIxMjI3NywiaWF0IjoxNzIzMTI1ODc3fQ.2jUENGvR_oUGNE99b4xTDEMxP0VptELruCjb-M1MrCk'
```

* response

```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Lập trình hướng đối tượng",
    "code": null,
    "description": "he lo mai fennn",
    "image": null,
    "template": "kjhsadhháđâsd",
    "title": "he lo mai fennn",
    "courseUrl": null,
    "createdDate": "2024-03-16T06:35:54Z",
    "totalStudents": 1,
    "publicDate": null,
    "industries": [
      {
        "id": 1,
        "name": "Giáo dục học",
        "code": "7140101",
        "industryGroupCode": "71401",
        "status": true
      },
      {
        "id": 2,
        "name": "Công nghệ giáo dục",
        "code": "7140111",
        "industryGroupCode": "71401",
        "status": true
      }
    ],
    "cost": 0,
    "assigners": [
      {
        "uuid": "84b44910479d4f5486c8a44f4b37ccd7",
        "name": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "slug": "NEU",
        "isSponsor": true
      }
    ],
    "sections": [],
    "courseTeacher": [],
    "updatedDate": null,
    "avgStar": 0,
    "totalComment": 0,
    "teacherNames": [],
    "endDate": null,
    "isRegistered": false,
    "isCommented": false,
    "isSaved": true,
    "isTrending": true,
    "isHasCertificate": 0,
    "isAbleToComment": false // Căn cứ hiện lên nút đánh giá
  },
  "message": "Thực hiện thành công"
}
```

# 5. API xem chi tiết học liệu

> Ngày cập nhật: 08/08/2024

> design figma: (UC896-897)

> Nội dung thay đổi

* link học liệu (field trước đó: <i>mainKey</i>, field hiện tại: <i>mainKeyUrl</i>)

* Cần đếm ngược thời gian để disable nút bấm tích chọn hoàn thành học liệu: căn cứ vào field <i>timeCompletedCondition</i> (tính theo giây)

> minh họa

* api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-course-unit/get-unit/2236' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzIxMjI3NywiaWF0IjoxNzIzMTI1ODc3fQ.2jUENGvR_oUGNE99b4xTDEMxP0VptELruCjb-M1MrCk'
```

* response

```json
{
  "success": true,
  "data": {
    "id": 2236,
    "name": "Thêm học liệu cho anh Nam Nê",
    "courseSequenceId": 589,
    "courseSequenceName": "Bài 1:",
    "courseSectionId": 5,
    "courseSectionName": "Chương 5",
    "description": "Nghị luận về một vấn đề xã hội - mẫu 1",
    "availableStatus": 2,
    "scheduleType": 0,
    "scheduleStartDate": null,
    "scheduleEndDate": null,
    "emailNotificationAll": false,
    "emailNotificationLearner": false,
    "isHide": false,
    "timeCompletedCondition": 0, // số giây đếm ngược tích hoàn thành học liệu
    "orderNumber": null,
    "isDeleted": false,
    "startedDate": null,
    "publishedDate": null,
    "imagePath": null,
    "module": "video",
    "documents": [
      {
        "id": 128,
        "courseUnitId": 2236,
        "courseBlockId": 812,
        "title": "Thêm học liệu cho anh Nam Nê",
        "description": "Nghị luận về một vấn đề xã hội - mẫu 1",
        "iconType": 1,
        "text": "",
        "referenceUrl": "",
        "fileName": "MOOC - Google Chrome 2024-06-11 07-51-36.mp4",
        "mainKey": "document/video/3/fae69245-2d14-4b91-a2ae-3b2996758675MOOC - Google Chrome 2024-06-11 07-51-36.mp4", // không dùng field này (cũ)
        "mainKeyUrl": "https://s3.moooc.xyz/dev-stable/document/video/3/fae69245-2d14-4b91-a2ae-3b2996758675MOOC%20-%20Google%20Chrome%202024-06-11%2007-51-36.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240808T142216Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240808%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7483341168004ab279852151fe82e40813a39c9e9aab741505ea01be0e95ef2c", // link học liệu (mới)
        "timeCompletedCondition": 0,
        "expectedTime": null,
        "expectedTimeType": null,
        "fileUploadFrom": 0,
        "attachments": [],
        "referenceType": null,
        "timeCompletedConditionSeconds": 0,
        "timeCompletedConditionMinutes": 0
      }
    ],
    "scorms": [],
    "quizGroups": [],
    "isCompleted": true,
    "totalNote": 3,
    "totalDiscussion": 10,
    "isUnitReviewed": true,
    "isSequenceReviewed": false,
    "totalView": 0,
    "totalShare": 0,
    "totalDownload": 0
  },
  "message": "Thực hiện thành công"
}
```