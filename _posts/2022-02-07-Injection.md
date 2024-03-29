---
title: OWASP API Security Injection
author: Eno
date: 2022-02-07 00:00:00 +0700
image: /assets/img/blogging/Injection.jpg
categories: [Blogging, 0x3n0, Injection]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Graphql API, jwt, SQL, Encode, parse, OWASP API Security, Injection]
---

![img-description](/assets/img/blogging/Injection.jpg)_OWASP API Security Injection_

kamu mungkin pernah mendengar tentang <kbd>Top 10 OWASP</kbd> atau sepuluh kerentanan teratas yang mengancam `Webapps`. OWASP juga secara berkala memilih daftar sepuluh besar kerentanan yang mengancam <kbd>API</kbd>, yang disebut <kbd>OWASP API Security Top 10</kbd>. Sepuluh besar API saat ini adalah :

- Broken Object Level Authorization 
- Broken User Authentication
- Excessive Data Exposure
- Lack of Resources & Rate Limiting
- Broken Function Level Authorization
- Mass Assignment
- Security Misconfiguration 
- Injection
- Improper Assets Management
- Insufficient Logging & Monitoring

## OWASP API Security Injection

OWASP API Security Injection adalah kerentanan yang paling memengaruhi API. Hari ini, mari kita bicara tentang `OWASP API Secururity #8`, **Injection**, jenis kerentanan yang memengaruhi sebagian besar aplikasi dan sistem API.

Injection adalah masalah mendasar untuk sejumlah besar kerentanan, seperti `SQL injection`, `OS command injection`, dan `XML Injection`, menyumbang persentase besar kerentanan yang ditemukan di `apps` dan `API`.

## Bagaimana injection terjadi?

Dalam satu kalimat, injection terjadi ketika aplikasi tidak dapat membedakan dengan benar antara data dan code user yang tidak dipercaya.

Data user yang tidak tepercaya dapat berupa parameter request <kbd>HTTP</kbd>, <kbd>header HTTP</kbd>, dan <kbd>cookie</kbd>. itu juga dapat berasal dari database atau file yang disimpan yang dapat dimodifikasi oleh user. Jika aplikasi tidak memproses data user yang tidak dipercaya dengan benar sebelum memasukkannya ke dalam perintah atau query, program akan mengacaukan masukan user sebagai bagian dari perintah atau query. Dalam hal ini, penyerang dapat mengirim data ke aplikasi dengan cara yang akan mengubah arti dari perintahnya.

Dalam serangan <kbd>SQL Injection</kbd>, misalnya, penyerang menyuntikkan data untuk memanipulasi perintah SQL. Dan dalam serangan Injection, penyerang memasukkan data yang memanipulasi logika perintah sistem OS di server hosting. Program yang menggabungkan data user dengan perintah atau code pemrograman berpotensi rentan.

Kerentanan Injection juga dapat memengaruhi sistem `API` karena API hanyalah cara lain untuk memasukkan input user yang tidak tepercaya ke dalam aplikasi. Mari kita lihat bagaimana kerentanan Injection muncul di <kbd>API</kbd>.

### Contoh OWASP API Security Injection #1: Mengambil postingan blog

Katakanlah <kbd>API</kbd> memungkinkan usernya untuk mengambil posting blog dengan mengirimkan request <kbd>GET</kbd> seperti ini:

```
GET /api/v1.1/posts?id=1337
```

request ini akan menyebabkan `API` mengembalikan posting 1337. Server akan mengambil posting blog yang sesuai dari database dengan query `SQL`, di mana `post_id` mengacu pada yang `id` diteruskan oleh user melalui URL.

```
GET /api/v1.1/posts?id=12358; DROP TABLE users
```

Server `SQL` akan menafsirkan bagian `id` setelah titik koma sebagai perintah SQL. Jadi SQL pertama-tama akan menjalankan perintah ini untuk mengambil posting blog seperti biasa:

```
SELECT * FROM posts WHERE post_id = 1337;
```

Kemudian akan menjalankan perintah ini untuk menghapus <kbd>TABLE USERS</kbd>, menyebabkan aplikasi kehilangan data yang disimpan dalam <kbd>TABLE</kbd> itu.

```
DROP TABLE users
```

ini disebut serangan `SQL Injection` dan dapat terjadi setiap kali input user diteruskan ke SQL query dengan cara yang tidak aman. Perhatikan bahwa input user dalam `API` tidak hanya berjalan melalui parameter <kbd>URL</kbd>, itu juga dapat mencapai aplikasi melalui request <kbd>POST</kbd>, parameter URL, dan sebagainya. Jadi, penting untuk mengamankan tempat-tempat itu juga.

### Contoh OWASP API Security Injection #2: Membaca file sistem

Katakanlah situs memungkinkan user untuk membaca file yang telah mereka upload melalui `API`:

```
GET /api/v1.1/files?id=1123581321
```

Request ini akan menyebabkan server mengambil file user melalui perintah sistem:

```
cat /var/www/html/users/tmp/1123581321
```

Dalam hal ini, user dapat menyuntikkan perintah baru ke dalam perintah OS sistem dengan menambahkan perintah tambahan setelah titik koma.

```
GET /api/v1.1/files?id=1123581321; rm -rf /var/www/html/users
```

Perintah ini akan memaksa server untuk menghapus folder yang terletak di <kbd>/var/www/html/users</kbd>, yang merupakan tempat aplikasi menyimpan informasi user.

```
rm -rf /var/www/html/users
```

## Mencegah kerentanan Injection di OWASP API Security Injection

Untuk menghindari kerentanan Injection, perlu diingat bahwa manipulasi data dapat terjadi kapan saja saat data sedang diproses atau digunakan, meskipun tidak selalu sejelas contoh sederhana yang sering ditunjukkan. Serangan ini bisa terjadi pada bagian data yang tidak dipercaya, bahkan jika tidak digunakan secara langsung oleh aplikasi. Hal ini dapat menyebabkan kerusakan pada aplikasi, datanya, atau pengguna.

Karena itu, mencegah Injection menjadi sulit, karena setiap bagian data yang diterima aplikasi harus diperiksa dan dinetralisir untuk menghindari serangan. Terkadang, data yang dianggap aman dapat menjadi berbahaya, seperti ketika karakter khusus digunakan untuk memicu SQL Injection oleh penyerang. Oleh karena itu, penting untuk dapat membedakan data yang aman dan tidak aman pada setiap aplikasi, meskipun tampilannya berbeda-beda.

## Input validation

Untuk melindungi dari ancaman Injection, ada beberapa tindakan yang dapat dilakukan. Salah satunya adalah dengan memvalidasi data yang tidak dipercaya menggunakan daftar blokir atau daftar yang diizinkan. Jika menggunakan daftar blokir, hindari karakter yang mungkin memengaruhi komponen aplikasi dan hanya mengizinkan string input dengan karakter yang diketahui pada daftar yang diizinkan.

Namun, daftar blokir mungkin sulit dilakukan karena tidak semua karakter yang signifikan bagi komponen aplikasi dapat diketahui. Sebaliknya, daftar yang diizinkan mungkin terlalu membatasi dan terkadang Anda perlu menerima karakter khusus seperti tanda kutip tunggal dalam bidang input user. Misalnya, jika user bernama OxO'Enogans mendaftar, dia harus diizinkan menggunakan satu kutipan dalam namanya.

Oleh karena itu, untuk meminimalkan risiko Injection, selain memvalidasi data, penting juga untuk mengamankan server dan database, menggunakan prepared statements dalam query database, dan membatasi akses pengguna sesuai dengan level aksesnya.

## Parameterization

Parameterisasi adalah salah satu pertahanan yang dapat digunakan untuk melawan Injection. Hal ini melibatkan mengompilasi bagian code dari perintah sebelum parameter yang disediakan oleh user dimasukkan. Daripada menggabungkan input user ke dalam perintah dan mengirimkannya ke server untuk dikompilasi, semua logika didefinisikan terlebih dahulu dan input user dimasukkan tepat sebelum perintah dieksekusi. Metode ini sangat efektif dalam mencegah beberapa kerentanan Injection, tetapi tidak dapat digunakan di setiap konteks dalam code.

## Escaping

Dan akhirnya, kamu dapat melarikan diri dari karakter khusus sebagai gantinya. Melarikan diri berarti kamu menyandikan karakter khusus dalam input user sehingga diperlakukan sebagai data dan bukan sebagai karakter khusus. Dengan menggunakan penanda dan syntax khusus untuk menandai karakter khusus dalam input user, pelolosan memungkinkan mengetahui bahwa data tidak dimaksudkan untuk dieksekusi.

Tetapi metode ini juga memiliki masalah. Pertama, kamu harus menggunakan syntax <kbd>Encode</kbd> yang tepat untuk setiap parser hilir atau nilai yang disandikan disalah artikan oleh parser. kamu mungkin juga lupa untuk menghindari beberapa karakter, yang dapat digunakan penyerang untuk menetralisir upaya penyandian kamu. Jadi, kunci untuk mencegah kerentanan Injection adalah memahami cara kerja parser dari berbagai bahasa, dan parser mana yang berjalan lebih dulu dalam proses kamu.
