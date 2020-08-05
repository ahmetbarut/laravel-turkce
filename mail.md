<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>

# Mail

* ### [Giriş](#giriş-1) 
  * ##### [Konfigürasyon](#konfigürasyon-1)
  * ##### [Sürücü Önkoşulları](#sürücü-önkoşulları-1)
* ### Mail Oluşturma
* ### Mail Yazma
    * ##### Göndereni Yapılandırma
    * ##### Görünümü Yapılandırma
    * ##### Veriyi gör
    * ##### Ekler
    * ##### Satır İçi Ekler
    * ##### SwiftMailer Mesajını Özelleştirme
* ### İşaretli Mail 
    * ##### İşaretli Mail Oluşturma
    * ##### İşaretli Mesajları Yazma
    * ##### Bileşenleri Özelleştirme
* ### Mail Gönderme
    * ##### Kuyruk (queue) Postası
* ### Mail İşleme
    * ##### Tarayıcıda Posta Önizleme
* ### lokalizasyon Mail
* ### Posta ve Yerel Kalkınma
* ### Etkinlikler

### [Giriş](#giriş-1) 
Laravel, popüler ![SwiftMailer](https://swiftmailer.symfony.com/docs/introduction.html) kütüphanesi üzerinden [SMTP](https://tr.wikipedia.org/wiki/SMTP), Mailgun, Postmark, Amazon SES ve sendmail sürücülerine sahip temiz ve basit bir API sağlayarak, seçtiğiniz yerel veya bulut tabanlı bir hizmet aracılığıyla hızlı bir şekilde posta göndermeye başlamanıza olanak tanır.

#### [Konfigürasyon](#konfigürasyon-1) 
Laravelin e-posta yapılandırma dosyası config/mail.php dosyasında bulunur.

###### varsayılan mail ayarları
> config/mail.php
Dosyasında ayarlar varsayılan olarak eklenmiştir. Kullandığınız mail servisine göre düzenleme yapmalısınız. 
```php
'mailers' => [
        // ...
    ]
```
içinden kullandığınız protokole göre düzenlenmesi gerekir varsayılan olarak _smtp_ geliyor.

> Desteklenen protokoller
* smtp 
* sendmail 
* mailgun 
* ses 
* postmark 
* log 
* array

Ana dizinde bulunan _.env_ dosyası içinden kendinize göre ayarlayabilirsiniz

```environment
    MAIL_MAILER=smtp
    MAIL_HOST=smtp.mailtrap.io
    MAIL_PORT=2525
    MAIL_USERNAME=null
    MAIL_PASSWORD=null
    MAIL_ENCRYPTION=null
    MAIL_FROM_ADDRESS=null
    MAIL_FROM_NAME="${APP_NAME}"
```
* MAIL_MAILER
    * Mail protokolünü belirtiyoruz
* MAIL_HOST
    * Kullandığımız mail servisinin hostu. Eğer gmail kullanacaksanız _smtp.gmail.com_ olarak değiştirin 
* MAIL_PORT
    * Mail portu smtp'de 587 veya 493
* MAIL_USERNAME
    * e-posta adresiniz
* MAIL_PASSWORD
    * e-posta adresinizin parolası
* MAIL_ENCRYPTION
    * ssl veya tls 
* MAIL_FROM_ADDRESS
    * e-posta adresiniz gönderildiğinde gösterilecek adres
* MAIL_FROM_NAME
    * e-posta adresiniz gönderildiğinde gösterilecek isim

##### [Sürücü Önkoşulları](#sürücü-önkoşulları-1)
Mailgun ve Postmark gibi API tabanlı sürücüler genellikle SMTP sunucularından daha basit ve daha hızlıdır. Mümkünse, bu sürücülerden birini kullanmalısınız. Tüm API sürücüleri, Composer paket yöneticisi aracılığıyla kurulabilen Guzzle HTTP kütüphanesini gerektirir.
```php 
    composer require guzzlehttp/guzzle
```