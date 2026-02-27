   ## Kullanıcı İşlemleri

1. **Kullanıcı Kayıt Olma**
- **API Metodu:** `POST /customers/register`  
- **Açıklama:** Yeni kullanıcıların sisteme kayıt olmasını sağlar. Kullanıcı adı, email, adres ve şifre bilgileri alınarak hesap oluşturulur.

2. **Kullanıcı Giriş**
- **API Metodu:** `POST /customers/login`  
- **Açıklama:** Kullanıcının email ve şifre ile sisteme giriş yapmasını sağlar. Başarılı girişte kimlik doğrulama için token döndürülür.

3. **Kullanıcı Bilgileri Görüntüleme**
- **API Metodu:** `GET /customers/{customerId}`  
- **Açıklama:** Kullanıcının profil bilgilerini getirir. Kullanıcı sadece kendi profilini görüntüleyebilir.

4. **Kullanıcı Bilgileri Güncelleme**
- **API Metodu:** `PUT /customers/{customerId}`  
- **Açıklama:** Kullanıcının profil bilgilerini güncellemesini sağlar.
     
5. **Kullanıcı Kaydı Silme**
- **API Metodu:** `DELETE /customers/{customerId}`  
- **Açıklama:** Kullanıcı hesabını kalıcı olarak siler.  

   ## Genel Sistem İşlemleri
   
7. **Ürün Detay Görüntüleme**
- **API Metodu:** `GET /products/{productId}`
- **Açıklama:**  Seçilen bir ürünün detaylı bilgilerini görüntüler.

8. **Ürün Arama**
- **API Metodu:** `GET /contents/search?q=...`
- **Açıklama:** Kullanıcının başlık/anahtar kelimeye göre içerik aramasını sağlar.
   
9. **Ürün Filtreleme**
- **API Metodu:** `GET /products?filter=…`
- **Açıklama:** Ürünlerin kategori, fiyat aralığı veya isim gibi kriterlere göre filtrelenmesini sağlar. Kullanıcılar aradıkları ürünü daha hızlı bulabilir.

10. **Sepete Ürün Ekleme**
- **API Metodu:** `POST /cart`
- **Açıklama:** Kullanıcının seçtiği ürünü sepete eklemesini sağlar. Ürün ID ve adet bilgisi gönderilir. Kullanıcı girişi yapılmadan da kullanılabilir.

11. **Sepet Listeleme**
- **API Metodu:** `GET /cart`
- **Açıklama:**  Kullanıcının sepetine eklediği ürünleri listeler. Kullanıcı girişi yapılmadan da kullanılabilir.

12. **Sepetten Ürün Silme**
- **API Metodu:** `DELETE /cart/{itemId}`
- **Açıklama:** Sepetteki belirli bir ürünü sepetten kaldırır. Kullanıcı girişi yapılmadan da kullanılabilir.

   ## Yönetici İşlemleri

13. **Ürün Güncelleme**
- **API Metodu:** `PUT /admin/products/{productId}`
- **Açıklama:** Sistemde mevcut bir ürünün bilgilerini düzenlemek için kullanılır.

14. **Ürün Ekleme**
- **API Metodu:** `POST /products`
- **Açıklama:** Sisteme yeni ürün eklenmesini sağlar. Ürün adı, fiyat, kategori ve stok bilgileri girilir.

15. **Ürün Silme**
- **API Metodu:** ` DELETE /products/{productId}`
- **Açıklama:** Sistemde bulunan bir ürünün silinmesini sağlar.  
