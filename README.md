
## API Kullanımı
Her post işleminde kesinliklike gitmesi gereken 2 veri var. Bunlar olmadığı zaman işlem yapılmaz.
#### Api endpoint

```http
  POST /dashboard/main/adminphp/api.php
```
#### Bilgilendirme
Tüm veriler json olarak gönderilmeli.
```http
  Test API anahtarı: ea6209490e01661f2daddd6f1a78
```
| Parametre | Tip     | Açıklama                |
| :-------- | :------- | :------------------------- |
| `key` | `string` | **Gerekli**. API anahtarınız. |
| `function` | `string` |  **Gerekli**. Yapılcak işlem ön bilgilendirme.

## Register API örneği

```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "register" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `username`      | `json` | **Gerekli**.  İsim soyisim |
| `password`      | `json` | **Gerekli**. Kullanıcı şifresi |
| `email`      | `json` | **Gerekli**. Kullanıcı email bilgisi |
| `phone`      | `json` | **Gerekli**. Kullanıcı telefon numarası |
| `job`      | `json` | **Gerekli**. Kullanıcı iş bilgisi |
| `birthday`      | `json` | **DİKKAT**. unix timestamp olarak gönderilmeli |
| `about`      | `json` | **Gerekli**. Kullanıcının hakkında bölümü |
| `is_search`      | `json` | **Gerekli**. Ev arama durumu (1 veya 0) |
| `gender`      | `json` | **Gerekli**. Cinsiyet bilgisi (1 = kadın, 2 = erkek , 3 = farketmez,  4 = diğer) |


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir.

```php
  (
      "success" => true,
      "message" => "Veriler başarılı bir şekilde kayıt edildi.",
      "user_id" => "user_64ez9da9caa0fc"
      "isim_soyisim" => (Örnek isim),
      "mail" => E-posta bilgisi,
      register_time" => kayıt olma tarihi (unix),
      "is_search" => ev arama durumu

)
```
  
## Kullanıcı Sorgulama
 Kullanıcı sorgulama işleminde 'email' veya 'phone' bilgilerinden bir tanesi yeterli. Tek veriyle sorgulama yapabilirsiniz email ve phone bilgisi veritabanında benzersiz olarak işaretlenir.
```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "get_user" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `email`      | `json` | **OPSİYONEL**. Kullanıcı email bilgisi |
| `phone`      | `json` | **OPSİYONEL**. Kullanıcı telefon numarası |



Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir.

```php
  {
  "success": true,
  "message": "1 eşleşme bulundu",
  "data": [
    {
      "user_id": "user4324_a12453",
      "isim_soyisim": "test user",
      "email": "1235@gmail.com",
      "phone": "113451323451",
      "password": "123241213451334",
      "job": "test",
      "about": "hi",
      "register_time": "1693224843"
    }
  ]
}
```
## Kullanıcı Güncelleme
 Kullanıcı Güncelleme işleminde 'email' ve 'phone' bilgilerinin gelmesi gerekiyor.
```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "user_update" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `email`      | `json` | **GEREKLİ**. Kullanıcı email bilgisi |
| `phone`      | `json` | **GEREKLİ**. Kullanıcı telefon numarası |
| `update`      | `json` | **GEREKLİ**. Kullanıcının hangi bilgisi güncellenecek bilgisi içeriyor. Başında "updated_" olmadan kullanabilirsin.  |
| `updated_email`      | `json` | **OPSİYONEL**. Kullanıcının email bilgisini güncelleme |
| `updated_name`      | `json` | **OPSİYONEL**. Kullanıcı isim soy isim güncelleme |
| `updated_about`      | `json` | **OPSİYONEL**. Kullanıcının hakkında bilgisini güncelleme |
| `updated_password`      | `json` | **OPSİYONEL**. Kullanıcının şifre bilgisini güncelleme |
| `updated_phone`      | `json` | **OPSİYONEL**. Kullanıcı telefon numarası güncelleme |



Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir.

```php
{
  "success": true,
  "user_id": "user_64ez9da9ca0fc",
  "function": "user_update",
  "update": "email",
  "message": "Kullanıcı email bilgileri güncellendi"
}
```
## Kullanıcı Silme
Kullanıcı Silme işleminde 'email' ve 'phone' bilgilerinin gelmesi gerekiyor.

```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "user_delete" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `email`      | `json` | **GEREKLİ**. Kullanıcı email bilgisi |
| `phone`      | `json` | **GEREKLİ**. Kullanıcı telefon numarası |





Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir.

```php
{
  "success": true,
  "funciton": "user_delete",
  "message": "Kullanıcı başarıyla silindi."
}
```
## Cevap ekleme
Kullanıcının kayıt olma ekranından aldığımız hobi bilgileri. Eşleştirme sistemi için kullanılacak. Key ve function bilgisini ilettikten sonra data diye alt array oluşturup 3 verimizi iletiyoruz.  
```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "quest_add" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `user_id`      | `json` | **GEREKLİ**. Kullanıcı data user_id bilgisi |
| `soru_id`      | `json` | **GEREKLİ**. Kullanıcının data soru idsi |
| `cevap_id`      | `json` | **GEREKLİ**. Kullanıcının data cevap idsi |


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir. Örnekte 2 data gönderilme örneği yapılmıştır. 

```php
[
  {
    "success": true,
    "error_code": "4x0",
    "function": "quest_add",
    "user_id": "user_64e9daac7a7bad",
    "soru_id": "00242",
    "cevap_id": "0014",
    "message": "Cevap güncellendi."
  },
  {
    "success": true,
    "error_code": "4x0",
    "function": "quest_add",
    "user_id": "user_64ez9da9caa0fc",
    "soru_id": "007645",
    "cevap_id": "00324",
    "message": "Cevap güncellendi."
  }
]
```
## Toplam kullanıcı 
Toplam kullanıcı sayısını sorgulamamıza yarıyan api bilgisi

```http
  POST /dashboard/main/adminphp/api.php
```
| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "get_total" |
| `key`      | `json` | **Gerekli**.  Secret Key |


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir. 
```
{
  "success": true,
  "message": "Toplam üye sayısı alındı.",
  "total_users": "3"
}
```
## Doğum Günü
Bugün içerisinde doğum günü olan tüm kullanıcıların bilgileri çekmek için kullandığımız api.

```http
  POST /dashboard/main/adminphp/api.php
```


| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "get_birthday" |
| `key`      | `json` | **Gerekli**.  Secret Key |


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir. 
```
{
  "success": true,
  "message": "Bugün doğum günü olan üyelerin bilgileri alındı.",
  "total_users": 2,
  "birthday_users": [
    {
      "user_id": "user_64ez9da9caa0fc",
      "name_surname": "yzx",
      "phone": "0000000000",
      "email": "1341345134513@gmail.com",
      "register_time": "1693224647",
      "gender": "Erkek"
    },
    {
      "user_id": "user4324_a1231432",
      "name_surname": "xyz",
      "phone": "12345123451",
      "email": "user2_update@test.com",
      "register_time": "1693224843",
      "gender": "Erkek"
    }
  ]
}
```
## Kullanıcı raporlama
Uygulama içerisindeki kurallara uymayan kullanıcıları bildirmek için kullanılan api.

```http
  POST /dashboard/main/adminphp/api.php
```

| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "report" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `user_id`      | `json` | **Gerekli**.  Raporlayan Kullanıcının user_id'si |
| `reported_user`      | `json` | **Gerekli**.  Raporlanan kullanıcının user_id bilgisi |
| `reason`      | `json` | **Gerekli**.  Şikayet sebebi. |


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir.
```html
{
  "success": true,
  "message": "Veriler başarılı bir şekilde kayıt edildi.",
  "reporter_id": "user4324_a1231432",
  "reason": "Şüpheli üye",
  "reported_user": "user_64ez9da9caa0fc"
}
```
## Login
Email ve şifre bilgisinin veritabanında olup olmadığını kontrol etme apisi.

```http
  POST /dashboard/main/adminphp/api.php
```
| Parametre | Tip     | Açıklama                       |
| :-------- | :------- | :-------------------------------- |
| `function`      | `json` | **Gerekli**.  "login" |
| `key`      | `json` | **Gerekli**.  Secret Key |
| `email`      | `json` | **Gerekli**.  Email bilgisi |
| `password`      | `json` | **Gerekli**.  Password bilgisi|


Eğer tüm veriler uygun şekilde gönderildiyse yanıt olarak aşağıdaki yanıt gelir. 
```
{
  "success": true,
  "message": "1 eşleşme bulundu",
  "data": {
    "user_name": "testset",
    "user_id": "user_64ez9da9caa0fc"
  }
}
```

