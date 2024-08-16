- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
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