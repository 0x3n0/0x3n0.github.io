---
title: OWASP API Security Broken Object Level Authorization
author: Eno
date: 2022-02-03 00:00:00 +0700
image: /assets/img/blogging/API_Security.jpg
categories: [Blogging, Tutorial, Broken Object Level Authorization]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, Broken Object Level Authorization, OWASP API Security]
---


Saat aplikasi modern menjadi lebih kompleks, mereka semakin dibangun menggunakan API. Terlebih lagi, API memiliki kemampuan untuk melakukan tindakan penting atau mengomunikasikan informasi sensitif. Ini menjadikan bug API sebagai sumber keamanan dan kebocoran data yang tersebar luas. Itu berarti ada baiknya memahami API, kerentanan yang termanifestasi di dalamnya, dan cara bertahan dari kerentanan ini.

## OWASP API Security Broken Object Level Authorization

Kamu mungkin pernah mendengar tentang <kbd>Top 10 OWASP</kbd> atau sepuluh kerentanan teratas yang mengancam aplikasi web. OWASP juga secara berkala memilih daftar sepuluh besar kerentanan yang mengancam API, yang disebut **`OWASP API Security Top 10`**. <kbd>API</kbd> teratas saat ini adalah 

- Broken Object Level Authorization
- Broken User Authentication
- Excessive Data Exposure
- Lack of Resources & Rate Limiting
- Broken Function Level Authorization
- Mass Assignment
- Security Misconfiguration
- Injection
- Improper Asset Management
- Insufficient Logging & Monitoring.

Banyak dari kerentanan ini mempengaruhi komponen aplikasi selain <kbd>API</kbd>, tetapi mereka cenderung memanifestasikan dirinya dalam `API`. mari kita bicara tentang kerentanan `OWASP API Security #1`, **Broken Object Level Authorization**.

![Desktop View](/assets/img/blogging/API_Security.jpg)_API Security Object Level Authorization_

### OWASP API Security Broken Object Level Authorization Vulnerability

API sering kali mengekspos pengidentifikasi objek yang digunakan untuk mengakses resource. Dan ketika akses kontrol tidak diterapkan dengan benar, penyerang dapat melihat atau mengoperasikan resource yang seharusnya tidak mereka akses. Kerentanan ini memengaruhi semua jenis arsitektur <kbd>API</kbd>, termasuk <kbd>SOAP</kbd>, <kbd>REST</kbd>, dan <kbd>GraphQL</kbd>.

Mari kita lihat sebuah contoh! Katakanlah bahwa `API` memungkinkan `user` untuk mengambil detail tentang metode pembayaran mereka berdasarkan `ID` user mereka:

```
https://api.contoh.com/v1.1/users/payment/show?user_id=12
```
Di sini, jika aplikasi tidak memerlukan bukti identitas tambahan dalam <kbd>API</kbd> dan hanya mengembalikan data yang diminta kepada siapa pun, aplikasi akan memaparkan informasi sensitif kepada penyerang. Penyerang dapat menebak, membocorkan, atau memaksa ID korban dan mencuri informasi pembayaran mereka melalui <kbd>API</kbd>.

Seringkali, aplikasi mengizinkan user untuk mengakses objek data berdasarkan <kbd>ID</kbd> objek, bukan ID user mereka. <kbd>contoh.com</kbd> juga memiliki <kbd>API</kbd> yang memungkinkan pengguna mengambil konten pesan pribadi mereka. Pesan direferensikan menggunakan `ID` numerik:

```
https://api.contoh.com/v1.1/messages/show?id=1337
```

Jika server tidak menerapkan akses kontrol, penyerang dapat memaksa <kbd>ID</kbd> numerik ini dan mengambil pesan user lain!

kerentanan ini adalah contoh **Broken Object Level Authorization.**. Tidak ada pemeriksaan identitas sebelum user mengakses objek data individual. Server tidak memverifikasi apakah Anda adalah user yang sah. Itu hanya mengembalikan informasi, seperti yang Anda minta.

Selain yang membaca objek data, masalah ini juga dapat memengaruhi <kbd>API</kbd> yang `memperbarui`, `menghapus`, atau membuat `entri data`. Misalnya, masalah umum dalam implementasi <kbd>GraphQL</kbd> adalah bahwa API mengizinkan user yang tidak sah untuk mengedit data dengan mengganti `ID` dalam request.

Apa yang bisa salah?

Dampak dari **Broken Object-Level Access** tergantung pada objek data yang diekspos. Jika objek penting seperti `PII` dan kredensial user terekspos, <kbd>bug</kbd> dapat menyebabkan penyalhgunaan data atau kompromi aplikasi.

Kerentanan ini dapat dieksploitasi lebih dalam: penyerang dapat menulis skrip untuk menanyakan semua `ID` user dan mengikis data secara otomatis. Jika kerentanan ini terjadi di situs **Ecommerce**, penyerang mungkin dapat mengambil jutaan rekening bank, nomor kartu kredit, dan alamat. Jika kerentanan ini ditemukan di situs perbankan, penyerang dapat membocorkan informasi kredit dan formulir pajak semua orang!

## Bagaimana cara mencegahnya ?

Cara ideal untuk mencegah masalah **broken object level authorization vulnerability** adalah menyimpulkan identitas user <kbd>API</kbd> dari akses token atau bentuk rahasia lainnya. Kemudian, terapkan akses kontrol pada semua <kbd>API sensitif</kbd> yang memerlukan beberapa hak akses, ingat bahwa setiap API dan metode request perlu diaudit dengan benar. Misalnya, saya sering melihat implementasi API di mana hanya mengubah ke metode request yang berbeda akan melewati kontrol.

Jika tidak memungkinkan, objek data dengan nilai acak alih-alih <kbd>ID</kbd> numerik sederhana. Namun, hanya menggunakan `ID` acak tidak dapat dianggap sebagai perlindungan menyeluruh karena ID dapat bocor atau dicuri. Katakanlah API tidak dibatasi oleh akses kontrol:

```
https://api.contoh.com/v1.1/messages/show?id= d0c240ea139206019f692d
```

Meskipun sulit untuk menebak ID yang digunakan untuk mereferensikan pesan, penyerang mungkin dapat mencuri atau membocorkan ID. ID ini mungkin juga tersedia untuk ekstensi browser dan riwayat penjelajahan.

Mencegah `Object Level Authorization` harus menjadi prioritas utama kamu sebagai developer. Tetapi bahkan API dengan `Object Level Authorization` yang tepat dapat rentan terhadap serangan. Menerapkan mekanisme otentikasi yang tepat untuk layanan API juga bisa rumit.
