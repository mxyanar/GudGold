# Mehmet Yanar'ın REST API Metotları

**API Test Videosu:** [Link buraya eklenecek](https://example.com)

## 1. Kullanıcı Kayıt Olma
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
- **Response:** `201 Created` - Kullanıcı başarıyla oluşturuldu.

## 2. Kullanıcı Giriş Yapma
- **Endpoint:** `POST /auth/login`
- **Request Body:**
```json
{
  "email": "mehmetyanar@example.com",
  "password": "Guvenli123!"
}
```
- **Response:** `200 OK` - Kullanıcı başarıyla giriş yaptı ve erişim tokenı oluşturuldu.

## 3. Kullanıcı Bilgilerini Görüntüleme
- **Endpoint:** `GET /users/{userId}`
- **Path Parameters:** 
  - `userId` (string, required) - Kullanıcı ID'si
- **Authentication:** Bearer Token gerekli
- **Response:** `200 OK` - Kullanıcı bilgileri başarıyla getirildi.

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
- **Response:** `200 OK` - Kullanıcı güncellendi.

## 5. Kullanıcı Kaydı Silme
- **Endpoint:** `DELETE /users/{userId}`
- **Path Parameters:** 
  - `userId` (string, required) - Kullanıcı ID'si
- **Authentication:** Bearer Token gerekli (Yönetici yetkisi veya kendi hesabını silme yetkisi)
- **Response:** `204 No Content` - Kullanıcı silindi.

## 6. Ürün Detay Görüntüleme
- **Endpoint:** `GET /products/{productId}`
- **Path Parameters:** `productId`
- **Response:** `200 OK` - Ürün Başarıyla Detaylandı.
- 
## 7. Ürün Arama
- **Endpoint:** `DELETE /products`
- **Path Parameters:** `search` - Arama Kelimesi
- **Response:** `200 OK` - Ürün Bulundu.
```json
  {
  "data": [
    {
      "id": "prd123",
      "name": "24 ayar altın",
      "price": 1250.50,
      "category": "Kolye",
      "description": "Takı",
      "createdAt": "2026-03-09T12:00:00Z"
      "stock": 50,
    }
  ],
  "meta": {
    "page": 1,
    "limit": 10,
    "total": 1
  }
}
  ```

## 8. Ürün Filtreleme
- **Endpoint:** `GET /products`
- **Query Parameters:**
  `category` - Kategori filtresi
  `minPrice` - (number, optional)
  `maxPrice` - (number, optional)
- **Response:** `200 OK` - Ürün Bulundu.

## 9. Sepete Ürün Ekleme
- **Endpoint:** `POST /cart`
- **Authentication:** Bearer Token gerekli
- **Request Body:**
```json
{
  "productId": "prd123",
  "quantity": 1
}
```
- **Response:** `200 OK` - Ürün Sepete Eklendi.

## 10. Sepet Listeleme
- **Endpoint:** `GET /cart`
- **Authentication:** Bearer Token gerekli
- **Response:** `200 OK` - Sepet Listelendi.
```json
{
  "data": {
    "id": "crt789",
    "items": [
      {
        "id": "item123",
        "product": {
          "id": "prd123",
          "name": "20 ayar altın bileklik",
          "price": 1250.50,
          "category": "Kolye",
          "stock": 50,
          "description": "Takı",
          "createdAt": "2026-03-09T12:00:00Z"
        },
        "quantity": 2
      }
    ],
    "totalPrice": 2501.00
  }
}
```

## 11. Sepetten Ürün Silme
- **Endpoint:** `DELETE /cart/{itemId}`
- **Path Parameters:** `itemId` (string, required)
- **Authentication:** Bearer Token gerekli.
- **Response:** `204 No Content` - Ürün Sepetten Silindi.

## 12. Admin - Ürün Güncelleme
- **Endpoint:** `PUT /admin/products/{productId}`
- **Path Parameters:** `productId`
- **Authentication:** Bearer Token (admin) gerekli.
- **Request Body:** (same as ürün ekleme)
- **Response:** `200 OK` - Ürün Güncellendi.

## 13. Admin - Ürün Ekleme
- **Endpoint:** `POST /admin/products`
- **Authentication:** Bearer Token (admin) gerekli.
```json
{
  "name": "20 ayar altın bileklik",
  "price": 1250.50,
  "category": "Kolye",
  "stock": 100,
  "description": "Takı"
}
```
- **Response:** `201 Created` - Ürün Eklendi.

## 14. Admin - Ürün Silme
- **Endpoint:** `DELETE /admin/products/{productId}`
- **Path Parameters:** `productId`
- **Authentication:** Bearer Token (admin) gerekli.
- **Response:** `200 No Content` - Ürün Silindi.
