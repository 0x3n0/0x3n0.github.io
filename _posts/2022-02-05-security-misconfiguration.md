---
title: OWASP API Security Misconfiguration
author: Eno
date: 2022-02-05 00:00:00 +0700
image: /assets/img/blogging/Security-Misconfiguration.jpeg
description: security misconfiguration error, ancaman konstan terhadap implementasi API.
categories: [Blogging, 0x3n0, Security Misconfiguration]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Graphql API, jwt, SQL, Encode, parse, OWASP API Security API Security, Injection, Security Misconfiguration]
---

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

**Security Misconfiguration** merupakan ancaman konstan terhadap <kbd>API</kbd> dan aplikasi <kbd>non-API</kbd>. mari kita bicara tentang `Security Misconfiguration` di API, dan bagaimana hal itu dapat memengaruhi API.

![img-description](/assets/img/blogging/Security-Misconfiguration.jpeg)_OWASP API Security Misconfiguration_

## Pesan kesalahan verbose

Pertama-tama, salah satu `Security Misconfiguration` yang paling umum adalah mengirim pesan kesalahan verbose kepada user. Pesan kesalahan verbose ini mungkin berisi jejak, informasi tentang sistem, seperti versi server atau struktur `database`, dan memberikan wawasan kepada user tentang cara kerja aplikasi. 
Dalam hal ini, penyerang dapat memaksa pesan kesalahan dari aplikasi (melalui penyediaan input yang salah atau ilegal) untuk mengumpulkan informasi tentang server.

Banyak halaman `404` default juga berisi tanda tangan khusus yang memungkinkan penyerang untuk menandai teknologi yang digunakan, contohnya adalah **framework Ruby on Rails**.

## Header HTTP yang salah diconfigurasi

configurasi umum lainnya adalah penyalahgunaan atau hilangnya <kbd>header HTTP</kbd>. Ada banyak header keamanan HTTP yang membantu meningkatkan keamanan aplikasi. Jika tidak diconfigurasi dengan benar, penyerang sering kali dapat menemukan celah keamanan yang memungkinkan mereka mengekstrak data, atau melakukan serangan pada user aplikasi.

Misalnya, header **Content-Security-Policy (CSP)** mengontrol resource mana yang boleh dimuat oleh browser untuk sebuah halaman. 
browser harus diatur untuk melarang scrip dari domain random, dan atribut HTML penanganan peristiwa untuk mencegah serangan <kbd>XSS (cross site script)</kbd>. Untuk detail tentang cara mengconfigurasi CSP dengan aman, baca posting saya tentang topik di sini: [Content Security Policy (CSP)](https://0x3n0.github.io/)

Kesalahan configurasi **CORS (Cross-Origin resource sharing)** juga merupakan masalah yang berasal dari kesalahan configurasi <kbd>header HTTP</kbd>.
Cross-origin resource sharing **(CORS)** adalah cara aman untuk melonggarkan same-origin policy **(SOP)**. ini juga memungkinkan server untuk secara eksplisit menentukan daftar asal yang diizinkan untuk mengakses resourcenya melalui header <kbd>Access-Control-Allow-Origin<kbd>. 

Access-Control-Allow-Origin harus diconfigurasi untuk mengizinkan komunikasi **cross-origin** dari situs tepercaya. Kebijakan CORS yang salah diconfigurasi memungkinkan penyerang mencuri data rahasia dengan mengacaukan komunikasi cross-origin. Anda dapat membaca lebih lanjut tentang bagaimana penyerang dapat mengeksploitasi CORS yang salah configurasi di sini: [**Hacking the Same-Origin Policy**](https://0x3n0.github.io/)

## Layanan yang tidak perlu atau HTTP methods

Kesalahan configurasi umum lainnya adalah gagal menutup layanan yang tidak perlu atau HTTP methods. Sebagai contoh, mari kita lihat contoh yang saya sebutkan di posting saya sebelumnya. **Access control bug** yang saya sebutkan disebabkan oleh tidak menutup <kbd>HTTP methods</kbd> yang tidak digunakan.

API memungkinkan usernya untuk mengambil posting blog dengan mengirimkan request `GET` ke akhir seperti ini:

```
GET /api/v1.1/user/12358/posts?id=32
```

Request ini akan menyebabkan <kbd>API</kbd> mengembalikan postingan `32` dari user `12358`. Karena semua postingan di platform ini bersifat publik, setiap user dapat mengirimkan request untuk mengakses postingan orang lain. 

Namun, karena hanya user itu sendiri yang boleh mengubah postingan blog, hanya user `12358` yang dapat mengirimkan request <kbd>POST</kbd> untuk mengubah atau mengedit postingan. Jika API tidak menempatkan batasan yang sama pada request yang dikirim dengan **HTTP methods** yang kurang populer, seperti <kbd>PUT</kbd> dan <kbd>DELETE</kbd>, pernyerang mungkin dapat mengubah atau menghapus postingan user lain dengan menggunakan HTTP methods yang berbeda.

```
DELETE /api/v1.1/user/12358/posts?id=32
```

saya juga berbicara tentang bagaimana situs memungkinkan admin untuk melihat statistik situs melalui API khusus:

```
GET /api/v1.1/site/stats/hd216zla
```

admin ini tidak menerapkan batasan user. Situs bergantung pada fakta bahwa `URL` berisi string random di akhir untuk mencegah user yang tidak sah mengaksesnya. Praktik ini disebut “**Security through Obscurity**”, yang berarti meningkatkan keamanan dengan menahan pengetahuan dari pihak luar.

Tetapi keamanan melalui ketidak jelasan tidak dapat diandalkan sebagai satu-satunya mekanisme keamanan. Jika penyerang dapat mengetahui `URL` yang tidak jelas melalui kebocoran informasi, penyerang dapat mengakses fungsionalitas sensitif yang tersembunyi di balik titik akhir. Membiarkan layanan sensitif seperti ini terbuka untuk orang luar dapat menyebabkan penyerang mendapatkan akses ke sana.

## configurasi default tidak aman

Banyak dependensi pihak ketiga seperti basis data dan web framework tidak aman secara default dan mengharuskan developer untuk memperketat keamanan melalui configurasi khusus. 
Misalnya, versi <kbd>MongoDB</kbd> yang lebih lama dapat diakses ke internet dan tidak memerlukan authentication secara default. Hal ini menyebabkan ribuan database terekspos ke publik jika developer tidak mengubah configurasi default.

configurasi default yang tidak aman seperti contoh ini dapat menyebabkan banyak masalah keamanan jika developer tidak menyadari konsekuensinya. 

Sampai sekarang, MongoDB masih tidak memerlukan authentication secara default. Untuk melihat bagaimana kamu dapat mengatur authentication ke database MongoDB kamu, baca dokumen di sini: [**enable-authentication**](https://docs.mongodb.com/manual/tutorial/enable-authentication/)
