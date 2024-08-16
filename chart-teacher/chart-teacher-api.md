- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Số lượng khóa học theo hình thức xuất bản](#1-Số-lượng-khóa-học-theo-hình-thức-xuất-bản)
- [2. Số lượng bài giảng theo trạng thái xuất bản](#2-Số-lượng-bài-giảng-theo-trạng-thái-xuất-bản)
- [3. Số lượng bài học theo khoa](#3-Số-lượng-bài-học-theo-khoa)
- [4. Số lượng Scorm & xAPI](#4-Số-lượng-Scorm-&-xAPI)
- [5. Số lượng học liệu đa phương tiện theo loại](#5-Số-lượng-học-liệu-đa-phương-tiện-theo-loại)
- [6. Số lượng học liệu theo khóa học](#6-Số-lượng-học-liệu-theo-khóa-học)
- [7. Tỷ lệ kết quả đánh giá theo khóa học](#7-Tỷ-lệ-kết-quả-làm-đánh-giá-theo-khóa-học)
- [8. Tỷ lệ kết quả làm đánh giá theo module](#8-lọc-trường)
- [9. Tỷ lệ kết quả đánh giá theo bài giảng](#9-Tỷ-lệ-kết-quả-đánh-giá-theo-bài-giảng)

# 0. Một số chú thích ban đầu
> giải thích payload bộ lọc chung

* giải thích

```json
{
  "timeUnit": 0, // đơn vị 
  "from": "2024-08-16T09:07:39.376Z",
  "to": "2024-08-16T09:07:39.376Z",
  "courseLevelIds": [
    0
  ],
  "industryGroupIds": [
    0
  ],
  "courseIds": [
    0
  ],
  "courseStructureType": 0,
  "moduleGroup": 0,
  "toDateTime": "2024-08-16",
  "fromDateTime": "2024-08-16",
  "modules": [
    "string"
  ]
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
      "criteria": "Thẻ ghi danh",
      "count": 258,
      "percentage": 98.85057
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
      "criteria": "Bản nháp",
      "count": 687,
      "percentage": 92.5876
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

# 3. Số lượng bài học theo khoa
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
      "type": 32,
      "criteria": "Công nghệ thông tin",
      "count": 2,
      "percentage": 0.17636684
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

# 4. Số lượng Scorm & xAPI
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
      "criteria": "scorm",
      "count": 8,
      "percentage": 12.5
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
      "criteria": "text",
      "count": 27,
      "percentage": 20.149254
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
        "type": 192,
        "criteria": "khoá học 105",
        "values": [
          {
            "count": 2,
            "percentage": null,
            "criteria": "Bài kiểm tra"
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
        "type": 3,
        "criteria": "Xác suất thống kê",
        "values": [
          {
            "count": 1,
            "percentage": 33.33,
            "criteria": "4 sao"
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

# 8. Tỷ lệ kết quả làm đánh giá theo module
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
        "criteria": "Scorm & xAPi",
        "values": [
          {
            "count": 1,
            "percentage": 33.33,
            "criteria": "4 sao"
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
        "type": 1268,
        "criteria": "Bài giảng 1",
        "values": [
          {
            "count": 4,
            "percentage": 100,
            "criteria": "4 sao"
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

