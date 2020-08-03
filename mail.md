<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>

# Mail

* ### Giriş 
  * ##### Konfigürasyon
  * ##### Sürücü Önkoşulları
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

### Giriş 
Laravel, popüler ![SwiftMailer](https://swiftmailer.symfony.com/docs/introduction.html) kütüphanesi üzerinden SMTP, Mailgun, Postmark, Amazon SES ve sendmail sürücülerine sahip temiz ve basit bir API sağlayarak, seçtiğiniz yerel veya bulut tabanlı bir hizmet aracılığıyla hızlı bir şekilde posta göndermeye başlamanıza olanak tanır.

##### Konfigürasyon 
Laravelin e-posta yapılandırma dosyası config/mail.php dosyasında bulunur.
    config/mail.php
    > defult