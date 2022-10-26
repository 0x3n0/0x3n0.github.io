---
title: OWASP API Security Injection
author: Eno
date: 2022-02-07 00:00:00 +0700
image: /assets/img/blogging/Injection.jpg
categories: [Blogging, Tutorial, Injection]
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

Ini adalah contoh sederhana dari kerentanan Injection. Pada kenyataannya, penting untuk diingat bahwa kerentanan injection tidak selalu sejelas ini. Dan manipulasi ini dapat terjadi kapan saja, bagian data ini sedang diproses atau digunakan. Bahkan jika data user yang berbahaya tidak langsung digunakan oleh aplikasi, data yang tidak dipercaya pada akhirnya dapat berpindah ke suatu tempat program di mana ia dapat melakukan sesuatu, seperti fungsi atau query yang tidak dilindungi. Dan di sinilah menyebabkan kerusakan pada aplikasi, datanya, atau usernya.

Itu sebabnya Injection sangat sulit dicegah. Data yang tidak dipercaya dapat menyerang komponen aplikasi yang disentuhnya. Dan untuk setiap bagian data tidak dipercaya yang diterima aplikasi, ia perlu mendeteksi dan menetralisir serangan yang menargetkan setiap bagian aplikasi. Dan aplikasi mungkin berpikir sepotong data aman karena tidak mengandung karakter khusus yang digunakan untuk memicu <kbd>XSS</kbd> ketika penyerang bermaksud memicu <kbd>SQL Injection</kbd> sebagai gantinya. Tidak selalu mudah untuk menentukan data mana yang aman dan mana yang tidak, karena data yang aman dan tidak aman terlihat, sangat berbeda di berbagai aplikasi.

## Input validation

Jadi bagaimana kamu melindungi dari ancaman ini? 
Hal pertama yang dapat kamu lakukan adalah memvalidasi data yang tidak dipercaya. Ini berarti kamu menerapkan daftar blokir untuk menolak input yang berisi karakter yang mungkin memengaruhi komponen aplikasi. Atau kamu bisa menerapkan daftar yang diizinkan yang hanya mengizinkan string input dengan karakter yang diketahui. Misalnya, kamu menerapkan fungsi pendaftaran. Karena kamu tau bahwa data akan dimasukkan ke dalam <kbd>SQL query</kbd>, kamu menolak input nama user yang merupakan karakter khusus dalam SQL, seperti tanda kutip tunggal. Atau, kamu juga dapat menerapkan aturan yang hanya mengizinkan karakter alfanumerik.

Namun terkadang daftar blokir sulit dilakukan karena Anda tidak selalu tahu karakter mana yang akan signifikan bagi komponen aplikasi. Jika kamu hanya melewatkan satu karakter khusus, itu dapat memungkinkan penyerang untuk melewati firewall.

Dan daftar yang diizinkan mungkin terlalu membatasi dan dalam beberapa kasus, dan terkadang kamu mungkin perlu menerima karakter khusus seperti tanda kutip tunggal ```(')``` di bidang input user. Misalnya, jika user bernama <kbd>OxO'Enogans</kbd> mendaftar, dia harus diizinkan menggunakan satu kutipan dalam namanya.

## Parameterisasi

Pertahanan lain yang mungkin melawan Injection adalah parameterisasi. Parameterisasi mengacu pada kompilasi bagian code dari suatu perintah sebelum parameter yang disediakan user dimasukkan.

berarti bahwa alih-alih menggabungkan input user ke dalam perintah program dan mengirimkannya ke server untuk dikompilasi, kamu mendefinisikan semua logika terlebih dahulu, mengompilasinya, lalu memasukkan input user ke dalam perintah tepat sebelum di eksekusi. 

Setelah input user dimasukkan ke dalam perintah terakhir, perintah tidak akan diurai dan dikompilasi lagi. Dan yang tidak ada dalam pernyataan asli akan diperlakukan sebagai data string, dan bukan code yang dapat dieksekusi. Jadi bagian logika program dari perintah kamu akan tetap utuh.

Hal ini memungkinkan `database` untuk membedakan antara bagian code dan bagian data dari perintah, terlepas dari seperti apa input user. 
Metode ini sangat efektif dalam mencegah beberapa kerentanan Injection, tetapi tidak dapat digunakan di setiap konteks dalam code.

## Escaping

Dan akhirnya, kamu dapat melarikan diri dari karakter khusus sebagai gantinya. Melarikan diri berarti kamu menyandikan karakter khusus dalam input user sehingga diperlakukan sebagai data dan bukan sebagai karakter khusus. Dengan menggunakan penanda dan syntax khusus untuk menandai karakter khusus dalam input user, pelolosan memungkinkan mengetahui bahwa data tidak dimaksudkan untuk dieksekusi.

Tetapi metode ini juga memiliki masalah. Pertama, kamu harus menggunakan syntax <kbd>Encode</kbd> yang tepat untuk setiap parser hilir atau nilai yang disandikan disalah artikan oleh parser. kamu mungkin juga lupa untuk menghindari beberapa karakter, yang dapat digunakan penyerang untuk menetralisir upaya penyandian kamu. Jadi, kunci untuk mencegah kerentanan Injection adalah memahami cara kerja parser dari berbagai bahasa, dan parser mana yang berjalan lebih dulu dalam proses kamu.
