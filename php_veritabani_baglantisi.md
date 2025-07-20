#### 1\. Veritabanı Nedir?

Veritabanı, bilgileri düzenli şekilde saklayan bir depodur. Örneğin:

* Kullanıcı bilgileri (ad, e-posta, şifre)
* Ürün bilgileri (ad, fiyat, stok)
* Sipariş bilgileri
* Tıpkı Excel tablosu gibi, ama çok daha güçlü.



#### 2\. Bağlantı İçin Gerekli Bilgiler

**MySQL'e bağlanmak için 4 temel bilgi gerekir:**



* Host (Sunucu adresi): Veritabanının nerede olduğu (genelde localhost)
* Veritabanı adı: Hangi veritabanına bağlanılacak
* Kullanıcı adı: Veritabanı kullanıcı adı
* Şifre: Veritabanı şifresi



#### 3\. PHP'de Veritabanı Bağlantısı - 3 Yöntem

##### Yöntem 1: PDO (Modern ve Güvenli – Önerilen)

<?php

$host = "localhost";

$dbname = "sirket\_db";

$username = "root";

$password = "123456";



try {

&nbsp;   $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);

&nbsp;   $pdo->setAttribute(PDO::ATTR\_ERRMODE, PDO::ERRMODE\_EXCEPTION);

&nbsp;   echo "Veritabanı bağlantısı başarılı!";

} catch (PDOException $e) {

&nbsp;   echo "Bağlantı hatası: " . $e->getMessage();

}

?>



##### Yöntem 2: MySQLi (Nesne Tabanlı)

<?php

$host = "localhost";

$username = "root";

$password = "123456";

$dbname = "sirket\_db";



$mysqli = new mysqli($host, $username, $password, $dbname);



if ($mysqli->connect\_error) {

&nbsp;   die("Bağlantı hatası: " . $mysqli->connect\_error);

}



echo "Veritabanı bağlantısı başarılı!";

?>



##### Yöntem 3: MySQLi (Fonksiyonel)

<?php

$host = "localhost";

$username = "root";

$password = "123456";

$dbname = "sirket\_db";



$connection = mysqli\_connect($host, $username, $password, $dbname);



if (!$connection) {

&nbsp;   die("Bağlantı hatası: " . mysqli\_connect\_error());

}



echo "Veritabanı bağlantısı başarılı!";

?>



#### 4\. Güvenli Bağlantı Dosyası

**config.php:**

<?php

define('DB\_HOST', 'localhost');

define('DB\_NAME', 'sirket\_db');

define('DB\_USER', 'root');

define('DB\_PASS', '123456');



function getDBConnection() {

&nbsp;   try {

&nbsp;       $dsn = "mysql:host=" . DB\_HOST . ";dbname=" . DB\_NAME . ";charset=utf8mb4";

&nbsp;       $pdo = new PDO($dsn, DB\_USER, DB\_PASS);

&nbsp;       $pdo->setAttribute(PDO::ATTR\_ERRMODE, PDO::ERRMODE\_EXCEPTION);

&nbsp;       return $pdo;

&nbsp;   } catch (PDOException $e) {

&nbsp;       die("Veritabanı bağlantı hatası: " . $e->getMessage());

&nbsp;   }

}

?>



**Ana dosyada kullanım:**

<?php

require\_once 'config.php';

$pdo = getDBConnection();

echo "Bağlantı başarılı!";

?>



#### 5\. Veri Ekleme

<?php

require\_once 'config.php';

$pdo = getDBConnection();



if (isset($\_POST\['kaydet'])) {

&nbsp;   $ad = $\_POST\['ad'];

&nbsp;   $eposta = $\_POST\['eposta'];

&nbsp;   $yas = $\_POST\['yas'];



&nbsp;   try {

&nbsp;       $sql = "INSERT INTO kullanicilar (ad, eposta, yas) VALUES (?, ?, ?)";

&nbsp;       $stmt = $pdo->prepare($sql);

&nbsp;       $stmt->execute(\[$ad, $eposta, $yas]);



&nbsp;       echo "Kullanıcı başarıyla eklendi!";

&nbsp;   } catch (PDOException $e) {

&nbsp;       echo "Hata: " . $e->getMessage();

&nbsp;   }

}

?>



**HTML Formu:**

<form method="POST">

&nbsp; <p>Ad: <input type="text" name="ad" required></p>

&nbsp; <p>E-posta: <input type="email" name="eposta" required></p>

&nbsp; <p>Yaş: <input type="number" name="yas" required></p>

&nbsp; <p><button type="submit" name="kaydet">Kaydet</button></p>

</form>



#### 6\. Veri Okuma

<?php

require\_once 'config.php';

$pdo = getDBConnection();



try {

&nbsp;   $sql = "SELECT \* FROM kullanicilar";

&nbsp;   $stmt = $pdo->query($sql);

&nbsp;   $kullanicilar = $stmt->fetchAll(PDO::FETCH\_ASSOC);



&nbsp;   echo "<h2>Kullanıcı Listesi:</h2>";

&nbsp;   echo "<table border='1'>";

&nbsp;   echo "<tr><th>ID</th><th>Ad</th><th>E-posta</th><th>Yaş</th></tr>";



&nbsp;   foreach ($kullanicilar as $kullanici) {

&nbsp;       echo "<tr>";

&nbsp;       echo "<td>" . $kullanici\['id'] . "</td>";

&nbsp;       echo "<td>" . $kullanici\['ad'] . "</td>";

&nbsp;       echo "<td>" . $kullanici\['eposta'] . "</td>";

&nbsp;       echo "<td>" . $kullanici\['yas'] . "</td>";

&nbsp;       echo "</tr>";

&nbsp;   }

&nbsp;   echo "</table>";



} catch (PDOException $e) {

&nbsp;   echo "Hata: " . $e->getMessage();

}

?>



#### 7\. Veri Güncelleme

<?php

require\_once 'config.php';

$pdo = getDBConnection();



if (isset($\_POST\['guncelle'])) {

&nbsp;   $id = $\_POST\['id'];

&nbsp;   $yeni\_ad = $\_POST\['ad'];

&nbsp;   $yeni\_eposta = $\_POST\['eposta'];



&nbsp;   try {

&nbsp;       $sql = "UPDATE kullanicilar SET ad = ?, eposta = ? WHERE id = ?";

&nbsp;       $stmt = $pdo->prepare($sql);

&nbsp;       $stmt->execute(\[$yeni\_ad, $yeni\_eposta, $id]);



&nbsp;       echo "Kullanıcı bilgileri güncellendi!";

&nbsp;   } catch (PDOException $e) {

&nbsp;       echo "Hata: " . $e->getMessage();

&nbsp;   }

}

?>



#### 8\. Veri Silme

<?php

require\_once 'config.php';

$pdo = getDBConnection();



if (isset($\_GET\['sil'])) {

&nbsp;   $silinecek\_id = $\_GET\['sil'];



&nbsp;   try {

&nbsp;       $sql = "DELETE FROM kullanicilar WHERE id = ?";

&nbsp;       $stmt = $pdo->prepare($sql);

&nbsp;       $stmt->execute(\[$silinecek\_id]);



&nbsp;       echo "Kullanıcı silindi!";

&nbsp;   } catch (PDOException $e) {

&nbsp;       echo "Hata: " . $e->getMessage();

&nbsp;   }

}

?>



##### Önemli Noktalar

✅ PDO kullan — En güvenli yöntem

✅ Prepared statements kullan — SQL Injection’dan korunursun

✅ Try-catch kullan — Hataları yakala

✅ Veritabanı bilgilerini ayrı dosyada tut — Güvenlik sağlar



###### PDO ve MySQLi Arasındaki Farklar

**MySQLi**: Sadece MySQL veritabanı ile çalışır

**PDO**: Farklı veritabanı türlerini destekler (MySQL, SQLite, PostgreSQL vb.)



**Avantaj - Dezavantaj:**

###### 

###### MySQLi

✅ MySQL’e özel özellikler

✅ Biraz daha hızlı

❌ Sadece MySQL desteği

❌ Daha karmaşık kullanım



###### PDO

✅ Birden fazla veritabanı ile uyumlu

✅ Daha temiz ve sade syntax

✅ Otomatik veri tipi belirleme

✅ Daha iyi hata yönetimi

❌ MySQL’e özel bazı özellikleri kullanamazsın

