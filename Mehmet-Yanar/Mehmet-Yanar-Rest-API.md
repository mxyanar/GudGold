# Mehmet Yanar'ın REST API Metotları

**API Test Videosu:** [Link buraya eklenecek](https://example.com)

## 1. Kayıt Olma
- **Endpoint:** `POST /auth/register`
- **Request Body:** 
  ```json
  {
    "email": "gudgold@example.com",
    "password": "Gudgold123!",
    "firstName": "Mehmet",
    "lastName": "Yanar"
  }
  ```
- **Response:** `201 Created` - Kullanıcı başarıyla oluşturuldu

## 2. Giriş Yap
- **Endpoint:** `POST /auth/login`
- **Request Body:**
```json
{
  "email": "ferhatdemir@example.com",
  "password": "Guvenli123!"
}
```
- **Response:** `200 OK` - Kullanıcı başarıyla giriş yaptı ve erişim tokenı oluşturuldu

## 3. Kullanıcı Bilgilerini Görüntüleme
- **Endpoint:** `GET /users/{userId}`
- **Path Parameters:** 
  - `userId` (string, required) - Kullanıcı ID'si
- **Authentication:** Bearer Token gerekli
- **Response:** `200 OK` - Kullanıcı bilgileri başarıyla getirildi

## 4. Kullanıcı Bilgilerini Güncelleme
- **Endpoint:** `PUT /users/{userId}`
- **Path Parameters:** 
  - `userId` (string, required) - Kullanıcı ID'si
- **Request Body:** 
  ```json
  {
    "firstName": "Mehmet",
    "lastName": "Yanar",
    "email": "yenigudgold@example.com",
    "phone": "+905555555555"
  }
  ```
- **Authentication:** Bearer Token gerekli
- **Response:** `200 OK` - Kullanıcı başarıyla güncellendi

## 5. Kullanıcı Hesabı Silme
- **Endpoint:** `DELETE /users/{userId}`
- **Path Parameters:** 
  - `userId` (string, required) - Kullanıcı ID'si
- **Authentication:** Bearer Token gerekli (Yönetici yetkisi veya kendi hesabını silme yetkisi)
- **Response:** `204 No Content` - Kullanıcı başarıyla silindi
