- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Api lấy danh sách trường](#1-api-lấy-danh-sách-trường)
- [2. Api số lượng trường liên kết](#2-số-lượng-trường-liên-kết)
- [3. Api số lượng khóa học theo trường](#3-số-lượng-khóa-học-theo-trường)
- [4. Api số lượng khóa học](#4-số-lượng-khóa-học)
- [5. Api số lượng khóa học theo khoa](#5-số-lượng-khóa-học-theo-khoa)
- [6. Api số lượng bài giảng theo khoa](#6-số-lượng-bài-giảng-theo-khoa)
- [7. Api số lượng bài kiểm tra](#7-số-lượng-bài-kiểm-tra)
- [8. Api số lượng tài liệu tham khảo](#8-số-lượng-tài-liệu-tham-khảo)
- [9. Api số lượng Scorm & xAPI](#9-số-lượng-Scorm-&-xAPI)
- [10. Api số lượng học liệu đa phương tiện](#10-số-lượng-học-liệu-đa-phương-tiện)

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

- universityIds:
  + nhập dựa trên api trả về 

- industryGroupIds: (int[])
  + nhập dựa trên api trả về 
  + bổ sung api sau ngày 19/08/2024

- courseIds: (int[])
  + nhập dựa trên api trả về 
  + dùng api khóa học của giảng viên, có thể thay đổi
```

# 1. Api lấy danh sách trường
> api
```json
curl -X 'GET' \
  'http://localhost:8080/api/chart-admin/filter-university-enroll' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs'
```

> response
```json
{
  "success": true,
  "data": [
    {
      "name": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
      "id": 1
    },
    {
      "name": "ĐẠI HỌC ĐÀ NẴNG",
      "id": 2
    },
    {
      "name": "ĐẠI HỌC HUẾ",
      "id": 3
    },
    {
      "name": "ĐẠI HỌC KINH TẾ TP. HỒ CHÍ MINH",
      "id": 4
    },
    {
      "name": "ĐẠI HỌC QUỐC GIA HÀ NỘI",
      "id": 5
    },
    {
      "name": "ĐẠI HỌC QUỐC GIA TP. HỒ CHÍ MINH",
      "id": 6
    },
    {
      "name": "ĐẠI HỌC THÁI NGUYÊN",
      "id": 7
    },
    {
      "name": "ĐẠI HỌC Y DƯỢC TP. HỒ CHÍ MINH",
      "id": 8
    },
    {
      "name": "HỌC VIỆN ÂM NHẠC HUẾ",
      "id": 9
    },
    {
      "name": "HỌC VIỆN ÂM NHẠC QUỐC GIA VIỆT NAM",
      "id": 10
    }
}

```

# 2. Số lượng trường liên kết
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-university-realtion' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> output

```json
{
  "success": true,
  "data": {
    "total": 11,
    "statistic": [
      {
        "type": 1,
        "criteria": "Hà Nội",
        "count": 7,
        "percentage": 77.77778
      },
      {
        "type": 46,
        "criteria": "Thừa Thiên Huế",
        "count": 1,
        "percentage": 11.111112
      },
      {
        "type": 36,
        "criteria": "Nam Định",
        "count": 1,
        "percentage": 11.111112
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 3. Số lượng khóa học theo trường
```
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-course-by-university-sponsor' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> output

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC THUỶ LỢI",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Phối hợp"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 178,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "values": [
          {
            "count": 54,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 256,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC XÂY DỰNG HÀ NỘI",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Phối hợp"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC KHOA HỌC, ĐẠI HỌC HUẾ",
        "values": [
          {
            "count": 3,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
        "values": [
          {
            "count": 50,
            "percentage": null,
            "criteria": "Phối hợp"
          },
          {
            "count": 101,
            "percentage": null,
            "criteria": "Chủ trì"
          }
        ]
      },
      {
        "type": null,
        "criteria": "ĐẠI HỌC QUỐC GIA HÀ NỘI",
        "values": [
          {
            "count": 4,
            "percentage": null,
            "criteria": "Phối hợp"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC KINH TẾ KỸ THUẬT CÔNG NGHIỆP",
        "values": [
          {
            "count": 6,
            "percentage": null,
            "criteria": "Phối hợp"
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

# 4. Số lượng khóa học
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-course-by-format-university' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> output

```json
{
  "success": true,
  "data": {
    "statistic": [
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC HÀ NỘI",
        "values": [
          {
            "count": 34,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC KINH TẾ QUỐC DÂN",
        "values": [
          {
            "count": 97,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          },
          {
            "count": 3,
            "percentage": null,
            "criteria": "Riêng tư"
          },
          {
            "count": 17,
            "percentage": null,
            "criteria": "Tự do"
          }
        ]
      },
      {
        "type": null,
        "criteria": "ĐẠI HỌC BÁCH KHOA HÀ NỘI",
        "values": [
          {
            "count": 13,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          },
          {
            "count": 1,
            "percentage": null,
            "criteria": "Tự do"
          }
        ]
      },
      {
        "type": null,
        "criteria": "TRƯỜNG ĐẠI HỌC KHOA HỌC, ĐẠI HỌC HUẾ",
        "values": [
          {
            "count": 1,
            "percentage": null,
            "criteria": "Thẻ ghi danh"
          }
        ]
      }
    ],
    "total": 166,
    "subTotal": []
  },
  "message": "Thực hiện thành công"
}
```

# 5. Số lượng khóa học theo khoa
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-course-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> output
```json
{
  "success": true,
  "data": {
    "total": 310,
    "statistic": [
      {
        "type": 29,
        "criteria": "Toán học",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 17,
        "criteria": "Văn thư, lưu trữ, bảo tàng",
        "count": 3,
        "percentage": 0.96774197
      },
      {
        "type": 34,
        "criteria": "Công nghệ Kỹ thuật cơ khí",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 5,
        "criteria": "Năng khiếu Nghe nhìn",
        "count": 18,
        "percentage": 5.806452
      },
      {
        "type": 2,
        "criteria": "Đào tạo giáo viên sư phạm",
        "count": 71,
        "percentage": 22.903227
      },
      {
        "type": 6,
        "criteria": "Năng khiếu Mỹ thuật ứng dụng",
        "count": 10,
        "percentage": 3.2258062
      },
      {
        "type": 32,
        "criteria": "Công nghệ thông tin",
        "count": 2,
        "percentage": 0.6451613
      },
      {
        "type": 3,
        "criteria": "Năng khiếu Mỹ thuật",
        "count": 39,
        "percentage": 12.580645
      },
      {
        "type": 7,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
        "count": 12,
        "percentage": 3.8709679
      },
      {
        "type": 37,
        "criteria": "Quản lý công nghiệp",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 35,
        "criteria": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 1,
        "criteria": "Khoa học giáo dục",
        "count": 97,
        "percentage": 31.290323
      },
      {
        "type": 31,
        "criteria": "Máy tính",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 15,
        "criteria": "Báo chí và truyền thông",
        "count": 3,
        "percentage": 0.96774197
      },
      {
        "type": 16,
        "criteria": "Thông tin – Thư viện",
        "count": 3,
        "percentage": 0.96774197
      },
      {
        "type": 13,
        "criteria": "Địa lý học",
        "count": 3,
        "percentage": 0.96774197
      },
      {
        "type": 8,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
        "count": 4,
        "percentage": 1.2903225
      },
      {
        "type": 4,
        "criteria": "Năng khiếu Trình diễn",
        "count": 33,
        "percentage": 10.645162
      },
      {
        "type": 36,
        "criteria": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 11,
        "criteria": "Xã hội học và nhân học",
        "count": 4,
        "percentage": 1.2903225
      },
      {
        "type": 33,
        "criteria": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
        "count": 1,
        "percentage": 0.32258064
      },
      {
        "type": 73,
        "criteria": "Hóa học",
        "count": 1,
        "percentage": 0.32258064
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 6. Số lượng bài giảng theo khoa
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-unit-by-industry-group' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> output

```json
{
  "success": true,
  "data": {
    "total": 3043,
    "statistic": [
      {
        "type": 29,
        "criteria": "Toán học",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 17,
        "criteria": "Văn thư, lưu trữ, bảo tàng",
        "count": 12,
        "percentage": 0.39434767
      },
      {
        "type": 34,
        "criteria": "Công nghệ Kỹ thuật cơ khí",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 5,
        "criteria": "Năng khiếu Nghe nhìn",
        "count": 161,
        "percentage": 5.290831
      },
      {
        "type": 2,
        "criteria": "Đào tạo giáo viên sư phạm",
        "count": 730,
        "percentage": 23.989483
      },
      {
        "type": 6,
        "criteria": "Năng khiếu Mỹ thuật ứng dụng",
        "count": 129,
        "percentage": 4.239238
      },
      {
        "type": 32,
        "criteria": "Công nghệ thông tin",
        "count": 8,
        "percentage": 0.26289847
      },
      {
        "type": 3,
        "criteria": "Năng khiếu Mỹ thuật",
        "count": 398,
        "percentage": 13.079198
      },
      {
        "type": 7,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa Việt Nam",
        "count": 93,
        "percentage": 3.0561945
      },
      {
        "type": 37,
        "criteria": "Quản lý công nghiệp",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 35,
        "criteria": "Công nghệ Kỹ thuật điện, điện tử và viễn thông",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 1,
        "criteria": "Khoa học giáo dục",
        "count": 1094,
        "percentage": 35.951363
      },
      {
        "type": 31,
        "criteria": "Máy tính",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 15,
        "criteria": "Báo chí và truyền thông",
        "count": 12,
        "percentage": 0.39434767
      },
      {
        "type": 16,
        "criteria": "Thông tin – Thư viện",
        "count": 12,
        "percentage": 0.39434767
      },
      {
        "type": 13,
        "criteria": "Địa lý học",
        "count": 12,
        "percentage": 0.39434767
      },
      {
        "type": 8,
        "criteria": "Ngôn ngữ, Văn học và Văn hóa nước ngoài",
        "count": 13,
        "percentage": 0.42721
      },
      {
        "type": 4,
        "criteria": "Năng khiếu Trình diễn",
        "count": 283,
        "percentage": 9.300033
      },
      {
        "type": 36,
        "criteria": "Công nghệ hóa học, vật liệu, luyện kim và môi trường",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 11,
        "criteria": "Xã hội học và nhân học",
        "count": 43,
        "percentage": 1.4130791
      },
      {
        "type": 33,
        "criteria": "Công nghệ kỹ thuật kiến trúc và công trình xây dựng",
        "count": 4,
        "percentage": 0.13144924
      },
      {
        "type": 73,
        "criteria": "Hóa học",
        "count": 15,
        "percentage": 0.4929346
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 7. Số lượng bài kiểm tra
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-university-test-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> out put
```json
{
  "success": true,
  "data": {
    "total": 124,
    "statistic": [
      {
        "type": 1,
        "criteria": "Bài Tập",
        "count": 96,
        "percentage": 77.41935
      },
      {
        "type": 2,
        "criteria": "Bài Kiểm Tra",
        "count": 21,
        "percentage": 16.935484
      },
      {
        "type": 3,
        "criteria": "Bài Thi",
        "count": 7,
        "percentage": 5.645161
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 8. Số lượng tài liệu tham khảo
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-university-reference-source-by-type' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> out put
```json
{
  "success": true,
  "data": {
    "total": 152,
    "statistic": [
      {
        "type": 3,
        "criteria": "Mp3",
        "count": 12,
        "percentage": 7.8947363
      },
      {
        "type": 1,
        "criteria": "Video",
        "count": 105,
        "percentage": 69.07895
      },
      {
        "type": 2,
        "criteria": "Pdf",
        "count": 35,
        "percentage": 23.026316
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 9. Số lượng Scorm & xAPI
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-university-scorm-xapi-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
}'
```
> out put
```json
{
  "success": true,
  "data": {
    "total": 8,
    "statistic": [
      {
        "type": 1,
        "criteria": "scorm",
        "count": 5,
        "percentage": 62.5
      },
      {
        "type": 2,
        "criteria": "xapi",
        "count": 3,
        "percentage": 37.5
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

# 10. Số lượng học liệu đa phương tiện
```json
curl -X 'POST' \
  'http://localhost:8080/api/chart-admin/get-university-multi-media-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJHacOhbSDEkeG7kWMiLCJLaGFvIHNhdCIsIlFUS0giLCJHaeG6o25nIHZpw6puIiwiUVRIVCIsInBoYW4gcXV5ZW4gZGVmYXVsdCJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyNDk4ODA5MiwiaWF0IjoxNzI0OTAxNjkyfQ.MXytjCpC4Yle1w_jbiYHyZjYlz-X_ixxm5VZmF7lCFs' \
  -H 'Content-Type: application/json' \
  -d '{
  "from": "2024-01-16T09:13:32.339Z",
  "to": "2024-08-16T09:13:32.339Z",
  "courseLevelIds": [],
  "industryGroupIds": [],
  "courseIds": [],
  "universityIds": []
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
        "type": 3,
        "criteria": "text",
        "count": 4,
        "percentage": 13.793103
      },
      {
        "type": 4,
        "criteria": "mp3",
        "count": 3,
        "percentage": 10.344828
      },
      {
        "type": 1,
        "criteria": "video",
        "count": 17,
        "percentage": 58.62069
      },
      {
        "type": 2,
        "criteria": "pdf",
        "count": 5,
        "percentage": 17.241379
      }
    ]
  },
  "message": "Thực hiện thành công"
}
```

