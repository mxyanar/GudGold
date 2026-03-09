# API Tasarımı - OpenAPI Specification

**OpenAPI Spesifikasyon Dosyası:** [gudgold.yml](gudgold.yml)

Bu doküman, Pick4Me projesi için OpenAPI Specification (OAS) 3.0 standardına göre hazırlanmış REST API tasarımını içermektedir.

## OpenAPI Specification

```yml
openapi: 3.0.3
info:
  title: GudGold E-Ticaret API
  version: 1.0.0
  description: |
    GudGold e-ticaret platformu için geliştirilmiş RESTful API.

    API aşağıdaki modülleri içerir:

    • Kullanıcı kayıt ve giriş işlemleri  
    • Kullanıcı profil yönetimi  
    • Ürün arama ve filtreleme  
    • Sepet yönetimi  
    • Yönetici ürün yönetimi  

  contact:
    name: Mehmet Yanar
    email: yanarxm@gmail.com

servers:
  - url: http://localhost:3000/api
    description: Development Server

tags:
  - name: Authentication
    description: Kullanıcı kayıt ve giriş işlemleri

  - name: Users
    description: Kullanıcı profil işlemleri

  - name: Products
    description: Ürün arama, filtreleme ve detay işlemleri

  - name: Cart
    description: Sepet yönetimi

  - name: Admin
    description: Yönetici ürün işlemleri

security:
  - BearerAuth: []

paths:

  /auth/register:
    post:
      tags: [Authentication]
      summary: Kullanıcı kayıt olma
      operationId: registerUser
      security: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RegisterRequest'
      responses:
        "201":
          description: Kullanıcı oluşturuldu
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserResponse'
        "400":
          description: Geçersiz kayıt verisi (Örn; email zaten kullanımda)
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /auth/login:
    post:
      tags: [Authentication]
      summary: Kullanıcı giriş yapma
      operationId: loginUser
      security: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        "200":
          description: Başarılı giriş
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AuthResponse'
        "401":
          description: E-posta veya şifre hatalı
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /users/me:
    get:
      tags: [Users]
      summary: Kullanıcı bilgilerini görüntüleme
      operationId: getUserProfile
      responses:
        "200":
          description: Kullanıcı bilgileri getirildi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    put:
      tags: [Users]
      summary: Kullanıcı bilgilerini güncelleme
      operationId: updateUserProfile
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserUpdateRequest'
      responses:
        "200":
          description: Kullanıcı güncellendi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserResponse'
        "400":
          description: Geçersiz güncelleme verisi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    delete:
      tags: [Users]
      summary: Kullanıcı hesabını silme
      operationId: deleteUser
      responses:
        "204":
          description: Kullanıcı silindi
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /products:
    get:
      tags: [Products]
      summary: Ürün arama ve filtreleme
      operationId: searchProducts
      parameters:
        - name: search
          in: query
          description: Ürün adı ile arama
          schema:
            type: string
        - name: category
          in: query
          description: Kategori filtresi
          schema:
            type: string
        - name: minPrice
          in: query
          schema:
            type: number
        - name: maxPrice
          in: query
          schema:
            type: number
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 10
      responses:
        "200":
          description: Ürünler listelendi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductListResponse'
        "400":
          description: Geçersiz filtreleme parametreleri
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /products/{productId}:
    get:
      tags: [Products]
      summary: Ürün detay görüntüleme
      operationId: getProductById
      parameters:
        - name: productId
          in: path
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Ürün detayları
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        "404":
          description: Ürün bulunamadı
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /cart:
    get:
      tags: [Cart]
      summary: Sepeti listeleme
      operationId: getCart
      responses:
        "200":
          description: Sepet getirildi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/CartResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    post:
      tags: [Cart]
      summary: Sepete ürün ekleme
      operationId: addItemToCart
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AddCartItemRequest'
      responses:
        "200":
          description: Ürün sepete eklendi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/CartResponse'
        "400":
          description: Geçersiz ürün veya miktar
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /cart/{itemId}:
    delete:
      tags: [Cart]
      summary: Sepetten ürün silme
      operationId: removeCartItem
      parameters:
        - name: itemId
          in: path
          required: true
          schema:
            type: string
      responses:
        "204":
          description: Ürün sepetten silindi
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "404":
          description: Sepette ürün bulunamadı
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /admin/products:
    post:
      tags: [Admin]
      summary: Ürün ekleme (Admin)
      operationId: createProduct
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductCreateRequest'
      responses:
        "201":
          description: Ürün oluşturuldu
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        "400":
          description: Geçersiz ürün verisi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /admin/products/{productId}:
    put:
      tags: [Admin]
      summary: Ürün güncelleme (Admin)
      operationId: updateProduct
      parameters:
        - name: productId
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductUpdateRequest'
      responses:
        "200":
          description: Ürün güncellendi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        "400":
          description: Geçersiz veri
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "404":
          description: Ürün bulunamadı
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    delete:
      tags: [Admin]
      summary: Ürün silme (Admin)
      operationId: deleteProduct
      parameters:
        - name: productId
          in: path
          required: true
          schema:
            type: string
      responses:
        "204":
          description: Ürün silindi
        "401":
          description: Yetkisiz erişim
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        "404":
          description: Ürün bulunamadı
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

components:

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:

    RegisterRequest:
      type: object
      required: [name,email,password]
      properties:
        name:
          type: string
        email:
          type: string
          format: email
        password:
          type: string
          minLength: 6

    LoginRequest:
      type: object
      required: [email,password]
      properties:
        email:
          type: string
        password:
          type: string

    UserUpdateRequest:
      type: object
      properties:
        name:
          type: string
        email:
          type: string

    ProductCreateRequest:
      type: object
      required: [name,price,category]
      properties:
        name:
          type: string
        price:
          type: number
        category:
          type: string
        stock:
          type: integer
        description:
          type: string

    ProductUpdateRequest:
      allOf:
        - $ref: '#/components/schemas/ProductCreateRequest'

    AddCartItemRequest:
      type: object
      required: [productId,quantity]
      properties:
        productId:
          type: string
        quantity:
          type: integer

    User:
      type: object
      properties:
        id:
          type: string
        name:
          type: string
        email:
          type: string
        role:
          type: string
          enum: [user,admin]
        createdAt:
          type: string
          format: date-time

    Product:
      type: object
      properties:
        id:
          type: string
        name:
          type: string
        price:
          type: number
        category:
          type: string
        stock:
          type: integer
        description:
          type: string
        createdAt:
          type: string
          format: date-time

    CartItem:
      type: object
      properties:
        id:
          type: string
        product:
          $ref: '#/components/schemas/Product'
        quantity:
          type: integer

    Cart:
      type: object
      properties:
        id:
          type: string
        items:
          type: array
          items:
            $ref: '#/components/schemas/CartItem'
        totalPrice:
          type: number

    AuthResponse:
      type: object
      properties:
        token:
          type: string

    UserResponse:
      type: object
      properties:
        data:
          $ref: '#/components/schemas/User'

    ProductResponse:
      type: object
      properties:
        data:
          $ref: '#/components/schemas/Product'

    ProductListResponse:
      type: object
      properties:
        data:
          type: array
          items:
            $ref: '#/components/schemas/Product'
        meta:
          type: object
          properties:
            page:
              type: integer
            limit:
              type: integer
            total:
              type: integer

    CartResponse:
      type: object
      properties:
        data:
          $ref: '#/components/schemas/Cart'

    ErrorResponse:
      type: object
      description: API hata durumlarında döndürülen standart hata modeli
      properties:
        error:
          type: string
          example: "VALIDATION_ERROR"
        message:
          type: string
          example: "Geçersiz veri gönderildi"
        statusCode:
          type: integer
          example: 400
