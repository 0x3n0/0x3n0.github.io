---
title: Hacking Same-Origin Policy
author: Eno
date: 2022-02-04 00:00:00 +0700
categories: [Blogging, 0x3n0, Hacking Same-Origin Policy]
image: /assets/img/blogging/Same-Origin-Policy.jpeg
tags: [0x3n0, Same-Origin Policy, SOP, CSS, HTML, Javascript, attacker, Cross-origin resource sharing, CORS, Cross-domain messaging, postMessage, JSON with Padding, JSONP, Attacking, XSS, Exploiting, Hacking Same-Origin Policy]
---


Same-Origin Policy adalah salah satu pertahanan dasar yang digunakan dalam situs web. ini membatasi bagaimana script dari satu asal dapat berinteraksi dengan resource dari asal yang berbeda. Sangat penting dalam mencegah sejumlah kerentanan web umum.

Namun, karena SOP cukup ketat dan tidak fleksibel, sebagian besar situs web menggunakan metode SOP. Dan di sinilah sering terjadi kesalahan. Hari ini, kita akan membahas secara detail SOP, bagaimana pengaruhnya terhadap situs web, dan bagaimana attacker mengeksploitasi fitur SOP.

![img-description](/assets/img/blogging/Same-Origin-Policy.jpeg)_Same-Origin Policy_

## Apa itu Same-Origin Policy (SOP)?

Dalam satu kalimat, Same-Origin Policy adalah sebagai berikut: script dari halaman A hanya dapat mengakses data dari halaman B jika berasal dari same-origin.

### Siapa yang memiliki same-origin?

Dua URL dikatakan memiliki same-origin jika memiliki <kbd>protocol</kbd>, nama <kbd>host</kbd>, dan <kbd>port</kbd> yang sama. Katakanlah halaman A ada di

```
[https://0x.3n0.us/](HTTPS pada port 443 secara default)
```
Manakah dari halaman berikut ini yang merupakan "same-origin" menurut Same-Origin Policy?

```
https://0x.3n0.us/ (same origin, same protocol, hostname & port)
https://0x.3n0.us/ (different origin, because protocol differs)
https://0x.3n0.us/(different origin, because hostname differs)
https://0x.3n0.us/:8080/0x3n0 (different origin, because port number differs)
```

### Apa yang membatasi SOP?

SOP tidak mengizinkan script dari halaman `A` mengakses data di halaman `B` jika tidak memiliki <kbd>same-origin</kbd>. Ini dimaksudkan untuk mencegah script berbahaya di halaman A mendapatkan informasi sensitif yang disematkan di DOM halaman B.

> **Catatan tambahan**: SOP membatasi akses data saja. resource yang disematkan seperti gambar, CSS, dan script tidak dibatasi dan dapat diakses serta dimuat di berbagai sumber.

situs web sering mendasarkan authenticationnya pada `cookie HTTP`, dan server mengambil tindakan berdasarkan cookie yang disertakan secara otomatis oleh browser. Hal ini membuat SOP sangat penting.

Bayangkan jika kamu masuk ke `onlinebank.com`, dan pada saat yang sama, kamu mengunjungi `attacker.com` di browser yang sama. Jika SOP tidak ada, script yang dihosting di attacker.com bebas mengakses informasi kamu di onlinebank.com , karena browser kamu akan secara otomatis menyertakan cookie onlinebank.com kamu di setiap permintaan yang kamu kirim ke onlinebank.com (Bahkan jika request yang berbahaya menghasilkan dari script yang dihosting di attacker.com ).

attacker.com dapat melakukan sesuatu seperti ini:

1. request <kbd>GET</kbd> ke onlinebank.com/personal_info menggunakan script. (Karena kamu login ke onlinebank.com, server dapat mengirim kembali halaman HTML yang berisi halaman info pribadi kamu.)

2. Terima dan parsing halaman HTML yang dikembalikan.

3. Ambil token <kbd>CSRF</kbd>, alamat email pribadi, alamat, dan informasi perbankan yang diuraikan dari halaman.

Di sinilah SOP berperan: SOP akan mencegah script berbahaya yang dihosting di attacker.com untuk membaca data HTML yang dikembalikan dari onlinebank.com.

## Melonggarkan SOP

Secara praktis, <kbd>SOP</kbd> seringkali terlalu membatasi untuk situs web. Misalnya, beberapa subdomain atau beberapa domain dari situs web besar yang sama tidak akan dapat berbagi informasi satu sama lain. Untuk mengatasi masalah ini, banyak cara untuk mengatasi SOP.

### Mengatur dokumen.domain

Menyetel domain dari subdomain yang berbeda menggunakan `document.domain` akan memungkinkan untuk berbagi resource. Misalnya setting domain dari a.domain.com dan b.domain.com menjadi `domain.com` agar bisa saling berinteraksi.

> **Catatan tambahan**: Melakukan ini akan menyetel port ke nol, yang mungkin ditafsirkan secara berbeda oleh browser yang berbeda. Dalam contoh di atas, https://a.domain.com mungkin tidak dapat berinteraksi dengan `https://domain.com` karena portnya berbeda (Null vs 443).

### Cross-origin resource sharing (CORS)

kamu juga dapat menggunakan <kbd>Cross-Origin resource sharing</kbd> (CORS) untuk melonggarkan SOP. CORS melindungi data dari server yang diminta. Ini memungkinkan server untuk secara eksplisit menentukan daftar origin yang diizinkan melalui header `Access-Control-Allow-Origin`. asal halaman yang mengirimkan request kemudian diperiksa dengan list origin yang diizinkan ini.

### Cross-domain messages (postMessage)

<kbd>PostMessage</kbd> adalah cara untuk mengatasi SOP. Teknik ini memungkinkan halaman untuk mengirim pesan berbasis teks ke halaman lain dengan memanggil method postMessage() di jendela. Jendela penerima kemudian menangani pesan menggunakan event handler onmessage

Karena menggunakan postMessage mengharuskan pengirim untuk mendapatkan objek jendela penerima, pesan hanya dapat dikirim antara jendela dan `iframe` atau popupnya.

### JSON dengan Padding (JSONP)

<kbd>JSONP</kbd> adalah teknik lain yang bekerja di sekitar SOP. Ini juga memungkinkan pengirim untuk mengirim data JSON dalam fungsi panggilan balik yang dievaluasi sebagai JS. Kemudian script yang terletak di origin yang berbeda dapat membaca data JSON dengan memproses fungsinya.

Karena tag `<script>` HTML diizinkan untuk memuat code JS terlepas dari asalnya, cara mudah untuk berbagi data cross origin adalah dengan membuatnya sebagai bagian dari tag `<script>`. JSONP membungkus data JSON dalam fungsi panggilan balik agar data ditafsirkan sebagai code JS yang valid.

Misalnya, katakanlah kita mencoba meneruskan JSON berikut ke seluruh origin:

```
// data located at https://0x.3n0.us/get_user_articles
{“username”: “eno”, “num_articles”: “39”}
```

Blok data ini tidak dapat dimuat secara langsung sebagai script karena dalam format JSON:

```
<script src=”https://0x.3n0.us/get_user_articles”></script>
```

Ini akan gagal karena `JSON` di atasnya bukan Javascript yang valid, dan kesalahan syntax JS akan muncul. JSONP mengatasi masalah ini dengan membungkus data dalam fungsi JS:

```
parse({“username”: eno, “num_articles”: “39”})
```

Halaman yang menerima data kemudian dapat mengekstrak data dari payload JSONP dengan memproses fungsinya.

Masalah dengan JSONP adalah bahwa situs `A` harus memercayai situs `B` sepenuhnya karena menyertakan Javascript arbitrary dari situs B. Sekarang `CORS` adalah opsi, JSONP lebih jarang digunakan.

## Attacking SOP

Selain bypass SOP yang dikendalikan dan dimaksudkan yang disebutkan di atas, ada cara yang dapat digunakan attacker untuk memanipulasi cross-source communication. Eksploitasi ini sering disebabkan oleh penerapan salah satu teknik relaxation SOP yang salah.

attacker yang dapat melewati SOP dan relaxation policy yang dimaksudkan oleh developer dapat menyebabkan kebocoran informasi pribadi dan sering kali menyebabkan lebih banyak kerentanan seperti bypass authentication, pengambilalihan akun.

Mari kita bicara tentang beberapa cara bagaimana attacker menggunakan teknik ini.

### XSS

<kbd>XSS</kbd> pada dasarnya adalah bypass SOP lengkap karena Javascript yang berjalan di halaman A akan beroperasi di bawah konteks keamanan halaman A. berarti bahwa jika attacker dapat mengeksekusi script di halaman korban, script tersebut dapat mengakses resource halaman dan data.

### Memanfaatkan CORS

CORS yang salah diconfigurasi adalah hal lain yang dapat dimanfaatkan attacker untuk mengacaukan <kbd>cross-origin communication</kbd>.

Salah satu kesalahan configurasi yang dapat dieksploitasi adalah ketika situs menggunakan regex yang lemah untuk memvalidasi origin. Misalnya, jika policy hanya memeriksa apakah URL origin dimulai dengan www.site.com, policy tersebut dapat diabaikan dengan menggunakan subdomain karakter pengganti. Jika attacker memiliki domain attacker.com, dia dapat mengaktifkan **entry wildcard** ke domainnya sendiri, sehingga <kbd>*.attacker.com</kbd> akan dialihkan ke attacker.com. kemudian dapat menggunakan <kbd>www.site.com.attacker.com</kbd> sebagai asal request untuk melewati SOP.

Kesalahan configurasi CORS umum lainnya yang dapat dieksploitasi adalah mengatur origin yang diizinkan ke NULL atau attacker.com. pada dasarnya tujuan SOP dan menghilangkan limit pada cross-source communication.

configurasi menarik yang tidak dapat dieksploitasi adalah mengatur origin yang diizinkan ke wildcard <kbd>*</kbd>. ini juga tidak dapat dieksploitasi karena `CORS` tidak mengizinkan credentials dikirim dengan request, sehingga tidak ada informasi pribadi yang dapat dibocorkan.

Kesalahan configurasi di CORS juga tidak dapat dieksploitasi ketika <kbd>header</kbd> khusus digunakan untuk authentication, atau ketika ada `key random` dan tidak dapat ditebak ditempatkan dalam request atau URI.

### Mengeksploitasi postMessage

Saat menggunakan <kbd>postMessage</kbd>, pengirim dan penerima pesan harus memverifikasi `origin` dari pihak lain. Kerentanan terjadi ketika halaman melakukan pemeriksaan origin yang buruk (regex lemah, misalnya), atau sama sekali tidak memiliki pemeriksaan origin.

Jika halaman pengirim tidak menerapkan **targetOrigin** penerima atau menggunakan wildcard targetOrigin, informasi dapat bocor ke situs lain menggunakan postMessage. (TargetOrigin dapat ditentukan dalam fungsi postMessage sebagai parameter.)

Untuk mengeksploitasi masalah ini, attacker dapat membuat halaman HTML sedang listen yang berasal dari halaman yang rentan. kemudian dapat mengelabui korban untuk memicu `postMessage` menggunakan link atau gambar palsu dan membuat halaman korban mengirim data ke halaman attacker.

Di sisi lain, jika penerima pesan tidak memvalidasi dari mana postMessage berasal, attacker dapat mengirim data sewenang-wenang ke situs web dan memicu tindakan yang tidak diinginkan atas nama korban.

Untuk melakukan itu, attacker dapat menyematkan atau membuka halaman korban di halaman HTML untuk mendapatkan referensinya. Kemudian, dia bebas mengirim pesan pos. Ketika halaman HTML ini diakses oleh korban, postMessage yang akan mengirim credentials korban.

Terima kasih sudah membaca.
