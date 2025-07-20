#### PHP ile form verileri nasıl alınır ve işlenir?



##### 1\. Form Nedir?

Web sitelerinde gördüğün kayıt formları, iletişim formları gibi kutucuklar. Kullanıcı bilgileri yazar, "Gönder" butonuna basar.



**<!-- Bu basit bir HTML formu -->**

<form action="kaydet.php" method="POST">

&nbsp;   <label>Adınız:</label>

&nbsp;   <input type="text" name="ad">

&nbsp;   

&nbsp;   <label>E-posta:</label>

&nbsp;   <input type="email" name="eposta">

&nbsp;   

&nbsp;   <button type="submit">Gönder</button>

</form>



##### 2\. PHP Nasıl Çalışır?



* Kullanıcı formu doldurur → "Gönder" butonuna basar
* Veriler sunucuya gider (senin bilgisayarından web sitesinin bilgisayarına)
* PHP kodu bu verileri alır ve işler



##### 3\. Verileri Alma - Temel Yöntem

PHP'de formdaki verileri almak için $\_POST kullanıyoruz:



<?php

**// kaydet.php dosyası**



**// Form gönderildi mi kontrol et**

if (isset($\_POST)) {

&nbsp;   **// Formdaki "ad" kutucuğunu al**

&nbsp;   $kullanici\_adi = $\_POST\['ad'];

&nbsp;   

&nbsp;   **// Formdaki "eposta" kutucuğunu al**

&nbsp;   $kullanici\_eposta = $\_POST\['eposta'];

&nbsp;   

&nbsp;   **// Ekrana yazdır**

&nbsp;   echo "Merhaba " . $kullanici\_adi;

&nbsp;   echo "<br>E-postanız: " . $kullanici\_eposta;

}

?>



##### 4\. Basit Örnekler ile Adım Adım Anlatım



######  **1. Adım: HTML formu (form.html)**

&nbsp;<form action="islem.php" method="POST">

&nbsp;    <p>Adınız: <input type="text" name="isim"></p>

&nbsp;    <p>Yaşınız: <input type="number" name="yas"></p>

&nbsp;    <p><button type="submit">Bilgileri Gönder</button></p>

&nbsp;</form>



######  **2. Adım: PHP ile verileri al (islem.php)**

&nbsp;<?php

 **// Kullanıcının yazdığı ismi al**

&nbsp;$isim = $\_POST\['isim'];



 **// Kullanıcının yazdığı yaşı al**

&nbsp;$yas = $\_POST\['yas'];



 **// Sonucu göster**

&nbsp;echo "<h1>Bilgileriniz Alındı!</h1>";

&nbsp;echo "İsminiz: " . $isim . "<br>";

&nbsp;echo "Yaşınız: " . $yas . " yaşında";

&nbsp;?>



##### **5. Tam Örnek - Basit İletişim Formu**

###### **HTML kısmı (iletisim.html):**

<!DOCTYPE html>

<html>

<body>

&nbsp;   <h2>Bize Mesaj Gönderin</h2>

&nbsp;   <form action="mesaj-al.php" method="POST">

&nbsp;       <p>Adınız: <input type="text" name="ad" required></p>

&nbsp;       <p>E-posta: <input type="email" name="eposta" required></p>

&nbsp;       <p>Mesajınız:<br>

&nbsp;          <textarea name="mesaj" rows="4" cols="40"></textarea></p>

&nbsp;       <p><input type="submit" value="Mesajı Gönder"></p>

&nbsp;   </form>

</body>

</html>



###### **PHP kısmı (mesaj-al.php):**

<?php

**// Veriler geldi mi kontrol et**

if (!empty($\_POST)) {

&nbsp;   

    **// Verileri al ve temizle**

&nbsp;   $ad = htmlspecialchars($\_POST\['ad']);

&nbsp;   $eposta = htmlspecialchars($\_POST\['eposta']);

&nbsp;   $mesaj = htmlspecialchars($\_POST\['mesaj']);

&nbsp;   

    **// Boş mu kontrol et**

&nbsp;   if (empty($ad) || empty($eposta) || empty($mesaj)) {

&nbsp;       echo "<h3 style='color: red;'>Hata: Tüm alanları doldurun!</h3>";

&nbsp;   } else {

        **// Her şey tamam, mesajı göster**

&nbsp;       echo "<h2>Mesajınız Alındı!</h2>";

&nbsp;       echo "<p><strong>Ad:</strong> " . $ad . "</p>";

&nbsp;       echo "<p><strong>E-posta:</strong> " . $eposta . "</p>";

&nbsp;       echo "<p><strong>Mesaj:</strong> " . $mesaj . "</p>";

&nbsp;       echo "<p>Teşekkürler, en kısa sürede dönüş yapacağız.</p>";

&nbsp;   }

}

?>



#### **Özet**



1. **$\_POST** = Formdan gelen verileri alır, Verileri gizli şekilde gönderir, URL'de görünmez
2. **$\_GET** = Verileri URL'de (adres çubuğunda) görürsün



Bu kadar! PHP'de form verileri almak bu kadar basit. Kullanıcı bir şey yazar, sen $\_POST ile alırsın, kontrol edersin, işlersin.











