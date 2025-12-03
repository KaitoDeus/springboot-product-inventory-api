# 📦 Product Inventory API  
![Java](https://img.shields.io/badge/Language-Java-orange)
![Spring Boot](https://img.shields.io/badge/Framework-SpringBoot-green)
![JWT](https://img.shields.io/badge/Security-JWT-blue)
![REST API](https://img.shields.io/badge/API-REST--API-yellow)
![Swagger](https://img.shields.io/badge/Docs-Swagger-brightgreen)
![Postman](https://img.shields.io/badge/Test-Postman-orange)

Dự án mô tả API quản lý sản phẩm sử dụng **Spring Boot**, tích hợp **JWT Authentication**, **Swagger UI**, **Validation**, và kiểm thử bằng **Postman**.

## Thông tin chung

-   **Database:** `summ2025productinventorydb`

##  1. Authentication & Authorization

Hệ thống yêu cầu đăng nhập để lấy JWT token.

### Roles được cấp token:

| Role | Quyền |
| :--- | :--- |
| **admin** | Full access (CRUD + search) |
| **manager** | Full access (CRUD + search) |
| **analyst** | Read + search |
| **others** | Không được cấp token |

### Endpoint Login

    POST /api/auth

### Request Example

``` json
{
  "email": "manager@system.com",
  "password": "123456"
}
```

### Response Example

``` json
{
  "token": "<JWT token>",
  "role": "admin"
}
```


## 2. Product API Endpoints

### GET /api/products

-   Lấy toàn bộ sản phẩm kèm thông tin category
-   **Roles:** Tất cả người dùng đã đăng nhập
-   **Status:** 200, 401, 403

### GET /api/products/{id}

-   Lấy thông tin sản phẩm theo ID
-   **Status:** 200, 404, 401, 403

### POST /api/products

-   Thêm sản phẩm mới
-   **Roles:** admin, manager

#### Validation:
    - productName phải match:
            ^[A-Z][a-zA-Z0-9\s]{2,50}$
    - price > 0
    - quantity ≥ 0

#### Request Body

``` json
{
  "productName": "SmartWatch Z3",
  "price": 149.99,
  "quantity": 30,
  "categoryId": 2
}
```
### PUT /api/products/{id}
-   Cập nhật sản phẩm
-   **Roles:** admin, manager

#### Request Body

``` json
{
  "productName": "SmartWatch Z3",
  "price": 149.99,
  "quantity": 30,
  "categoryId": 2
}
```
### DELETE /api/products/{id}

-   Xóa sản phẩm
-   **Roles:** admin
-   **Status:** 200, 404, 401, 403

### GET /api/products/search?name=...&category=...

-   Tìm kiếm sản phẩm theo tên + category
-   Kết quả được **group theo category**
-   **Roles:** tất cả người dùng có token

## 3. Error Code Format

### JSON Error Response

``` json
{
  "errorCode": "PR40001",
  "message": "Product name is required"
}
```
### Error Codes

| Error Code | HTTP | Meaning |
| :--- | :--- | :--- |
| PR40001 | `400` | Invalid input |
| PR40101 | `401` | Authentication error |
| PR40301 | `403` | Not authorized |
| PR40401 | `404` | Not found |
| PR50001 | `500` | Server error |

## 4. Swagger Integration 

-   Document toàn bộ API
-   Cho phép test API bằng JWT token
-   Hiển thị validation schema

## 5. Postman Test Suite 

###  Danh sách test:

    1.  Login success
    2.  Login failure
    3.  Add product (admin/manager)
    4.  Update product
    5.  Delete product
    6.  Search / Get product by ID
  
------------------------------------------------------------------------
✨ **Good luck & happy coding!**
