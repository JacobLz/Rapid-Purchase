# Rapid-Purchase
Rapid Purchase , kendimi geliştirmek adına üzerinde çalıştığım bir full stack projesi olarak planlandı ve temel amacı online olarak basit el yapımı veya 3d baskı ürünleri satan bir platform olmak . 

bu projedeki ana hedefim satın alma işlemini site içerisinde yapmadan satın alınan ürünlerin siteden satın alınabilmesi .

stack olarak MERN kullanmayı planlıyorum.

proje ön taslağı : 

# 📘 **Proje Gereksinimleri ve Yol Haritası**

## ✅ **1. Temel Fonksiyonel Gereksinimler**

| Özellik                                | Durum           | Açıklama                                               |
| -------------------------------------- | --------------- | ------------------------------------------------------ |
| Ürünleri listeleme                     | **Olacak**      | Tüm ziyaretçilere açık ürün listesi                    |
| Ürün detay sayfası                     | **Olacak**      | Başlık, açıklama, görsel, puan ortalaması, yorumlar    |
| “Satın al” yönlendirmesi               | **Olacak**      | Shopier linkine `window.location.href` ile yönlendirme |
| Kullanıcı kaydı (email & şifre)        | **Olacak**   | Şifreler bcrypt ile hashlenecek                        |
| Kullanıcı girişi                       | **Olacak**   | JWT ile oturum doğrulama                               |
| Giriş yapan kullanıcının yorum yazması | **Olacak**   | POST `/api/products/:id/comment`                       |
| Giriş yapan kullanıcının puan vermesi  | **Olacak**   | POST `/api/products/:id/rate`                          |
| Kullanıcı yorum ve puan geçmişi        | **Planlanıyor** | Profil sayfası üzerinden gösterilecek                  |

---

## 🛠️ **2. Admin Paneli Fonksiyonları**

| Özellik               | Durum           | Açıklama                                             |
| --------------------- | --------------- | ---------------------------------------------------- |
| Admin girişi          | **Olacak**      | Normal girişten ayrı değil, `isAdmin` ile belirlenir |
| Admin 2FA doğrulaması | **Yapılacak**   | 6 haneli kod → geçici token sonrası doğrulama        |
| Ürün ekleme           | **Olacak**   | Başlık, açıklama, resim, shopier linki               |
| Ürün düzenleme        | **Olacak**   | PUT `/api/products/:id`                              |
| Ürün silme            | **Olacak**   | DELETE `/api/products/:id`                           |
| Admin panel tasarımı  | **Yapılacak**   | Tailwind ile izole admin sayfası                     |
| Admin yorum kontrolü  | **Planlanıyor** | Yorumları silme / yanıt verme opsiyonu               |

---

## 🔐 **3. Güvenlik Gereksinimleri**

| Özellik                             | Durum           | Açıklama                                                             |
| ----------------------------------- | --------------- | -------------------------------------------------------------------- |
| Şifre hashleme                      | **Olacak**      | `bcryptjs` kullanılacak                                              |
| JWT ile kimlik doğrulama            | **Olacak**      | Token 1 saat geçerli olacak                                          |
| Token ile route koruma (middleware) | **Olacak**   | Kullanıcı ve admin için ayrı erişim                                  |
| Rate limiting                       | **Olacak**   | Brute-force saldırılara karşı `express-rate-limit`                   |
| Girdi temizliği                     | **Olacak**   | XSS, script tag vs. engelleme (`express-validator`, `sanitize-html`) |
| Admin 2FA sistemi                   | **Yapılacak**   | Kod üret, doğrula, token oluştur                                     |
| HTTPS / SSL desteği                 | **Olacak**      | Cloudflare veya Let's Encrypt üzerinden                              |
| HTTP-only cookie (opsiyonel)        | **Planlanıyor** | Güvenli oturum için alternatif token saklama yöntemi                 |

---

## 🌐 **4. Domain, Hosting ve WAF Koruması**

| Özellik                        | Durum         | Açıklama                              |
| ------------------------------ | ------------- | ------------------------------------- |
| Cloudflare entegrasyonu        | **Olacak**    | CDN + DNS + WAF koruması sağlanacak   |
| WAF (Web Application Firewall) | **Olacak**    | XSS, bot, DDoS önleme                 |
| Domain registrar lock          | **Olacak**    | Domain transferine karşı koruma       |
| Domain yönetimi 2FA            | **Olacak**    | Domain sağlayıcı paneli için güvenlik |
| HTTPS zorlama (redirect)       | **Yapılacak** | Tüm istekleri HTTPS'e yönlendirme     |

---

## 🧱 **5. Teknik Yapı ve Altyapı**

| Katman                   | Teknoloji                        | Durum         |
| ------------------------ | -------------------------------- | ------------- |
| Frontend                 | HTML, Tailwind CSS, JavaScript   | **Olacak**    |
| Backend                  | Node.js, Express.js              | **Olacak**    |
| Veritabanı               | MongoDB + Mongoose               | **Olacak**    |
| Dosya yükleme            | Upload klasörü veya Cloudinary   | **Olacak** |
| API haberleşmesi         | `fetch` API veya `axios`         | **Olacak**    |
| Admin panel izole yapısı | `/admin/` klasörü veya sub-route | **Olacak** |

---

## 📦 **6. Veritabanı Yapısı**

| Koleksiyon | Alanlar                                                              | Durum      |
| ---------- | -------------------------------------------------------------------- | ---------- |
| `users`    | `_id`, `username`, `email`, `passwordHash`, `isAdmin`, `createdAt`   | **Olacak** |
| `products` | `_id`, `title`, `description`, `imageUrl`, `shopierUrl`, `createdAt` | **Olacak** |
| `comments` | `_id`, `productId`, `userId`, `text`, `createdAt`                    | **Olacak** |
| `ratings`  | `_id`, `productId`, `userId`, `value (1–5)`, `createdAt`             | **Olacak** |

---

## 📌 **7. Opsiyonel ve Planlanan Gelişmiş Özellikler**

| Özellik                                         | Durum           |
| ----------------------------------------------- | --------------- |
| Kullanıcı profil sayfası                        | **Planlanıyor** |
| Ürün yıldız puanı görseli                       | **Planlanıyor** |
| Arama ve kategori filtreleme                    | **Planlanıyor** |
| Yorumlara yanıt / beğeni                        | **Planlanıyor** |
| Admin yorum yönetimi arayüzü                    | **Planlanıyor** |
| E-posta ile 2FA kod gönderimi                   | **Planlanıyor** |
| Ürün istatistikleri (görüntüleme, yorum sayısı) | **Planlanıyor** |

---

## 🗂️ Notlar

* Projede zaman kısıtı olmadığından özellikler önceliklendirilerek sıralı biçimde geliştirilecek.
* Her modül tamamlandıkça test senaryoları hazırlanacak.
* Minimum viable product (MVP) için: **kayıt, giriş, ürün listeleme, detay, satın al linki, yorum ve puanlama + admin paneli ile ürün ekleme yeterlidir.**
