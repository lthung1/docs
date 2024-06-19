- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API lấy ra các thảo luận của học liệu](#1-api-lấy-ra-các-thảo-luận-của-học-liệu)
- [2. API thêm mới thảo luận cho sinh viên](#2-api-thêm-mới-thảo-luận-cho-sinh-viên)
- [3. API cập nhật bình luận cho sinh viên](#3-api-cập-nhật-thảo-luận-cho-sinh-viên)
- [4. API xóa bình luận cho sinh viên](#4-api-xóa-thảo-luận-cho-sinh-viên)
- [5. API ghim ghim thảo luận cho sinh viên](#5-api-ghim-thảo-luận-cho-sinh-viên)
- [6. API trả lời thảo luận cho sinh viên](#6-api-trả-lời-thảo-luận-cho-sinh-viên)
- [7. API like và dislike thảo luận cho sinh viên](#7-api-like-và-dislike-thảo-luận-cho-sinh-viên)
- [8. API xem toàn bộ thảo luận của khóa học cho sinh viên](#8-api-xem-toàn-bộ-thảo-luận-của-khóa-học-cho-sinh-viên)
- [9. API đếm số thảo luận của khóa học(Tất cả, Của tôi, Đã ghim)](#9-api-đếm-số-thảo-luận-của-khóa-học-tất-cả-của-tôi-đã-ghim)
- [10. API đếm số thảo luận của học liệu(Tất cả, Của tôi, Đã ghim)](#10-api-đếm-số-thảo-luận-của-học-liệu-tất-cả-của-tôi-đã-ghim)
- [11. Một số bổ sung cho api cũ](#11-một-số-bổ-sung-cho-api-cũ)


# 0.Một số chú thích ban đầu

> Các type thảo luận:

| Type   | Chú thích | 
|-------------| --------- 
| 1  | Thảo luận của giảng viên |
| 2  | Thảo luận của sinh viên |

> Các type bày tỏ cảm xúc về bình luận:

| Type   | Chú thích | 
|-------------| --------- 
| 1  | LIKE |
| 2  | DISLIKE |

> Luồng tạo mới thảo luận:

* Thêm mới một thảo luận chính là thêm mới một comment level 1
* Thảo luận chính là một vùng lưu trữ các comment
* Có 3 mức comment tương ứng là 1, 2, 3

# 1. API lấy ra các thảo luận của học liệu

> use case tương ứng:
```
UC910
```

> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/get-all-by-unit' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "string"
  ],
  "unitId": 2236,
  "discussionType": 2,
  "isPinned": false,
  "isMine": false
}'
}'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | n         | int     | trang số  ||
| size  | n         | int     | số thảo luận||
| sort  | n         | string     | |  không truyền|
| unitId  | y         | int     | id của học liệu  |
| discussionType  | y         | int     | type thảo luận  |xem lại mục #0|
| isPinned  | n         | boolean     |đã ghim ||
| isMine  | n         | boolean     |của tôi ||

> output:
```json
{
  "success": true,
  "data": {
    "discussions": [
      {
        "id": 10,
        "userId": 84,
        "createdDate": "2024-06-17T16:48:30Z",
        "rootComment": {
          "id": 32,
          "content": "Tạo mới thảo luận của sinh viên",
          "createdDate": "2024-06-17T16:48:30Z",
          "totalReply": null,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 10,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": [
            {
              "id": 36,
              "commentId": 32,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ee411abc-5ae7-4f55-b48d-6b69518c2828bun-cha-ha-noi-2_1688011803.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=ee15f959967d50b63af0a2a013792cc24999f720b8e2b1ea860d75e8b5d74e63",
              "fileName": "bun-cha-ha-noi-2_1688011803.jpg",
              "attachmentType": "image"
            },
            {
              "id": 37,
              "commentId": 32,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/e1578b17-906b-4ba3-9f5e-d350016cc704jack-new-2274.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=8375ecf16aed149520425390e2bb8f69cc544ee1af1c50b895597857e5c21367",
              "fileName": "jack-new-2274.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [],
        "isPinned": true
      },
      {
        "id": 9,
        "userId": 84,
        "createdDate": "2024-06-17T15:33:52Z",
        "rootComment": {
          "id": 30,
          "content": "Thêm mới thảo luận của sinh viên",
          "createdDate": "2024-06-17T15:33:52Z",
          "totalReply": 1,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": 2,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 9,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [
            {
              "reactionType": 2,
              "count": 1
            }
          ],
          "attachments": [
            {
              "id": 30,
              "commentId": 30,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/453f7675-7fe7-4cbf-aca6-7ebbea931c8bAnime-Jujutsu-Kaisen-yuta-okkotsu.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=579c631adf5ab586379f4f2e1b495b278258745c37b2f2bf414f40eaa7f66e7c",
              "fileName": "Anime-Jujutsu-Kaisen-yuta-okkotsu.jpg",
              "attachmentType": "image"
            },
            {
              "id": 31,
              "commentId": 30,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/23737e6c-1cea-4ff0-a32e-770e1425d967images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4443c8dcc5c629aaa7aee883b8a3150ca8d57af2bf3462136e978cbfdf176125",
              "fileName": "images.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 31,
            "content": "Thôi ông đừng có mồm điêu",
            "createdDate": "2024-06-17T15:45:13Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 30,
            "isMine": true,
            "discussionId": 9,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": [
              {
                "id": 35,
                "commentId": 31,
                "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/32a1493f-0e30-4c19-8ab3-18e932b448c5AHuan.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=73be1c95b48637acb4798ca0d4be2015d77e86c68b613b8d58035ede0b6e14c4",
                "fileName": "AHuan.jpg",
                "attachmentType": "image"
              }
            ]
          }
        ],
        "isPinned": false
      },
      {
        "id": 8,
        "userId": 84,
        "createdDate": "2024-06-17T10:51:55Z",
        "rootComment": {
          "id": 28,
          "content": "Sửa lại comment",
          "createdDate": "2024-06-17T10:51:55Z",
          "totalReply": null,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 8,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": []
        },
        "subComments": [],
        "isPinned": false
      },
      {
        "id": 7,
        "userId": 84,
        "createdDate": "2024-06-14T07:27:55Z",
        "rootComment": {
          "id": 26,
          "content": "Đến Hà Nội là phải ăn bún chả",
          "createdDate": "2024-06-14T07:27:55Z",
          "totalReply": 1,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 7,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": [
            {
              "id": 20,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ce6b3fb4-5d4e-4218-b85f-0748b7096033o-xuan-4binbolt-15312882917041602193834.webp?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=cfd69522cc526c037cc56bb59083c92dbbe8da15529209a2010799a023da3d6e",
              "fileName": "o-xuan-4binbolt-15312882917041602193834.webp",
              "attachmentType": "image"
            },
            {
              "id": 21,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/06e7434e-f5b8-486a-8288-30227251dc3da3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=f1e91ebf9a90ca33579e4f2c1e24b98c18488ad025733dcce1e9224a9363e06c",
              "fileName": "a3.jpg",
              "attachmentType": "image"
            },
            {
              "id": 22,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/fe4f7b9b-f44d-4958-b52f-ec250838085bpho-ha-noi-09_1677399161.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=ff2ae9203da9982ca2b4585f9512d83d8b678577ccbdafb74976ad32fa3e0e7b",
              "fileName": "pho-ha-noi-09_1677399161.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 27,
            "content": "Tôi không thích ăn sầu riêng",
            "createdDate": "2024-06-14T07:36:30Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 26,
            "isMine": false,
            "discussionId": 7,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2e6caba2ac8d5be9429dc7cba9a3e4d898849e58c361f3fac5b004c0b7d9acd3",
            "commenterUserId": 4,
            "reactionCount": [],
            "attachments": []
          }
        ],
        "isPinned": false
      },
      {
        "id": 6,
        "userId": 84,
        "createdDate": "2024-06-06T07:21:16Z",
        "rootComment": {
          "id": 25,
          "content": "ahoho",
          "createdDate": "2024-06-06T07:21:16Z",
          "totalReply": null,
          "author": {
            "id": 38,
            "email": "vantungdeveloper@gmail.com",
            "username": "vantungdeveloper@gmail.com",
            "firstName": "Nguyễn",
            "lastName": "Văn Tùng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": false,
          "discussionId": 6,
          "avatar": null,
          "commenterUserId": 38,
          "reactionCount": [],
          "attachments": [
            {
              "id": 18,
              "commentId": 25,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/81d448bc-bf49-435d-a0f9-0546cd120152Capture.JPG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=1ff82a5eebec5dc8fbb96b2de26bbc81b197b4c7611ae08f4f0d9774f3216a86",
              "fileName": "Capture.JPG",
              "attachmentType": "image"
            },
            {
              "id": 19,
              "commentId": 25,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ab9da0ec-41ac-4bbb-9fad-c43fe151592dBurger-Shrimp.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=93c8cd0217948f39b0306b6baceda620b8814dd202baab651bd951e204fbcfeb",
              "fileName": "Burger-Shrimp.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [],
        "isPinned": false
      },
      {
        "id": 3,
        "userId": 84,
        "createdDate": "2024-05-28T17:37:06Z",
        "rootComment": {
          "id": 7,
          "content": "GS Đặng Bảo Chung muốn tích hợp cờ tỷ phú vào học liệu này",
          "createdDate": "2024-05-28T17:37:06Z",
          "totalReply": 4,
          "author": {
            "id": 4,
            "email": "edx@example.com",
            "username": "edx",
            "firstName": "Nguyễn",
            "lastName": "Minh Hồng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": false,
          "discussionId": 3,
          "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2e6caba2ac8d5be9429dc7cba9a3e4d898849e58c361f3fac5b004c0b7d9acd3",
          "commenterUserId": 4,
          "reactionCount": [],
          "attachments": [
            {
              "id": 14,
              "commentId": 7,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/9649d77d-54a3-4d2b-88de-e75c8442d68ajack-va-thien-an-5805.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7fc89cdf71b59afc61539e688eb9ccef9ceec911ea676c3b6c8f91e2e20b1319",
              "fileName": "jack-va-thien-an-5805.jpeg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 8,
            "content": "GS Bùi Ngọc Châu phản đối ý kiến của GS Chung",
            "createdDate": "2024-05-28T17:38:48Z",
            "totalReply": null,
            "author": {
              "id": 3,
              "email": "cms@openedx",
              "username": "cms",
              "firstName": "",
              "lastName": ""
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": false,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 3,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 20,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:39Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 21,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:42Z",
            "totalReply": 1,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2e6caba2ac8d5be9429dc7cba9a3e4d898849e58c361f3fac5b004c0b7d9acd3",
            "commenterUserId": 4,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 22,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:43Z",
            "totalReply": 2,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 23,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:19:04Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 21,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2e6caba2ac8d5be9429dc7cba9a3e4d898849e58c361f3fac5b004c0b7d9acd3",
            "commenterUserId": 4,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 24,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:19:07Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 22,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 29,
            "content": "Tôi xin phép được trả lời như sau",
            "createdDate": "2024-06-17T15:13:39Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 22,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=2e6caba2ac8d5be9429dc7cba9a3e4d898849e58c361f3fac5b004c0b7d9acd3",
            "commenterUserId": 4,
            "reactionCount": [],
            "attachments": [
              {
                "id": 29,
                "commentId": 29,
                "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/251fef53-cceb-4576-9488-c338b60d0177images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T174201Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=f165f23aa79f0826d35200f7e5e6cfde7315e6aad47ea0c8faffffc641c0bcaa",
                "fileName": "images.jpg",
                "attachmentType": "image"
              }
            ]
          }
        ],
        "isPinned": false
      }
    ],
    "total": 6
  },
  "message": "Thực hiện thành công"
}
```

> các field cần chú ý:
* mỗi discussion sẽ trả về một rootComment(comment gốc - level 1) và một list các subComment(comment con, có chứa level và parentId ở trong)
* myReaction (value giống với reactionType) : đây là react của người đang đăng nhập về bình luận.
* level: level của comment
* reactionCount: chứa reactionType và count
* totalReply: tổng số phản hổi
* isMine: comment có phải của người đang đăng nhập không

# 2. API thêm mới thảo luận cho sinh viên
> use case tương ứng:
```
UC910
```

> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/create' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: multipart/form-data' \
  -F 'unitId=2236' \
  -F 'courseId=3' \
  -F 'content=Tạo mới thảo luận của sinh viên' \
  -F 'attachments=@bun-cha-ha-noi-2_1688011803.jpg;type=image/jpeg' \
  -F 'attachments=@jack-new-2274.jpg;type=image/jpeg' \
  -F 'discussionType=2'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| unitId  | y         | int     | id của học liệu  |
| content  | y         | string     | nội dung  |
| discussionType  | y         | int     | type thảo luận  |xem lại mục #0|
| courseId  | y         | int     |id của khóa học ||
| attachments  | n         | file     |file đính kèm | có thể truyền nhiều file|

# 3. API cập nhật thảo luận cho sinh viên
> use case tương ứng:
```
UC910
```
> request
```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/unit-discussion/update-comment' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: multipart/form-data' \
  -F 'id=28' \
  -F 'content=Sửa lại comment' \
  -F 'attachments=@Screenshot 2024-06-05 093206.png;type=image/png' \
  -F 'deleteAttachmentIds=32,33'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id comment  |
| content  | n         | string     | nội dung  ||
| attachments  | n         | file     |các file muốn thêm |có thể truyền nhiều|
| deleteAttachmentIds  | n         | string     |id các file muốn xóa | ngăn cách nhau bằng dấu phảy|

# 4. API xóa thảo luận cho sinh viên
> use case tương ứng:
```
UC910
```
> request
```json
curl -X 'DELETE' \
  'https://be.moooc.xyz/v2/api/unit-discussion/delete/28' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id comment  |

# 5. API ghim thảo luận cho sinh viên
> use case tương ứng:
```
UC910
```
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/pin' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: application/json' \
  -d '{
  "discussionId": 10,
  "courseId": 3
}'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| discussionId  | y         | int     | id thảo luận  |
| courseId  | y         | int     | id khóa học  |

# 6. API trả lời thảo luận cho sinh viên
> use case tương ứng:
```
UC911
```
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/reply' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: multipart/form-data' \
  -F 'content=Thôi ông đừng có mồm điêu' \
  -F 'parentId=30' \
  -F 'attachments=@AHuan.jpg;type=image/jpeg'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| parentId  | y         | int     | id comment gốc  |
| content  | y         | string     | nội dung  |
| attachments  | n         | file     |các file muốn thêm |có thể truyền nhiều|

# 7. API like và dislike thảo luận cho sinh viên
> use case tương ứng:
```
UC912, UC913
```
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/react' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 30,
  "reactionType": 2
}'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id comment|
| reactionType  | y         | int     |type bày tỏ |xem lại mục #0|

# 7. API like và dislike thảo luận cho sinh viên
> use case tương ứng:
```
UC910
```
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/react' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 30,
  "reactionType": 2
}'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id comment|
| reactionType  | y         | int     |type bày tỏ |xem lại mục #0|

# 8. API xem toàn bộ thảo luận của khóa học cho sinh viên
> use case tương ứng:
```
BS 5.3
```
> request
```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/unit-discussion/get-all-by-course' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaG9hbmd2eEBnbWFpbC5jb20iLCJlbWFpbCI6ImhvYW5ndnhAZ21haWwuY29tIiwiaWQiOjg0LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfc3YiLCJyb2xlcyI6W10sImlhdCI6MTcxODYzODM4MywiZXhwIjoxNzE4NzI0NzgzfQ.gfxbbj3VEkfB7LKFTnBQW2A23sqN4c7jVPmwbLHZ1s4' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "sort": [
    "string"
  ],
  "courseId": 3,
  "discussionType": 2,
  "isPinned": false,
  "isMine": false
}'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| page  | n         | int     | trang số  ||
| size  | n         | int     | số thảo luận||
| sort  | n         | string     | |  không truyền|
| courseId  | y         | int     | id của khóa học  |
| discussionType  | y         | int     | type thảo luận  |xem lại mục #0|
| isPinned  | n         | boolean     |đã ghim ||
| isMine  | n         | boolean     |của tôi ||

> output:
```json
{
  "success": true,
  "data": {
    "discussions": [
      {
        "id": 10,
        "userId": 84,
        "createdDate": "2024-06-17T16:48:30Z",
        "rootComment": {
          "id": 32,
          "content": "Tạo mới thảo luận của sinh viên",
          "createdDate": "2024-06-17T16:48:30Z",
          "totalReply": null,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 10,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": [
            {
              "id": 36,
              "commentId": 32,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ee411abc-5ae7-4f55-b48d-6b69518c2828bun-cha-ha-noi-2_1688011803.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=22506beb1778c66dee544d21f03fcc11505bc929757e7b16981286da4f38226a",
              "fileName": "bun-cha-ha-noi-2_1688011803.jpg",
              "attachmentType": "image"
            },
            {
              "id": 37,
              "commentId": 32,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/e1578b17-906b-4ba3-9f5e-d350016cc704jack-new-2274.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=e08c38a9b90ba0699c0ee869326ea12f668cb93f010e51589744e74036da3381",
              "fileName": "jack-new-2274.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [],
        "isPinned": true
      },
      {
        "id": 9,
        "userId": 84,
        "createdDate": "2024-06-17T15:33:52Z",
        "rootComment": {
          "id": 30,
          "content": "Thêm mới thảo luận của sinh viên",
          "createdDate": "2024-06-17T15:33:52Z",
          "totalReply": 1,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": 2,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 9,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [
            {
              "reactionType": 2,
              "count": 1
            }
          ],
          "attachments": [
            {
              "id": 30,
              "commentId": 30,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/453f7675-7fe7-4cbf-aca6-7ebbea931c8bAnime-Jujutsu-Kaisen-yuta-okkotsu.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=0880f698f76fb07939b2887ce5e00f3220ed990d32a859fcdc05c985582a02a3",
              "fileName": "Anime-Jujutsu-Kaisen-yuta-okkotsu.jpg",
              "attachmentType": "image"
            },
            {
              "id": 31,
              "commentId": 30,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/23737e6c-1cea-4ff0-a32e-770e1425d967images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25199&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=a4a0d0ac38158a07fe24a4c006f6db539af518c6f26b8089f8a57c6389a66686",
              "fileName": "images.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 31,
            "content": "Thôi ông đừng có mồm điêu",
            "createdDate": "2024-06-17T15:45:13Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 30,
            "isMine": true,
            "discussionId": 9,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": [
              {
                "id": 35,
                "commentId": 31,
                "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/32a1493f-0e30-4c19-8ab3-18e932b448c5AHuan.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=506b82f4ca504b39f4e68e8b2c8bd518f6fe11966272b6e26bb6dfc4760479d1",
                "fileName": "AHuan.jpg",
                "attachmentType": "image"
              }
            ]
          }
        ],
        "isPinned": false
      },
      {
        "id": 8,
        "userId": 84,
        "createdDate": "2024-06-17T10:51:55Z",
        "rootComment": {
          "id": 28,
          "content": "Sửa lại comment",
          "createdDate": "2024-06-17T10:51:55Z",
          "totalReply": null,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 8,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": []
        },
        "subComments": [],
        "isPinned": false
      },
      {
        "id": 7,
        "userId": 84,
        "createdDate": "2024-06-14T07:27:55Z",
        "rootComment": {
          "id": 26,
          "content": "Đến Hà Nội là phải ăn bún chả",
          "createdDate": "2024-06-14T07:27:55Z",
          "totalReply": 1,
          "author": {
            "id": 84,
            "email": "hoangvx@gmail.com",
            "username": "hoangvx@gmail.com",
            "firstName": "Vũ",
            "lastName": "Xuân Hoàng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": true,
          "discussionId": 7,
          "avatar": null,
          "commenterUserId": 84,
          "reactionCount": [],
          "attachments": [
            {
              "id": 20,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ce6b3fb4-5d4e-4218-b85f-0748b7096033o-xuan-4binbolt-15312882917041602193834.webp?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=87409fa6b67e2da269a6d207704456259cbfc6bdb08c25f8e2b62697a174f0bf",
              "fileName": "o-xuan-4binbolt-15312882917041602193834.webp",
              "attachmentType": "image"
            },
            {
              "id": 21,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/06e7434e-f5b8-486a-8288-30227251dc3da3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=f62000cd56dc6ed480466a40b18729ab2d2bbd4caf9357f494c4cfd28b4ed49e",
              "fileName": "a3.jpg",
              "attachmentType": "image"
            },
            {
              "id": 22,
              "commentId": 26,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/fe4f7b9b-f44d-4958-b52f-ec250838085bpho-ha-noi-09_1677399161.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=8bbba911840ae51cb921e4b9ac2206247ddd497dc594d5231c4d6758e7c50b59",
              "fileName": "pho-ha-noi-09_1677399161.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 27,
            "content": "Tôi không thích ăn sầu riêng",
            "createdDate": "2024-06-14T07:36:30Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 26,
            "isMine": false,
            "discussionId": 7,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7f149855736c5f9c3674d2cceae077a21bcc2ff7f66c6bb6c883be04cbcfd689",
            "commenterUserId": 4,
            "reactionCount": [],
            "attachments": []
          }
        ],
        "isPinned": false
      },
      {
        "id": 6,
        "userId": 84,
        "createdDate": "2024-06-06T07:21:16Z",
        "rootComment": {
          "id": 25,
          "content": "ahoho",
          "createdDate": "2024-06-06T07:21:16Z",
          "totalReply": null,
          "author": {
            "id": 38,
            "email": "vantungdeveloper@gmail.com",
            "username": "vantungdeveloper@gmail.com",
            "firstName": "Nguyễn",
            "lastName": "Văn Tùng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": false,
          "discussionId": 6,
          "avatar": null,
          "commenterUserId": 38,
          "reactionCount": [],
          "attachments": [
            {
              "id": 18,
              "commentId": 25,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/81d448bc-bf49-435d-a0f9-0546cd120152Capture.JPG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4399de01c93e6f717151dfc455b291a9c77df53f4dbbc621ba2728fe9686d404",
              "fileName": "Capture.JPG",
              "attachmentType": "image"
            },
            {
              "id": 19,
              "commentId": 25,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/ab9da0ec-41ac-4bbb-9fad-c43fe151592dBurger-Shrimp.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=b10dc916b10365bf2c3eb651b5e9b5e9b7f6f1b7c873125995ed31bcfcef92a0",
              "fileName": "Burger-Shrimp.jpg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [],
        "isPinned": false
      },
      {
        "id": 3,
        "userId": 84,
        "createdDate": "2024-05-28T17:37:06Z",
        "rootComment": {
          "id": 7,
          "content": "GS Đặng Bảo Chung muốn tích hợp cờ tỷ phú vào học liệu này",
          "createdDate": "2024-05-28T17:37:06Z",
          "totalReply": 4,
          "author": {
            "id": 4,
            "email": "edx@example.com",
            "username": "edx",
            "firstName": "Nguyễn",
            "lastName": "Minh Hồng"
          },
          "myReaction": null,
          "level": 1,
          "parentId": null,
          "isMine": false,
          "discussionId": 3,
          "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7f149855736c5f9c3674d2cceae077a21bcc2ff7f66c6bb6c883be04cbcfd689",
          "commenterUserId": 4,
          "reactionCount": [],
          "attachments": [
            {
              "id": 14,
              "commentId": 7,
              "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/9649d77d-54a3-4d2b-88de-e75c8442d68ajack-va-thien-an-5805.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9beb4f705e6d2bbcfe8c3359da861aa06bf3a9a3b8c5c4d360b39ec6ecf78df8",
              "fileName": "jack-va-thien-an-5805.jpeg",
              "attachmentType": "image"
            }
          ]
        },
        "subComments": [
          {
            "id": 8,
            "content": "GS Bùi Ngọc Châu phản đối ý kiến của GS Chung",
            "createdDate": "2024-05-28T17:38:48Z",
            "totalReply": null,
            "author": {
              "id": 3,
              "email": "cms@openedx",
              "username": "cms",
              "firstName": "",
              "lastName": ""
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": false,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 3,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 20,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:39Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 21,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:42Z",
            "totalReply": 1,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7f149855736c5f9c3674d2cceae077a21bcc2ff7f66c6bb6c883be04cbcfd689",
            "commenterUserId": 4,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 22,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:18:43Z",
            "totalReply": 2,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 2,
            "parentId": 7,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 23,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:19:04Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 21,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7f149855736c5f9c3674d2cceae077a21bcc2ff7f66c6bb6c883be04cbcfd689",
            "commenterUserId": 4,
            "reactionCount": [
              {
                "reactionType": 1,
                "count": 1
              }
            ],
            "attachments": []
          },
          {
            "id": 24,
            "content": "Thêm level 3 cho anh Nam",
            "createdDate": "2024-06-02T07:19:07Z",
            "totalReply": null,
            "author": {
              "id": 84,
              "email": "hoangvx@gmail.com",
              "username": "hoangvx@gmail.com",
              "firstName": "Vũ",
              "lastName": "Xuân Hoàng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 22,
            "isMine": true,
            "discussionId": 3,
            "avatar": null,
            "commenterUserId": 84,
            "reactionCount": [],
            "attachments": []
          },
          {
            "id": 29,
            "content": "Tôi xin phép được trả lời như sau",
            "createdDate": "2024-06-17T15:13:39Z",
            "totalReply": null,
            "author": {
              "id": 4,
              "email": "edx@example.com",
              "username": "edx",
              "firstName": "Nguyễn",
              "lastName": "Minh Hồng"
            },
            "myReaction": null,
            "level": 3,
            "parentId": 22,
            "isMine": false,
            "discussionId": 3,
            "avatar": "https://s3.moooc.xyz/dev-stable/user-profile-images/1708920027517_image.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7f149855736c5f9c3674d2cceae077a21bcc2ff7f66c6bb6c883be04cbcfd689",
            "commenterUserId": 4,
            "reactionCount": [],
            "attachments": [
              {
                "id": 29,
                "commentId": 29,
                "mainKey": "https://s3.moooc.xyz/dev-stable/unit_discussion/251fef53-cceb-4576-9488-c338b60d0177images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240617T175404Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240617%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7a90c45e6b62e1feed850927c083ce83d1fac207d1ec9bef09a7dc68cad7ac75",
                "fileName": "images.jpg",
                "attachmentType": "image"
              }
            ]
          }
        ],
        "isPinned": false
      }
    ],
    "total": 6
  },
  "message": "Thực hiện thành công"
}
```
> một số field cần chú ý:
* mỗi discussion sẽ trả về một rootComment(comment gốc - level 1) và một list các subComment(comment con, có chứa level và parentId ở trong)
* myReaction (value giống với reactionType) : đây là react của người đang đăng nhập về bình luận.
* level: level của comment
* reactionCount: chứa reactionType và count
* totalReply: tổng số phản hổi
* isMine: comment có phải của người đang đăng nhập không
* isPinned: thảo luận có được ghim không

# 9. API đếm số thảo luận của khóa học (Tất cả, của tôi, đã ghim)
> note :

* cần sửa lại, chưa dùng được, đổi tên đường dẫn thành get-count-by-course

> use case tương ứng:
```
BS 5.3
```
> request:
```json
curl -X 'GET' \
  curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/unit-discussion/get-count-by-course/3?discussionType=2' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbImdoYURTSEdKSEpTREEiXSwiaWF0IjoxNzE4Nzc5NTE4LCJleHAiOjE3MTg3ODMxMTh9.JY4CqmtOxbzpnst6IkTxfBSU_HztlMHSGJwVYCKoCYM'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id khóa học|path|
| discussionType  | y         | int     | id khóa học|param|

> output :
```json
{
  "success": true,
  "data": {
    "totalNumber": 7,
    "pinnedNumber": 1,
    "mineNumber": 7
  },
  "message": "Thực hiện thành công"
}
```

# 10. API đếm số thảo luận của học liệu (Tất cả, của tôi, đã ghim)
> use case tương ứng:
```
UC910
```
> request
```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/unit-discussion/get-count-by-unit/2236?discussionType=2' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbImdoYURTSEdKSEpTREEiXSwiaWF0IjoxNzE4Nzc5NTE4LCJleHAiOjE3MTg3ODMxMTh9.JY4CqmtOxbzpnst6IkTxfBSU_HztlMHSGJwVYCKoCYM'
```

> input:

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| id  | y         | int     | id học liệu| path|
| discussionType  | y         | int     | loại thảo luận| param|

> output: 

```json
{
  "success": true,
  "data": {
    "totalNumber": 8,
    "pinnedNumber": 1,
    "mineNumber": 2
  },
  "message": "Thực hiện thành công"
}
```

# 11. Một số bổ sung cho api cũ

> api đã được bổ sung thêm field:

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/mooc-course-unit/get-unit/2236' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbImdoYURTSEdKSEpTREEiXSwiaWF0IjoxNzE4Nzc5NTE4LCJleHAiOjE3MTg3ODMxMTh9.JY4CqmtOxbzpnst6IkTxfBSU_HztlMHSGJwVYCKoCYM'
```

> chức năng chính : lấy ra chi tiết học liệu

> field bổ sung thêm :

* Đếm tổng số ghi chú: totalNote
* Đếm tổng số thảo luận: totalDiscussion

> use case tương ứng cần thêm field này:

```json
UC910
```