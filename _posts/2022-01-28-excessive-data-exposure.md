---
title: OWASP API Security Excessive Data Exposure
author: Eno
date: 2022-01-28 00:00:00 +0000
image: /assets/img/blogging/owasp.jpg
categories: [Blogging, Tutorial, Excessive Data Exposure]
tags: [OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Grapql API, Excessive Data Exposure, API Security]
---

Anda mungkin pernah mendengar tentang <kbd>Top 10 OWASP</kbd> atau sepuluh kerentanan teratas yang mengancam `Webapps`. OWASP juga secara berkala memilih daftar sepuluh besar kerentanan yang mengancam <kbd>API</kbd>, yang disebut <kbd>OWASP API Security Top 10</kbd>. Sepuluh besar API saat ini adalah :

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

Banyak dari kerentanan ini mempengaruhi komponen aplikasi selain `API`, tetapi mereka cenderung memanifestasikan dirinya dalam API. Kali ini, mari kita selami kerentanan di `API: OWASP API #3`, **Excessive Data Exposure**.

Mengapa paparan data yang berlebihan merupakan kerentanan <kbd>API</kbd>? Karena saya menyadari bahwa saya telah mencarinya sepanjang waktu untuk mencari bug dan tanpa menyadari bahwa itu adalah salah satu kerentanan teratas yang memengaruhi API! mari kita bicara tentang kerentanan ini, bagaimana saya biasanya mencarinya, dan bagaimana kamu dapat mencegahnya.

![Desktop View](/assets/img/blogging/owasp.jpg)

## OWASP API Security #3 Excessive Data Exposure
Apa itu OWASP API Security #3, **Excessive Data Exposure**? Saat itulah aplikasi mengungkapkan lebih banyak informasi dari yang diperlukan kepada user melalui respons <kbd>API</kbd>.

Mari kita pertimbangkan kasus penggunaan API yang sederhana. Aplikasi web mengambil informasi menggunakan layanan API, kemudian menggunakan informasi tersebut untuk mengisi halaman web dan ditampilkan ke browser user.

```
displays data           requests data
user <----------------- application -------------------> API service
(browser)               (API client) 
```

Untuk banyak layanan API, aplikasi <kbd>API client</kbd>. tidak memiliki kemampuan untuk memilih bidang data mana yang dikembalikan dalam panggilan API. Katakanlah sebuah aplikasi mengambil informasi user dari API untuk mengisi profil user. Panggilan API untuk mengambil informasi user terlihat seperti ini:

```
https://api.example.com/v1.1/users/show?user_id=12
```

Server API akan merespons dengan seluruh objek user yang sesuai:

```
{ 
  "id": 6253282, 
  "username": "Omaigot", 
  "screen_name": "darksec", 
  "location": "Blk 335 Smith Street", 
  "bio": "Hacker. .", 
  "api_token": "8a48c14b04d94d81ca484e8f32daf6dc", 
  "phone_number": "123-456-7890", 
  "address": "Blk 335 Smith Street, SG" 
}

```

Kamu melihat bahwa selain informasi dasar tentang user, panggilan API ini juga mengembalikan `token API`, `nomor telepon`, dan `alamat user` tersebut. Karena panggilan ini digunakan untuk mengambil data untuk mengisi halaman profil user, aplikasi hanya perlu mengirimkan username, screen_name, location, dan bio ke browser.

Beberapa pengembang aplikasi berasumsi bahwa jika mereka tidak menampilkan informasi sensitif di halaman web, user tidak dapat melihatnya. Jadi mereka pada gilirannya mengirim seluruh respons API ini ke browser user tanpa menyaring informasi sensitif terlebih dahulu dan mengandalkan code dari sisi client untuk menyaring informasi pribadi. Ketika ini terjadi, siapa pun yang mengunjungi halaman profil akan dapat mencegat respons API ini dan membaca info sensitif tentang user itu!

Penyerang mungkin juga dapat membaca data sensitif dengan mengunjungi halaman tertentu yang membocorkan informasi atau melakukan serangan <kbd>MITM</kbd> untuk mencuri respons API yang dikirim ke korban.

## Mencagah excessive data exposure

Eksposur data yang berlebihan terjadi ketika aplikasi `cliet API` tidak memfilter hasil yang didapatnya sebelum mengembalikan data ke user aplikasi.

Saat API mengirim data yang sensitif, aplikasi client harus memfilter data sebelum meneruskannya ke user. Tentukan dengan cermat apa yang harus diketahui user dan pastikan untuk memfilter apa pun yang tidak boleh diakses oleh user. Idealnya, kembalikan jumlah minimum data yang diperlukan untuk merender halaman web.

Jika API mengizinkannya, Kamu juga dapat meminta jumlah minimum data yang diperlukan dari `server API`. Misalnya, `GraphQL API` memungkinkan kamu menentukan bidang objek persis yang kamu butuhkan dalam request API.

Terakhir, hindari pengiriman informasi sensitif dengan trafic yang tidak terenkripsi.

saya selalu memperhatikan kerentanan ini ketika saya mencari <kbd>bug</kbd>. Sebagai bug hunter dan penguji, saya terbiasa menangkap setiap respons server untuk kata kunci seperti <kbd>key</kbd>, <kbd>token</kbd>, dan <kbd>secret</kbd>. Dan lebih sering daripada tidak, saya menemukan kebocoran informasi sensitif dengan cara ini.

Sering kali, kebocoran info sensitif ini disebabkan oleh masalah yang saya jelaskan di sini: server terlalu mengembalikan seluruh `respons API` dari server API alih-alih memfilternya sebelum meneruskannya ke user.

Excessive Data Exposure, sayangnya, sangat umum. Dan ketika dikombinasikan dengan OWASP API #4, Lack of Resources & Rate Limiting, bisa menjadi masalah yang lebih besar.