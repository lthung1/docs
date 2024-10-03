- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API bắt đầu làm bài kiểm tra](#1-api-bắt-đầu-làm-bài-kiểm-tra)
- [2. API khóa học để bạn bắt đầu](#2-api-khóa-học-để-bạn-bắt-đầu)
- [3. API tìm kiếm khóa học của tôi](#3-api-tìm-kiếm-khóa-học-của-tôi)
- [4. API xem chi tiết khóa học](#4-api-xem-chi-tiết-khóa-học)
- [5. API xem chi tiết học liệu](#5-api-xem-chi-tiết-học-liệu)
- [6. API bắt đầu khoá học](#6-api-bắt-đầu-khoá-học)
- [7. API lấy mã lớp của sinh viên](#7-api-lấy-mã-lớp-của-sinh-viên)
- [8. API lấy mã khoa của sinh viên](#8-api-lấy-mã-khoa-của-sinh-viên)
- [9. API tìm kiếm học liệu của màn ghi chú](#9-api-tìm-kiếm-học-liệu-của-màn-ghi-chú)
- [10. API chi tiết khoá học](#10-api-chi-tiết-khoá-học)
- [11. API cập nhật thông tin cá nhân của quản trị](#11-api-cập-nhật-thông-tin-cá-nhân-của-quản-trị)
- [12. API tìm kiếm bài tập, bài kiểm tra, bài thi](#12-api-tìm-kiếm-bài-tập-bài-kiểm-tra-bài-thi)
- [13. API tìm kiếm bài tập, bài kiểm tra, bài thi](#13-api-tìm-kiếm-bài-tập-bài-kiểm-tra-bài-thi)
- [14. API lịch](#14-API-lịch)

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

# 6. API bắt đầu khoá học

> ngày cập nhật: 09/08/2024

> design figma: (UC890, UC888)

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=63-57758&t=TZPmQ94XmjN3kNDK-0
```



> Nội dung thay đổi

* đối với nút đi đến cấu trúc khoá học, có 3 loại <b>Bắt đầu học</b>, <b>Tiếp tục học</b>, <b>Học lại</b> => khi bấm vào nút <b>Bắt đầu học</b> thì call api này để bắt đầu tính thời gian sinh viên phát sinh tiến trình học, các nút còn lại không call.

* đối với màn tìm kiếm khoá học của tôi, khi điều hướng đến cấu trúc khoá học => check list khoá học (learningStatus = 1) => call api


> api: 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/my-registration/start-learning-course/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDgxMTEyMywiaWF0IjoxNzI0NzI0NzIzfQ.BTZTeDgSxEj5Ri23YeEutQGz2aqun-orumbJCyZYw1c'
```

# 7. API lấy mã lớp của sinh viên

> ngày cập nhật: 06/09/2024

> nội dung thay đổi

* thêm mới api lấy mã khoa của sinh viên

> api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/my-registration/get-student-class-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU2ODQ2MzMsImlhdCI6MTcyNTU5ODIzM30.Xr7bufz9VF2NRavCJAlKMCaZ1n8IP6KKaYUrSY-lwc4'
```

> response

```json
{
  "success": true,
  "data": [
    {
      "name": "khanhalo",
      "id": 18
    },
    {
      "name": "lớp học",
      "id": 22
    },
    {
      "name": "Lớp 1",
      "id": 23
    },
    {
      "name": "Course 3",
      "id": 3
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 8. API lấy mã khoa của sinh viên

> ngày cập nhật: 06/09/2024

> nội dung

* api lấy mã khoa của sinh viên (dùng cho bộ lọc cho phần thống kê biểu đồ của màn sinh viên)

> api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/my-registration/get-industry-group-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU2ODQ2MzMsImlhdCI6MTcyNTU5ODIzM30.Xr7bufz9VF2NRavCJAlKMCaZ1n8IP6KKaYUrSY-lwc4'
```


> response

```json
{
  "success": true,
  "data": [
    {
      "name": "Năng khiếu Mỹ thuật ứng dụng",
      "id": 6
    },
    {
      "name": "Năng khiếu Trình diễn",
      "id": 4
    },
    {
      "name": "Năng khiếu Mỹ thuật",
      "id": 3
    },
    {
      "name": "Khoa học giáo dục",
      "id": 1
    },
    {
      "name": "Đào tạo giáo viên sư phạm",
      "id": 2
    },
    {
      "name": "Năng khiếu Nghe nhìn",
      "id": 5
    },
    {
      "name": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
      "id": 8
    },
    {
      "name": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
      "id": 7
    },
    {
      "name": "Xã hội học và nhân học",
      "id": 11
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 9. API tìm kiếm học liệu của màn ghi chú

> ngày cập nhật: 06/09/2024

> màn hình tương ứng (UC907 - phần lọc học liệu theo bài giảng)

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=304-142491&node-type=CANVAS&t=HJEykxqXB1hEuWBd-0
```

> nội dung thay đổi

* ở màn này, không lọc ra các học liệu quiz do không thể ghi chú cho loại học liệu này

* thêm vào cuối endpoint "includingQuiz=false"

> api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-course-unit/get-by-sequence/589?includingQuiz=false' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU2ODQ2MzMsImlhdCI6MTcyNTU5ODIzM30.Xr7bufz9VF2NRavCJAlKMCaZ1n8IP6KKaYUrSY-lwc4'
```

# 10. API chi tiết khoá học

> ngày cập nhật: 06/09/2024

> Thay đổi trong màn hình trình bày giao diện khoá học (UC890)

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=63-57758&node-type=CANVAS&t=HJEykxqXB1hEuWBd-0
```

> nội dung thay đổi của màn trình bày giao diện khoá học (UC890)

* Phần trình giao diện khoá học, phần lộ trình: check học liệu, => có key isFree = true => bỏ khoá, kể cả isAccessible = false. Do đây là giao diện trình bày khoá học => học liệu miễn phí sẽ không bị khoá.

* Note: chỉ thay đổi trong màn giao diện khoá học => màn cấu trúc khoá học (sau khi chọn 1 khoá từ màn khoá học của tôi) => không thay đổi

> api

```json
{
  "success": true,
  "data": {
    "id": 459,
    "name": "test chia sẻ",
    "code": "share01",
    "description": null,
    "image": null,
    "template": null,
    "title": null,
    "courseUrl": "https://moooc.xyz/courses/share01",
    "createdDate": "2024-09-04T10:50:39Z",
    "totalStudents": 1,
    "publicDate": "2024-09-04T07:09:20.351997Z",
    "industries": [
      {
        "id": 4,
        "name": "Kinh tế Giáo dục",
        "code": "7140199",
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
        "isSponsor": false
      },
      {
        "uuid": "84b44910479d4f5486c8a44f4b37cc10",
        "name": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "slug": "HANU",
        "isSponsor": true
      }
    ],
    "sections": [
      {
        "id": 1145,
        "name": "Chương 1",
        "orderNumber": 1,
        "scheduleStartDate": null,
        "scheduleEndDate": null,
        "children": [
          {
            "id": 1643,
            "name": "Mở bài",
            "courseTeacherUserId": 4,
            "courseTeacherUserName": null,
            "orderNumber": 1,
            "sectionId": 1145,
            "children": [
              {
                "id": 3278,
                "name": "Bài kiểm tra số 1",
                "orderNumber": null,
                "block": [
                  {
                    "id": 1460,
                    "module": "quiz",
                    "orderNumber": null,
                    "iconType": 3,
                    "title": "Bài kiểm tra số 1",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": null,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 240,
                "totalDiscussion": 0,
                "availableStatus": 2,
                "createdDate": "2024-09-04T03:52:13Z",
                "isFree": true, // => không khoá
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              },
              {
                "id": 3277,
                "name": "Video điểm danh 01",
                "orderNumber": 1,
                "block": [
                  {
                    "id": 1459,
                    "module": "video",
                    "orderNumber": null,
                    "iconType": 1,
                    "title": "Video điểm danh 01",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": 0,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 0,
                "totalDiscussion": 0,
                "availableStatus": 2,
                "createdDate": "2024-09-04T03:52:01Z",
                "isFree": true,
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              },
              {
                "id": 3280,
                "name": "em tùng test",
                "orderNumber": 2,
                "block": [
                  {
                    "id": 1462,
                    "module": "scorm",
                    "orderNumber": null,
                    "iconType": 1,
                    "title": "em tùng test",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": 0,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 0,
                "totalDiscussion": 0,
                "availableStatus": null,
                "createdDate": "2024-09-04T10:14:49Z",
                "isFree": true,
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              },
              {
                "id": 3281,
                "name": "em tùng test",
                "orderNumber": 3,
                "block": [
                  {
                    "id": 1463,
                    "module": "scorm",
                    "orderNumber": null,
                    "iconType": 1,
                    "title": "em tùng test",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": 0,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 0,
                "totalDiscussion": 0,
                "availableStatus": null,
                "createdDate": "2024-09-04T10:47:59Z",
                "isFree": true,
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              },
              {
                "id": 3282,
                "name": "sc",
                "orderNumber": 4,
                "block": [
                  {
                    "id": 1464,
                    "module": "scorm",
                    "orderNumber": null,
                    "iconType": 1,
                    "title": "sc",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": 0,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 0,
                "totalDiscussion": 0,
                "availableStatus": null,
                "createdDate": "2024-09-04T10:48:41Z",
                "isFree": true,
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              },
              {
                "id": 3283,
                "name": "em tùng test",
                "orderNumber": 5,
                "block": [
                  {
                    "id": 1465,
                    "module": "xapi",
                    "orderNumber": null,
                    "iconType": 1,
                    "title": "em tùng test",
                    "description": null,
                    "referenceType": null
                  }
                ],
                "timeCompletedCondition": 0,
                "sequenceId": 1643,
                "isCompleted": false,
                "totalTime": 0,
                "totalDiscussion": 0,
                "availableStatus": null,
                "createdDate": "2024-09-04T10:49:17Z",
                "isFree": true,
                "lockedReason": null,
                "isRegisteredCourse": false,
                "isAccessible": false
              }
            ],
            "completedPercentage": 0,
            "videoNumber": 1,
            "totalTime": 240,
            "totalUnit": 6
          }
        ],
        "completedPercentage": 0,
        "videoNumber": 1,
        "totalTime": 240,
        "totalUnit": 6
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 11. API cập nhật thông tin cá nhân của quản trị

> ngày cập nhật: 06/09/2024

> Màn hình thay đổi: (UC885)

```json
https://www.figma.com/design/untUrfdnnOhMEfKY2rCsVC/INNO-(QT)?node-id=1141-6135&node-type=CANVAS&t=HJEykxqXB1hEuWBd-0
```

> Nội dung thay đổi

* Khi cập nhật trình độ học vấn của giảng viên, chỉ truyền duy nhất 1 loại trình độ học vấn lên (có thể truyền mảng có tối đa 1 phần tử)

> api

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/account/update-profile' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU2ODQ2MzMsImlhdCI6MTcyNTU5ODIzM30.Xr7bufz9VF2NRavCJAlKMCaZ1n8IP6KKaYUrSY-lwc4' \
  -H 'Content-Type: multipart/form-data' \
  -F 'academicLevelIds=1'
```

# 12. API tìm kiếm bài tập, bài kiểm tra, bài thi

> ngày cập nhật: 10/09/2024

> Màn hình cập nhật: (UC915)

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=2286-216260&node-type=canvas&t=2o7kkVgXWvuBSgYr-0
```

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/search/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjYwNDE0MjksImlhdCI6MTcyNTk1NTAyOX0.yopw5wGXDvsyiUd51xGVR0P9ZHxq71oxallESYCbnl0' \
  -H 'Content-Type: application/json' \
  -d '{
  
}'
```

> payload

```json
{
    "status": 1,
    => trạng thái
    + Tất cả: 0
    + Đã làm: 1
    + Chưa làm: 2
    + Sắp đến hạn nộp: 3

    "submitDateFrom": "2023-09-04T17:00:00.000Z",
    "submitDateTo": "2024-10-25T17:00:00.000Z",
    => Thời gian

    "resultStatus": 1,
    => Kết quả
    + Đạt: 1
    + Chưa đạt: 0
    + Chưa có kết quả: -1
    + Tất cả: null
    (không còn option "Khác" như trên design)

    "submitTime": 6,
    => Số lần nộp

    "type": 1,
    => tab (tất cả, bài tập, bài kiểm tra, bài thi)
    + Tất cả: null
    + Bài tập: 1
    + Bài kiểm tra: 2
    + Bài thi: 3

    "page": 1,
    "size": 10
}
```

> response

```json
{
    "success": true,
    "data": {
        "exams": [
            {
                "id": 502, // blockId
                "examType": 1, // loại bài (tương ứng với "type" ở payload)
                "name": "bài tập 1", // tên bài
                "totalQuestions": 2, // tổng câu hỏi
                "duration": 300, // tổng thời lượng (theo giây)
                "dateToCompleteBefore": "2024-09-29T00:00:00Z", 
                // Hoàn thành trước => nếu null thì hiện "--"
                "submitDate": "2024-08-27T08:22:28Z", 
                // Thời gian nộp => nếu null thì hiện "--"
                "submitTime": 6, // Số lần nộp
                "allowedSubmitTime": null, // số lần nộp tối đa cho phép
                "resultStatus": 1, // bỏ qua
                "unitId": 1719, 
                "sequenceId": 592,
                "sectionId": 368,
                "blockId": 502,
                "point": null, // bỏ qua
                "result": "2.0", // kết quả (trả về String) => null = "--"
                "isSuccess": false,
                "overdue": false, // quá hạn
                "isRequired": true // bắt buộc 
            },
            {
                "id": 507,
                "examType": 2,
                "name": "bài kiểm tra 1",
                "totalQuestions": 2,
                "duration": null,
                "dateToCompleteBefore": "2024-09-30T00:00:00Z",
                "submitDate": "2024-08-23T18:42:17Z",
                "submitTime": 1,
                "allowedSubmitTime": null,
                "resultStatus": -1,
                "unitId": 1724,
                "sequenceId": 592,
                "sectionId": 368,
                "blockId": 507,
                "point": null,
                "result": null,
                "isSuccess": false,
                "overdue": false,
                "isRequired": false
            },
            {
                "id": 559,
                "examType": 1,
                "name": "BT 01",
                "totalQuestions": 4,
                "duration": null,
                "dateToCompleteBefore": "2024-09-30T00:00:00Z",
                "submitDate": "2024-08-23T18:46:06Z",
                "submitTime": 1,
                "allowedSubmitTime": null,
                "resultStatus": -1,
                "unitId": 1824,
                "sequenceId": 640,
                "sectionId": 427,
                "blockId": 559,
                "point": null,
                "result": null,
                "isSuccess": false,
                "overdue": false,
                "isRequired": false
            },
            {
                "id": 560,
                "examType": 1,
                "name": "Câu hỏi không bắt buộc",
                "totalQuestions": 3,
                "duration": null,
                "dateToCompleteBefore": "2024-09-30T00:00:00Z",
                "submitDate": "2024-08-22T04:20:37Z",
                "submitTime": 1,
                "allowedSubmitTime": null,
                "resultStatus": -1,
                "unitId": 1825,
                "sequenceId": 640,
                "sectionId": 427,
                "blockId": 560,
                "point": null,
                "result": null,
                "isSuccess": false,
                "overdue": false,
                "isRequired": false
            },
            {
                "id": 666,
                "examType": 1,
                "name": "Bài tập 2",
                "totalQuestions": 2,
                "duration": null,
                "dateToCompleteBefore": "2024-09-30T00:00:00Z",
                "submitDate": "2024-09-09T09:51:41Z",
                "submitTime": 1,
                "allowedSubmitTime": null,
                "resultStatus": -1,
                "unitId": 1950,
                "sequenceId": 640,
                "sectionId": 427,
                "blockId": 666,
                "point": null,
                "result": null,
                "isSuccess": false,
                "overdue": false,
                "isRequired": false
            }
        ],
        "totalNumber": 5, // tất cả
        "testNumber": 1, // bài kiểm tra
        "exerciseNumber": 4, // bài tập
        "examNumber": 0 // bài thi
    },
    "message": "Thực hiện thành công"
}
```

# 13. API tìm kiếm bài tập, bài kiểm tra, bài thi

> ngày cập nhật : 26/09/2024

> màn hình: UC914

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=2286-216260&node-type=canvas&t=XUmPfBjxjJDPDWWP-0
```

> Nội dung thay đổi

* Các bài không thể truy cập sẽ điều hướng tới màn cấu trúc khoá học (căn cứ theo field isAccessible)

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/search/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6W10sIm5hbWUiOiJubGg0NjMxNSIsImlzU3VwZXJVc2VyIjpmYWxzZSwiaWQiOjQyNCwicG9zaXRpb24iOiJpc19zdiIsImVtYWlsIjoibmxoNDYzMTVAbm93bmkuY29tIiwiZXhwIjoxNzI3NDA0ODE3LCJpYXQiOjE3MjczMTg0MTd9.ZWJzFeqKNiD3HN2DfwN40QgxdxajBfLswMX9xeV24mA' \
  -H 'Content-Type: application/json' \
  -d '{
}'
```

> response

```json
{
  "success": true,
  "data": {
    "exams": [
      {
        "id": 902,
        "examType": 1,
        "name": "Bài tập",
        "totalQuestions": 2,
        "duration": null,
        "dateToCompleteBefore": "2024-09-29T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": null,
        "resultStatus": -1,
        "unitId": 2361,
        "sequenceId": 1178,
        "sectionId": 846,
        "blockId": 902,
        "point": null,
        "result": null,
        "isSuccess": false,
        "overdue": false,
        "isRequired": false,
        "isAccessible": true // nếu false thì điều hướng tới cấu trúc khoá học
      },
      {
        "id": 903,
        "examType": 2,
        "name": "Bài kiểm tra ",
        "totalQuestions": 3,
        "duration": null,
        "dateToCompleteBefore": "2024-07-31T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": null,
        "resultStatus": -1,
        "unitId": 2362,
        "sequenceId": 1178,
        "sectionId": 846,
        "blockId": 903,
        "point": null,
        "result": null,
        "isSuccess": false,
        "overdue": true,
        "isRequired": false,
        "isAccessible": true
      },
      {
        "id": 904,
        "examType": 3,
        "name": "Bài thi",
        "totalQuestions": 7,
        "duration": null,
        "dateToCompleteBefore": "2024-08-09T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": null,
        "resultStatus": -1,
        "unitId": 2363,
        "sequenceId": 1178,
        "sectionId": 846,
        "blockId": 904,
        "point": null,
        "result": null,
        "isSuccess": false,
        "overdue": true,
        "isRequired": false,
        "isAccessible": true
      },
      {
        "id": 910,
        "examType": 1,
        "name": "Bài kiểm tra mới trong bài giảng mới của chương mới",
        "totalQuestions": 4,
        "duration": null,
        "dateToCompleteBefore": "2024-10-03T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": null,
        "resultStatus": -1,
        "unitId": 2369,
        "sequenceId": 1180,
        "sectionId": 847,
        "blockId": 910,
        "point": null,
        "result": null,
        "isSuccess": false,
        "overdue": false,
        "isRequired": false,
        "isAccessible": true
      }
    ],
    "totalNumber": 4,
    "testNumber": 1,
    "exerciseNumber": 2,
    "examNumber": 1
  },
  "message": "Thực hiện thành công"
}
```

# 14. API lịch

> ngày cập nhật : 26/09/2024

> màn hình: UC 921/922/923

```json
https://www.figma.com/design/lnmbWi8rsyfWVfNGzWRzvS/INNO-(SV)?node-id=2286-216260&node-type=canvas&t=XUmPfBjxjJDPDWWP-0
```

> Nội dung thay đổi

* Thêm trường isAccessible để điều hướng
* Các học liệu nào có thông tin là "Cần hoàn thành trước" => lấy giá trị trả về theo field "dateToCompleteBefore" (không hiện giờ)
* Lịch học nào của cả ngày thì căn cứ vào field "allDay"
* Nếu allDay = false, các lịch học mà có thời gian từ a giờ -> b giờ: căn cứ vào các field timeStartInDay và timeEndInDay

> api 

```json
curl -X 'POST' \
  'http://localhost:8080/api/course/structure/study/schedule-search' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJnaWFuZyB2aWVuIEZpbmFsIl0sIm5hbWUiOiJWb2hvbmcuMjgxMCIsImlzU3VwZXJVc2VyIjpmYWxzZSwiaWQiOjEwOCwicG9zaXRpb24iOiJpc19zdiIsImVtYWlsIjoiVm9ob25nLjI4MTBAZ21haWwuY29tIiwiZXhwIjoxNzI4MDEwMDk3LCJpYXQiOjE3Mjc5MjM2OTd9.KkBbRCOtv3WOxi8t0r3BNU90Y-P7pl1UA4fP_s4GIWY' \
  -H 'Content-Type: application/json' \
  -d '{
  "scheduleTypes": [
    0, 1, 2, 3, 4
  ],
  "dateFrom": "2023-10-03T07:54:22.787Z",
  "dateTo": "2024-10-03T07:54:22.787Z"
}'
```
> response

```json
{
  "success": true,
  "data": [
    {
      "id": 1846,
      "blockId": 575,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-26T00:00:00Z",
      "end": "2024-10-03T23:59:59.999999999Z",
      "title": "video",
      "type": 0,
      "allDay": true, // cả ngày
      "quizInfo": {
        "totalQuestions": 0,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 654,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1848,
      "blockId": 577,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-08-27T00:00:00Z",
      "end": "2024-09-12T00:00:00Z",
      "title": "mp4",
      "type": 0,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 0,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 654,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1849,
      "blockId": 578,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-10T00:00:00Z",
      "end": "2024-09-30T00:00:00Z",
      "title": "văn bản ",
      "type": 0,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 0,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1850,
      "blockId": 579,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-08-28T00:00:00Z",
      "end": "2024-09-07T00:00:00Z",
      "title": "tham khảo nhé",
      "type": 4,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 0,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1851,
      "blockId": 580,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-08-28T00:00:00Z",
      "end": "2024-09-30T00:00:00Z",
      "title": "tham khảo 1",
      "type": 4,
      "allDay": false,
      "quizInfo": {
        "totalQuestions": 0,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": "12:30:45", // giờ bắt đầu
      "timeEndInDay": "19:30:45" // giờ kết thúc
    },
    {
      "id": 1852,
      "blockId": 581,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-28T00:00:00Z",
      "end": "2024-09-30T00:00:00Z",
      "title": "bài tập 1",
      "type": 1,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 2,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1857,
      "blockId": 586,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-08-28T00:00:00Z",
      "end": "2024-09-25T00:00:00Z",
      "title": "bài tập 2",
      "type": 1,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 2,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1863,
      "blockId": 592,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-25T00:04:00Z",
      "end": "2024-09-28T00:19:00Z",
      "title": "bài kiểm tra 1",
      "type": 2,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 2,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 1864,
      "blockId": 593,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-18T00:11:00Z",
      "end": "2024-09-20T00:33:00Z",
      "title": "bài thi 2",
      "type": 3,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 2,
        "totalTime": 0
      },
      "sectionId": 439,
      "sequenceId": 655,
      "isAccessible": true,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    },
    {
      "id": 2340,
      "blockId": 1035,
      "courseId": 344,
      "courseName": "khóa học 278",
      "start": "2024-09-22T00:00:00Z",
      "end": "2024-09-28T00:00:00Z",
      "title": "Test19/9",
      "type": 1,
      "allDay": true,
      "quizInfo": {
        "totalQuestions": 2,
        "totalTime": 0
      },
      "sectionId": 441,
      "sequenceId": 657,
      "isAccessible": false,
      "dateToCompleteBefore": "2024-12-27T00:06:00Z",
      "timeStartInDay": null,
      "timeEndInDay": null
    }
  ],
  "message": "Thực hiện thành công"
}
```