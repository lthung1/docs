- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API bắt đầu làm bài kiểm tra](#1-api-bắt-đầu-làm-bài-kiểm-tra)
- [2. API tạm dừng làm bài kiểm tra](#2-api-tạm-dừng-làm-bài-kiểm-tra)
- [3. API tiếp tục làm bài kiểm tra](#3-api-tiếp-tục-làm-bài-kiểm-tra)
- [4. API bắt đầu riêng lẻ các câu hỏi](#4-api-bắt-đầu-riêng-lẻ-các-câu-hỏi)
- [5. API nộp cả bài](#5-api-nộp-cả-bài)
- [6. API nộp riêng lẻ từng câu](#6-api-nộp-riêng-lẻ-từng-câu)
- [7. API xem kết quả](#7-api-xem-kết-quả)
- [8. API xem kết quả theo ngày](#8-api-xem-kết-quả-theo-ngày)
- [9. API lưu report bài kiểm tra theo phiên](#9-api-lưu-report-bài-kiểm-tra-theo-phiên)
- [10. API tìm kiếm bài tập, bài kiểm tra, bài thi](#10-api-tìm-kiếm-bài-tập-bài-kiểm-tra-bài-thi)
# 0. Một số chú thích ban đầu
<h2>Phần thi</h2>

> các type của câu hỏi :

| Type   | Chú thích | loại câu hỏi |
|-------------| --------- |----------|
| 1  | Câu hỏi nhiều lựa chọn văn bản         | Trắc nghiệm     |
| 2  | Câu hỏi nhiều lựa chọn ảnh        | Trắc nghiệm     |
| 3  | Câu hỏi nhiều lựa chọn video         | Trắc nghiệm     |
| 4  | Câu hỏi dạng đúng sai         | Trắc nghiệm     |
| 5  | Câu hỏi dạng danh sách         | Trắc nghiệm     |
| 6 | Câu hỏi dạng nhiều câu trả lời văn bản         | Trắc nghiệm     |
| 7  | Câu hỏi dạng nhiều câu trả lời ảnh         | Trắc nghiệm     |
| 8  | Câu hỏi dạng nhiều câu trả lời video         | Trắc nghiệm     |
| 9  | Câu hỏi trả lời dạng văn bản ngắn         | Trắc nghiệm     |
| 11  | Câu hỏi dạng kết nối         | nối     |
| 12  | Câu hỏi trả lời bằng file đính kèm         | content    |
| 13  | Câu hỏi trả lời bằng ghi hình         | content    |
| 14  | Câu hỏi trả lời bằng ghi âm         | content    |

<br/>
<hr/>
<br/>

<h2>Phần tìm kiếm bài thi, bài tập, kiểm tra</h2>
> các type trạng thái (status) : dùng cho UC 914, 915, 916

| Type   | Chú thích |
|-------------| --------- |
|1| Đã làm |
|2| Chưa làm |
|3| Sắp đến hạn nộp |

> các type kết quả (resultStatus): dùng cho UC 914, 915, 916

Chưa có use case để lưu trũ dữ liệu này

> Type loại bài (type)

| Type   | Chú thích |
|-------------| --------- |
|1| Bài tập |
|2| Bài kiểm tra |
|3| Bài thi |

# 1. API bắt đầu làm bài kiểm tra
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgxNjA3MDEsImV4cCI6MTcxODI0NzEwMX0.OGRF1em_A-I1Qr7-HhAzShumpqULEroaTFutiUdLIWg' \
  -H 'Content-Type: application/json' \
  -d '{
  "courseId": 242,
  "blockId": 787
}'
```

> input

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| courseId  | y         | long     | mã khoá học  |
| blockId  | y         | long     | mã block của học liệu  |


> UseCase tương ứng 
```
UseCase 570
```

> output

```json
{
  "success": true,
  "data": {
    "blockId": 787,
    "sessionId": "17e3d728-e6ed-4c7a-97fa-0120340ae3d3",
    "groups": [
      {
        "id": 2058,
        "courseUnitId": 2211,
        "title": "Phần bắt đầu",
        "description": "Chào mừng bạn, đây là phần mở đầu!",
        "orderNumber": 1,
        "quiz": []
      },
      {
        "id": 2059,
        "courseUnitId": 2211,
        "title": "Phần 1",
        "description": null,
        "orderNumber": 2,
        "quiz": [
          {
            "id": 3678,
            "courseBlockGroupId": 2059,
            "type": 1,
            "timeToCompleted": 60,
            "question": "<p>Lý Thái Tổ tên thật là gì ?</p>",
            "mustAnswer": null,
            "quizOrder": 1,
            "questions": [
              {
                "uuid": "459dff7e-1a85-43a8-a126-64eb07c9c4bc",
                "filePath": null,
                "orderNumber": 1,
                "point": 0,
                "content": "Lý Thường Kiệt"
              },
              {
                "uuid": "4b7b88f7-d156-4251-be7e-7f4a086a9d8e",
                "filePath": null,
                "orderNumber": 2,
                "point": 0,
                "content": "Lý Công Uẩn"
              },
              {
                "uuid": "f9628da4-1573-450c-b3c5-2501b97f7db7",
                "filePath": null,
                "orderNumber": 3,
                "point": 0,
                "content": "Lý Đắc Kỳ"
              },
              {
                "uuid": "afdd96d5-318a-492b-9e67-491c4c35173f",
                "filePath": null,
                "orderNumber": 4,
                "point": 0,
                "content": "Lý Luận"
              }
            ],
            "settingGeneral": {
              "showForViewer": true,
              "requiredAnswer": true,
              "haveCorrectAnswer": true,
              "shuffleQuestion": true,
              "displayScoreCriteria": null,
              "numberingType": 4,
              "numberingType2": null,
              "fileQuantity": 0,
              "fileCapacity": 0,
              "quizCorrectKeyValues": null
            },
            "settingPointDto": null,
            "settingHint": {
              "isDisplayInstruction": true,
              "content": "Hướng dẫn"
            },
            "settingResponse": {
              "isDisplayPerResponse": false,
              "correct": "",
              "incorrect": "",
              "notYet": ""
            },
            "pauseInfo": null,
            "result": null,
            "isSubmitQuestions": null,
            "isCurrentQuestion": false
          },
          {
            "id": 3687,
            "courseBlockGroupId": 2059,
            "type": 11,
            "timeToCompleted": 60,
            "question": "<p>Câu hỏi dạng kết nối</p>",
            "mustAnswer": null,
            "quizOrder": 10,
            "questions": [
              {
                "uuid": null,
                "filePath": "",
                "orderNumber": 1,
                "point": 0,
                "content": {
                  "left": {
                    "key": "e67a61dc-18cf-49f0-bcf2-47b19a2f0d84",
                    "content": "Minh"
                  },
                  "right": {
                    "key": "bfe6dc82-a678-4afd-8d43-6ac60efc74be",
                    "content": "khắm"
                  }
                }
              },
              {
                "uuid": null,
                "filePath": "",
                "orderNumber": 2,
                "point": 0,
                "content": {
                  "left": {
                    "key": "459a7bc3-20fc-40b9-8921-4001014674e5",
                    "content": "Nam Nê "
                  },
                  "right": {
                    "key": "6fc60f3a-2e83-4ca9-ac66-31be9c7a085d",
                    "content": "nói lắm"
                  }
                }
              }
            ],
            "settingGeneral": {
              "showForViewer": true,
              "requiredAnswer": true,
              "haveCorrectAnswer": true,
              "shuffleQuestion": true,
              "displayScoreCriteria": null,
              "numberingType": 1,
              "numberingType2": null,
              "fileQuantity": 0,
              "fileCapacity": 0,
              "quizCorrectKeyValues": null
            },
            "settingPointDto": null,
            "settingHint": {
              "isDisplayInstruction": false,
              "content": ""
            },
            "settingResponse": {
              "isDisplayPerResponse": false,
              "correct": "",
              "incorrect": "",
              "notYet": ""
            },
            "pauseInfo": null,
            "result": null,
            "isSubmitQuestions": null,
            "isCurrentQuestion": false
          },
          {
            "id": 3689,
            "courseBlockGroupId": 2059,
            "type": 13,
            "timeToCompleted": 60,
            "question": "<p>Câu hỏi trả lời bằng ghi hình ?</p>",
            "mustAnswer": null,
            "quizOrder": 12,
            "questions": [
              {
                "uuid": "8a7c1364-77e7-4600-98dd-3117691b2c61",
                "filePath": "",
                "orderNumber": 1,
                "point": null,
                "content": "HÌnh rõ ràng"
              }
            ],
            "settingGeneral": {
              "showForViewer": true,
              "requiredAnswer": true,
              "haveCorrectAnswer": true,
              "shuffleQuestion": true,
              "displayScoreCriteria": null,
              "numberingType": 1,
              "numberingType2": null,
              "fileQuantity": 1,
              "fileCapacity": 20,
              "quizCorrectKeyValues": null
            },
            "settingPointDto": null,
            "settingHint": {
              "isDisplayInstruction": false,
              "content": ""
            },
            "settingResponse": {
              "isDisplayPerResponse": false,
              "correct": "",
              "incorrect": "",
              "notYet": ""
            },
            "pauseInfo": null,
            "result": null,
            "isSubmitQuestions": null,
            "isCurrentQuestion": false
          }
        ]
      },
      {
        "id": 2060,
        "courseUnitId": 2211,
        "title": "Phần kết thúc",
        "description": "Tạm biệt, đây là phần kết thúc",
        "orderNumber": 999,
        "quiz": []
      }
    ],
    "config": {
      "id": "66676246391b27973f22731b",
      "blockId": 787,
      "isShowResult": true,
      "isLimitedTimeToStart": true,
      "limitedTime": null,
      "isLimitTimeFinishAllQuestion": true,
      "isLimitTimeFinishSingleQuestion": true,
      "totalTime": 5,
      "singleTime": 1,
      "retryTime": 2147483647,
      "showResponseType": null,
      "isShowResultWhenDone": true,
      "showTotalCorrectAnswer": false,
      "showTotalRecord": false,
      "showRecordByGroup": false,
      "showTotalTimeComplete": false,
      "showTotalTime": false,
      "showTotalTryTime": false,
      "showDownloadPdfButton": false,
      "layout": null,
      "timeToRetry": 0,
      "deltaTime": 1000
    },
    "timeToCompleted": 300,
    "result": null
  },
  "message": "Thực hiện thành công"
}
```

> note các field chính phần ngoài cùng (Phần ngoài cục group): 

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| blockId  | y         | long     | mã block của học liệu  |
| sessionId  | y         | string     | Phiên làm bài hiện tại  |
| groups | y | arr | các phần của bài kiểm tra , chỉ làm các phần có groups khác rỗng |
| config | y | object | global config của một bài kiểm tra |
| timeToCompleted | y | int | thời gian tối đa hoàn thành bài này không có thì là 0 hoặc null , đơn vị là giây|

> note các field phần groups (Phần ngoài cục quiz): 

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| id  | y         | long     | mã group  |
| courseUnitId   | y         | long     | mã của unit  |
| title | y | string | Tên phần |
| description | y | string | description |
| orderNumber | y | long | thứ tự của phần |


> note các field trong quiz (Phần ngoài cục questions) :

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| id  | y         | long     | mã quiz  |
| courseBlockGroupId   | y         | long     | mã group  |
| type | y | int | type của câu hỏi (note ở phần trên) |
| timeToCompleted | y | int | thời gian tối đa hoàn thành câu hỏi này không có thì là 0 hoặc null , đơn vị là giây|
| question | y | string | Nội dung của câu hỏi |
| mustAnswer | y | bool | câu hỏi có bắt buộc phải trả lời không |
| quizOrder | y | int | thứ tự của câu hỏi |

* Các phần setting trong object câu hỏi chưa có nhiều ý nghĩa nên chỉ sử dụng các field có trên bảng để hiển thị

> note các response các đáp án lựa chọn

>> Câu hỏi chọn đáp án :

```json
{
  "uuid": "78fd8ebf-36b6-4c04-aa27-56c9ed7ea37b", // uuid của câu hỏi , sử dụng để gửi đáp án lên
  "filePath": null, // file path của của câu trả lời , có thể là ảnh , video
  "orderNumber": 1,
  "point": 0, // điểm tối đa của câu hỏi
  "content": "Đáp án 1" // text của câu hỏi
}
```


>> Câu hỏi dạng nối :

```json
Các câu hỏi dạng nối sẽ là 1 mảng các object bao gồm phần bên trái và phần bên phải của câu đố
{
  "uuid": null,
  "filePath": "",
  "orderNumber": 1,
  "point": 0,
  "content": {
    "left": {
      "key": "e67a61dc-18cf-49f0-bcf2-47b19a2f0d84",
      "content": "Minh"
    },
    "right": {
      "key": "bfe6dc82-a678-4afd-8d43-6ac60efc74be",
      "content": "khắm"
    }
  }
}
```

>> Câu hỏi dạng gửi file :

```json
{
  "uuid": "8a7c1364-77e7-4600-98dd-3117691b2c61",
  "filePath": "",
  "orderNumber": 1,
  "point": null,
  "content": "HÌnh rõ ràng"
}
```

>> Chú thích các field trong global_config : field config

```json
{
      "id": "66676246391b27973f22731b",
      "blockId": 787,
      "isShowResult": true, // show kết quả sau khi hoàn thành
      "isLimitedTimeToStart": true, // có thời gian giới hạn để start
      "limitedTime": "2024-01-01 00:00:00Z", // thời gian tối đa để hoàn thành bài này
      "isLimitTimeFinishAllQuestion": true, // có thời gian hoàn thành toàn bộ bài kiểm tra
      "isLimitTimeFinishSingleQuestion": true, // có thời gian hoàn thành từng câu hỏi
      "totalTime": 5, // thời gian tối đa hoàn thành bài kiểm tra (số phút)
      "singleTime": 1, // thời gian tối đa hoàn thành từng câu (số giây)
      "retryTime": 2147483647, // số lần thử còn lại
      "showResponseType": null,
      "isShowResultWhenDone": true,
      "showTotalCorrectAnswer": false,
      "showTotalRecord": false,
      "showRecordByGroup": false,
      "showTotalTimeComplete": false,
      "showTotalTime": false,
      "showTotalTryTime": false,
      "showDownloadPdfButton": false,
      "layout": null,
      "timeToRetry": 1,  // thời gian thử lại còn lại
      "deltaTime": 1000
    }
```

* Các field results và pauseInfo sẽ không hiển thị tại api này mà sẽ sử dụng ở các api lấy kết quả và start lại sau khi tạm dừng.


# 2. API tạm dừng làm bài kiểm tra

> request
```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/pause' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgxNjA3MDEsImV4cCI6MTcxODI0NzEwMX0.OGRF1em_A-I1Qr7-HhAzShumpqULEroaTFutiUdLIWg' \
  -H 'Content-Type: application/json' \
  -d '{
  "blockId": 843,
  "currentQuizId": 3774,
  "quizRequests": [
    {
      "type": 1,
      "quizId": 3774,
      "questionType": "ChoosingRequest",
      "answer": [
        "973ca72b-4017-4c38-880a-464ca0344cf8"
      ]
    }
  ]
}'
```

> UseCase tương ứng 
```
UseCase 571
```

> input

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| currentQuizId  | y         | long     | mã câu hỏi hiện tại đang thực hiện  |
| blockId  | y         | long     | mã block của học liệu  |
| questionType  | y         | string     | loại câu hỏi của câu hiện tại : ChoosingRequest : câu hỏi trắc nghiệm , ConnectingRequest : câu hỏi nối , ContentRequest : câu hỏi dạng điền file và text|
| type  | y         | long     | type của câu hỏi , đã chú thích ở trên  |

> object answer với từng loại câu hỏi 

* Object answer lưu lại câu trả lời của user tại các câu hỏi đã làm khi nhấn pause

>> Câu hỏi dạng trắc nghiệm 
```
"answer": ["973ca72b-4017-4c38-880a-464ca0344cf8" , "973ca72b-4017-4c38-880a-464ca0344cf9"]
```

>> Câu hỏi dạng nối : 
```
"answer": [
  {
    "left": {
      "key": "ada68c9f-5f7f-4f2b-afa0-e808803d3819",
      "content": "Hùng"
    },
    "right": {
      "key": "d625bbf8-3f25-44ea-b7b3-4ca81cdf4db3",
      "content": "Nhân viên"
    }
  },
  {
    "left": {
      "key": "6ded75c6-7a6d-4765-a65c-b4359c5e35ad",
      "content": "Minh"
    },
    "right": {
      "key": "4b28ef00-3e2b-4189-bcfd-e61cefa62ca0",
      "content": "Chủ tịch"
    }
  }
]
```

>> Câu hỏi dạng link hoặc text

```
"answer": ["s3.moooc.xyz"]
```

> response

```json
{
    "success": true,
    "data": "Tạm dừng bài kiểm tra thành công",
    "message": "Thực hiện thành công"
}
```

# 3. API tiếp tục làm bài kiểm tra

> request
```json
curl --location --request PUT 'https://be.moooc.xyz/v2api/course/structure/exam/continue' \
--header 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgyNDM3NzEsImV4cCI6MTcxODMzMDE3MX0.7aY7hwY2X3m7iH8Cz62MT_87-zBwxHiWn2zeEsT3l0Y' \
--data '{"sessionId":"158be8b1-8c4d-47ef-89cf-ace3e718b190","blockId":786}'
```

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| sessionId  | y         | long     | session đã tạm dừng |
| blockId  | y         | long     | mã block của học liệu  |


> UseCase tương ứng 
```
UseCase 571
```

> response 

* Object trả về sẽ tương đương với object ở api số 1 , tuy nhiên nếu truyền lên đáp án của các câu trước đó , sẽ có thông tin của object pauseInfo

>> Với các câu hỏi trắc nghiệm

```json
"pauseInfo": {
  "currentAnswer": {
    "questionType": "ChoosingRequest",
    "quizId": 3677,
    "type": 1,
    "answer": [
      "46ad9feb-8a8b-4f2b-ac17-47d64a46e09c"
    ]
  }
}
```

>> Với các câu hỏi trắc nghiệm

```json
"pauseInfo": {
  "currentAnswer": {
    "questionType": "ChoosingRequest",
    "quizId": 3677,
    "type": 1,
    "answer": [
      "46ad9feb-8a8b-4f2b-ac17-47d64a46e09c"
    ]
  }
}
```

>> Với các câu hỏi dạng nối

```json
"pauseInfo": {
  "currentAnswer": {
    "questionType": "ConnectingRequest",
    "quizId": 3677,
    "type": 11,
    "answer": [
      {
        "left": {
          "key": "ada68c9f-5f7f-4f2b-afa0-e808803d3819",
          "content": "Hùng"
        },
        "right": {
          "key": "d625bbf8-3f25-44ea-b7b3-4ca81cdf4db3",
          "content": "Nhân viên"
        }
      },
      {
        "left": {
          "key": "6ded75c6-7a6d-4765-a65c-b4359c5e35ad",
          "content": "Minh"
        },
        "right": {
          "key": "4b28ef00-3e2b-4189-bcfd-e61cefa62ca0",
          "content": "Chủ tịch"
        }
      }
    ]
  }
}
```

>> Với các câu hỏi dạng link , text

```json
"pauseInfo": {
  "currentAnswer": {
    "questionType": "ContentRequest",
    "quizId": 3677,
    "type": 11,
    "answer": ["s3.moooc.xyz"]
  }
}
```

# 4. API bắt đầu riêng lẻ các câu hỏi
* API này chỉ sử dụng cho các câu hỏi cần phải đếm giờ (timeToCompleted khác null và khác 0)
```
UseCase 570.BS
```
> request

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/start-single' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgxNjA3MDEsImV4cCI6MTcxODI0NzEwMX0.OGRF1em_A-I1Qr7-HhAzShumpqULEroaTFutiUdLIWg' \
  -H 'Content-Type: application/json' \
  -d '{
  "blockId": 787,
  "quizId": 3688
}'
```

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| quizId  | y         | long     | mã câu hỏi  |
| blockId  | y         | long     | mã block của học liệu  |

> response 

```json
{
  "success": true,
  "data": {
    "time": 60, // thời gian tính giờ cho câu hỏi đó
    "message": "Bắt đầu tính giờ làm câu hỏi thành công"
  },
  "message": "Thực hiện thành công"
}
```


# 5. API nộp cả bài

> UseCase tương ứng 
```
UseCase 572
```

> request

```json
curl --location 'https://be.moooc.xyz/v2/api/course/structure/exam/submit' \
--header 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgyNDM3NzEsImV4cCI6MTcxODMzMDE3MX0.7aY7hwY2X3m7iH8Cz62MT_87-zBwxHiWn2zeEsT3l0Y' \
--data '{
    "blockId": 787,
    "quizRequests": [
        {
            "type": 1,
            "quizId": 3678,
            "questionType": "ChoosingRequest",
            "answer": [
                "459dff7e-1a85-43a8-a126-64eb07c9c4bc"
            ]
        }
        {
            "type": 9,
            "quizId": 3686,
            "questionType": "ContentRequest",
            "answer": [
                "không"
            ]
        },
        {
            "type": 11,
            "quizId": 3687,
            "questionType": "ConnectingRequest",
            "answer": [
                {
                    "left": {
                        "key": "46a3e525-76a9-4ce2-b6f2-1d910cbee746",
                        "content": "Tôi đi"
                    },
                    "right": {
                        "key": "6fc60f3a-2e83-4ca9-ac66-31be9c7a085d",
                        "content": "nói lắm"
                    }
                },
                {
                    "left": {
                        "key": "e67a61dc-18cf-49f0-bcf2-47b19a2f0d84",
                        "content": "Minh"
                    },
                    "right": {
                        "key": "bfe6dc82-a678-4afd-8d43-6ac60efc74be",
                        "content": "khắm"
                    }
                }
            ]
        },
        {
            "type": 14,
            "quizId": 3688,
            "questionType": "ContentRequest",
            "answer": [
                "https://s3.moooc.xyz/dev-stable/quiz/20240613081252763.?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240613T081253Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240613%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=ecc9a14e4a86e2023223c23417217b72f086eac4e973ba3b7fccabaae76587da"
            ]
        },
        {
            "type": 13,
            "quizId": 3689,
            "questionType": "ContentRequest",
            "answer": [
                "https://s3.moooc.xyz/dev-stable/quiz/20240613081306308.?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240613T081306Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240613%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=c4ad32b47289d43c7407fd90fd1a4c018c5c055360dce831150fa8ff5d2f9943"
            ]
        }
    ]
}'
```

* các object truyền lên tương đương với các object phía trên của các api 3 và 4

> response

```json
{
    "success": true,
    "data": {
        "startTime": "2024-06-13T08:19:14Z",
        "endTime": "2024-06-13T08:19:36.080251528Z", // thời gian kết thúc
        "sessionId": "04bf0ede-c5f8-4e67-b87c-182883ced949", // session của bài
        "answerSendTime": "2024-06-13T08:19:36.080252367Z", // thời gian gửi bài
        "isAbleToRetry": true, // có được thử lại không
        "isShowResult": true, // có được show đáp án không
        "remainingTimeToRetry": 0, // thời gian thử lại đếm 
        "totalTrainTime": 21 // tổng thời gian làm bài
    },
    "message": "Thực hiện thành công"
}
```

# 6. API nộp riêng lẻ từng câu

* API này chỉ sử dụng cho các câu hỏi đếm giờ nhằm nộp đáp án lên khi hết giờ làm câu đó
> UseCase tương ứng 
```
UseCase 570
```

> request

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/submit-single' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgxNjA3MDEsImV4cCI6MTcxODI0NzEwMX0.OGRF1em_A-I1Qr7-HhAzShumpqULEroaTFutiUdLIWg' \
  -H 'Content-Type: application/json' \
  -d '{
  "blockId": 787,
  "quizRequests": [
    {
      "type": 1,
      "quizId": 3691,
      "questionType": "ChoosingRequest",
      "answer": [
        "00ac3be5-048f-43ef-9c9e-6f2d72bb8db5"
      ]
    }
  ]
}'
```

* các object truyền lên tương đương với các object phía trên của các api 3 và 4

> response

```json
{
    "success": true,
    "data": {
        "startTime": "2024-06-13T08:19:14Z",
        "endTime": "2024-06-13T08:19:36.080251528Z", // thời gian kết thúc
        "sessionId": "04bf0ede-c5f8-4e67-b87c-182883ced949", // session của bài
        "answerSendTime": "2024-06-13T08:19:36.080252367Z", // thời gian gửi bài
        "isAbleToRetry": true, // có được thử lại không
        "isShowResult": true, // có được show đáp án không
        "remainingTimeToRetry": 0, // thời gian thử lại đếm 
        "totalTrainTime": 21 // tổng thời gian làm bài
    },
    "message": "Thực hiện thành công"
}
```

# 7. API xem kết quả

> UseCase tương ứng 
```
UseCase 573
```

> request
```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/result/5e2e748f-b429-4a44-80af-d59639c768ad' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgxNjA3MDEsImV4cCI6MTcxODI0NzEwMX0.OGRF1em_A-I1Qr7-HhAzShumpqULEroaTFutiUdLIWg'
```

* Object trả về sẽ tương đương với object ở api số 1 , tuy nhiên nếu truyền lên đáp án của các câu trước đó , sẽ có thông tin của object result (lưu kết quả)

| Parameter   | Mandatory | datatype | Description | example |
|-------------| --------- |----------|-------------|---------|
| sessionId  | y         | long     | mã phiên làm bài  | 5e2e748f-b429-4a44-80af-d59639c768ad |


* Hiện api này chỉ support tự động chấm các câu hỏi trắc nghiệm và loại câu hỏi nối , các loại câu hỏi khác sẽ bổ sung vào sprint sau

> response
>> Với các câu hỏi trắc nghiệm
```json
[
  [
    {
      "uuid": "05f36b07-ba46-446c-b909-e9f2f5b6fdae", // uuid của câu hỏi
      "message": "", // message trả ra nếu sai hoặc đúng
      "isTrue": true,
      "points": 1 // điểm của câu này
    },
    {
      "uuid": "4b5f0b37-d57d-4c29-a4a8-39ce69c7ff89",
      "message": "",
      "isTrue": true,
      "points": 2
    },
    {
      "uuid": "f539f4b9-baf6-4317-a9b6-aab860bb533d",
      "message": "",
      "isTrue": true,
      "points": 3
    },
    {
      "uuid": "8a9dc0d5-0cb1-4fc2-98d0-ca9821b8b9cf",
      "message": "",
      "isTrue": true,
      "points": 4
    }
  ]
]
```

>> Với các câu hỏi nối

```json
[
  {
    "content": {
      "left": {
        "key": "6ded75c6-7a6d-4765-a65c-b4359c5e35ad"
      },
      "right": {
        "key": "d625bbf8-3f25-44ea-b7b3-4ca81cdf4db3"
      }
    },
    "isTrue": false,
    "points": 0
  },
  {
    "content": {
      "left": {
        "key": "ada68c9f-5f7f-4f2b-afa0-e808803d3819"
      },
      "right": {
        "key": "4b28ef00-3e2b-4189-bcfd-e61cefa62ca0"
      }
    },
    "isTrue": false,
    "points": 0
  }
]
```

# 8. API xem kết quả theo ngày

> UseCase tương ứng 
```
UseCase 573 - 10
```

> request

```json
curl --location 'https://be.moooc.xyz/v2/api/course/structure/exam/submit-history-date/786' \
--header 'accept: */*' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgyMDI5MTYsImV4cCI6MTcxODI4OTMxNn0.E8ksRD0MhIWWvs50p34KsXeFJxXJwBI6fa6bZCFyQ5Q'
```

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| blockId  | y         | long     | id của block  |

> response

```json
{
  "success": true,
  "data": [
    {
      "date": "2024-06-06T09:21:34Z",
      "sessionId": "f28d8cff-bc2a-4333-8907-4ca940edfcd7"
    },
    {
      "date": "2024-06-13T08:33:53Z",
      "sessionId": "b194d4db-5759-4f76-908c-9dcb2c98e3de"
    }
  ],
  "message": "Thực hiện thành công"
}
```

* Note : API này trả ra list ngày và sessionId , để xem kết quả , call api số 7 để lấy kết quả theo sessionId

# 9. API lưu report bài kiểm tra theo phiên

> UseCase tương ứng 
```
UseCase 573 - 3
```

> request

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/report' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTgyMDI5MTYsImV4cCI6MTcxODI4OTMxNn0.E8ksRD0MhIWWvs50p34KsXeFJxXJwBI6fa6bZCFyQ5Q' \
  -H 'Content-Type: application/json' \
  -d '{
  "blockId": 786,
  "sessionId": "ab836460-83c7-4cfd-a8cf-d5067bbae99e",
  "content": "dev chấm sai"
}'
```

| Parameter   | Mandatory | datatype | Description |
|-------------| --------- |----------|-------------|
| blockId  | y         | long     | mã block  |
| sessionId  | y         | string     | mã phiên làm bài  |
| content  | y         | string     | nội dung report  |

> response

```json
{
  "success": true,
  "data": null,
  "message": "Thực hiện thành công"
}
```

# 10. API tìm kiếm bài tập, bài kiểm tra, bài thi

> UseCase tương ứng 
```
UseCase 920
```

> request

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/course/structure/exam/search/3' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MTk0NjExNDQsImV4cCI6MTcxOTU0NzU0NH0.doHM2KTEhxJWgYuIWtrpk3ig1t1A435NYSxjU3alqG4' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyword": "",
  "status": 0,
  "submitDateFrom": "",
  "submitDateTo": "",
  "resultStatus": null,
  "submitTime": null,
  "type": null,
  "sortByName": null,
  "page": 1,
  "size": 10
}'
```

> request

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|-------------|
|  keyword | n         | string     | từ khoá tìm kiếm  ||
|  status | n | int|  Trạng thái |Xem lại phần chú thích (0. không lọc)|
|  submitDateFrom | n |  date    | thời gian nộp bài từ  ||
|  submitDateFrom | n |  date    | thời gian nộp bài đến  ||
|  resultStatus | n |  int    | kết quả  |tạm thời không truyền gì (do chưa có dữ liệu)|
|  submitTime | n |  int    | số lần nộp  bài||
|  type | n |  int    | loại bài|Xem lại phàn chú thích (0. không lọc)|
|  sortByName | n |  string    | sắp xếp|asc, desc|

> response 

```json
{
  "success": true,
  "data": {
    "exams": [
      {
        "id": 373, //blockId
        "examType": 1, // tương ứng với "type" ở request
        "name": "Bài tập về nhà",
        "totalQuestions": 0, // tổng số câu hỏi trong bài
        "duration": 4, // thời gian của bài, tính theo phút
        "dateToCompleteBefore": null, // thời gian cần hoàn thành trước
        "submitDate": "2024-06-27T04:28:46Z", // ngày nộp bài
        "submitTime": 1, // số lần nộp
        "allowedSubmitTime": 1000, // số lần nộp tối đa cho phép
        "resultStatus": null, // kết quả 
        "unitId": 1452,
        "sequenceId": 589,
        "sectionId": 5,
        "overdue": false, // đã quá hạn chưa
        "isRequired": true // bắt buộc hay không
      },
      {
        "id": 417,
        "examType": 1,
        "name": "Test Group",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": null,
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 5,
        "resultStatus": null,
        "unitId": 1520,
        "sequenceId": 589,
        "sectionId": 5,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 832,
        "examType": 1,
        "name": "Bài test 1",
        "totalQuestions": 0,
        "duration": 4,
        "dateToCompleteBefore": null,
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 4,
        "resultStatus": null,
        "unitId": 2256,
        "sequenceId": 1142,
        "sectionId": 13,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 898,
        "examType": 1,
        "name": "Hóa học vô cơ",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": "2024-12-29T21:11:35Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 8,
        "resultStatus": null,
        "unitId": 2357,
        "sequenceId": 1180,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 899,
        "examType": 2,
        "name": "Hóa học hữu cơ",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": "2024-12-29T21:11:35Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 8,
        "resultStatus": null,
        "unitId": 2358,
        "sequenceId": 1180,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 900,
        "examType": 3,
        "name": "Bài tập điện phân",
        "totalQuestions": 0,
        "duration": 4,
        "dateToCompleteBefore": "2024-12-29T21:11:35Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 4,
        "resultStatus": null,
        "unitId": 2359,
        "sequenceId": 1180,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 901,
        "examType": 1,
        "name": "Giao động điều hòa ",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": "2024-11-10T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 4,
        "resultStatus": null,
        "unitId": 2360,
        "sequenceId": 1181,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 902,
        "examType": 2,
        "name": "Phản ứng hạt nhân",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": "2024-11-10T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 3,
        "resultStatus": null,
        "unitId": 2361,
        "sequenceId": 1181,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      },
      {
        "id": 903,
        "examType": 3,
        "name": "Sóng ánh sáng",
        "totalQuestions": 0,
        "duration": 6,
        "dateToCompleteBefore": "2024-11-10T00:00:00Z",
        "submitDate": null,
        "submitTime": 0,
        "allowedSubmitTime": 8,
        "resultStatus": null,
        "unitId": 2362,
        "sequenceId": 1181,
        "sectionId": 850,
        "overdue": false,
        "isRequired": true
      }
    ],
    "totalNumber": 9, // tổng số tất cả
    "testNumber": 2, // tổng số bài thi
    "exerciseNumber": 5, // tổng số bài tập
    "examNumber": 2 // tổng số bài thi
  },
  "message": "Thực hiện thành công"
}
```
