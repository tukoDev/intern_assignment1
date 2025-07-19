### HTTP İsteği Nasıl Çalışır?

HTTP (HyperText Transfer Protocol), web üzerindeki iletişimin temel protokolüdür. Bir HTTP isteğinin çalışma süreci oldukça karmaşık ve çok adımlıdır.

###### 1\. URL Analizi ve DNS Çözümleme

Kullanıcı tarayıcıya "https://example.com/sayfa" yazdığında, tarayıcı önce URL'yi analiz eder. Protokol (https), domain (example.com) ve path (/sayfa) bilgilerini ayırır.

Ardından DNS (Domain Name System) süreci başlar. Tarayıcı "example.com" domain adını IP adresine çevirmek için DNS sunucularına sorgu gönderir. Bu süreç genellikle yerel DNS önbelleği, ISP DNS sunucusu ve kök DNS sunucuları arasında hiyerarşik olarak gerçekleşir.



###### 2\. TCP Bağlantısı Kurulumu

IP adresi öğrenildikten sonra, tarayıcı hedef sunucuyla TCP bağlantısı kurar. Bu "three-way handshake" süreci ile gerçekleşir: istemci SYN paketi gönderir, sunucu SYN-ACK ile yanıtlar, istemci ACK ile onaylar. Böylece güvenilir bir bağlantı kurulur.

HTTPS kullanılıyorsa, TCP bağlantısından sonra TLS/SSL handshake süreci de gerçekleşir. Bu süreçte şifreleme anahtarları değiş tokuş edilir ve güvenli kanal oluşturulur.



###### 3\. HTTP İsteğinin Gönderilmesi

Bağlantı kurulduktan sonra tarayıcı HTTP isteğini oluşturur ve gönderir. Bir HTTP isteği şu bölümlerden oluşur:

İstek Satırı (Request Line): HTTP metodu (GET, POST, PUT vb.), URL path'i ve HTTP versiyonu

Başlıklar (Headers): User-Agent, Accept, Cookie gibi meta bilgiler

Gövde (Body): POST isteklerinde form verileri veya JSON



###### 4\. Sunucu Tarafında İşleme

Web sunucusu (Apache, Nginx, IIS vb.) isteği alır ve analiz eder. İstek türüne göre farklı işlemler gerçekleştirilir:

Statik içerik için sunucu dosyayı disk üzerinden okur ve gönderir. Dinamik içerik için (PHP, Python, Node.js vb.) uygulamaya yönlendirme yapar. Bu durumda uygulama sunucusu devreye girer, veritabanı sorguları çalıştırılır, iş mantığı işletilir ve sonuç üretilir.



###### 5\. HTTP Yanıtının Oluşturulması

Sunucu işlem tamamlandıktan sonra HTTP yanıtını oluşturur. Yanıt şu bölümlerden oluşur:

Durum Satırı: HTTP versiyonu, durum kodu (200, 404, 500 vb.) ve durum mesajı

Yanıt Başlıkları: Content-Type, Content-Length, Set-Cookie gibi bilgiler

Yanıt Gövdesi: HTML, JSON, görsel vb. gerçek içerik



###### 6\. Yanıtın İşlenmesi

Tarayıcı yanıtı alır ve durum kodunu kontrol eder. 200 OK ise içeriği işlemeye başlar. HTML içeriği parse edilir, CSS stilleri uygulanır, JavaScript kodları çalıştırılır.

Eğer HTML içinde başka kaynaklara (görsel, CSS, JS dosyaları) referanslar varsa, tarayıcı bunlar için de ayrı HTTP istekleri gönderir. Modern tarayıcılar bu istekleri paralel olarak gerçekleştirebilir.



###### 7\. Bağlantının Sonlandırılması

İşlem tamamlandıktan sonra TCP bağlantısı kapatılır. HTTP/1.1'de "Connection: keep-alive" başlığı varsa bağlantı bir süre açık tutulabilir. HTTP/2'de multiplexing sayesinde tek bağlantı üzerinden birden fazla istek gönderilebilir.

Performans ve Optimizasyon Faktörleri

Bu süreçte performansı etkileyen birçok faktör vardır. DNS çözümleme süresi, coğrafi mesafe, sunucu yanıt süresi, ağ gecikmesi, içerik boyutu gibi unsurlar toplam yükleme süresini belirler.

Modern web uygulamaları CDN (Content Delivery Network) kullanarak içeriği kullanıcıya yakın sunuculardan servis eder, önbellekleme stratejileri uygular ve sıkıştırma teknikleri kullanarak bu süreci optimize eder.

Bu karmaşık süreç saniyenin çok küçük bir bölümünde gerçekleşir ve kullanıcıya kesintisiz web deneyimi sunar.



#### PHP bu sürecin neresindedir?

###### PHP'nin HTTP İstek Sürecindeki Yeri

PHP, HTTP isteği sürecinin 4. adımında (Sunucu Tarafında İşleme) devreye girer ve kritik rol oynar.



###### PHP'nin Tam Olarak Girdiği An

Web sunucusu (Apache/Nginx) bir HTTP isteği aldığında, dosya uzantısına bakar. Eğer istek .php uzantılı bir dosyaya geliyorsa, sunucu bu isteği doğrudan disk üzerinden statik dosya olarak serviss etmez. Bunun yerine PHP yorumlayıcısına (PHP-FPM, mod\_php vb.) yönlendirir.



###### Süreçteki Detaylı Adımlar

**Adım 1 - İstek Analizi:**

GET /urunler.php?kategori=elektronik HTTP/1.1

Host: alisveris.com

Sunucu bu isteği görür ve .php uzantısı nedeniyle PHP'ye yönlendirir.



**Adım 2 - PHP Çalışma Süreci:**

<?php

// PHP burada devreye girer

$kategori = $\_GET\['kategori']; // 'elektronik'

$veritabani = new PDO("mysql:host=localhost;dbname=magaza");

$sorgu = $veritabani->prepare("SELECT \* FROM urunler WHERE kategori = ?");

$sorgu->execute(\[$kategori]);

$urunler = $sorgu->fetchAll();

?>



**Adım 3 - HTML Üretimi:**

<?php foreach($urunler as $urun): ?>

&nbsp;   <div class="urun">

&nbsp;       <h3><?= $urun\['isim'] ?></h3>

&nbsp;       <p><?= $urun\['fiyat'] ?> TL</p>

&nbsp;   </div>

<?php endforeach; ?>



###### PHP'nin Yaptığı İşlemler



1. **URL Parametrelerini Okuma**: $\_GET, $\_POST dizileri ile gelen verileri alır
2. **Veritabanı Bağlantısı**: MySQL, PostgreSQL gibi veritabanlarına bağlanır
3. **İş Mantığı**: Hesaplamalar, validasyonlar, güvenlik kontrolleri yapar
4. **Oturum Yönetimi**: $\_SESSION ile kullanıcı oturumlarını kontrol eder
5. **HTML Çıktısı Üretme**: Dinamik içeriği HTML formatında oluşturur



###### Sunucu Mimarisi İçindeki Konum

1\. \[Tarayıcı] → HTTP İsteği

2\. \[Web Sunucusu] → İstek analizi (.php tespit)

3\. \[PHP Yorumlayıcısı] ← Dosya yönlendirme

4\. \[PHP Kodu] ← Veritabanı sorgusu

5\. \[Veritabanı] → Veri döndürme

6\. \[PHP] → HTML üretimi

7\. \[Web Sunucusu] ← İşlenmiş HTML

8\. \[Tarayıcı] ← HTTP Yanıtı



**Kritik Nokta**

PHP kodu asla tarayıcıya ulaşmaz. PHP sunucuda çalışır, HTML çıktısı üretir ve bu HTML kullanıcıya gönderilir. Kullanıcı "Sayfa Kaynağını Görüntüle" dediğinde PHP kodunu değil, yalnızca PHP'nin ürettiği HTML'yi görür.

Kullanıcının Gördüğü:

&nbsp;   <div class="urun">

&nbsp;   <h3>iPhone 14</h3>

&nbsp;   <p>25000 TL</p>

</div>



Sunucudaki PHP Kodu:

// Bu kod gizli kalır

<h3><?= $urun\['isim'] ?></h3>

<p><?= $urun\['fiyat'] ?> TL</p>

Bu sayede PHP, statik HTML'den farklı olarak her kullanıcıya özel, güncel ve interaktif içerik sunabilir.



**Yani özetle işlemler şu şekilde olur:**



Tarayıcı → HTTP İsteği → Web Sunucusu → PHP → Veritabanı

&nbsp;                                     ↑         ↓

Tarayıcı ← HTTP Yanıtı ← Web Sunucusu ← PHP ← Veritabanı (Veri)



1. **Tarayıcı** → HTTP İsteği gönderir
2. **Web Sunucusu** → İsteği alır, .php dosyası olduğunu görür
3. **PHP** → Devreye girer, kodu çalıştırmaya başlar
4. **Veritabanı** → PHP'nin sorgusu sonucu veriyi PHP'ye geri döner
5. **PHP** → Gelen veriyi işler ve HTML çıktısı üretir
6. **Web Sunucusu** → PHP'den gelen HTML'yi alır
7. **Tarayıcı** → HTTP yanıtı olarak HTML'yi alır
