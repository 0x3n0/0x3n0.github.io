---
title: OWASP API Security Broken User Authentication
author: Eno
date: 2022-02-06 00:00:00 +0700
image: /assets/img/blogging/owasp1.jpg
categories: [Blogging, 0x3n0, Broken User Authentication]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Graphql API, JWT, Broken User Authentication, OWASP API Security, API Security]
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

Banyak dari kerentanan ini memengaruhi komponen aplikasi selain API, tetapi cenderung memanifestasikan dalam API. Terakhir kali, saya berbicara tentang salah satu kerentanan API yang paling umum: [**Broken Object Level Authorization.**](https://0x3n0.github.io/Object-Level-Authorization/)

![img-description](/assets/img/blogging/owasp1.jpg)_API Security_

## OWASP API Security Broken User Authentication

Dari pengalaman saya meretas <kbd>API</kbd>, saya yakin bahwa sebagian besar implementasi API mengalami setidaknya satu contoh **Broken Object Level Authorization**. Kali ini, mari kita bicara tentang `OWASP API #2`: **OWASP API Security Broken User Authentication.**

Otentikasi untuk <kbd>API</kbd>. Seringkali, meminta kredensial user atau menggunakan autentikasi multi-faktor tidak mungkin dilakukan selama panggilan API. Jadi otentikasi dalam sistem API sering diimplementasikan menggunakan akses token: token yang disematkan ke dalam panggilan API individual untuk mengautentikasi user. Jika otentikasi tidak diterapkan dengan benar, penyerang dapat mengeksploitasi kesalahan konfigurasi untuk menyamar sebagai orang lain.

## OWASP API Security tanpa otentikasi

Pertama-tama, <kbd>API</kbd> dapat kekurangan mekanisme otentikasi sama sekali. Terkadang, pengembang API berasumsi bahwa API hanya akan diakses oleh aplikasi resmi dan tidak akan ditemukan oleh orang lain. Jadi API tersedia bagi siapa saja yang mengetahui dan struktur query nya. Dalam hal ini, siapa pun bebas meminta data atau menjalankan tindakan melalui `API` jika mereka mengetahui struktur query nya.

## Implementasi otentikasi yang salah

API yang tidak memiliki autentikasi menjadi kurang umum. Sebagian besar waktu, **OWASP API Security Broken User Authentication** disebabkan oleh desain atau implementasi Broken User Authentication token yang salah.

Satu kesalahan umum adalah tidak menghasilkan akses token dengan benar. Pertama-tama, jika token pendek, sederhana, atau dapat diprediksi, penyerang mungkin dapat melakukan <kbd>brute force token</kbd>. Ini dapat terjadi ketika token dihasilkan dengan entropi yang tidak mencukupi atau berasal dari informasi user menggunakan enkripsi atau algoritma hashing yang lemah. Misalnya, apa yang salah dengan token API berikut?

```
access_token=RW5v==
```

Token hanyalah pengkodean <kbd>base64</kbd> dari nama user, "Eno"!

<kbd>API</kbd> yang tidak menggunakan string akses token sederhana juga bisa tidak aman. Misalnya, <kbd>JSON Web Tokens</kbd> (JWTs) juga dapat ditandatangani dengan tidak benar atau tidak ada tanda tangan sama sekali. Masalah ini sangat berbahaya jika token tidak aman digunakan untuk mengautentikasi `admin` atau orang lain dengan hak akses ke dalam API. Jika kamu tertarik untuk mempelajari lebih lanjut tentang potensi jebakan JWT, baca posting saya di sini: [**Token Web JSON**](https://0x3n0.github.io)

## Token berumur panjang

Bahkan jika token dihasilkan dengan benar, pembatalan token yang tidak tepat juga dapat menyebabkan masalah. Token berumur panjang adalah masalah keamanan besar di banyak implementasi API.

`Token API` harus kedaluwarsa secara berkala dan setelah tindakan sensitif seperti `logout`, perubahan sandi, pemulihan akun, dan penghapusan akun. Jika akses token tidak divalidasi dengan benar, penyerang dapat mempertahankan akses ke sistem tanpa batas waktu setelah mencuri token.

## Kebocoran token

Terkadang, pengembang mengirimkan akses token secara tidak aman, seperti di <kbd>URL</kbd> atau melalui trafic yang tidak terenkripsi.

Jika token dikirimkan melalui <kbd>URL</kbd>, siapa pun yang memiliki akses ke URL melalui ekstensi browser atau riwayat penelusuran dapat mencuri token tersebut.

```
https://api.example.com/v1.1/users/payment/show?user_id=1337&access_token=360f91d065e56a15a0d9a0b4e170967b
```

Dan jika token ditransmisikan melalui trafic yang tidak terenkripsi, penyerang dapat meluncurkan serangan Man in the Middle <kbd>MITM</kbd> untuk menyadap trafic korban dan mencuri `token API`.

## Mencegah Broken User Authentication

User Authentication sangat merusak API karena satu kesalahan dapat memungkinkan penyerang mengambil alih akun user, mengakses data dan fungsionalitas yang dibatasi.

Mencegah masalah ini membutuhkan pendekatan yang komprehensif. Pertama, Kamu perlu memastikan bahwa kamu menerapkan akses kontrol untuk semua data dan fungsi sensitif. Ini dibahas dalam posting blog terakhir saya tentang [**Broken Object Level Authorization**](hhttps://0x3n0.github.io/Object-Level-Authorization). Lagi pula, otentikasi sia-sia kecuali kamu menggunakannya untuk membatasi akses ke sistem!

Selanjutnya, pastikan `API token` kamu berupa string yang `panjang`, `acak`, dan `tidak dapat diprediksi`. Jika kamu menggunakan token yang berasal dari informasi user, gunakan algoritme yang kuat dan <kbd>secret key</kbd> untuk memastikan bahwa user tidak dapat memalsukan token mereka sendiri. Terakhir, jika API kamu menggunakan autentikasi berbasis tanda tangan seperti JWT, terapkan tanda tangan yang kuat pada token dan validasikan dengan benar.

Batalkan token secara berkala dan setelah tindakan seperti `logout`, `reset kata sandi`, `pemulihan akun`, dan `penghapusan akun`. Terakhir, perlakukan akses token sebagai key dan jangan pernah mengirimkannya dalam `URL` atau trafic yang tidak terenkripsi.

Broken User Authentication dapat menyebabkan insiden keamanan yang serius, jadi mencegahnya harus menjadi prioritas utama kamu sebagai pengembang. Lain kali, mari kita lihat sepuluh besar API OWASP #3, [**Excessive Data Exposure**](https://0x3n0.github.io/Excessive-Data-Exposure/), kerentanan yang paling sering saya temukan di API.
