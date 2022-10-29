---
title: Mengenal Email Security
author: Eno
date: 2022-01-14 00:00:00 +0700
image: /assets/img/blogging/Email_security.jpg
categories: [Blogging, 0x3n0, Email security]
tags: [Email, 2FA metadata, Protect, header, encrypt, private key, private key, PGP, session key]
---

Untuk melindungi akun dan data pelanggan dari penyerang, penyedia layanan email memiliki langkah-langkah perlindungan email. Langkah-langkah ini melibatkan server email dengan kerangka kerja yang kuat untuk kata sandi dan otentikasi, email yang aman (baik inbox maupun dalam perjalanan); firewall untuk aplikasi web; dan tools pendeteksi spam.

## Apa itu Email Security?

Sebagai platform untuk mengirimkan <kbd>virus</kbd>, <kbd>spam</kbd>, dan <kbd>phishing</kbd>, email menonjol di antara para penyerang. Untuk memanipulasi user agar mendapatkan informasi pribadi, Mereka menggoda user untuk mendaftarkan file atau mengklik `LINK` di komputer user yang memungkinkan untuk melakukan kejahatan (seperti malware email). Untuk ancaman, siapa pun yang ingin menembus arsitektur jaringan dan meretas informasi sensitif pelanggan, email sering kali menjadi titik masuk utama. Karakteristik keamanan E-mail seringkali fleksibel, dan sesuai dengan kebutuhan user

![img-description](/assets/img/blogging/Email_security.jpg)_Email Security_

### Fitur penyedia layanan email
Bukannya, semua layanan email terpercaya memang rahasia dan terlindungi. Beberapa alternatif gratis dapat menyebabkan kerusakan. Oleh karena itu, ia memenuhi beberapa atau sebagian besar persyaratan berikut saat mencari penyedia email yang dapat diandalkan:

Beberapa fitur yang paling umum dari penyedia layanan email:

#### End to end encryption

Tidak ada layanan email yang dapat menyebut dirinya aman tanpa <kbd>End-to-end encryption</kbd>. Pesan kamu hanya di codekan hingga masuk ke `Gmail` atau `yahoo` mail saat kamu menggunakan layanan standar. Jika End-to-end encryption digunakan, teks hanya dapat dibaca oleh pengirim dan penerima. End-to-end encryption yang paling populer untuk pesan yang dilindungi adalah yang disebut **Pretty Good Protection** atau <kbd>PGP</kbd> secara umum.

#### Two-factor authentication (2FA)

<kbd>Two-factor authentication</kbd> memberi kamu perlindungan lebih dan melindungi akun kamu jika ada yang mengetahui kata sandi kamu. kamu merasa lebih sulit untuk meretas inbox masuk kamu dengan memasukkan apa pun yang harus kamu miliki, seperti smartphone. Ada beberapa opsi 2FA, bervariasi dari Google dan SMS
lainnya hingga aplikasi authenticate.

#### Menghapus header dari metadata.

Setiap pesan mencakup data data atau <kbd>metadata</kbd>, seperti browser internet, dan bahkan penerima. Demi kerahasiaan pengirim dan penerima, penyedia email yang dilindungi menghapus metadata header.

#### Posisi server.

Banyak negara tidak ramah informasi pribadi. Beberapa bahkan memiliki peraturan untuk perlindungan data yang memungkinkan informasi pribadi kamu disimpan untuk waktu tertentu. Perwakilan dari <kbd>Five Eyes</kbd> atau biasa dikenal dengan `organisasi intelijen Five Eyes` berasal dari negara Amerika Serikat, Inggris, Kanada, dan Australia. Mereka bertukar informasi tentang indikator dan merupakan salah satu lokasi tersulit bagi penyedia email yang aman untuk mendaftar.

### Kebutuhan akan layanan email yang aman

Manfaat menggunakan layanan email yang dilindungi harus jelas bagi kamu. Jika kamu masih memiliki beberapa pertanyaan, meskipun, saat beralih ke `Gmail`, pastikan untuk memperhatikan pertimbangan berikut:

1. Protect email
Setelah pesan mengenai server mereka, Gmail, Hotmail, dan layanan populer lainnya tidak menyandikan informasi rahasia kamu. Ini berarti bahwa mereka dapat menerjemahkannya, membuat dan membaca lebih mudah bagi penyerang.

2. Metadata header hiding
Metadata header hiding tidak langsung menutupi header dengan metadata jika sistem email harian kamu mengotentikasi email kamu. Ini juga mencakup akun email, laptop, browser, dan jaringan kamu, serta penerima.

3. Jangan menjadi komoditas.
Jika email kamu bagus dan gratis untuk digunakan, mungkin ada beberapa kemungkinan bahwa kamu diperlakukan sebagai komoditas. Namun, sangat sedikit user yang menyadari bahwa `Gmail` terus-menerus mencari kata-kata di inbox dan menggunakannya untuk menampilkan iklan yang disesuaikan. Dengan menggunakan cara ini, kamu membantu `Google` untuk mendapatkan uang dari data kamu dengan bantuan Gmail.

4. Di tempat ramah informasi pribadi, simpan email kamu.
Amerika Serikat dan negara berbagi kemampuan kognitif mana pun dengan <kbd>Fourteen Eyes</kbd> suatu hari nanti akan ingin mengakses inbox kamu. Jika database vendor ada di salah satu negara tersebut, akan jauh lebih cepat untuk melakukannya daripada mendapatkan akses ke bunker nuklir Swiss mana pun.

Pada akhirnya, harap diingat bahwa sistem email sama terlindunginya dengan kata sandi yang kamu punya. Jika seseorang dapat meretas kata sandi kamu dalam beberapa menit, semua end-to-end autentikasi dan peraturan tanpa pencatatan akan diterapkan.

### dengan layanan email yang aman

End-to-end autentikasi adalah karakteristik yang membedakan dari pesan terenkripsi. bahwa tidak ada pilihan untuk layanan atau pihak ketiga untuk memecahkan code pesan kamu, yang hanya dapat di peroleh oleh penerima. Di konter, pesan kamu dapat dibaca oleh penyedia layanan email standar seperti Google (mereka sudah menyaring email untuk kata-kata!) dan membuatnya lebih mudah didapat oleh penyerang.

Untuk perlindungan, <kbd>Pretty Good Privacy</kbd> (PGP) dan  <kbd>Secure/multipurpose internet mail extension</kbd> (S/MIME) adalah opsi yang paling menonjol. PGP menggabungkan perlindungan simetris dan asimetris, sedangkan S/MIME memberikan sertifikat yang harus disetujui oleh otoritas sertifikasi di tingkat regional atau publik. Memanfaatkan sertifikat menjamin bahwa kamu adalah penyedia pesan dan tidak diganggu oleh orang lain.

Karena enkripsi, baik pelaku maupun pemerintah, seperti akun email, tidak akan mengintip komunikasi atau metadata kamu.

### Tingkat Enkripsi

Di sini, kita telah membahas beberapa jenis tingkat enkripsi yang digunakan untuk mengamankan email.

- Enkripsi tingkat transportasi

Otentikasi tingkat transportasi menjamin bahwa email kamu bergerak dengan aman di seluruh jaringan, seperti yang telah dibahas sebelumnya. Lagi pula, penyedia akan melihat edisi yang tidak terenkripsi setelah muncul di server mereka, itu tidak akan cukup untuk memungkinkan transmisi email yang aman. Meskipun yang terakhir masih digunakan, keamanan lapisan Transport, adalah mitra dari lapisan socket Aman. Ini diconfigurasi untuk mengenkripsi email <kbd>IMAP, SMTP</kbd> serta protokol lain, seperti HTTP <kbd>Hyper-text transfer protocol</kbd>
atau FTP <kbd>File transfer protocol</kbd>, di atas TCP (Transmission Control Protocol). Sayangnya, itu masih belum termasuk dalam semua sistem email. Untuk user yang sering, mungkin tidak jelas karena tidak ada kemampuan untuk menentukan kapan enkripsi tingkat transportasi berlaku saat menggunakan email, tidak seperti browser internet yang menampilkan kunci hijau atau ikon yang setara.

- End to end encrypt

End-to-end encryption berarti bahwa teks kamu tidak dapat didekripsi baik oleh penyedia layanan email maupun pihak ketiga lainnya. Hanya pengirim dan penerima yang berisi public key dan privat yang diperlukan untuk membukanya.

- cara Kerja end-to-end encrypt

kamu menyandikan teks dengan `public key` dengan pacar kamu. Sekarang, hanya dapat di decodekan dengan `private key` dengan pacar kamu. Sebelum mengenai pacar kamu, data kamu yang disandikan melewati server. Dia menggunakan private key untuk memecahkan code pesan kamu sebagai gantinya.

- PGP email encrypt

User tidak perlu membagikan private key; Otentikasi email PGP menggabungkan algoritma hashing, enkripsi simetris dan otentikasi public key. Di balik ini, sistem email yang melakukannya, jadi kamu tidak perlu memikirkan pro dan kontra.

- Bagaimana PGP bekerja

Tepat setelah `session key` dibuat oleh protokol Privasi, penerima mengcodekannya. Pengirim memberikan session key yang disandikan dan didekripsi dengan private keynya oleh penerima.

Pada akhirnya, session key yang tidak dienkripsi digunakan oleh penerima untuk membaca email.
