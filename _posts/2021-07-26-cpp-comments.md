---
title: C++ Comments
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, C++ Comments]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, Comments, Single Line, Multi line, Debugging]
---

![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang komentar C++, mengapa kita menggunakannya, dan bagaimana menggunakannya dengan bantuan contoh.

Comment C++ adalah petunjuk yang dapat ditambahkan oleh programmer untuk membuat code mereka lebih mudah dibaca dan dipahami. Comment diabaikan oleh compiler C++.

Ada dua cara untuk menambahkan comment ke code:

- `//` -comment Baris Tunggal

- `/* */` -comment Multi-baris

## Comment Satu Baris
Di C++, setiap baris yang dimulai dengan Comment `//` adalah Sebagai contoh,

```cpp
// deklarasikan sebuah variable
int a;

// inisialisasi variable 'a' dengan nilai 2
a = 2;
```

Di sini, kita telah menggunakan dua Comment satu baris:

- `//` deklarasikan sebuah variable
-  `//` inisialisasi variable 'a' dengan nilai 2

kita juga dapat menggunakan Comment satu baris seperti ini:

```cpp
int a;    // deklarasikan sebuah variable
```

## Comment multi-baris
Di C++, setiap baris antara `/*` dan `*/` juga merupakan Comment. Sebagai contoh,

```cpp
/* deklarasikan variable
untuk menyimpan gaji karyawan
*/
int gaji = 2000;
```

Syntax ini dapat digunakan untuk menulis Comment satu baris dan multi-baris.

## Menggunakan Comment untuk Debugging

Comment juga dapat digunakan untuk menonaktifkan code agar tidak dieksekusi. Sebagai contoh,

```cpp
#include <iostream>
using namespace std;
int main() {
   cout << "beberapa code";
   cout << ''kesalahan code;
   cout << "code lainnya";

   return 0;
}
```

Jika kita mendapatkan kesalahan saat menjalankan program, alih-alih menghapus code yang rawan kesalahan, kita dapat menggunakan comment untuk menonaktifkannya agar tidak dieksekusi; ini bisa menjadi alat debugging yang berharga.

```cpp
#include <iostream>
using namespace std;
int main() {
   cout << "beberapa code";
   // cout << ''kesalahan code;
   cout << "code  lainnya";

   return 0;
}
```

## Mengapa menggunakan comment?
Jika kita menulis comment pada code kita, akan lebih mudah bagi kita untuk memahami code di tersebut. Selain itu, akan lebih mudah bagi teman developer Anda untuk memahami code tersebut.

> **Catatan: comment tidak boleh menjadi pengganti cara untuk menjelaskan code yang ditulis. Kita harus selalu menulis code yang terstructur dengan baik dan cukup jelas, kemudian gunakan comment.**

Sebagai aturan umum, gunakan comment untuk menjelaskan Mengapa Anda melakukan sesuatu daripada Bagaimana Anda melakukan sesuatu.
