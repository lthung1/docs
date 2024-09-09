- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Api số lượng giảng viên theo trình độ học vấn](#1-Số-lượng-giảng-viên-theo-trình-độ-học-vấn)
- [2. Api số lượng học viên](#2-số-lượng-học-viên)
- [3. Api số lượng khóa học](#3-số-lượng-khóa-học)
- [4. Api số lượng tài nguyên](#4-số-lượng-tài-nguyên)
- [5. Api số lượng khóa học theo hình thức xuất bản](#5-số-lượng-khóa-học-theo-hình-thức-xuất-bản)
- [6. Api số lượng khóa học theo khoa](#6-số-lượng-khóa-học-theo-khoa)
- [7. Api số lượng khóa học theo giảng viên](#7-số-lượng-khóa-học-theo-giảng-viên)
- [8. Api số lượng bài giảng theo khoa](#8-số-lượng-bài-giảng-theo-khoa)
- [9. Api số lượng bài kiểm tra](#9-số-lượng-bài-kiểm-tra)
- [10. Api số lượng học tài liệu tham khảo](#10-số-lượng-tài-liệu-tham-khảo)
- [11. Api số lượng SCORM & xAPI](#11-số-lượng-SCORM-&-xAPI)
- [12. Api số lượng học liệu đa phương tiện theo loại](#12-số-lượng-học-liệu-đa-phương-tiện-theo-loại)
- [13. Api Số lượng phản hồi theo thời gian](#13-Số-lượng-phản-hồi-theo-thời-gian)
- [14. Api Số lượng phản hồi theo khóa học](#14-Số-lượng-phản-hồi-theo-khóa-học)
- [15. Api Số lượt đánh giá vs số lượng hoàn thành học liệu](#15-Số-lượt-đánh-giá-vs-số-lượng-hoàn-thành-học-liệu)
- [16. Api Tỷ lệ đánh giá học liệu theo phân loại](#16-Tỷ-lệ-đánh-giá-học-liệu-theo-phân-loại)
- [17. Api Tỷ lệ đánh giá khóa học](#17-Tỷ-lệ-đánh-giá-khóa-học)
- [18. Api Tỷ lệ đánh giá bài giảng](#18-Tỷ-lệ-đánh-giá-bài-giảng)
- [19. Số lượt tìm kiếm tài nguyên](#19-Số-lượt-tìm-kiếm-tài-nguyên)
- [20. Số lượt tìm kiếm theo từ khóa](#20-Số-lượt-tìm-kiếm-theo-từ-khóa)
- [21. Số lượt xem tài nguyên](#21-Số-lượt-xem-tài-nguyên)
- [22. Số lượt chia sẻ tài nguyên](#22-Số-lượt-chia-sẻ-tài-nguyên)
- [23. Số lượt tải xuống tài nguyên](#23-Số-lượt-tải-xuống-tài-nguyên)

# 0. Một số chú thích ban đầu
> giải thích payload bộ lọc chung

* giải thích

```json
{
  "timeUnit": "string", // đơn vị thời gian
  "from": "2024-08-18T23:19:14.912Z",
  "to": "2024-08-18T23:19:14.912Z",
  "universityIds": [ // mã trường
    0
  ],
  "teacherIds": [ // mã giáo viên
    0
  ],
  "courseLevelIds": [ // cấp khóa học
    0
  ],
  "industryGroupIds": [ // mã khoa
    0
  ],
  "courseIds": [ // mã khóa học
    0
  ]
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

- teacherIds:
  + nhập dựa trên api trả về 

- industryGroupIds: (int[])
  + nhập dựa trên api trả về 
  + bổ sung api sau ngày 19/08/2024

- courseIds: (int[])
  + nhập dựa trên api trả về 
  + dùng api khóa học của giảng viên, có thể thay đổi
```

# 1. Số lượng giảng viên theo trình độ học vấn
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-teacher-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-02-29T17:00:00.000Z","to":"2024-09-08T17:00:00.000Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "Năng khiếu Mỹ thuật",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Cử nhân"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Khoa học giáo dục",
        "values": [
          {
            "count": 5,
            "percentage": null,
            "criteria": "Cử nhân"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Tiến sĩ"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thạc sĩ"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Khác",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Cử nhân"
          },
          {
            "count": 22,
            "percentage": null,
            "criteria": "Khác"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Tiến sĩ"
          }
        ]
      }
    ],
    "total": 167,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 2. Số lượng học viên
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-student-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-02-29T17:00:00.000Z","to":"2024-09-08T17:00:00.000Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "Khoa học giáo dục",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Học viên đăng ký mới"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Khác",
        "values": [
          {
            "count": 112,
            "percentage": null,
            "criteria": "Học viên đăng ký mới"
          }
        ]
      }
    ],
    "total": 167,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 3. Số lượng khóa học
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-course-by-university-sponsor' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "Hóa học",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Mỹ thuật",
        "values": [
          {
            "count": 16,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 86,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Máy tính",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ Kỹ thuật cơ khí",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Thông tin – Thư viện",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Báo chí và truyền thông",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Toán học",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Thú y",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 17,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Trình diễn",
        "values": [
          {
            "count": 10,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 62,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Đào tạo giáo viên sư phạm",
        "values": [
          {
            "count": 32,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 140,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ thông tin",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Xã hội học và nhân học",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 4,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Văn thư, lưu trữ, bảo tàng",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Quản lý công nghiệp",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Khoa học giáo dục",
        "values": [
          {
            "count": 35,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 157,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 5,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Nghe nhìn",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 30,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Địa lý học",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Mỹ thuật ứng dụng",
        "values": [
          {
            "count": 5,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 16,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      }
    ],
    "total": 0,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 4. Số lượng tài nguyên
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-unit-resources' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": null,
    "statistic": [
      {
        "type": 1,
        "criteria": "Tài liệu tham khảo",
        "count": 5,
        "percentage": null
      },
      {
        "type": 2,
        "criteria": "Scorm & xAPI",
        "count": 10,
        "percentage": null
      },
      {
        "type": 3,
        "criteria": "Bài kiểm tra",
        "count": 84,
        "percentage": null
      },
      {
        "type": 4,
        "criteria": "Đa phương tiện",
        "count": 55,
        "percentage": null
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 5. Số lượng khóa học theo hình thức xuất bản
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-course-by-format-university' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 137,
    "statistic": [
      {
        "type": 1,
        "criteria": "Thẻ ghi danh",
        "count": 51,
        "percentage": 100
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 6. Số lượng khóa học theo khoa
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-course-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "Hóa học",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Mỹ thuật",
        "values": [
          {
            "count": 17,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Máy tính",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Thông tin – Thư viện",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ Kỹ thuật cơ khí",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Báo chí và truyền thông",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Trình diễn",
        "values": [
          {
            "count": 14,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
        "values": [
          {
            "count": 8,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Đào tạo giáo viên sư phạm",
        "values": [
          {
            "count": 32,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ thông tin",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Xã hội học và nhân học",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Văn thư, lưu trữ, bảo tàng",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Quản lý công nghiệp",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Khoa học giáo dục",
        "values": [
          {
            "count": 21,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Nghe nhìn",
        "values": [
          {
            "count": 12,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Địa lý học",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Năng khiếu Mỹ thuật ứng dụng",
        "values": [
          {
            "count": 5,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      }
    ],
    "total": 51,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 7. Số lượng khóa học theo giảng viên
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-teacher-assign-by-instruct' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": 122,
        "criteria": "ManhTQ",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 397,
        "criteria": "TaoMoiEHH",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 260,
        "criteria": "Test Học Vấn",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 124,
        "criteria": "Test123",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 126,
        "criteria": "em tung",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 98,
        "criteria": "Giảng Viên 99",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 123,
        "criteria": "TestCreate",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 161,
        "criteria": "TestImport",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 139,
        "criteria": "TestHHH",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 152,
        "criteria": "Nguyễn Văn A",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 308,
        "criteria": "em tung test",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 107,
        "criteria": "hanhvtm",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 143,
        "criteria": "TestHHH",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 174,
        "criteria": "Nguyễn Thu H",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 120,
        "criteria": "Trần Mạnh",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 259,
        "criteria": "Test Chức vụ",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 392,
        "criteria": "string",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 125,
        "criteria": "CaseHHH",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 389,
        "criteria": "string",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 180,
        "criteria": "Neo test",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 97,
        "criteria": "Giảng Viên 99",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 134,
        "criteria": "QUAN GV",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 390,
        "criteria": "string",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 179,
        "criteria": "Pin XiJing",
        "values": [
          {
            "count": null,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": null,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      },
      {
        "type": 144,
        "criteria": "QUAN GV 2",
        "values": [
          {
            "count": 7,
            "percentage": null,
            "criteria": "Hướng dẫn"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Xây dựng"
          }
        ]
      }
    ],
    "total": 25,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 8. Số lượng bài giảng theo khoa
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-unit-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 742,
    "statistic": [
      {
        "type": 17,
        "criteria": "Văn thư, lưu trữ, bảo tàng",
        "count": 12,
        "percentage": 1.6172506
      },
      {
        "type": 34,
        "criteria": "Công nghệ Kỹ thuật cơ khí",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 5,
        "criteria": "Năng khiếu Nghe nhìn",
        "count": 54,
        "percentage": 7.277628
      },
      {
        "type": 2,
        "criteria": "Đào tạo giáo viên sư phạm",
        "count": 229,
        "percentage": 30.862534
      },
      {
        "type": 6,
        "criteria": "Năng khiếu Mỹ thuật ứng dụng",
        "count": 19,
        "percentage": 2.5606468
      },
      {
        "type": 32,
        "criteria": "Công nghệ thông tin",
        "count": 8,
        "percentage": 1.0781671
      },
      {
        "type": 3,
        "criteria": "Năng khiếu Mỹ thuật",
        "count": 97,
        "percentage": 13.072777
      },
      {
        "type": 7,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
        "count": 41,
        "percentage": 5.5256066
      },
      {
        "type": 37,
        "criteria": "Quản lý công nghiệp",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 35,
        "criteria": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 1,
        "criteria": "Khoa học giáo dục",
        "count": 138,
        "percentage": 18.598383
      },
      {
        "type": 31,
        "criteria": "Máy tính",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 15,
        "criteria": "Báo chí và truyền thông",
        "count": 12,
        "percentage": 1.6172506
      },
      {
        "type": 16,
        "criteria": "Thông tin – Thư viện",
        "count": 12,
        "percentage": 1.6172506
      },
      {
        "type": 13,
        "criteria": "Địa lý học",
        "count": 12,
        "percentage": 1.6172506
      },
      {
        "type": 8,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
        "count": 13,
        "percentage": 1.7520216
      },
      {
        "type": 4,
        "criteria": "Năng khiếu Trình diễn",
        "count": 44,
        "percentage": 5.929919
      },
      {
        "type": 36,
        "criteria": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 11,
        "criteria": "Xã hội học và nhân học",
        "count": 12,
        "percentage": 1.6172506
      },
      {
        "type": 33,
        "criteria": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
        "count": 4,
        "percentage": 0.53908354
      },
      {
        "type": 73,
        "criteria": "Hóa học",
        "count": 15,
        "percentage": 2.0215635
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 9. Số lượng bài kiểm tra
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-university-test-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 84,
    "statistic": [
      {
        "type": 1,
        "criteria": "Bài Tập",
        "count": 62,
        "percentage": 73.809525
      },
      {
        "type": 2,
        "criteria": "Bài Kiểm Tra",
        "count": 18,
        "percentage": 21.428572
      },
      {
        "type": 3,
        "criteria": "Bài Thi",
        "count": 4,
        "percentage": 4.7619047
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 10. Số lượng tài liệu tham khảo
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-university-reference-source-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 55,
    "statistic": [
      {
        "type": 3,
        "criteria": "Mp3",
        "count": 4,
        "percentage": 7.272727
      },
      {
        "type": 1,
        "criteria": "Video",
        "count": 39,
        "percentage": 70.90909
      },
      {
        "type": 2,
        "criteria": "Pdf",
        "count": 12,
        "percentage": 21.818182
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 11. Số lượng SCORM & xAPI
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-university-scorm-xapi-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 0,
    "statistic": []
  },
  "message": "Thực hiện thành công"
}
```

# 12. Số lượng học liệu đa phương tiện theo loại
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-university-multi-media-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzYxNzAsImlhdCI6MTcyNTg0OTc3MH0.DxPeEvCl9CAAGL7nQU6hYZIhACmPjLEibxWQ85RjgJc' \
  -H 'Content-Type: application/json' \
  -d '{"from":"2024-06-09T02:44:32.852Z","to":"2024-09-09T02:44:32.852Z","courseLevelIds":[],"industryGroupIds":[],"courseIds":[]}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 9,
    "statistic": [
      {
        "type": 1,
        "criteria": "video",
        "count": 7,
        "percentage": 77.77778
      },
      {
        "type": 2,
        "criteria": "pdf",
        "count": 2,
        "percentage": 22.222223
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```
# 13. Số lượng phản hồi theo thời gian
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/by-time/get-unit-discuss' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2024-01-09T10:01:24.743Z",
  "to": "2024-09-09T10:01:24.743Z"
}'
```
> out put
```json
{
  "success": true,
  "data": {
    "total": 29,
    "statistic": [
      {
        "type": null,
        "criteria": "18-24/08",
        "values": [
          {
            "count": 6,
            "percentage": null,
            "criteria": "Đa phương tiện"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài tập/Bài kiểm tra/Bài thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài liệu tham khảo"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Scorm & xAPI"
          }
        ]
      },
    ]
  },
  "message": "Thực hiện thành công"
}
```
# 14. Số lượng phản hồi theo khóa học
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-discuss-course-action' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-09T10:13:00.500Z",
  "to": "2024-09-09T10:13:00.500Z"
}'
```
> out put
```json
{
  "success": true,
  "data": {
    "total": 47,
    "statistic": [
      {
        "type": 415,
        "criteria": "Bài 7",
        "values": [
          {
            "count": 1,
            "percentage": 11.11,
            "criteria": "Đa phương tiện"
          },
          {
            "count": 4,
            "percentage": 44.44,
            "criteria": "Tài liệu tham khảo"
          },
          {
            "count": 2,
            "percentage": 22.23,
            "criteria": "Bài tập/Bài kiểm tra/Bài thi"
          },
          {
            "count": 2,
            "percentage": 22.22,
            "criteria": "Scorm & xAPI"
          },
          {
            "count": 0,
            "percentage": 0,
            "criteria": ""
          }
        ]
      },
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 15. Số lượt đánh giá vs số lượng hoàn thành học liệu
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/by-time/get-unit-review-and-access' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2024-01-09T10:22:29.058Z",
  "to": "2024-09-09T10:22:29.058Z"
}'
```
> out put
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

# 16. Tỷ lệ đánh giá học liệu theo phân loại
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-rate-unit-by-module' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-09T10:25:03.781Z",
  "to": "2024-09-09T10:25:03.781Z"
}'
```
> out put
```json
{
  "success": true,
  "data": [
    {
        "type": 1,
        "criteria": "Đa phương tiện",
        "values": [
          {
            "count": 2,
            "percentage": 13.33,
            "criteria": "1 sao"
          },
          {
            "count": 3,
            "percentage": 20,
            "criteria": "2 sao"
          },
          {
            "count": 2,
            "percentage": 13.34,
            "criteria": "3 sao"
          },
          {
            "count": 3,
            "percentage": 20,
            "criteria": "4 sao"
          },
          {
            "count": 5,
            "percentage": 33.33,
            "criteria": "5 sao"
          }
        ]
      },
  ],
  "message": "Thực hiện thành công"
}
```
# 17. Tỷ lệ đánh giá khóa học
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-rate-unit-by-course' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "string",
  "from": "2024-01-09T10:26:46.481Z",
  "to": "2024-09-09T10:26:46.481Z"
}'
```
> out put
```json
{
  "success": true,
  "data": [
    {
        "type": 415,
        "criteria": "Khóa học Tùng CS test",
        "values": [
          {
            "count": 1,
            "percentage": 11.11,
            "criteria": "1 sao"
          },
          {
            "count": 2,
            "percentage": 22.22,
            "criteria": "2 sao"
          },
          {
            "count": 5,
            "percentage": 55.56,
            "criteria": "3 sao"
          },
          {
            "count": 0,
            "percentage": 0,
            "criteria": "4 sao"
          },
          {
            "count": 1,
            "percentage": 11.11,
            "criteria": "5 sao"
          }
        ]
      },
  ],
  "message": "Thực hiện thành công"
}
```
# 18. Tỷ lệ đánh giá bài giảng
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-rate-unit-by-sequence' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "string",
  "from": "2024-01-09T10:28:07.669Z",
  "to": "2024-09-09T10:28:07.669Z"
}'
```
> out put
```json
{
  "success": true,
  "data": [
    {
        "type": 10,
        "criteria": "Bài 10",
        "values": [
          {
            "count": 1,
            "percentage": 14.29,
            "criteria": "1 sao"
          },
          {
            "count": 3,
            "percentage": 42.85,
            "criteria": "2 sao"
          },
          {
            "count": 0,
            "percentage": 0,
            "criteria": "3 sao"
          },
          {
            "count": 3,
            "percentage": 42.86,
            "criteria": "4 sao"
          },
          {
            "count": 0,
            "percentage": 0,
            "criteria": "5 sao"
          }
        ]
      },
  ],
  "message": "Thực hiện thành công"
}
```

# 19. Số lượt tìm kiếm tài nguyên
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/by-time/get-search-history' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "week",
  "from": "2024-01-09T10:29:35.609Z",
  "to": "2024-09-09T10:29:35.609Z"
}'
```
> out put
```json
{
  "success": true,
  "data": [
   {
        "type": null,
        "criteria": "14-20/01",
        "values": [
          {
            "count": 0,
            "percentage": null,
            "criteria": "Đa phương tiện"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Bài tập/Bài kiểm tra/Bài thi"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Tài liệu tham khảo"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Scorm & xAPI"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Bài giảng"
          },
          {
            "count": 0,
            "percentage": null,
            "criteria": "Khóa học"
          }
        ]
      },
  ],
  "message": "Thực hiện thành công"
}
```
# 20. Số lượt tìm kiếm theo từ khóa
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/get-search-keyword-count' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "timeUnit": "string",
  "from": "2024-01-09T10:30:54.939Z",
  "to": "2024-09-09T10:30:54.939Z"
}'
```
> out put
```json
{
  "success": true,
  "data": [
   {
      "type": null,
      "criteria": "nam nê",
      "count": 1,
      "percentage": 9.090909
    },
    {
      "type": null,
      "criteria": "acc",
      "count": 1,
      "percentage": 9.090909
    },
    {
      "type": null,
      "criteria": "tuyến tính",
      "count": 1,
      "percentage": 9.090909
    },
    {
      "type": null,
      "criteria": "lập trình",
      "count": 2,
      "percentage": 18.181818
    },
    {
      "type": null,
      "criteria": "đại số",
      "count": 1,
      "percentage": 9.090909
    },
  ],
  "message": "Thực hiện thành công"
}
```
# 21. Số lượt xem tài nguyên
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-university/by-time/get-unit-action' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCIsIlRlc3QgMTIzNDUiXSwibmFtZSI6ImVkeDEyMyIsImlzU3VwZXJVc2VyIjp0cnVlLCJpZCI6NCwicG9zaXRpb24iOiJpc19xdGNzIiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJleHAiOjE3MjU5MzMxNzMsImlhdCI6MTcyNTg0Njc3M30.sfPlQSEs6EOp2qYWFjrUGCZeTMVbBm_sh0bYebX3iIQ' \
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
> out put
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
  ],
  "message": "Thực hiện thành công"
}
```
# 22. Số lượt chia sẻ tài nguyên

* tương tự số lượt xem tài nguyên => unitActionType = 2

# 23. Số lượt tải xuống tài nguyên

* tương tự số lượt xem tài nguyên => unitActionType = 3