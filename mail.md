<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>

# Mail

* ### [Giriş](#giriş-1) 
  * ##### [Konfigürasyon](#konfigürasyon-1)
  * ##### [Sürücü Önkoşulları](#sürücü-önkoşulları-1)
* ### [Mail Oluşturma](#mail-oluşturma-1)
* ### [Mail Yazma](#mail-yazma-1)
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
Mailgun ve Postmark gibi API tabanlı sürücüler genellikle SMTP sunucularından daha basit ve daha hızlıdır. Mümkünse, bu sürücülerden birini kullanmalısınız. Tüm API sürücüleri, Composer paket yöneticisi aracılığıyla kurulabilen [Guzzle HTTP](http://docs.guzzlephp.org/en/stable/) kütüphanesini gerektirir.

```php 
    composer require guzzlehttp/guzzle
```
#### Mailgun Sürücüsü
Mailgun sürücüsünü kullanmak için önce [Guzzle](http://docs.guzzlephp.org/en/stable/)'ı yükleyin, ardından ```config/mail.php``` yapılandırma dosyanızdaki varsayılan seçeneği mailgun olarak ayarlayın. Ardından, ```config/services.php``` yapılandırma dosyanızın aşağıdaki seçenekleri içerdiğini doğrulayın:

```php 
'mailgun' => [
    'domain' => env('MAILGUN_DOMAIN'),
    'secret' => env('MAILGUN_SECRET'),
    'endpoint' => env('MAILGUN_ENDPOINT', 'api.mailgun.net'),
    ],
```
Bu şekilde olup _.env_ dosyanızda düzenlemeleri size verildiği gibi doldurun
```environment
    MAIL_MAILER=mailgun
    MAIL_HOST=smtp.mailgun.org
    MAIL_PORT=587
    MAIL_FROM_ADDRESS=ornek_eposta@domain.com
    MAILGUN_DOMAIN=subdomain.domain.com
    MAILGUN_SECRET=mailgun-api-key
```
* MAIL_MAILER=mailgun
    * Mail protokolünü belirtiyoruz.
* MAIL_HOST=smtp.mailgun.org
    * Kullandığımız mail servisinin hostu.
* MAIL_FROM_ADDRESS=ornek_eposta@domain.com
    * mailgun'de başvuru yaptığınız e-posta adresiniz
* MAILGUN_DOMAIN=subdomain.domain.com
    *   mailgun subdomain kullanmanızı tavsiye ediyor [mailgun döküman](https://documentation.mailgun.com/en/latest/)
* MAILGUN_SECRET=mailgun-api-key
    * mailgun tarafından size sunulan api-secret-key (anahtarı)
    Mailgun konfigürasyonu bu kadar.
#### Postmark Sürücüsü 
    Postmark henüz test edilmediği için eklenmedi ilerleyen zamanlarda güncellenecektir.

#### Amazon SES Sürücüsü 
    Amazon SES henüz test edilmediği için eklenmedi ilerleyen zamanlarda güncellenecektir.

### [Mail Oluşturma](#mail-oluşturma-1)
Laravel'de kullandığınız servis tarafından her türlü e-posta gönderilebilir. Laravel posta gönderme sınıfları ```app/Mail``` dizininde bulunur.
Posta gönderme sınıfı oluşturmak için aşşağıdaki komutunu çalıştırıyoruz.
```php
    php artisan make:mail YeniGonderi
```
> Ben örnek için ```YeniGonderi``` diye isimlendirdim.

### [Mail Yazma](#mail-yazma-1)
E-posta gönderme işlemleri, yapılandırma derleme gibi işlemler  ```build()``` fonksiyonu'nda yapılır.
```php
   /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        return $this->view('view.name');
    }
```
Laravelde posta gönderme işlemlerinde html dosyası gönderilir. Kullancıya göndermek istediğiniz herşey oraya yazılır. Örnek göstererek açıklamaya çalışacağım.

```resources/views/``` _mail_ diye bir dizin oluşturup içinde ```yeni_gonderi.blade.php``` dosyası oluşturacağım.

```php artisan make:controller GonderiController``` diye bir controller oluşturacağım.
Sadece örnek göstermek amacıyla controllerde herşeyi statik yapacağım mantığı göstermek amacıyla.

```app/Http/Controllers/GonderiController.php     ``` dosyasına 
```php
 use App\Mail\YeniGonderi; 
 use Illuminate\Support\Facades\Mail;
```
```App\Mail\YeniGonderi``` benim posta göndermem için kullandığım sınıf.
## 
```Illuminate\Support\Facades\Mail``` postayı kime göndereceğimizi ve göndermemiz için kullanılan sınıf.
bunları dahil ediyorum