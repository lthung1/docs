- [0. Một số chú thích ban đầu](#0-một-số-chú-thích-ban-đầu)
- [1. Lấy ra thông tin giảng viên](#1-lấy-ra-thông-tin-giảng-viên)
- [2. Cập nhật thông tin giảng viên](#2-cập-nhật-thông-tin-giảng-viên)
- [3. Lấy ra danh sách chức vụ của giảng viên](#3-lấy-ra-danh-sách-chức-vụ-của-giảng-viên)
- [4. Lấy ra danh sách trình độ học vấn của giảng viên](#4-lấy-ra-danh-sách-trình-độ-học-vấn-của-giảng-viên)
- [5. Lấy ra danh sách đơn vị công tác của giảng viên](#5-lấy-ra-danh-sách-đơn-vị-công-tác-của-giảng-viên)
- [6. Gửi yêu cầu xoá tài khoản của giảng viên](#6-gửi-yêu-cầu-xoá-tài-khoản-của-giảng-viên)

# 0. Một số chú thích ban đầu

* các use case đổi mật khẩu, quên mật khẩu tương tự như màn sinh viên
* riêng có use case xoá tài khoản khác api gửi yêu cầu xoá tài khoản, còn lại tương tự màn sinh viên
* Xem api tài khoản sinh viên ở file account.md

# 1. Lấy ra thông tin giảng viên

> note: vì một số lí do khách quan nên field trả về hơi khó hiểu, anh/ chị chịu khó giúp em nhé ạ :>

>curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/api/account/get-teacher-profile' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjM5NzU1MiwiaWF0IjoxNzIyMzExMTUyfQ.2K4z1YgYTBJKQzwK_AUcp8wEHfts_HSu6jpIEskao-U'
```

> response

```json
{
  "statusCode": 200,
  "message": "Success",
  "data": {
    "id": 4,
    "username": "edx123", // tên đăng nhập
    "email": "edx@example.com", // email
    "enterpriseUuid": "84b44910479d4f5486c8a44f4b37cc10", // mã trường
    "permission": 2001, // bỏ qua
    "anhDaiDien": "https://s3.moooc.xyz/dev-stable/user-profile-images/3fc428e0-5edc-4c46-9f53-defa2e8c9e531000000019.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240730T071506Z&X-Amz-SignedHeaders=host&X-Amz-Expires=25200&X-Amz-Credential=ihWotP7nBIXENZiD%2F20240730%2Fap-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7ee67ab9811f9d3bd7e731eea8fe33fcef32388777c044088feda324474c3122", // avatar
    "hoVaTen": "test change account info", // họ và tên
    "ngaySinh": "2014-06-01T00:00:00Z", // ngày sinh
    "gioiTinh": "male", // giới tính
    "tenTruong": "TRƯỜNG ĐẠI HỌC HÀ NỘI", // trường
    "chucVus": [ // chức vụ
      {
        "id": 1,
        "code": "CV001",
        "name": "Bộ trưởng"
      },
      {
        "id": 3,
        "code": "CV003",
        "name": "Lãnh đạo cục"
      }
    ],
    "chuyenNganh": [], // chuyên ngành
    "trinhDo": [ // trình độ học vấn
      {
        "id": 1,
        "levelName": "Cử nhân"
      },
      {
        "id": 2,
        "levelName": "Thạc sĩ"
      },
      {
        "id": 3,
        "levelName": "Tiến sĩ"
      }
    ],
    "dienThoai": "09876543222", // điện thoại
    "quocGia": { // bỏ qua
      "code": 4,
      "name": "Việt Nam",
      "name_en": "Viet Nam",
      "full_name": "Viet Nam",
      "full_name_en": "Viet Nam",
      "code_name": "VN"
    },
    "tinhThanh": { // bỏ qua
      "code": "02",
      "name": "Hà Giang",
      "nameEn": "Ha Giang",
      "fullName": "Tỉnh Hà Giang",
      "fullNameEn": "Ha Giang Province",
      "codeName": "ha_giang",
      "regionId": 1,
      "countryId": "4"
    },
    "quanHuyen": { // bỏ qua
      "code": "024",
      "name": "Hà Giang",
      "nameEn": "Ha Giang",
      "fullName": "Thành phố Hà Giang",
      "fullNameEn": "Ha Giang City",
      "codeName": "ha_giang",
      "provinceCode": "02"
    },
    "phuongXa": { // bỏ qua
      "code": "00688",
      "name": "Quang Trung",
      "nameEn": "Quang Trung",
      "fullName": "Phường Quang Trung",
      "fullNameEn": "Quang Trung Ward",
      "codeName": "quang_trung",
      "districtCode": "024"
    },
    "diaChi": "Số 31, Ngõ INNO 5", // địa chỉ chi tiết
    "tieuSu": "Tôi không còn là chính tôi", //  tiểu sử
    "ngonNgu": "Vietnamese", // ngôn ngữ
    "muiGio": "(UTC -11:00) Pacific/Pago_Pago", // múi giờ
    "vaiTros": [ // vai trò
      {
        "id": 11,
        "name": "Lãnh đạo",
        "description": "lãnh đạo vippro",
        "status": true,
        "createdBy": null
      },
      {
        "id": 124,
        "name": "QTKH",
        "description": "Quản trị khóa học",
        "status": true,
        "createdBy": null
      },
      {
        "id": 125,
        "name": "Giảng viên",
        "description": "Nhóm quyền cho giảng viên",
        "status": true,
        "createdBy": null
      }
    ],
    "trangThai": true, // bỏ qua
    "donViCongTac": "Bộ giáo dục và đào tạo", // đơn vị công tác
    "chiTietDonViCongtac": { // chi tiết đơn vị công tác
      "id": 3,
      "code": "DV003",
      "name": "Bộ giáo dục và đào tạo"
    }
  }
}
```

# 2. Cập nhật thông tin giảng viên

> curl

```json
curl -X 'PUT' \
  'https://be.moooc.xyz/v2/api/account/update-profile' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjM5NzU1MiwiaWF0IjoxNzIyMzExMTUyfQ.2K4z1YgYTBJKQzwK_AUcp8wEHfts_HSu6jpIEskao-U' \
  -H 'Content-Type: multipart/form-data' \
  -F 'gender=male' \
  -F 'roleIds=1,2' \
  -F 'countryCode=4' \
  -F 'wardCode=00001' \
  -F 'name=Tôi tên là tôi' \
  -F 'profileStory=Tôi là quản trị' \
  -F 'organizationId=1' \
  -F 'positionIds=1,2' \
  -F 'address=Số 27, Phố INNO' \
  -F 'phoneNumber=0924443333' \
  -F 'avatar=@Screenshot (1).png;type=image/png' \
  -F 'dateOfBirth=2014-06-01T00:00:00Z' \
  -F 'industryIds=1,2' \
  -F 'districtCode=001' \
  -F 'academicLevelIds=1,2' \
  -F 'enterpriseUuid=84b44910479d4f5486c8a44f4b37cc10' \
  -F 'email=' \
  -F 'provinceCode=01'
```

>input

| Parameter   | Mandatory | datatype | Description | Note |
|-------------| --------- |----------|-------------|------|
| gender  | n        | string     | giới tính  |(male, female)|
| countryCode  | n       | string     | mã qg  | |
| provinceCode  | n       | string     | mã tt  | |
| districtCode  | n       | string     | mã qh  | |
| wardCode  | n       | string     | mã px  | |
| address  | n       | string     | địa chỉ  | |
| phoneNumber  | n       | string     | sđt  | |
| academicLevelIds  | n       | int[]     | mã trình độ học vấn  | |
| industryIds  | n       | int[]     | mã trình chuyên ngành  | |
| dateOfBirth  | n       | date     | ngày sinh  | |
| profileStory  | n       | string     | tiểu sử  | |
| avatar  | n       | file     | avatar  | |
| name  | n       | string     | tên  | |
| enterpriseUuid  | n       | string     | mã trường  | |
| roleIds  | n       | int[]     | mã vai trò  | |
| organizationId  | n       | int     | mã tổ chức  | |
| positionIds  | n       | int[]     | mã chức vụ  | |

# 3. Lấy ra danh sách chức vụ của giảng viên
>curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/open-api/profile/get-positions' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiZWR4IiwiZW1haWwiOiJlZHhAZXhhbXBsZS5jb20iLCJpZCI6NCwiaXNTdXBlclVzZXIiOnRydWUsInBvc2l0aW9uIjoiaXNfcXRjcyIsInJvbGVzIjpbIkzDo25oIMSR4bqhbyIsImNhc2NhY2Fjc2MxMjMyMSJdLCJpYXQiOjE3MjA2NjYyMzMsImV4cCI6MTcyMDc1MjYzM30.mKYfUdpVwYe2hTg5WaegoBZpGtXdTFJFBRxWAdoTkM0'
```

> response

```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "code": "CV001",
      "name": "Bộ trưởng"
    },
    {
      "id": 2,
      "code": "CV002",
      "name": "Lãnh đạo vụ"
    },
    {
      "id": 3,
      "code": "CV003",
      "name": "Lãnh đạo cục"
    },
    {
      "id": 4,
      "code": "CV004",
      "name": "Chuyên viên"
    },
    {
      "id": 5,
      "code": "CV005",
      "name": "Giám đốc"
    },
    {
      "id": 6,
      "code": "CV006",
      "name": "Phó Giám đốc"
    },
    {
      "id": 7,
      "code": "CV007",
      "name": "Hiệu trưởng"
    },
    {
      "id": 8,
      "code": "CV008",
      "name": "Chuyên viên"
    },
    {
      "id": 9,
      "code": "CV009",
      "name": "Giảng viên"
    },
    {
      "id": 10,
      "code": "CV0010",
      "name": "Trưởng khoa"
    },
    {
      "id": 11,
      "code": "CV0011",
      "name": "Phó khoa"
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 4. Lấy ra danh sách trình độ học vấn của giảng viên

> curl

```json
curl -X 'GET' \
  'https://be.moooc.xyz/v2/open-api/profile/get-academic-level' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjM5NzU1MiwiaWF0IjoxNzIyMzExMTUyfQ.2K4z1YgYTBJKQzwK_AUcp8wEHfts_HSu6jpIEskao-U'
```

> response

```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "teacherUserId": null,
      "academicLevel": 1,
      "levelCodeName": "CN",
      "levelName": "Cử nhân"
    },
    {
      "id": 2,
      "teacherUserId": null,
      "academicLevel": 2,
      "levelCodeName": "Ths",
      "levelName": "Thạc sĩ"
    },
    {
      "id": 3,
      "teacherUserId": null,
      "academicLevel": 3,
      "levelCodeName": "TS",
      "levelName": "Tiến sĩ"
    },
    {
      "id": 4,
      "teacherUserId": null,
      "academicLevel": 4,
      "levelCodeName": "PGS",
      "levelName": "Phó giáo sư"
    },
    {
      "id": 5,
      "teacherUserId": null,
      "academicLevel": 5,
      "levelCodeName": "GS",
      "levelName": "Giáo sư"
    }
  ],
  "message": "Thực hiện thành công"
}
```

# 5. Lấy ra danh sách đơn vị công tác của giảng viên

> note: post method

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/open-api/profile/get-all-teacher-organization' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjM5NzU1MiwiaWF0IjoxNzIyMzExMTUyfQ.2K4z1YgYTBJKQzwK_AUcp8wEHfts_HSu6jpIEskao-U' \
  -H 'Content-Type: application/json' \
  -d '{
}'
```
> response

```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "code": "DV001",
        "name": "NKG"
      },
      {
        "id": 2,
        "code": "DV002",
        "name": "Techainer"
      },
      {
        "id": 3,
        "code": "DV003",
        "name": "Bộ giáo dục và đào tạo"
      }
    ],
    "pageable": {
      "pageNumber": 0,
      "pageSize": 10,
      "sort": [],
      "offset": 0,
      "unpaged": false,
      "paged": true
    },
    "totalElements": 3,
    "totalPages": 1,
    "last": true,
    "size": 10,
    "number": 0,
    "sort": [],
    "numberOfElements": 3,
    "first": true,
    "empty": false
  },
  "message": "Thực hiện thành công"
}
```

# 6. Gửi yêu cầu xoá tài khoản của giảng viên

> curl

```json
curl -X 'POST' \
  'https://be.moooc.xyz/v2/api/account/delete-account/request-del-account-of-teacher' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJyb2xlcyI6WyJMw6NuaCDEkeG6oW8iLCJRVEtIIiwiR2nhuqNuZyB2acOqbiJdLCJuYW1lIjoiZWR4MTIzIiwiaXNTdXBlclVzZXIiOnRydWUsImlkIjo0LCJwb3NpdGlvbiI6ImlzX3F0Y3MiLCJlbWFpbCI6ImVkeEBleGFtcGxlLmNvbSIsImV4cCI6MTcyMjM5NzU1MiwiaWF0IjoxNzIyMzExMTUyfQ.2K4z1YgYTBJKQzwK_AUcp8wEHfts_HSu6jpIEskao-U' \
  -H 'Content-Type: application/json' \
  -d '{
  
}'
```