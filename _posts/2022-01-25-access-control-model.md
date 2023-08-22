---
title: Teknik mengamankan Web dengan Access Control Model
author: Eno
date: 2022-01-25 00:00:00 +0700
categories: [Blogging, 0x3n0, Teknik Menyerang web aplikasi]
image: /assets/img/Access-Control-Model/Ascend_Media.gif
tags: [0x3n0, Access Control Models, Broken Access Control Model, Testing Broken Access control Models, Web Applications, users, Documents, logs, Reports]
---

<a href="https://twitter.com/0x3n0?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="large" data-show-count="false">Follow @Enogembok</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Sejauh ini kamu mungkin telah menemukan berbagai web aplikasi di mana kamu dapat mengundang anggota dengan akses terbatas ke informasi dalam organisasi. developer dapat membuat aplikasi atau layanan tersebut dengan menerapkan Access Control Model dalam aplikasi mereka.

![img-description](/assets/img/Access-Control-Model/Ascend_Media.gif)_Access Control Model_

## Apa itu Access Control Model

Access Control Model adalah untuk mengontrol akses user ke resource dan bagaimana mereka berinteraksi dengannya. Dalam konteks web aplikasi, Access Control Model digunakan untuk mengontrol akses user ke resource dan bagaimana mereka berinteraksi dengannya. Misalnya, jika user adalah administrator, dia mungkin diizinkan untuk mengakses semua resource dalam aplikasi. Namun, jika user adalah anggota, dia mungkin hanya diizinkan untuk mengakses resource yang sangat spesifik dalam aplikasi.

![img-description](/assets/img/Access-Control-Model/Access_Control_Model1.png)_Access Control Model_

Dalam contoh Access Control Model Berbasis Peran berikut, kamu dapat melihatnya memiliki 3 peran berbeda yang ditentukan dengan set izin berbeda yang ditetapkan untuk setiap peran, Misalnya, peran admin memiliki akses ke `All(users, Documents, logs, dan Reports)` dalam Organisasi tetapi manajer hanya memiliki akses `users`, `documents` dan `reports` saat karena peran user dibatasi lebih lanjut dan hanya diizinkan untuk mengakses users dan documents dalam organisasi.

Mari kita gali lebih dalam untuk mengetahui berbagai jenis Access Control Model yang diimplementasikan dalam aplikasi sehari-hari yang kita gunakan:

- **Role-Based access controls(RBAC)**: Model ini memberikan hak akses kepada user berdasarkan pekerjaan yang mereka lakukan dalam suatu organisasi. Dalam Access Control Model ini, administrator dapat menetapkan user ke satu atau beberapa peran sesuai dengan tugas kerja mereka. Setiap peran memungkinkan akses ke resource tertentu

- **Discretionary Access Control (DAC)**: Dalam jenis akses kontrol izin diberikan atau dibatasi berdasarkan kebijakan akses yang ditentukan oleh pemilik organisasi atau aset.

- **Mandatory Access Control (MAC)**: Model ini memungkinkan pengelompokan resource menurut model sensitivitas. Model ini terutama ditemukan di lingkungan militer atau pemerintah di mana dapat dipahami dalam kelompok-kelompok seperti confidential, secret, top-secret dll.

## Broken Access Control Model(rusak):

Seperti yang kita ketahui dengan baik akan fakta bahwa web aplikasi telah berkembang jauh lebih kompleks dan besar dalam hal penanganan dan pemrosesan informasi. jadi tidak diragukan lagi meningkatkan kompleksitas dalam implementasi Access Control Model yang aman dan sempurna dalam aplikasi ini.

Access Control Model yang memungkinkan user dengan permission terbatas dalam organisasi untuk mengakses informasi terbatas dalam organisasi itu dianggap rusak dan cacat. Dari situlah lahir istilah <kbd>Broken Access Control</kbd>. Dan apa pun yang rusak itu membuka jalan bagi <kbd>HACKER JAHAT</kbd> untuk mengeksploitasinya.

## Kesalahan yang terjadi

Kamu mungkin bertanya `masalah apa yang dapat muncul jika Access Control Model tidak diimplementasikan dengan benar` ? dan `apa dampaknya jika isu-isu tersebut dieksploitasi dalam skenario dunia nyata`? Jawabannya cukup sederhana, setiap kali model permission gagal mengimplementasikan dengan benar, kemungkinan eskalasi privilege muncul di dalam sistem dan tingkat serangan akan tergantung pada bagian mana dari sistem atau aplikasi yang terpengaruh atau terpapar. user/peran.

Sekarang, Kembali ke pertanyaan kami apa yang bisa salah saat menerapkan `Access Control Model`. Selama pengalaman saya, ada 3 kemungkinan berbeda:

- **Permission tidak diterapkan dengan Benar** Dalam kasus ini beberapa terpapar ke peran/user yang tidak sah tanpa Permission yang diperlukan diterapkan dengan benar pada mereka, Misalnya jika <kbd>/api/users</kbd> diperlukan Permission `read:users`, penyerang akan dapat menjelajah <kbd>/api/users</kbd> tanpa Permission `read:users`.
    
- **Permission X override Permission Y**: Dalam hal ini jika user diberikan Permission <kbd>read:users</kbd> untuk mengakses `/api/user` API Endpoint, dia juga secara otomatis diberikan akses ke <kbd>/api/reports</kbd> endpoint. Jadi, kita dapat mengatakan Permission `read:users` mengesampingkan `read:reports`.
    
- **Set of Permission override Permission X** : Dalam hal ini, jika user diberikan <kbd>read:users</kbd> dan Permission <kbd>read:reports</kbd> untuk mengakses `/api/user` dan `/api/reports` API, dia juga secara otomatis diberikan akses ke `/api/files`, Harap dicatat bahwa kombinasi random Permission mengarah ke masalah Permission di sini, Jadi dalam hal ini, kita dapat mengatakan kombinasi random dari Permission <kbd>read:W</kbd> <kbd>read:X</kbd> dan <kbd>read:Y</kbd> memungkinkan akses <kbd>read:Z<kbd> juga.

Sekarang, challage sebenarnya adalah membangun metodologi penetratin testing yang mencakup semua skenario ini dan memberi cakupan penuh dari model target. Untuk melakukan itu, kita merancang teknik yang berbeda untuk setiap jenis skenario yang dapat muncul dalam sistem. Yang akhirnya membawa kita ke teknik yang disebut berikut.

## testing Access Control Model yang Rusak

bagian favorit saya di mana saya akan memaparkan berbagai teknik dan strategi untuk menguji `Access Control Model` yang rusak dalam aplikasi. Dengan pengalaman selama beberapa tahun sebagai pentester dan menganalisis `BACM(broken access control models)`, kita telah menemukan beberapa teknik efektif untuk pentest Access Control Model.

Tiga teknik/pendekatan utama kami yang efektif adalah sebagai berikut:

- Forwards Approach
- PBackword Approach
- Mixed Approach
    
Untuk memahami pendekatan ini secara efektif, mari kita asumsikan kita sedang pentest ke web aplikasi (dengan menerapkan Access Control Model) yang memungkinkan kita sebagai `admin` mengundang `user` ke organisasi kita dengan Permission khusus. Permission digambarkan dalam gambar di bawah bersama dengan API yang dapat diakses. Harus jelas bahwa user dengan Permission saja akan dapat mengakses API terkait yang berdekatan dengannya. Jika dengan cara apa pun dia dapat mengakses API lain, Access Control Model akan dianggap rusak.
    
![img-description](/assets/img/Access-Control-Model/Access_Control_Model2.png)_Access Control Model_

Mari kita mulai :

### Forward Approach

Dalam strategi `Forward Approach`, user harus diundang hanya dengan satu permission (misalkan adalah permission berwarna hijau pertama) dan Kemudian user yang diundang dengan hanya satu permission akan mencoba mengakses semua API terbatas lainnya secara berurutan. Setelah menyelesaikan kasus penetest pertama, user harus diundang dengan permission ke-2 dan kemudian akan mencoba mengakses semua API terbatas lainnya secara berurutan dan seterusnya.

Beberapa kasus testing yang dihasilkan oleh Forward Approach seperti yang tercantum di bawah ini:

#### Contoh Forward Approach 1 :

Dalam kasus Forward Approach berikut, user diberikan permission `read:users` dalam model dan kemudian dia mencoba mengakses API yang dibatasi lainnya dalam model permission.

![img](/assets/img/Access-Control-Model/Access_Control_Model3.png)

#### Contoh Forward Approach 2 :

Dalam kasus Forward Approach berikut, user diberikan permission `write:users` dalam model dan kemudian dia mencoba mengakses API yang dibatasi lainnya dalam model permission.

![img](/assets/img/Access-Control-Model/Access_Control_Model4.png)

#### Contoh Forward Approach 3 :

Dalam kasus Forward Approach berikut, user diberikan permission `read:documents` dalam model dan kemudian dia mencoba mengakses API yang dibatasi lainnya dalam model permission.

![img](/assets/img/Access-Control-Model/Access_Control_Model5.png)

### Backword Approach:
    
Dalam Backword Approach, user harus diberikan semua permission dalam model kecuali satu permission dan kita akan mencoba mengakses API masing-masing dari permission tanpa permission.

#### Contoh Backword Approach 1 :

Dalam kasus Backword Approach berikut, user diberikan semua permission kecuali permission `read:user` dalam model dan kemudian ia mencoba mengakses informasi user dari <kbd>GET /api/users</kbd> seperti yang ditunjukkan pada gambar di bawah ini.

![img](/assets/img/Access-Control-Model/Access_Control_Model6.png)

#### Contoh Backword Approach 2 :

Dalam kasus Backword Approach berikut, user diberikan semua permission kecuali permission `write:users` dalam model dan kemudian ia mencoba untuk mengubah informasi user dari  titik <kbd>POST /api/users</kbd> yang tidak memiliki permission.

![img](/assets/img/Access-Control-Model/Access_Control_Model7.png)

### Mixed Approach
    
Dalam Mixed Approach, user harus diundang dengan serangkaian permission campuran dari daftar permission dan kemudian dia akan mencoba mengakses titik API terkait dari peran terbatas.

#### contoh Mixed Approach 1 :

Dalam kasus Mixed Approach berikut, user diberikan permission `read:users`, `write:docs`, `write:logs` kemudian semua titik API terbatas lainnya harus diuji terhadap permission campuran ini untuk memeriksa kontrol yang rusak.

![img](/assets/img/Access-Control-Model/Access_Control_Model8.png)

#### Contoh Mixed Approach 2 :

Dalam kasus Mixed Approach berikut user diberikan permission `write:docs`, `read:logs`, `write:logs` maka semua titik API yang dibatasi harus diuji terhadap permission ini seperti yang ditunjukkan pada gambar di bawah ini.

![img](/assets/img/Access-Control-Model/Access_Control_Model9.png)

## Penutup
Dalam hal ini, titik API harus memiliki penunjuk yang dapat berupa nama, id, atau Uid ketika direferensikan ke organisasi lain atau user dari organisasi lain mengarah ke `IDOR`. Oleh karena itu, semua IDOR adalah masalah Access control Tetapi semua masalah Access control bukan milik IDOR. .

Saya harap bisa membantu. Jika kamu memiliki pertanyaan, saran, atau permintaan, silakan hubungi kami melalui 
  
[0x3n0.github.io](mailto:0x3n0.github.io)

See you next time.
    

