---
title: C++ while dan do while Loop
author: Eno
date: 2021-07-27 00:00:00 +0000
categories: [Programming CPP, CPP Flow Control, C++ while dan do while Loop]
image: /assets/img/programming/CPP/cpp-do-while-loop-flowchart.png
tags: [Programming, C++, for, while, do while, initialization, condition, true_, false_, update, array, int, collection, variable, char, looping, positive, negative]
---

![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan mempelajari penggunaan while dan do... while dalam pemrograman C++ dengan bantuan beberapa contoh.

Dalam pemrograman komputer, loop digunakan untuk mengulang blok kode.

Sebagai contoh, katakanlah kita ingin menampilkan pesan sebanyak 100 kali. Kemudian alih-alih menulis pernyataan print 100 kali, kita bisa menggunakan loop.

Itu hanya contoh sederhana; kami dapat mencapai lebih banyak efisiensi dan kecanggihan dalam program kami dengan memanfaatkan loop secara efektif.

Ada **3** jenis loop dalam C++.

- `for` loop
- `while` loop
- `do while` loop

Pada tutorial sebelumnya, kita telah membahas tentang C++ for loop . Di sini, kita akan membahas tentang `while` dan `do while` loop.

## C++ while loop
Syntax while loopnya adalah:

```cpp
while (condition) {
    // body dari loop
}
```

Di Sini,

- Sebuah while loop mengevaluasi `condition`
- Jika `condition` mengevaluasi ke `true`, code di dalam while loop dieksekusi.
- `condition` dievaluasi lagi.
- Proses ini berlanjut sampai `condition` adalah `false`.

Ketika `condition` mengevaluasi ke false, loop berakhir.

## Flowchart dari while Loop

![Desktop View](/assets/img/programming/CPP/cpp-while-loop-flowchart.png)_Flowchart dari C++ while loop_

### Contoh 1: Tampilkan Angka dari 1 hingga 5

```cpp
// Program C++ untuk print angka dari 1 hingga 5

#include <iostream>

using namespace std;

int main() {
    int i = 1; 

    // while loop dari 1 ke 5
    while (i <= 5) {
        cout << i << " ";
        ++i;
    }
    
    return 0;
}
```

Output

```cpp
1 2 3 4 5
```

Berikut adalah cara kerja program.

|looping| 	Variable |	i <= 5 |	Tindakan
|:---|:--|:--|:--
`1` |	`i = 1` |	`true` |	`1` diprint dan `i` ditingkatkan menjadi `2`.
`ke-2` |	`i = 2` |	`true` |	`2` diprint dan `i` ditingkatkan menjadi `3`.
`ke-3` |	`i = 3` |	`true` |	`3` diprint dan `i` ditingkatkan menjadi `4`
`tanggal 4` |	`i = 4` |	`true` |	`4` diprint dan `i` ditingkatkan menjadi `5`.
`tanggal 5` |	`i = 5` |	`true` |	`5` diprint dan `i` ditingkatkan menjadi `6`.
`tanggal 6` |	`i = 6` |	`false` |	Loop dihentikan

### Contoh 2: Jumlah angka Positive Saja

```cpp
// program mencari jumlah angka positive
// jika user memasukkan angka negative, loop berakhir
// angka negative yang dimasukkan tidak ditambahkan ke jumlah

#include <iostream>
using namespace std;

int main() {
    int angka;
    int jumlah = 0;

    // mengambil masukan dari user
    cout << "Masukkan sebuah angka: ";
    cin >> angka;

    while (angka >= 0) {
        // tambahkan semua angka posistive
        sum += angka;

        // ambil input lagi jika angkanya positive
        cout << "Masukkan sebuah angka: ";
        cin >> angka;
    }

    // tampilkan jumlah
    cout << "\nJumlahnya adalah " << jumlah << endl;
    
    return 0;
}
```
Output

```cpp
Masukkan sebuah angka: 6
Masukkan sebuah angka: 12
Masukkan sebuah angka: 7
Masukkan sebuah angka: 0
Masukkan sebuah angka: -2

Jumlahnya adalah 25
```

Dalam program ini, user diminta untuk memasukkan angka, yang disimpan dalam variable `angka`.

Untuk menyimpan jumlah angka, kita mendeklarasikan variable jumlah dan inisialisasi ke nilai `0`.

`while` Loop berlanjut sampai user memasukkan angka negative. Selama setiap iterasi, angka yang dimasukkan oleh user ditambahkan ke variable `jumlah `.

Ketika user memasukkan angka negative, loop berakhir. Akhirnya, jumlah total ditampilkan.

## C++ do while Loop

`do while` Loop adalah varian dari `while` dengan satu perbedaan penting: body do while loop dieksekusi sekali sebelum condition diperiksa.

Syntaxnya adalah:

```cpp
do {
   // body dari loop;
}
while (condition);
```

Di Sini,

- body loop dieksekusi pada awalnya. Kemudian `condition` dievaluasi.
- Jika `condition` mengevaluasi ke `true`, body loop di dalam statement `do` dieksekusi lagi.
- `condition` dievaluasi sekali lagi.
- Jika `condition` mengevaluasi ke `true`, body loop di dalam statement `do` dieksekusi lagi.
- Proses ini berlanjut sampai `condition` evaluasi ke `false`. Kemudian loop berhenti.

## Flowchart do while Loop

![Desktop View](/assets/img/programming/CPP/cpp-do-while-loop-flowchart.png)_Flowchart dari C++ do...while loop_

```cpp
Contoh 3: Menampilkan Angka dari 1 hingga 5
// Program C++ untuk print angka dari 1 hingga 5

#include <iostream>

using namespace std;

int main() {
    int i = 1; 

    // do...while loop dari 1 hinggga 5
    do {
        cout << i << " ";
        ++i;
    }
    while (i <= 5);
    
    return 0;
}
```

Output

```
1 2 3 4 5
```

Berikut adalah cara kerja program.

|looping |	Variable |	i <= 5 |	Tindakan
|:---|:--|:--|:--
kosong |	`i = 1` |	tidak dipriksa |	`1` diprint dan `i`d itingkatkan menjadi `2`
`1` |	`i = 2` |	`true` |	`2` diprint dan `i` ditingkatkan menjadi `3`
ke-2 |	`i = 3` |	`true` |	`3` diprint dan `i` ditingkatkan menjadi `4`
ke-3 |	`i = 4` |	`true` |	`4` diprint dan `i` ditingkatkan menjadi `5`
4th |	`i = 5` |	`true` |	`5` diprint dan `i` ditingkatkan menjadi `6`
tanggal 5 |	`i = 6` |	`false` |	Loop dihentikan

### Contoh 4: Jumlah anngka Positive Saja

```cpp
// program mencari jumlah bilangan positive
// Jika user memasukkan angka negative, loop berakhir
// angka negative yang dimasukkan tidak ditambahkan ke jumlah

#include <iostream>
using namespace std;

int main() {
    int angka = 0;
    int jumlah = 0;

    do {
        sum += angka;

        // mengambil masukan dari user
        cout << "Masukkan sebuah angka: ";
        cin >> angka;
    }
    while (angka >= 0);
    
    // tampilkan jumlah
    cout << "\nJumlahnya adalah" << jumlah << endl;
    
    return 0;
}
```

Output 1

```cpp
Masukkan sebuah angka: 6
Masukkan sebuah angka: 12
Masukkan sebuah angka: 7
Masukkan sebuah angka: 0
Masukkan sebuah angka: -2

Jumlahnya adalah 25
```

Di sini, `do while` loop berlanjut hingga user memasukkan angka negative. Ketika angkanya negative, loop berakhir; angka negative tidak ditambahkan ke variable jumlah.

Output 2

```cpp
Masukkan nomor: -6
Jumlahnya adalah 0.
```

body `do while` loop hanya berjalan sekali jika user memasukkan angka negative.

## while loop Tak terbatas
Jika `condition` loop selalu `true`, loop berjalan untuk waktu yang tak terbatas (sampai memori penuh). Sebagai contoh,

```cpp
// while loop Tak terbatas
while(true) {
    // body dari loop
}
```

Berikut adalah contoh `do while` loop tak terbatas.

```cpp
// do while loop Tak terbatas

int count = 1;

do {
   // body dari loop
} 
while(count == 1);
```

Dalam program di atas, `condition` selalu `true`. Oleh karena itu, body loop akan berjalan untuk waktu yang tak terbatas.

## for vs while loop
Sebuah `for` loop biasanya digunakan ketika jumlah iterasi diketahui. Sebagai contoh,

```cpp
// Loop ini diulang 5 kali
for (int i = 1; i <=5; ++i) {
   // body dari loop
}
```

Di sini, kita tau bahwa for-loop akan dieksekusi 5 kali.

Namun, `while` dan `do while` loop biasanya digunakan ketika jumlah iterasi tidak diketahui. Sebagai contoh,

```cpp
while (condition) {
    // body dari loop
}
```
