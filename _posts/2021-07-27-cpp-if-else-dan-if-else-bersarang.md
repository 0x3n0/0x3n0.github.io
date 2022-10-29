---
title: C++ if else dan if else Bersarang
author: 0x3n0
date: 2021-07-27 00:00:00 +0000
categories: [Programming CPP, CPP Flow Control, C++ if else dan if else Bersarang]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, if Statement, condition, true_, false_, if else, if else Statement, else if, if else Bersarang, if Bersarang, inner, outer]
---

![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang Statement if else untuk membuat program pengambilan keputusan dengan bantuan contoh.

Dalam pemrograman komputer, kami menggunakan Statement `if` untuk menjalankan code block hanya ketika kondisi tertentu.

Misalnya, pemberian nilai (A, B, C) berdasarkan nilai yang diperoleh seorang siswa..

- jika persentasenya di atas **90**, berikan nilai **A**
- jika persentasenya di atas **75**, berikan nilai **B**
- jika persentasenya di atas **65**, berikan nilai **C**

Ada tiga bentuk Statement `if else` dalam C++.

- Statement `if` 
- Statement `if else`
- Statement `if else` `if else` 

## C++ if Statement
Syntax dari Statement `if` tersebut adalah:

```cpp
if (condition) {
   // body dari statement if
}
```

Statement `if` mengevaluasi dalam `condition` tanda kurung `( )`.

- Jika code `condition` mengevaluasi ke `true`, code di dalam body `if` di eksekusi.
- Jika code `condition` mengevaluasi ke `false`, code di dalam body `if` akan dilewati.

> **Catatan: code di dalam `{ }` adalah isi statement `if`**

![Desktop View](/assets/img/programming/CPP/cpp-condition.png)

### Contoh 1: C++ if Statement

```cpp
// Program untuk print integer positive yang dimasukkan oleh user
// Jika user memasukkan angka negative, akan dilewati

#include <iostream>
using namespace std;

int main() {
    int angka;

    cout << "Masukan sebuah integer: ";
    cin >> angka;

    if (angka > 0) {
        cout << "Anda memasukkan sebuah integer: " << angka << endl;
    }
    cout << "Statement ini selalu dieksekusi.";
    return 0;
}
```

Output 1

```cpp
Masukkan sebuah integer: 5
Anda memasukkan angka positive: 5
Statement ini selalu dieksekusi.
```

Ketika `5` user masuk, kondisi `angka > 0` dievaluasi `true` dan Statement di dalam body `if` di eksekusi.

Output 2

```cpp
Masukkan angka: -5
Statement ini selalu dieksekusi.
```

Ketika `-5` user masuk kondisi `angka > 0` dievaluasi `false` dan Statement di dalam body `if` tidak dieksekusi.

## C++ if else
Statement `if` dapat memiliki opsional else. Syntaxnya adalah:

```cpp
if (condition) {
    // block dari code if condition adalah true
}
else {
    // block dari code if condition adalah false
}
```

Statement `if..else` mengevaluasi `condition` dalam kurung.

![Desktop View](/assets/img/programming/CPP/cpp-if-else.png)

Jika code `condition` mengevaluasi `true`,

- code di dalam body `if` di eksekusi
- code di dalam body `else` dilwati dari eksekusi

Jika code `condition` mengevaluasi `false`,

- code di dalam body else dieksekusi
- code di dalam body if dilewati dari eksekusi

### Contoh 2: C++ Statement if else

```cpp
// Program untuk memeriksa apakah integer positive atau negative
// Program ini menganggap angka 0 positive

#include <iostream>
using namespace std;

int main() {
     int angka;

    cout << "Masukkan sebuah integer: ";
    cin >> angka;
    if (angka >= 0) {
        cout << "Anda memasukkan integer positive: " << angka << endl;
    }
    else {
        cout << "Anda memasukkan integer negative: " << angka << endl;
    }
    cout << "Baris ini selalu diprint.";
    return 0;
}
```

Output 1

```cpp
Masukkan sebuah integer: 4
Anda memasukkan integer positive: 4.
Baris ini selalu diprint.
```

Dalam program di atas, kita memiliki condition `angka >= 0`. Jika kita memasukkan angka yang lebih besar atau sama dengan `0`, maka condition dievaluasi `true`.

Di sini, kita masuk 4. Jadi, syaratnya adalah `true`. Oleh karena itu, Statement di dalam body `if` di eksekusi.

Output 2

```cpp
Masukkan integer: -4
Anda memasukkan integer negatif: -4.
Baris ini selalu diprint.
```

Di sini, kita masuk `-4`. Jadi, syaratnya adalah `false`. Oleh karena itu, Statement di dalam body `else` dieksekusi.

## C++ if else, else if Statement

Statement `if else`  digunakan untuk mengeksekusi block code antara dua alternatif. Namun, jika kita perlu membuat pilihan di antara lebih dari dua alternatif, kita menggunakan Statement `if else if else`.

Syntax dari `if else if else` Statement tersebut adalah:

```cpp
if (condition1) {
    // code block 1
}
else if (condition2){
    // code block 2
}
else {
    // code block 3
}
```

Di Sini,

- Jika `condition1` bernilai `true`, maka code `block 1` dieksekusi.
- Jika `condition1` bernilai `false`, maka `condition2` dievaluasi.
- Jika `condition2` adalah `true`, yang code `block 2` dijalankan.
- Jika `condition2` adalah `false`, yang code `block 3` dijalankan.

![Desktop View](/assets/img/programming/CPP/cpp-else-statement.png)

> **Catatan: Boleh lebih dari satu else if Statement tetapi hanya satu `if` dan Statement else.**

### Contoh 3: C++ if else, else if

```cpp
// Program untuk memeriksa apakah integer positif, negatif atau 0

#include <iostream>
using namespace std;

int main() {
     int angka;

    cout << "Masukkan sebuah integer: ";
    cin >> angka;
    if (angka > 0) {
        cout << "Anda memasukkan integer positive: " << angka << endl;
    } 
else if (angka < 0) {
      cout << "Anda memasukkan integer negative: " << angka << endl;
     } 
else {
        cout << "Anda memasukkan 0." << endl;
    }
     cout << "Baris ini selalu diprint.";
    return 0;
}
```

Output 1

```cpp
Masukkan sebuah integer: 1
Anda memasukkan integer positive: 1.
Baris ini selalu diprint.
```

Output 2

```cpp
Masukkan sebuah integer: -2
Anda memasukkan integer negative: -2.
Baris ini selalu diprint.
```

Output 3

```cpp
Masukkan sebuah integer: 0
Anda memasukkan 0.
Baris ini selalu diprint.
```

Dalam program ini, kita mengambil angka dari user. kemudian menggunakan `if else if else` untuk memeriksa apakah angkanya positive, negative, atau 0.

Jika jumlahnya lebih besar dari `0`, code di dalam block `if` dieksekusi. Jika jumlahnya kurang dari `0`, code di dalam block `else if` akan dieksekusi. Jika tidak, code di dalam block `else` akan dieksekusi.

## C++ if else Bersarang
Terkadang, kita perlu menggunakan Statement `if` di dalam Statement `if` lain . Ini dikenal sebagai if else Bersarang.

Anggap saja sebagai beberapa lapisan statement if Ada if Statement, dan di dalamnya ada if Statement lainnya . Syntaxnya adalah:

```cpp
// if statement luar
if (condition1) {
    // statement

    // if statement dalam
    if (condition2) {
        // statement
    }
}
```
> **Catatan:
Kita dapat menambahkan `else` dan `else if` Statement ke if Statement dalam sesuai kebutuhan.
Statement `if` dalam juga dapat disisipkan di dalam Statement luar `else` atau `else if` (jika ada).
Kita dapat membuat banyak lapisan statement if**

### Contoh 4: C++ if Bersarang

```cpp
// Program C++ untuk mengetahui apakah suatu sebuah integer adalah genap atau ganjil atau tidak keduanya (0)
// menggunakan statements if Bersarang

#include <iostream>
using namespace std;

int main() {
    int num;
    
    cout << "Masukan sebuah integer: ";  
     cin >> num;    

    // luar if condition
    if (num != 0) {
        
        // dalam if condition
        if ((num % 2) == 0) {
            cout << "Jumlahnya genap." << endl;
        }
         // bagian dalam else condition
        else {
            cout << "Nomornya ganjil." << endl;
        }  
    }
    // luar else condition
    else {
        cout << "Bilangannya 0 dan bukan genap maupun ganjil." << endl;
    }
    cout << "Baris ini selalu diprint." << endl;
}
```

Output 1

```cpp
Masukan sebuah integer: 34
Jumlahnya genap.
Baris ini selalu diprint.
```

Output 2

```cpp
Masukkan sebuah integer: 35
Jumlahnya ganjil.
Baris ini selalu diprint.
```

Output 3

```cpp
Masukkan sebuah integer: 0
Bilangannya adalah 0 dan tidak genap maupun ganjil.
Baris ini selalu diprint.
```

Dalam contoh di atas,

- kita mengambil integer sebagai input dari user dan menyimpannya ke dalam variable `num`
- kita kemudian menggunakan Statement `if else` untuk memeriksa apakah `num` tidak sama dengan `0`.
    - Jika `true`, maka Statement **dalam** `if else` akan dieksekusi.
    - ika `false`, code di dalam **luar** condition `else` dijalankan, yang menampilkan "Angkanya adalah 0 dan tidak genap maupun ganjil."
- **bagian dalam** Statement `if else` cek apakah jumlah input habis dibagi `2`.
    - Jika `true`, maka kita akan mencetak Statement yang menyatakan bahwa bilangan tersebut genap.
    - Jika `false`, kita print bahwa jumlahnya ganjil.

Perhatikan bahwa `0` juga habis dibagi `2`, tetapi sebenarnya bukan bilangan genap. Inilah sebabnya mengapa pertama-tama kita memastikan bahwa input num tidak `0` dalam `if` condition luar.

> **Catatan: Seperti yang Anda lihat, `if...else` Bersarang membuat logika Anda rumit. Jika memungkinkan, Anda harus selalu berusaha menghindari `if else` Bersarang.**

## body if else Dengan Hanya Satu Statement
Jika body `if else` hanya memiliki satu Statement, Anda dapat menghilangkannya `{ }` dalam program. Misalnya, Anda dapat mengganti

```cpp
int num = 5;

    if (num > 0) {
        cout << "Jumlahnya positive." << endl;
    }
    else {
        cout << "Nomornya adalah negative." << endl;
    }
```

dengan

```cpp
int num = 5;

    if (num > 0)
        cout << "Nomornya adalah positive." << endl;
    else
        cout << "Nomornya adalah negative." << endl;
```

Output dari kedua program akan sama.

> **Catatan: Meskipun tidak perlu digunakan `{ }` jika isi `if else` hanya memiliki satu Statement, menggunakan `{ }` membuat code Anda lebih mudah dibaca.**
