---
title: OWASP API Security Lack of Resources & Rate Limiting
author: Eno
date: 2022-02-01 00:00:00 +0700
image: /assets/img/blogging/Lack-of-Resources-&-Rate-Limiting.jpg
categories: [Blogging, 0x3n0, Lack of Resources & Rate Limiting]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Grapql API, jwt, Broken User Authentication, Lack of Resources & Rate Limiting, OWASP API Security]
---

![img-description](/assets/img/blogging/Lack-of-Resources-&-Rate-Limiting.jpg)_API SECURITY 101 Lack of Resources & Rate Limiting_

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

Banyak dari kerentanan ini mempengaruhi komponen aplikasi selain <kbd>API</kbd>, tetapi mereka cenderung memanifestasikan dirinya dalam `API`. mari kita bicara tentang kerentanan `OWASP API Secururity #4`, **Lack of Resources & Rate Limiting.**.

### OWASP API Security Lack of Resources & Rate Limiting

OWASP API Security Lack of Resources & Rate Limiting adalah ketika <kbd>API</kbd> tidak membatasi jumlah atau frekuensi request dari client `API` tertentu. Jadi client API dapat membuat ribuan atau bahkan lebih panggilan API per detik, atau meminta ratusan atau ribuan catatan data sekaligus, dan server akan tetap berusaha memenuhi request.

terdengar cukup menarik? Dalam banyak kasus, kurangnya resource dan Limit bukanlah masalah. Tapi terkadang, bisa membiarkan penyerang melakukan sesuatu yang lebih.

### kenapa Lack of Resources & Rate Limiting menjadi masalah?

Pertama-tama, kurangnya pembatasan kecepatan dapat memengaruhi kinerja <kbd>server API</kbd> dan memungkinkan penyerang melakukan serangan DoS. Ketika satu client atau beberapa client terlalu banyak request sekaligus, request dari client tersebut dapat membebani kemampuan server untuk memproses request dan menjadi lambat atau tidak tersedia untuk user lain.

Masalah lainnya adalah kurangnya pembatasan kecepatan dapat menyebabkan serangan paksa otentikasi dan dengan <kbd>Broken Object Level Authorization</kbd>. Misalnya, jika tidak ada batasan berapa kali user dapat mengirimkan request masuk, penyerang dapat memaksa kata sandi user dengan mencoba masuk dengan kata sandi yang berbeda hingga berhasil. 

Di sisi lain, jika aplikasi <kbd>Object Level Authorization</kbd>, penyerang dapat menggunakan yang tidak membatasi kecepatan untuk memaksa `ID` yang mengarah ke data sensitif.

Terakhir, kurangnya pembatasan kecepatan dapat membantu penyerang mengekstrak data sensitif lebih cepat jika <kbd>API</kbd> membocorkan informasi. Misalnya, digunakan untuk mengambil email user dan tidak dibatasi oleh akses kontrol. ini akan mengembalikan 20 konten email:

### Contoh OWASP API Security Injection Lack of Resources & Rate Limiting

```
https://api.example.com/v1.1/emails/view?user_id=123&entries=20
```

dia akan mengembalikan 5000, memungkinkan penyerang membaca semua email user dalam satu panggilan API:

```
https://api.example.com/v1.1/profile/email/view?user_id=1337
```

Penyerang menjalankan sejumlah besar request `API` untuk memanenkan alamat email user:

```
https://api.example.com/v1.1/profile/email/view?user_id=1337 
https://api.example.com/v1.1/profile/email/view?user_id=124 
https:// api.example.com/v1.1/profile/email/view?user_id=125 
=============
https://api.example.com/v1.1/profile/email/view?user_id= 2345
```

### Mencegah masalah Lack of Resources & Rate Limiting

Jadi bagaimana kamu bisa mencegah masalah ini? 
kamu perlu membatasi akses user ke resource! Tapi itu lebih mudah diucapkan daripada dilakukan.

Tingkat yang sesuai dan batas resource untuk setiap fungsi seringkali harus berbeda. Misalnya, batas kecepatan untuk otentikasi harus jauh lebih rendah untuk mencegah serangan <kbd>brute-forcing</kbd>. Hal pertama yang dapat kamu lakukan adalah menentukan apa itu "penggunaan normal" untuk fungsi tertentu itu. Kemudian, blokir user yang meminta resource pada tingkat yang jauh lebih tinggi dari biasanya.

Menentukan resiko masalah Rate Limit adalah di mana kerentanan berada dalam konteks aplikasi. Lain kali, mari kita lihat masalah `API` lain yang juga berarti berbeda dalam konteks yang berbeda: `OWASP API Security #5`, [**Broken Function Level Authorization**](https://0x.3n0.us/Function-Level-Authorizationd), dan cara menentukan dampaknya pada aplikasi. Lain kali, mengapa kamu harus mengaudit fungsionalitas sensitif di `OWASP API` kamu terlebih dahulu.
