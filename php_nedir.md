### PHP NEDİR ?

PHP (PHP: Hypertext Preprocessor), web geliştirme için özel olarak tasarlanmış açık kaynak kodlu bir programlama dilidir.

1995 yılında Rasmus Lerdorf tarafından geliştirilmeye başlanan PHP, günümüzde internet sitelerinin büyük bir kısmında kullanılmaktadır.



#### **PHP'nin Temel Özellikleri**

PHP sunucu tarafında (server-side) çalışan bir betik dilidir. Bu demektir ki PHP kodu web sunucusunda işlenir ve sonuç HTML formatında kullanıcının tarayıcısına gönderilir.

Kullanıcı PHP kodunu göremez, yalnızca sonuçlarını görür.





#### Neden PHP Popüler?

PHP'nin yaygın kullanılmasının birkaç önemli sebebi vardır. İlk olarak öğrenmesi kolaydır ve yeni başlayanlar için erişilebilir bir dildir. 

Ücretsiz ve açık kaynak kodlu olması, küçük projelerden büyük ölçekli uygulamalara kadar her türlü geliştirme için maliyet avantajı sağlar. 

Ayrıca neredeyse tüm web sunucularında çalışabilir ve çok geniş bir topluluk desteğine sahiptir.



#### Teknik Yetenekleri

PHP, veritabanı işlemleri konusunda oldukça güçlüdür. MySQL, PostgreSQL, Oracle gibi birçok veritabanı sistemiyle kolayca entegre olabilir. 

Dosya işlemleri, form verilerini işleme, oturum yönetimi, e-posta gönderimi gibi web geliştirmede sık ihtiyaç duyulan işlevleri yerine getirebilir.

Dil, nesne yönelimli programlamayı (OOP) destekler ve modern PHP sürümleri ile birlikte tip bildirimi, namespace desteği, trait'ler gibi gelişmiş özellikler eklenmiştir. 

Composer gibi paket yöneticileri sayesinde binlerce hazır kütüphane ve çerçeve kullanılabilir.



#### Günümüzdeki Durumu

PHP, sürekli gelişen ve güncellenen bir dildir. PHP 8.x sürümleri ile birlikte performans iyileştirmeleri, yeni özellikler ve daha modern bir syntax kazanmıştır. 

Facebook, Wikipedia, WordPress.com gibi büyük platformlar PHP kullanmaktadır.

Sonuç olarak PHP, web geliştirme dünyasında önemli bir yere sahip, öğrenmesi kolay ama aynı zamanda güçlü projeler geliştirebileceğiniz pratik bir programlama dilidir.





### WEB GELİŞTİRMEDE NASIL BİR ROL OYNAR ?

PHP, web geliştirmede merkezi bir rol oynar ve modern internet altyapısının temel taşlarından biridir. İşte PHP'nin web geliştirmedeki rolü detaylarıyla:

#### Sunucu Tarafı İşlemler

PHP'nin en temel rolü sunucu tarafında dinamik içerik üretmektir. Kullanıcı bir web sayfası talep ettiğinde, PHP sunucuda çalışır ve veritabanından veri çeker, hesaplamalar yapar, 

koşullu mantık uygular ve sonucu HTML formatında tarayıcıya gönderir. Bu sayede her kullanıcıya özelleştirilmiş içerik sunulabilir.



#### Veritabanı ve PHP İlişkisi

Web uygulamalarının kalbi veritabanı işlemleridir ve PHP bu konuda oldukça güçlüdür. Kullanıcı kayıt sistemi, ürün katalogları, blog yazıları, 

yorumlar gibi dinamik içeriklerin tümü PHP aracılığıyla veritabanından çekilir ve işlenir. MySQL ile olan güçlü entegrasyonu sayesinde e-ticaret sitelerinden sosyal medya platformlarına kadar geniş bir yelpazede kullanılır.



#### Form İşleme ve Kullanıcı Etkileşimi

Web sitelerinde kullanıcıların gönderdiği formlar (iletişim formları, kayıt formları, arama kutuları) PHP tarafından işlenir. PHP, form verilerini alır, doğrular, 

güvenlik kontrollerinden geçirir ve gerekli işlemleri gerçekleştirir. Bu, web sitelerinin interaktif olmasını sağlayan temel mekanizmadır.



#### İçerik Yönetim Sistemlerinin Temeli

WordPress, Drupal, Joomla gibi popüler CMS'ler PHP ile geliştirilmiştir. Bu sistemler milyonlarca web sitesinin altyapısını oluşturur. 

Bloglardan kurumsal web sitelerine, e-ticaret sitelerinden haber portallarına kadar geniş bir kullanım alanına sahiptir.



#### E-ticaret ve İş Uygulamaları

Online alışveriş sitelerinin karmaşık işlevleri PHP ile yönetilir. Ürün katalogları, sepet işlemleri, ödeme entegrasyonları, stok takibi, sipariş yönetimi gibi kritik süreçler PHP'nin güçlü veritabanı desteği sayesinde sorunsuz çalışır.



#### Oturum Yönetimi ve Güvenlik

PHP, kullanıcı oturumlarını yönetir, kimlik doğrulama işlemlerini gerçekleştirir ve güvenlik protokollerini uygular. Kullanıcı giriş sistemi, yetkilendirme, CSRF koruması gibi web güvenliğinin temel unsurları PHP ile sağlanır.



#### Performans ve Ölçeklenebilirlik

Modern PHP sürümleri, yüksek trafikli web sitelerinin ihtiyaçlarını karşılayabilecek performans sunar. Önbellekleme mekanizmaları, optimize edilmiş kod yapısı ve çeşitli performans araçları sayesinde büyük ölçekli uygulamalarda da başarıyla kullanılır.



Özetle PHP, web geliştirmede dinamik, interaktif ve kullanıcı odaklı deneyimler yaratmak için vazgeçilmez bir araçtır. İnternetin bugünkü halini almasında önemli bir rol oynamış ve gelecekte de web teknolojilerinin merkezinde olmaya devam edecek gibi görünmektedir.



### WEB SUNUCULARINDA NASIL ÇALIŞIR VE HTML İLE İLİŞKİSİ NEDİR ?



#### Web Sunucularında PHP'nin Çalışma Prensibi

PHP, web sunucusunda şu adımları izleyerek çalışır:



###### Kullanıcı Talebi: Bir kullanıcı tarayıcısında "example.com/sayfa.php" adresine girer

###### Sunucu Algılama: Web sunucusu (Apache, Nginx vb.) dosyanın .php uzantısını görür

###### PHP Motoruna Yönlendirme: Sunucu dosyayı PHP yorumlayıcısına (PHP engine) gönderir

###### Kod İşleme: PHP motoru kodu satır satır okur ve çalıştırır

###### HTML Üretimi: PHP kodu çalışarak HTML çıktısı üretir

###### Kullanıcıya Gönderim: Üretilen HTML tarayıcıya gönderilir



#### HTML ile İlişkisi

PHP ve HTML arasındaki ilişki çok basittir.PHP kodu içinde HTML yazabilirsiniz,HTML içinde PHP kodu yazabilirsiniz.Kullanıcı asla PHP kodunu göremez. Tarayıcıya yalnızca PHP'nin ürettiği HTML sonucu ulaşır. PHP sunucuda işlenir ve "pişmiş" HTML olarak kullanıcıya servis edilir. Bu sayede hem güvenlik sağlanır hem de dinamik içerik üretilebilir.

Kısaca: PHP, HTML'yi "akıllı" hale getirir ve web sayfalarının değişken, kişiselleştirilmiş içerik göstermesini sağlar.





