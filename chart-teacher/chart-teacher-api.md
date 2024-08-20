- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [0.1 Api lấy khoa của giảng viên](#0-1-api-lấy-khoa-của-giảng-viên)
- [0.1 Api lấy khóa học ghi danh của giảng viên](#0-2-api-lấy-khóa-học-ghi-danh-của-giảng-viên)
- [1. Số lượng khóa học theo hình thức xuất bản](#1-Số-lượng-khóa-học-theo-hình-thức-xuất-bản)
- [2. Số lượng bài giảng theo trạng thái xuất bản](#2-Số-lượng-bài-giảng-theo-trạng-thái-xuất-bản)
- [3. Số lượng bài giảng theo khoa](#3-Số-lượng-bài-học-theo-khoa)
- [4. Số lượng học liệu theo Scorm & xAPI](#4-Số-lượng-Scorm-&-xAPI)
- [5. Số lượng học liệu đa phương tiện theo loại](#5-Số-lượng-học-liệu-đa-phương-tiện-theo-loại)
- [6. Số lượng học liệu theo khóa học](#6-Số-lượng-học-liệu-theo-khóa-học)
- [7. Tỷ lệ kết quả đánh giá theo khóa học](#7-Tỷ-lệ-kết-quả-làm-đánh-giá-theo-khóa-học)
- [8. Tỷ lệ kết quả làm đánh giá theo học liệu](#8-Tỷ-lệ-kết-quả-làm-đánh-giá-theo-học-liệu)
- [9. Tỷ lệ kết quả đánh giá theo bài giảng](#9-Tỷ-lệ-kết-quả-đánh-giá-theo-bài-giảng)
- [10. Số lượng bài kiểm tra theo loại](#10-Số-lượng-bài-kiểm-tra-theo-loại)
- [11. Số lượng tài liệu tham khảo theo loại](#11-Số-lượng-tài-liệu-tham-khảo-theo-loại)
- [12. Thống kê phản hồi theo bài giảng](#12-Thống-kê-phản-hồi-theo-bài-giảng)
- [13. Thống kê phản hồi theo lớp học](#13-Thống-kê-phản-hồi-theo-lớp-học)
- [14. Thống kê hành vi người dùng, tab xem](#14-Thống-kê-hành-vi-người-dùng-tab-xem)
- [15. Thống kê hành vi người dùng, tab chia sẻ](#15-Thống-kê-hành-vi-người-dùng-tab-chia-sẻ)
- [16. Số lượng đánh giá theo thời gian](#16-Số-lượng-đánh-giá-theo-thời-gian)
- [17. Số lượng khoá học theo phân công](#17-Số-lượng-khoá-học-theo-phân-công)
- [18. Thống kê số lượng tìm kiếm toàn hệ thống theo thời gian](#18-thống-kê-số-lượng-tìm-kiếm-toàn-hệ-thống-theo-thời-gian)
- [19. Số lượng tìm kiếm theo từ khoá](#19-số-lượng-tìm-kiếm-theo-từ-khoá)
- [20. Thống kê số lượng phản hồi](#20-thống-kê-số-lượng-phản-hồi)

# 0. Một số chú thích ban đầu
> giải thích payload bộ lọc chung

* giải thích

```json
{
  "timeUnit": "string", // đơn vị thời gian
  "from": "2024-08-18T23:19:14.912Z",
  "to": "2024-08-18T23:19:14.912Z",
  "courseLevelIds": [ // cấp khóa học
    0
  ],
  "industryGroupIds": [ // mã khoa
    0
  ],
  "courseIds": [ // mã khóa học
    0
  ],
  "courseStructureType": "string", // loại cấu trúc khóa học
  "moduleGroup": 0, // nhóm các module học liệu
  "unitActionType": 0 // hành vi người dùng đối với học liệu
}
```
* Các giá trị nhận vào của request body

```json
- timeUnit (string)
  + luôn luôn phải có đối với các biểu đồ thống kê theo thời gian 
  + truyền vào đơn vị thời gian muốn làm tiêu chí thống kê
  + Các giá trị nhận vào: day, week, month, year
  + Logic nhập tương ứng với bộ lọc khoảng thời gian
    . 7 ngày => day
    . 1 tháng => week
    . 3 tháng => month
    . Tùy chọn => nhập vào theo giá trị tương ứng của bộ lọc đơn vị (thời gian)

- from, to: giới hạn thời gian muốn thống kê

- courseLevelIds: (int[])
  + chưa có thông tin về field này (bổ sung api sau)

- industryGroupIds: (int[])
  + nhập dựa trên api trả về 
  + bổ sung api sau ngày 19/08/2024

- courseIds: (int[])
  + nhập dựa trên api trả về 
  + dùng api khóa học của giảng viên, có thể thay đổi

- courseStructureType (string)
  + dùng cho bộ lọc riêng trên từng biểu đồ
  + giá trị nhận vào
    . khóa học: "course"
    . bài giảng: "sequence"
    . các giá trị khác: "unit"

- moduleGroup (int)
  + dùng khi courseStructureType = "unit"
  + các giá trị nhận vào
    . Đa phương tiện:  1
    . Tài liệu tham khảo: 2
    . Bài Tập/Bài Kiểm Tra/Bài Thi: 3
    . Scorm & Xapi: 4

- unitActionType (int)
  + các giá trị nhận vào
    . Xem: 1
    . Chia sẻ: 2
    . Tải về: 3
```

# 0.1 Api lấy khoa của giảng viên

> api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-industry-group-filter' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMDQ5NSwiaWF0IjoxNzI0MDM0MDk1fQ.GF93H3r8_f1UuIsn1xkyN0GKdUsyn2bUsDPYebFrHRw'
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
      "name": "Máy tính",
      "id": 31
    },
    {
      "name": "Năng khiếu Mỹ thuật",
      "id": 3
    },
    {
      "name": "Năng khiếu Trình diễn",
      "id": 4
    },
    {
      "name": "Quản lý công nghiệp",
      "id": 37
    },
    {
      "name": "Đào tạo giáo viên sư phạm",
      "id": 2
    },
    {
      "name": "Thú y",
      "id": 54
    },
    {
      "name": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
      "id": 8
    },
    {
      "name": "Công nghệ thông tin",
      "id": 32
    },
    {
      "name": "Công nghệ Kỹ thuật cơ khí",
      "id": 34
    },
    {
      "name": "Khoa học giáo dục",
      "id": 1
    },
    {
      "name": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
      "id": 33
    },
    {
      "name": "Xã hội học và nhân học",
      "id": 11
    },
    {
      "name": "Báo chí và truyền thông",
      "id": 15
    },
    {
      "name": "Năng khiếu Nghe nhìn",
      "id": 5
    },
    {
      "name": "Toán học",
      "id": 29
    },
    {
      "name": "Văn thư, lưu trữ, bảo tàng",
      "id": 17
    },
    {
      "name": "Địa lý học",
      "id": 13
    },
    {
      "name": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
      "id": 35
    },
    {
      "name": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
      "id": 36
    },
    {
      "name": "Thông tin – Thư viện",
      "id": 16
    },
    {
      "name": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
      "id": 7
    },
    {
      "name": "Hóa học",
      "id": 73
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 0.2 Api lấy khóa học ghi danh của giảng viên

> api

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/teacher-possession/filter-class-enroll' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDIxNDM1NSwiaWF0IjoxNzI0MTI3OTU1fQ.ACtH1IkgEey9Nq5oWw6LbS4_aE6BEvDGAbxlvK_cH1o'
```

> response

```json

{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Course 1"
    },
    {
      "id": 2,
      "name": "Course 2"
    },
    {
      "id": 3,
      "name": "Course 3"
    },
    {
      "id": 4,
      "name": "Course 4"
    },
    {
      "id": 5,
      "name": "Course 5"
    },
    {
      "id": 7,
      "name": "Lop ghi danh thang 60606"
    },
    {
      "id": 8,
      "name": "test1"
    },
    {
      "id": 9,
      "name": "test2"
    },
    {
      "id": 10,
      "name": "test3"
    },
    {
      "id": 11,
      "name": "test4"
    },
    {
      "id": 12,
      "name": "test5"
    },
    {
      "id": 13,
      "name": "lớp cccccccccccc"
    },
    {
      "id": 14,
      "name": "test3"
    },
    {
      "id": 15,
      "name": "test6"
    },
    {
      "id": 16,
      "name": "test1"
    },
    {
      "id": 19,
      "name": "Lopws sssa"
    },
    {
      "id": 20,
      "name": "gfgfgf"
    }
  ],
  "message": "Thực hiện thành công"
}
```



# 1. Số lượng khóa học theo hình thức xuất bản
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-teacher/get-course-by-format' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiIsIlFUSFQiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjM4NjAyMDQsImlhdCI6MTcyMzc3MzgwNH0.3AjzCrCXPCwL2tx1hQJBad66-SuQfKN7UgptZSdGru8' \
  -H 'Content-Type: application/json' \
  -d '{

  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [
    
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 1,
      "criteria": "Thẻ ghi danh", // tên hình thức xuất bản
      "count": 258, // số lượng khóa học
      "percentage": 98.85057 // số phần trăm của khóa học theo hình thức xuất bản
    },
    {
      "type": 2,
      "criteria": "Riêng tư",
      "count": 2,
      "percentage": 0.7662835
    },
    {
      "type": 3,
      "criteria": "Tự do",
      "count": 1,
      "percentage": 0.38314176
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 2. Số lượng bài giảng theo trạng thái xuất bản
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-sequence-by-available-status' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzUxODEyNSwiaWF0IjoxNzIzNDMxNzI1fQ.z3ZrJY8P_1r521Uy9ppOnQI6qVQGDFVRD_wdDjoYwQo' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-12T10:11:37.092Z",
  "to": "2024-08-12T10:11:37.092Z",
  "courseLevelIds": [
    
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 0,
      "criteria": "Bản nháp", // tên trạng thái xuất bản
      "count": 687, // số lượng bài giảng
      "percentage": 92.5876 // số phần trăm bài giảng theo trạng thái xuất bản
    },
    {
      "type": 1,
      "criteria": "Riêng tư",
      "count": 13,
      "percentage": 1.7520216
    },
    {
      "type": 2,
      "criteria": "Công khai",
      "count": 42,
      "percentage": 5.6603775
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 3. Số lượng bài giảng theo khoa
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-sequence-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzUxODEyNSwiaWF0IjoxNzIzNDMxNzI1fQ.z3ZrJY8P_1r521Uy9ppOnQI6qVQGDFVRD_wdDjoYwQo' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-12T10:13:22.297Z",
  "to": "2024-08-12T10:13:22.297Z",
  "courseLevelIds": [
    
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 32, // id của khoa
      "criteria": "Công nghệ thông tin", // tên khoa
      "count": 2, // số lượng bài giảng của khoa
      "percentage": 0.17636684 // số phần trăm bài giảng theo khoa
    },
    {
      "type": 5,
      "criteria": "Năng khiếu Nghe nhìn",
      "count": 42,
      "percentage": 3.7037036
    },
    {
      "type": 11,
      "criteria": "Xã hội học và nhân học",
      "count": 8,
      "percentage": 0.70546734
    },
    {
      "type": 6,
      "criteria": "Năng khiếu Mỹ thuật ứng dụng",
      "count": 50,
      "percentage": 4.409171
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 4. Số lượng học liệu theo Scorm & xAPI
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-scorm-and-xapi-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzUxODEyNSwiaWF0IjoxNzIzNDMxNzI1fQ.z3ZrJY8P_1r521Uy9ppOnQI6qVQGDFVRD_wdDjoYwQo' \
  -H 'Content-Type: application/json' \
  -d '{

  "from": "2024-01-12T10:23:50.560Z",
  "to": "2024-08-12T10:23:50.560Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 1,
      "criteria": "scorm", //tên loại học liệu
      "count": 8, // số lượng học liệu
      "percentage": 12.5 // số phần trăm của học liệu theo scorm & xapi
    },
    {
      "type": 2,
      "criteria": "xapi",
      "count": 56,
      "percentage": 87.5
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 5. Số lượng học liệu đa phương tiện theo loại
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-multi-media-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzUxODEyNSwiaWF0IjoxNzIzNDMxNzI1fQ.z3ZrJY8P_1r521Uy9ppOnQI6qVQGDFVRD_wdDjoYwQo' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-12T10:26:35.747Z",
  "to": "2024-08-12T10:26:35.747Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 3,
      "criteria": "text", // loại học liệu đa phương tiện
      "count": 27, // số lượng của học liệu đa phương tiện
      "percentage": 20.149254 // số phần trăm của học liệu đa phương tiện theo loại
    },
    {
      "type": 4,
      "criteria": "mp3",
      "count": 10,
      "percentage": 7.4626865
    },
    {
      "type": 1,
      "criteria": "video",
      "count": 79,
      "percentage": 58.955223
    },
    {
      "type": 2,
      "criteria": "pdf",
      "count": 18,
      "percentage": 13.432837
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 6. Số lượng học liệu theo khóa học
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-unit-by-course' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzYwOTEzNCwiaWF0IjoxNzIzNTIyNzM0fQ.jb0rV1rRXlQSINFHZnZwHqOELzwitKlNUAxystm0Wj8' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-13T06:13:05.891Z",
  "to": "2024-08-13T06:13:05.891Z",
  "courseLevelIds": [
    
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
   
  ]
}'
```
> output

```json
"success": true,
  "data": {
    "statistic": [
      {
        "type": 192, // id của khóa học
        "criteria": "khoá học 105", // tên khóa học
        "values": [
          {
            "count": 2, // số lượng học liệu
            "percentage": null,
            "criteria": "Bài kiểm tra" // loại học liệu
          }
        ]
      },
      {
        "type": 209,
        "criteria": "khoá học test của MN",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Bài kiểm tra"
          },
          {
            "count": 2,
            "percentage": null,
            "criteria": "Đa phương tiện"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Scorm & xAPI"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Tài liệu tham khảo"
          }
        ]
      }
    ],
    "total": 408,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
```

# 7. Tỷ lệ kết quả đánh giá theo khóa học
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-rate-unit-by-course' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiIsIlFUSFQiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjM3NzM2NDIsImlhdCI6MTcyMzY4NzI0Mn0.hsXES4MDc5hCptTjPSm6A5wNPEOlLVjHmE1qNscKq4A' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-15T02:18:17.128Z",
  "to": "2024-05-15T02:18:17.128Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
   
  ]
}'
```
> output

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 3, // id của khóa học
        "criteria": "Xác suất thống kê", // tên của khóa học
        "values": [
          {
            "count": 1, // số lượng đánh giá
            "percentage": 33.33, // số phần trăm đánh giá
            "criteria": "4 sao" //loại sao
          },
          {
            "count": 3,
            "percentage": 66.67,
            "criteria": "5 sao"
          }
        ]
      }
    ],
    "total": 4,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 8. Tỷ lệ kết quả làm đánh giá theo học liệu
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-rate-unit-by-module' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiIsIlFUSFQiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjM3NzM2NDIsImlhdCI6MTcyMzY4NzI0Mn0.hsXES4MDc5hCptTjPSm6A5wNPEOlLVjHmE1qNscKq4A' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-15T05:45:52.062Z",
  "to": "2024-08-15T05:45:52.062Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 3, 
        "criteria": "Scorm & xAPi", // loại học liệu
        "values": [
          {
            "count": 1, // số lượng đánh giá
            "percentage": 33.33, // số phần trăm đánh giá
            "criteria": "4 sao" // loại sao
          },
          {
            "count": 3,
            "percentage": 66.67,
            "criteria": "5 sao"
          }
        ]
      }
    ],
    "total": 4,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 9. Tỷ lệ kết quả đánh giá theo bài giảng
```json
curl -X 'POST' \
  'http://be.moooc.xyz/v2/api/chart-teacher/get-rate-unit-by-sequence' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiIsIlFUSFQiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjM4NjAyMDQsImlhdCI6MTcyMzc3MzgwNH0.3AjzCrCXPCwL2tx1hQJBad66-SuQfKN7UgptZSdGru8' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T08:58:30.196Z",
  "to": "2024-08-16T08:58:30.196Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    
  ],
  "courseIds": [
    
  ]
}'
```
> output

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 1268,  //id của bài giảng
        "criteria": "Bài giảng 1", //Tên bài giảng
        "values": [
          {
            "count": 4,    //số lượng đánh giá
            "percentage": 100, // phần trăm đánh giá
            "criteria": "4 sao" // loại sao
          }
        ]
      },
      {
        "type": 1274,
        "criteria": "Bài giảng 4",
        "values": [
          {
            "count": 1,
            "percentage": 100,
            "criteria": "4 sao"
          }
        ]
      }
    ],
    "total": 9,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 10. Số lượng bài kiểm tra theo loại
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-reference-source-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzg5MDgxMiwiaWF0IjoxNzIzODA0NDEyfQ.xcQTd239p7F2cnutlpC6y0blFhKZFSvpZuToWFtqO3s' \
  -H 'Content-Type: application/json' \
  -d '{

  "from": "2024-01-16T10:31:40.061Z",
  "to": "2024-08-16T10:31:40.061Z"
  
}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 3, 
      "criteria": "Mp3", //Loại Học liệu
      "count": 15, // Số lượng học liệu
      "percentage": 7.317073 // Số Phần trăm học liệu
    },
    {
      "type": 1,
      "criteria": "Video", 
      "count": 129,
      "percentage": 62.92683
    },
    {
      "type": 2,
      "criteria": "Pdf",
      "count": 61,
      "percentage": 29.7561
    }
  ],
  "message": "Thực hiện thành công"
}
```
# 11. Số lượng tài liệu tham khảo theo loại
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-test-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMzg5MDgxMiwiaWF0IjoxNzIzODA0NDEyfQ.xcQTd239p7F2cnutlpC6y0blFhKZFSvpZuToWFtqO3s' \
  -H 'Content-Type: application/json' \
  -d '{

  "from": "2024-01-16T10:35:44.429Z",
  "to": "2024-08-16T10:35:44.429Z"

}'
```
> output

```json
{
  "success": true,
  "data": [
    {
      "type": 1,
      "criteria": "Bài Tập",
      "count": 481, 
      "percentage": 84.53427
    },
    {
      "type": 2,
      "criteria": "Bài Kiểm Tra",
      "count": 69, 
      "percentage": 12.126538
    },
    {
      "type": 3,
      "criteria": "Bài Thi",
      "count": 19,
      "percentage": 3.3391914
    }
  ],
  "message": "Thực hiện thành công"
}
```
# 12. Thống kê phản hồi theo bài giảng
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-rate-sequence-action' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMTEwMywiaWF0IjoxNzI0MDM0NzAzfQ._Pr-8sCeeHQ1mjhwoDNjnld4AFTrpTZP-hEscsgyd4o' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-19T02:31:17.246Z",
  "to": "2024-08-19T02:31:17.246Z"
}'
```
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 1136, //Id bài giảng
        "criteria": "Bài giảng đạo đức", //Tên bài giảng
        "values": [
          {
            "count": 2,
            "percentage": 100,
            "criteria": "Đa Phương Tiện"
          }
        ]
      },
      {
        "type": 1139,
        "criteria": "Sơn Tùng M-TP",
        "values": [
          {
            "count": 1,
            "percentage": 100,
            "criteria": "Đa Phương Tiện"
          }
        ]
      },
      {
        "type": 589,
        "criteria": "Bài 1:",
        "values": [
          {
            "count": 1,
            "percentage": 100,
            "criteria": "Đa Phương Tiện"
          }
        ]
      }
    ],
    "total": 4,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```
# 13. Thống kê phản hồi theo lớp học
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-rate-class-action' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMTEwMywiaWF0IjoxNzI0MDM0NzAzfQ._Pr-8sCeeHQ1mjhwoDNjnld4AFTrpTZP-hEscsgyd4o' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-19T02:32:54.041Z",
  "to": "2024-08-19T02:32:54.041Z"
}'
```
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 0, //Id lớp học
        "criteria": "string", //Tên lớp học
        "values": [
          {
            "count": 0,
            "percentage": 0,
            "criteria": "string"
          }
        ]
      }
    ],
    "total": 0,
    "subTotal": [
      {
        "type": 0,
        "criteria": "string",
        "total": "string"
      }
    ]
  },
  "message": "string"
}
```

# 14. Thống kê hành vi người dùng, tab xem

> api 

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/by-time/get-unit-action' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMDQ5NSwiaWF0IjoxNzI0MDM0MDk1fQ.GF93H3r8_f1UuIsn1xkyN0GKdUsyn2bUsDPYebFrHRw' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2023-08-19T11:05:02.302Z",
  "to": "2024-08-19T11:05:02.302Z",
  "courseStructureType": "unit",
  "moduleGroup": 1,
  "unitActionType": 1
}'
```

> response

```json
{
  "success": true,
  "data": [
    {
      "criteria": "17-23/09",
      "value": 1
    },
    {
      "criteria": "15-21/10",
      "value": 1
    },
    {
      "criteria": "22-28/10",
      "value": 2
    },
    {
      "criteria": "17-23/12",
      "value": 1
    },
    {
      "criteria": "16-22/06",
      "value": 2
    },
    {
      "criteria": "23-29/06",
      "value": 1
    },
    {
      "criteria": "07-13/07",
      "value": 1
    },
    {
      "criteria": "28-03/07",
      "value": 1
    },
    {
      "criteria": "04-10/08",
      "value": 3
    },
    {
      "criteria": "11-17/08",
      "value": 121
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 15. Thống kê hành vi người dùng, tab chia sẻ

* tương tự tab xem => unitActionType = 2

# 16. Số lượng đánh giá theo thời gian

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/by-time/get-unit-review-and-access' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMDQ5NSwiaWF0IjoxNzI0MDM0MDk1fQ.GF93H3r8_f1UuIsn1xkyN0GKdUsyn2bUsDPYebFrHRw' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2023-08-19T11:05:02.302Z",
  "to": "2024-08-19T11:05:02.302Z",
  "moduleGroup": 1
}'
```

> response

```json
{
  "success": true,
  "data": [
    {
      "criteria": "18-24/02", // tiêu chí
      "columnValue": 0, // giá trị cột
      "lineValue": 1 // giá trị đường
    },
    {
      "criteria": "16-22/06",
      "columnValue": 0,
      "lineValue": 1
    },
    {
      "criteria": "28-03/07",
      "columnValue": 4,
      "lineValue": 0
    },
    {
      "criteria": "24-30/12",
      "columnValue": 0,
      "lineValue": 1
    },
    {
      "criteria": "14-20/01",
      "columnValue": 0,
      "lineValue": 2
    },
    {
      "criteria": "17-23/03",
      "columnValue": 0,
      "lineValue": 1
    },
    {
      "criteria": "20-26/08",
      "columnValue": 1,
      "lineValue": 0
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 17. Số lượng khoá học theo phân công

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/by-time/get-course-assign-teacher' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDEyMDQ5NSwiaWF0IjoxNzI0MDM0MDk1fQ.GF93H3r8_f1UuIsn1xkyN0GKdUsyn2bUsDPYebFrHRw' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2023-08-19T11:05:02.302Z",
  "to": "2024-09-19T11:05:02.302Z",
  "courseStructureType": "unit",
  "moduleGroup": 1,
  "unitActionType": 1
}'
```

> response

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "18-24/08",
        "values": [
          {
            "count": 299,
            "percentage": null,
            "criteria": "Xây dựng"
          },
          {
            "count": 292,
            "percentage": null,
            "criteria": "Hướng dẫn"
          }
        ]
      }
    ],
    "total": 591,
    "subTotal": [
      {
        "type": 1,
        "criteria": "Xây dựng",
        "total": 292
      },
      {
        "type": 2,
        "criteria": "Hướng dẫn",
        "total": 299
      },
      {
        "type": 3,
        "criteria": "Tổng số",
        "total": 591
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 18. Thống kê số lượng tìm kiếm toàn hệ thống theo thời gian

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/by-time/get-search-history' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDIwNTMxMywiaWF0IjoxNzI0MTE4OTEzfQ._kDAkF8TgMyiFZx5z9K1wpzoxISktaCSu62nYVnEzhk' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "year",
  "from": "2023-08-20T03:39:02.900Z",
  "to": "2024-08-20T03:39:02.900Z",
  "courseStructureType": "course"
}'
```

> response

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "2023",
        "values": [
          {
            "count": 0,
            "percentage": null,
            "criteria": "Đa Phương Tiện"
          },
          {
            "count": 5,
            "percentage": null,
            "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài Liệu Tham Khảo"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài giảng"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Khoá học"
          }
        ]
      },
      {
        "type": null,
        "criteria": "2024",
        "values": [
          {
            "count": 35,
            "percentage": null,
            "criteria": "Đa Phương Tiện"
          },
          {
            "count": 8,
            "percentage": null,
            "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài Liệu Tham Khảo"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài giảng"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Khoá học"
          }
        ]
      }
    ],
    "total": 48, // tổng
    "subTotal": [
      {
        "type": null,
        "criteria": "Bài giảng",
        "total": 0
      },
      {
        "type": null,
        "criteria": "Đa Phương Tiện",
        "total": 35
      },
      {
        "type": null,
        "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi",
        "total": 13
      },
      {
        "type": null,
        "criteria": "Khoá học",
        "total": 0
      },
      {
        "type": null,
        "criteria": "Tài Liệu Tham Khảo",
        "total": 0
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 19. Số lượng tìm kiếm theo từ khoá

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/get-search-keyword-count' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDIwNTMxMywiaWF0IjoxNzI0MTE4OTEzfQ._kDAkF8TgMyiFZx5z9K1wpzoxISktaCSu62nYVnEzhk' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2023-08-20T11:03:35.795Z",
  "to": "2024-08-20T11:03:35.795Z",
  "courseStructureType": "unit",
  "moduleGroup": 1
}'
```


> response

```json
{
  "success": true,
  "data": [
    {
      "type": null,
      "criteria": "con ga",
      "count": 12,
      "percentage": 34.285717
    },
    {
      "type": null,
      "criteria": "Học liệu video ",
      "count": 6,
      "percentage": 17.142859
    },
    {
      "type": null,
      "criteria": "Sửa học liệu ccccc 123",
      "count": 17,
      "percentage": 48.57143
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 20. Thống kê số lượng phản hồi

> api

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/chart-teacher/by-time/get-unit-discuss' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDIwNTMxMywiaWF0IjoxNzI0MTE4OTEzfQ._kDAkF8TgMyiFZx5z9K1wpzoxISktaCSu62nYVnEzhk' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2023-08-20T11:07:27.091Z",
  "to": "2024-08-20T11:07:27.091Z",
  "courseStructureType": "unit",
  "moduleGroup": 1
}'
```

> response

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "2023",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Đa Phương Tiện"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài Liệu Tham Khảo"
          },
          {
            "count": 4,
            "percentage": null,
            "criteria": "Bài giảng"
          },
          {
            "count": 4,
            "percentage": null,
            "criteria": "Khoá học"
          }
        ]
      },
      {
        "type": null,
        "criteria": "2024",
        "values": [
          {
            "count": 11,
            "percentage": null,
            "criteria": "Đa Phương Tiện"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài Liệu Tham Khảo"
          },
          {
            "count": 11,
            "percentage": null,
            "criteria": "Bài giảng"
          },
          {
            "count": 11,
            "percentage": null,
            "criteria": "Khoá học"
          }
        ]
      }
    ],
    "total": 15,
    "subTotal": [
      {
        "type": null,
        "criteria": "Bài giảng",
        "total": 15
      },
      {
        "type": null,
        "criteria": "Đa Phương Tiện",
        "total": 15
      },
      {
        "type": null,
        "criteria": "Bài Tập/Bài Kiểm Tra/Bài Thi",
        "total": 0
      },
      {
        "type": null,
        "criteria": "Khoá học",
        "total": 15
      },
      {
        "type": null,
        "criteria": "Tài Liệu Tham Khảo",
        "total": 0
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```