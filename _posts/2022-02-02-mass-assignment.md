---
title: OWASP API Security Mass Assignment
author: Eno
date: 2022-02-02 00:00:00 +0700
image: /assets/img/blogging/Mass-Assignment.jpg
categories: [Blogging, Tutorial, Mass Assignment]
tags: [0x3n0, OWASP API, OWASP API Security Top 10, post, get, put, delete, server API, CLient API, Graphql API, jwt, Broken User Authentication, OWASP API Security, Mass Assignment]
---

![img-description](/assets/img/blogging/Mass-Assignment.jpg)_API OWASP Security_

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

Kerentanan yang akan kita bicarakan adalah <kbd>OWASP API Security Top 10</kbd>, **Mass Assignment**. (_Penugasan massal_) mengacu pada praktik pemberian nilai ke beberapa variabel atau properti objek sekaligus. Tetapi bagaimana fitur ini dapat menyebabkan kerentanan keamanan? Mari kita mulai dengan melihat contoh objek.

## OWASP API Security Properti object

Objek aplikasi seringkali memiliki banyak properti yang menggambarkan objek tersebut. Misalnya, katakanlah objek `user` digunakan untuk menyimpan informasi user di aplikasi kamu. objek ini berisi properti yang menggambarkan user seperti <kbd>ID user</kbd>, <kbd>name</kbd>, <kbd>location</kbd>, dan sebagainya.

```
{ 
  "id": 1337, 
  "name": "eno", 
  "location": "Blk 335 Smith Street, SG", 
  "admin": false, 
  "group_membership": [121, 322, 457] 
}
```
Dalam hal ini, user harus dapat memodifikasi beberapa properti yang disimpan di objek mereka, seperti properti `location` dan `name`. Tetapi bagian lain dari objek user ini harus dibatasi dari user, seperti properti `admin`, yang menunjukkan apakah user adalah admin, dan properti `group_membership`, yang mencatat grup user mana yang menjadi anggotanya.

## OWASP API Security Mass Assignment

Mass Assignment adalah kerentanan di mana catatan aktif dalam sebuah website disalahgunakan untuk mengubah item data yang biasanya tidak boleh diakses oleh <kbd>user</kbd> seperti <kbd>password</kbd>, <kbd>permission</kbd>, atau status <kbd>admin</kbd>.

Kerentanan Mass Assignment terjadi ketika aplikasi secara otomatis memberikan input user ke beberapa variabel atau objek program. Ini adalah fitur dalam banyak framework aplikasi yang dirancang untuk menyederhanakan pengembangan aplikasi.

Namun fitur ini terkadang memungkinkan penyerang untuk menimpa, memodifikasi, atau membuat variabel program atau properti objek baru sesuka hati. Misalnya, katakanlah situs mengizinkan user untuk mengubah nama mereka melalui request PUT seperti ini. request ini akan memperbarui name user <kbd>1337</kbd> dari <kbd>eno</kbd> menjadi <kbd>enogans</kbd>.

### Contoh OWASP API Security #1 Mass Assignment

```
PUT /api/v1.1/user/1337
{ 
  "name": "eno" 
}
```
Sekarang, bagaimana jika user mengirimkan request ini?

```
PUT /api/v1.1/user/1337
{ 
  "name": "enogans", 
  "admin": true 
}
```
Jika aplikasi menggunakan Mass Assignment untuk memperbarui properti objek user secara otomatis, request ini juga akan mengupdate bidang `admin`, dan memberikan hak admin kepada user `1337`. Seperti inilah kerentanan Mass Assignment. Demikian pula, user mungkin dapat menambahkan  sendiri ke grup user pribadi dengan menetapkan diri mereka sendiri ke grup baru.

### Contoh OWASP API Security #2 Mass Assignment

```
PUT /api/v1.1/user/1337
{ 
  "name": "eno", 
  "admin": true, 
  "group_membership": [1, 35, 121, 322, 457] 
}
```
## Cara Mencegah Mass Assignment

Untuk cara mencegah Mass Assignment, kamu dapat menonaktifkan fitur Mass Assignment dengan framework yang kamu gunakan, atau menggunakan daftar putih untuk mengizinkan pada properti atau variabel tertentu.
