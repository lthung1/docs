- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. API quên mật khẩu](#1-api-quên-mật-khẩu)
- [1.1. Xác thực email, lấy mã OTP](#11-xác-thực-email-lấy-mã-otp)
- [1.2. Gửi lại mã OTP](#12-gửi-lại-mã-otp)
- [1.3. Xác thực tài khoản với mã OTP](#13-xác-thực-tài-khoản-với-mã-otp)
- [1.4. Đổi mật khẩu sau xác thực](#14-đổi-mật-khẩu-sau-xác-thực)
- [2. API quản lý tài khoản cá nhân](#2-api-quản-lý-tài-khoản-cá-nhân)
- [2.1. Lấy ra thông tin tài khoản, hồ sơ cá nhân của sinh viên](#21-lấy-ra-thông-tin-tài-khoản-hồ-sơ-cá-nhân-của-sinh-viên)
- [3. API đổi mật khẩu](#3-api-đổi-mật-khẩu)
- [4. API đăng ký tài khoản](#4-api-đăng-ký-tài-khoản)
- [4.1. Nhập thông tin đăng ký ban đầu](#41-nhập-thông-tin-đăng-ký-ban-đầu)
- [4.2. Gửi lại mã OTP](#42-gửi-lại-mã-otp)
- [4.3. Xác thực OTP, hoàn tất đăng ký](#43-xác-thực-otp-hoàn-tất-đăng-ký)
- [4.4. Thêm sở thích ban đầu](#44-thêm-sở-thích-ban-đầu)
- [4.5. Thêm chuyên ngành quan tâm](#45-thêm-chuyên-ngành-quan-tâm)

# 0. Một số chú thích ban đầu
> những api nào cần sử dụng OTP, cần phải test trên email thực tế

> Các output về OTP không hợp lệ

* Với OTP đã hết hạn

```json
{
  "message": "Mã OTP đã hết hạn",
  "success": false,
  "messageCode": "EXPIRED_OTP"
}
```

* Với OTP bị nhập sai

```json
{
  "message": "Mã OTP chưa chính xác",
  "success": false,
  "messageCode": "INCORRECT_OTP"
}
```

# 1. API quên mật khẩu
> use case: 880

# 1.1. Xác thực email, lấy mã OTP

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/check-email-to-reset-password?email=jhgjagdf%40gmail.com' \
  -H 'accept: */*'
```

> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y         | string     | email  ||

# 1.2. Gửi lại mã OTP

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/resend-otp-to-reset-password?email=fff%40gmail.com' \
  -H 'accept: */*'
```
> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y         | string     | email  ||

# 1.3. Xác thực tài khoản với mã OTP

> curl : 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/verify-otp-to-reset-password?email=email%40gmail.com&otp=124321' \
  -H 'accept: */*'
```
> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y         | string     | email  ||
| otp  | y         | string     | otp  | size = 6|

# 1.4. Đổi mật khẩu sau xác thực

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/reset-password?email=%C3%A1dff%40dags.com&password=nsfgsafqw3' \
  -H 'accept: */*'
```
> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y        | string     | email  ||
| otp  | y       | string     | otp  | size = 6|

# 2. API quản lý tài khoản cá nhân

> use case : 883, 885

> note: đang thiếu bổ sung quốc gia: có thể ghép sau ngày 17/7/2024

# 2.1. Lấy ra thông tin tài khoản, hồ sơ cá nhân của sinh viên

> curl :

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/account/get-student-profile' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6W10sIm5hbWUiOiJoZ3Z4dW4iLCJpc1N1cGVyVXNlciI6ZmFsc2UsImlkIjo4NCwicG9zaXRpb24iOiJpc19xdGh0IiwiZW1haWwiOiJob2FuZ3Z4QGdtYWlsLmNvbSIsImV4cCI6MTcyMTI2MjYzMiwiaWF0IjoxNzIxMTc2MjMyfQ.COG3GgMb6zJgsDPuaV9pu8_6zUJZ2xEgK1s3Z9jwsjE'
```

> output

```json
{
  "statusCode": 200,
  "message": "Success",
  "data": {
    "id": 84,
    "username": "hgvxun",
    "email": "hoangvx@gmail.com",
    "language": "vi", // ngôn ngữ
    "timeZone": null, // múi giờ
    "dateOfBirth": null, // sinh nhật
    "cardId": null, // bỏ qua
    "specialized": null, // bỏ qua
    "academicLevel": [ //trình độ học vấn
      {
        "id": 1,
        "levelName": "Đại học chính quy"
      },
      {
        "id": 2,
        "levelName": "Cao Đẳng"
      }
    ],
    "phoneNumber": "",
    "location": null, // bỏ qua
    "provinceId": "01", // mã tỉnh thành
    "districtId": "001", // mã quận huyện
    "wardId": "00001", // mã phường xã
    "provinceName": "Hà Nội", // tên tỉnh thành
    "districtName": "Ba Đình", // tên quận huyện
    "wardName": "Phúc Xá", // tên phường xã
    "province": { // có thể dùng hoặc bỏ qua
      "code": "01",
      "name": "Hà Nội",
      "nameEn": "Ha Noi",
      "fullName": "Thành phố Hà Nội",
      "fullNameEn": "Ha Noi City",
      "codeName": "ha_noi",
      "regionId": 3,
      "countryId": "4"
    },
    "district": { // có thể dùng hoặc bỏ qua
      "code": "001",
      "name": "Ba Đình",
      "nameEn": "Ba Dinh",
      "fullName": "Quận Ba Đình",
      "fullNameEn": "Ba Dinh District",
      "codeName": "ba_dinh",
      "provinceCode": "01"
    }, 
    "ward": { // có thể dùng hoặc bỏ qua
      "code": "00001",
      "name": "Phúc Xá",
      "nameEn": "Phuc Xa",
      "fullName": "Phường Phúc Xá",
      "fullNameEn": "Phuc Xa Ward",
      "codeName": "phuc_xa",
      "districtCode": "001"
    },
    "gender": "male", // giới tính => quy đổi ra Nam, Nữ
    "industries": [ // chuyên ngành
      {
        "id": 1,
        "name": "Giáo dục học"
      },
      {
        "id": 2,
        "name": "Công nghệ giáo dục"
      },
      {
        "id": 3,
        "name": "Quản lý giáo dục"
      },
      {
        "id": 4,
        "name": "Kinh tế Giáo dục"
      }
    ],
    "country": null, // bỏ qua
    "address": "Số 31, Phố Trạch Mỹ Lộc", // địa chỉ cụ thể
    "profileStory": "Tôi tên là Hoàng", // tiểu sử
    "studentFavorites": [ // sở thích
      {
        "id": 1,
        "name": "Khoa học dữ liệu,Khai thác dữ liệu",
        "createdAt": "2024-06-18T03:37:51Z",
        "updatedAt": "2024-06-18T03:37:51Z"
      },
      {
        "id": 3,
        "name": "Thiết kế web",
        "createdAt": "2024-06-18T03:37:51Z",
        "updatedAt": "2024-06-18T03:37:51Z"
      },
      {
        "id": 5,
        "name": "Sở thích khác,Nấu ăn",
        "createdAt": "2024-06-18T03:37:51Z",
        "updatedAt": "2024-06-18T03:37:51Z"
      },
      {
        "id": 7,
        "name": "Giáo dục mầm non",
        "createdAt": "2024-06-18T03:37:51Z",
        "updatedAt": "2024-06-18T03:37:51Z"
      }
    ],
    "fullName": "Vũ Xuân Hoàng", // tên
    "schoolId": 1, // mã trường
    "school": "ĐẠI HỌC BÁCH KHOA HÀ NỘI", // tên trường
    "image": "https://s3.moooc.xyz/dev-stable/user-profile-images/db53e4da-a55c-4e23-b4fd-727bae9640d5avatar.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240717T003215Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240717%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=234b5396bdca3bd75c929f139162e83f2f2bf455c836966cbf5e50d0e1cfed91" // avatar
  }
}
```


# 3. API đổi mật khẩu

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/auth/change-password' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoidmFudHVuZ2RldmVsb3BlckBnbWFpbC5jb20iLCJlbWFpbCI6InZhbnR1bmdkZXZlbG9wZXJAZ21haWwuY29tIiwiaWQiOjM4LCJpc1N1cGVyVXNlciI6ZmFsc2UsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbInRlc3QyIiwidGVzdDQiLCJ0ZXN0MTIzIiwidGVzdDUzMTIzMTMiXSwiaWF0IjoxNzIwNDEzNzM4LCJleHAiOjE3MjA1MDAxMzh9.kru4rNEiMK4H1e39aMCCJ06kW7Qujk39-1jVbMRKyDQ' \
  -H 'Content-Type: application/json' \
  -d '{
  "oldPassword": "MarkZuckerBucky99@@9",
  "newPassword": "MarkZuckerBucky99@@99"
}'
```

> input 

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| oldPassword  | y        | string     | pass cũ  ||
| newPassword  | y         | string     | pass mới  ||

# 4. API đăng ký tài khoản
> use case: 881

# 4.1. Nhập thông tin đăng ký ban đầu

> curl:

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/account/register-account' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "fullName": "Lê Phương Nam",
  "email": "namne@gmail.com",
  "password": "3j*4ztI@hSh"
}'
```

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| fullName  | y        | string     | tên  ||
| email  | y         | string     | email  ||
| password  | y         | string     | mật khẩu  ||

> note: mã OTP sẽ được gửi đến mail sau khi thông tin được gửi đi hợp lệ

# 4.2. Gửi lại mã OTP

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/resend-otp-to-register?email=n%C3%A2mmsd%40gmail.com' \
  -H 'accept: */*'
```
> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y         | string     | email  ||

# 4.3. Xác thực OTP, hoàn tất đăng ký

> curl 

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/account/complete-register-account?email=%C4%91%E1%BA%A5%40gmal.com&otp=135345346' \
  -H 'accept: */*'
```
> input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| email  | y         | string     | email  ||
| otp  | y         | string     | otp  ||

> Note: sau khi đăng ký thành công, hệ thống sẽ trả ra accessToken và refreshToken

# 4.4. Thêm sở thích ban đầu

> curl: thêm sở thích cho sinh viên

```json
curl -X 'POST' \
  'https://mooc-api.tunnel.techainer.com/student-favorite/create' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiaGd2eHVuIiwiZW1haWwiOiJob2FuZ3Z4QGdtYWlsLmNvbSIsImlkIjo4NCwiaXNTdXBlclVzZXIiOmZhbHNlLCJwb3NpdGlvbiI6ImlzX3N2Iiwicm9sZXMiOltdLCJpYXQiOjE3MjA3NjQ3MjIsImV4cCI6MTcyMDg1MTEyMn0.hYmGfdwSI3pmDmEZy9Oi2dYq2mx_WMjK35a6VPWajR8' \
  -H 'Content-Type: application/json' \
  -d '{
  "tag_ids": [
    1, 2
  ]
}'

```

> curl: lấy ra các sở thích có sẵn trong hệ thống

```json
curl -X 'POST' \
  'https://mooc-api.tunnel.techainer.com/recommendation/get-all' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  
}'
```

# 4.5. Thêm chuyên ngành quan tâm

> curl : thêm chuyên ngành quan tâm cho sinh viên

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/industry-student-interest/create' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "ids": [
    1, 2
  ]
}'
```

> curl : lấy ra danh sách chuyên ngành

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/open-api/course/get-all-industry' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MjA2NjYyMzMsImV4cCI6MTcyMDc1MjYzM30.mKYfUdpVwYe2hTg5WaegoBZpGtXdTFJFBRxWAdoTkM0' \
  -H 'Content-Type: application/json' \
  -d '{
  "page": 1,
  "size": 10,
  "keyword": ""
}'
//đây là open-api, không cần token, bỏ keyword nếu muốn lấy tất cả
```
