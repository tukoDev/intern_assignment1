##### 1\. Veritabanı Nedir?

Veritabanı, bilgileri düzenli şekilde saklayan bir depodur. Örneğin:



* Kullanıcı bilgileri (ad, e-posta, şifre)
* Ürün bilgileri (ad, fiyat, stok)
* Sipariş bilgileri



Tıpkı Excel tablosu gibi, ama çok daha güçlü.



##### 2\. Bağlantı İçin Gerekli Bilgiler

MySQL'e bağlanmak için 4 temel bilgi gerekir:



* **Host (Sunucu adresi)**: Veritabanının nerede olduğu (genelde "localhost")
* **Veritabanı adı**: Hangi veritabanına bağlanacağın
* **Kullanıcı adı**: Veritabanı kullanıcı adın
* **Şifre**: Veritabanı şifresi



##### 3\. PHP'de Veritabanı Bağlantısı - 3 Yöntem Mevcut



###### **Yöntem 1: PDO (Modern ve Güvenli - Önerilen)**

<?php

// Veritabanı bilgileri

$host = "localhost";

$dbname = "sirket\\\\\\\_db";

$username = "root";

$password = "123456";



try {

    \\\*\\\*// Bağlantı kur\\\*\\\*

\\\&nbsp;   $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);

\\\&nbsp;   

\\\&nbsp;   \\\*\\\*// Hata ayarları\\\*\\\*

\\\&nbsp;   $pdo->setAttribute(PDO::ATTR\\\\\\\_ERRMODE, PDO::ERRMODE\\\\\\\_EXCEPTION);

\\\&nbsp;   

\\\&nbsp;   echo "Veritabanı bağlantısı başarılı!";

\\\&nbsp;   

} catch (PDOException $e) {

\\\&nbsp;   echo "Bağlantı hatası: " . $e->getMessage();

}






###### \*\*Yöntem 2: MySQLi (Nesne Tabanlı)\*\*

<?php

$host = "localhost";

$username = "root";

$password = "123456";

$dbname = "sirket\\\\\\\_db";



\\\*\\\*// Bağlantı kur\\\*\\\*

$mysqli = new mysqli($host, $username, $password, $dbname);



\\\*\\\*// Bağlantı kontrolü\\\*\\\*

if ($mysqli->connect\\\\\\\_error) {

\\\&nbsp;   die("Bağlantı hatası: " . $mysqli->connect\\\\\\\_error);

}



echo "Veritabanı bağlantısı başarılı!";






###### Yöntem 3: MySQLi (Fonksiyonel)

<?php

$host = "localhost";

$username = "root";

$password = "123456";

$dbname = "sirket\\\\\\\_db";



\\\*\\\*// Bağlantı kur\\\*\\\*

$connection = mysqli\\\\\\\_connect($host, $username, $password, $dbname);



\\\*\\\*// Bağlantı kontrolü\\\*\\\*

if (!$connection) {

\\\&nbsp;   die("Bağlantı hatası: " . mysqli\\\\\\\_connect\\\\\\\_error());

}



echo "Veritabanı bağlantısı başarılı!";






##### 4\\. Güvenli Bağlantı Dosyası (Önerilen Yöntem)

Veritabanı bilgilerini ayrı dosyada tut:

config.php:

<?php

\\\*\\\*// Veritabanı ayarları\\\*\\\*

define('DB\\\\\\\_HOST', 'localhost');

define('DB\\\\\\\_NAME', 'sirket\\\\\\\_db');

define('DB\\\\\\\_USER', 'root');

define('DB\\\\\\\_PASS', '123456');



\\\*\\\*// Bağlantı fonksiyonu\\\*\\\*

function getDBConnection() {

\\\&nbsp;   try {

\\\&nbsp;       $dsn = "mysql:host=" . DB\\\\\\\_HOST . ";dbname=" . DB\\\\\\\_NAME . ";charset=utf8mb4";

\\\&nbsp;       $pdo = new PDO($dsn, DB\\\\\\\_USER, DB\\\\\\\_PASS);

\\\&nbsp;       $pdo->setAttribute(PDO::ATTR\\\\\\\_ERRMODE, PDO::ERRMODE\\\\\\\_EXCEPTION);

\\\&nbsp;       return $pdo;

\\\&nbsp;   } catch (PDOException $e) {

\\\&nbsp;       die("Veritabanı bağlantı hatası: " . $e->getMessage());

\\\&nbsp;   }

}




\*\*Ana dosyanda kullanım:\*\*

<?php

\\\*\\\*// Bağlantı dosyasını dahil et\\\*\\\*

require\\\\\\\_once 'config.php';



\\\*\\\*// Bağlantıyı al\\\*\\\*

$pdo = getDBConnection();



echo "Bağlantı başarılı!";






##### 5\\. Veri Ekleme İşlemi

<?php

require\\\\\\\_once 'config.php';

$pdo = getDBConnection();



\\\*\\\*// Form verilerini al\\\*\\\*

if (isset($\\\\\\\_POST\\\\\\\['kaydet'])) {

\\\&nbsp;   $ad = $\\\\\\\_POST\\\\\\\['ad'];

\\\&nbsp;   $eposta = $\\\\\\\_POST\\\\\\\['eposta'];

\\\&nbsp;   $yas = $\\\\\\\_POST\\\\\\\['yas'];

\\\&nbsp;   

\\\&nbsp;   try {

        \\\*\\\*// Güvenli veri ekleme (SQL Injection korunması)\\\*\\\*

\\\&nbsp;       $sql = "INSERT INTO kullanicilar (ad, eposta, yas) VALUES (?, ?, ?)";

\\\&nbsp;       $stmt = $pdo->prepare($sql);

\\\&nbsp;       $stmt->execute(\\\\\\\[$ad, $eposta, $yas]);

\\\&nbsp;       

\\\&nbsp;       echo "Kullanıcı başarıyla eklendi!";

\\\&nbsp;       

\\\&nbsp;   } catch (PDOException $e) {

\\\&nbsp;       echo "Hata: " . $e->getMessage();

\\\&nbsp;   }

}


\*\*<!-- HTML formu -->\*\*

<form method="POST">

    <p>Ad: <input type="text" name="ad" required></p>

    <p>E-posta: <input type="email" name="eposta" required></p>

    <p>Yaş: <input type="number" name="yas" required></p>

    <p><button type="submit" name="kaydet">Kaydet</button></p>

</form>





##### 6\\. Veri Okuma İşlemi

<?php

require\\\\\\\_once 'config.php';

$pdo = getDBConnection();



try {

    \\\*\\\*// Tüm kullanıcıları getir\\\*\\\*

\\\&nbsp;   $sql = "SELECT \\\\\\\* FROM kullanicilar";

\\\&nbsp;   $stmt = $pdo->query($sql);

\\\&nbsp;   $kullanicilar = $stmt->fetchAll(PDO::FETCH\\\\\\\_ASSOC);

\\\&nbsp;   

\\\&nbsp;   echo "<h2>Kullanıcı Listesi:</h2>";

\\\&nbsp;   echo "<table border='1'>";

\\\&nbsp;   echo "<tr><th>ID</th><th>Ad</th><th>E-posta</th><th>Yaş</th></tr>";

\\\&nbsp;   

\\\&nbsp;   foreach ($kullanicilar as $kullanici) {

\\\&nbsp;       echo "<tr>";

\\\&nbsp;       echo "<td>" . $kullanici\\\\\\\['id'] . "</td>";

\\\&nbsp;       echo "<td>" . $kullanici\\\\\\\['ad'] . "</td>";

\\\&nbsp;       echo "<td>" . $kullanici\\\\\\\['eposta'] . "</td>";

\\\&nbsp;       echo "<td>" . $kullanici\\\\\\\['yas'] . "</td>";

\\\&nbsp;       echo "</tr>";

\\\&nbsp;   }

\\\&nbsp;   echo "</table>";

\\\&nbsp;   

} catch (PDOException $e) {

\\\&nbsp;   echo "Hata: " . $e->getMessage();

}






##### 7\\. Veri Güncelleme

<?php

require\\\\\\\_once 'config.php';

$pdo = getDBConnection();



if (isset($\\\\\\\_POST\\\\\\\['guncelle'])) {

\\\&nbsp;   $id = $\\\\\\\_POST\\\\\\\['id'];

\\\&nbsp;   $yeni\\\\\\\_ad = $\\\\\\\_POST\\\\\\\['ad'];

\\\&nbsp;   $yeni\\\\\\\_eposta = $\\\\\\\_POST\\\\\\\['eposta'];

\\\&nbsp;   

\\\&nbsp;   try {

\\\&nbsp;       $sql = "UPDATE kullanicilar SET ad = ?, eposta = ? WHERE id = ?";

\\\&nbsp;       $stmt = $pdo->prepare($sql);

\\\&nbsp;       $stmt->execute(\\\\\\\[$yeni\\\\\\\_ad, $yeni\\\\\\\_eposta, $id]);

\\\&nbsp;       

\\\&nbsp;       echo "Kullanıcı bilgileri güncellendi!";

\\\&nbsp;       

\\\&nbsp;   } catch (PDOException $e) {

\\\&nbsp;       echo "Hata: " . $e->getMessage();

\\\&nbsp;   }

}






##### 8\\. Veri Silme

<?php

require\\\\\\\_once 'config.php';

$pdo = getDBConnection();



if (isset($\\\\\\\_GET\\\\\\\['sil'])) {

\\\&nbsp;   $silinecek\\\\\\\_id = $\\\\\\\_GET\\\\\\\['sil'];

\\\&nbsp;   

\\\&nbsp;   try {

\\\&nbsp;       $sql = "DELETE FROM kullanicilar WHERE id = ?";

\\\&nbsp;       $stmt = $pdo->prepare($sql);

\\\&nbsp;       $stmt->execute(\\\\\\\[$silinecek\\\\\\\_id]);

\\\&nbsp;       

\\\&nbsp;       echo "Kullanıcı silindi!";

\\\&nbsp;       

\\\&nbsp;   } catch (PDOException $e) {

\\\&nbsp;       echo "Hata: " . $e->getMessage();

\\\&nbsp;   }

}






###### Önemli Noktalar



\* \*\*PDO kullan\*\* - En güvenli yöntem
\* \*\*Prepared statements kullan\*\* - SQL Injection'dan korunur
\* \*\*Try-catch kullan\*\* - Hataları yakala
\* \*\*Veritabanı bilgilerini ayrı dosyada tut\*\* - Güvenlik





##### PDO VE MySQLi ARASINDAKI FARKLAR

###### Temel Fark

**MySQLi** = Sadece MySQL veritabanı ile çalışır

**PDO** = Birçok veritabanı türü ile çalışır (MySQL, PostgreSQL, SQLite vb.)





**Avantajlar ve Dezavantajlar**

**MySQLi**

✅ **Avantajları**:



* MySQL'e özel özellikler kullanabilirsin
* Biraz daha hızlı (sadece MySQL için optimize)
* MySQL prosedürlerini çağırabilirsin



❌ **Dezavantajları**:



* Sadece MySQL ile çalışır
* Daha karmaşık syntax
* Veri tiplerini manuel belirtmelisin



**PDO**

✅ **Avantajları**:



* Birçok veritabanı türü destekler
* Daha temiz ve basit syntax
* Otomatik veri tipi belirleme
* Daha iyi hata yönetimi
* Modern ve objektif



❌ **Dezavantajları**:



* MySQL'e özel özellikler kullanamayabilirsin
* Çok az performans farkı (ihmal edilebilir)
  
