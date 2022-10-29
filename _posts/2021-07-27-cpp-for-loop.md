---
title: C++ for Loop
author: Eno
date: 2021-07-27 00:00:00 +0000
categories: [Programming CPP, CPP Flow Control, C++ for Loop]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, for, while, do while, initialization, condition, true_, false_, update, array, int, collection]
---

![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang C++ `for` loop dan cara kerjanya dengan beberapa contoh.

Dalam pemrograman komputer, loop digunakan untuk mengulang block code.

Sebagai contoh, katakanlah kita ingin menampilkan pesan sebanyak 100 kali. Kemudian alih-alih menulis statement print 100 kali, kita bisa menggunakan loop.

Itu hanya contoh sederhana; kami dapat mencapai lebih banyak efisiensi dan kecanggihan dalam program kami dengan memanfaatkan loop secara efektif.

Ada 3 jenis loop dalam C++.

- `for` loop
- `while` loop
 `do while` loop

Tutorial ini berfokus pada `for` loop C++ . Kita akan belajar tentang jenis loop lainnya dalam tutorial yang akan datang.

## C++ for loop
Syntax for-loop adalah:

```cpp
for (inisialisasi; condition; update) {
    // body dari-loop 
}
```

Di Sini,

- `inisialisasi` - menginisialisasi variable dan dieksekusi hanya sekali
- `condition` - jika `true`, body for loop dieksekusi
jika `false`, for loop dihentikan
- `update` - memperbarui nilai variable yang diinisialisasi dan kembali memeriksa condition

## C++ Flowchart for Loop

![Desktop View](/assets/img/programming/CPP/cpp-for-loop-flowchart.png)

### Contoh 1: Print Angka Dari 1 hingga 5

```cpp
#include <iostream>

using namespace std;

int main() {
        for (int i = 1; i <= 5; ++i) {
        cout << i << " ";
    }
    return 0;
}
```

Output

```cpp
1 2 3 4 5
```

Berikut adalah cara kerja program ini

|looping |	Variable |	i <= 5 |	Tindakan
|:---|:--|:--|:--
1 |	`i = 1` |	`true` |	`1` diprint. `i` ditingkatkan menjadi `2`
ke-2 |	`i = 2` |	`true` |	`2` diprint. `i` ditingkatkan menjadi `3`
ke-3 |	`i = 3` |	`true`  |	`3` diprint. `i` ditingkatkan menjadi `4`
4th |	`i = 4` |	`true` |	`4` diprint. `i` ditingkatkan menjadi `5`
tanggal 5 |	`i = 5` |	`true` |	`5` diprint. `i` ditingkatkan menjadi `6`
tanggal 6 |	`i = 6` |	`false` |	Loop dihentikan

### Contoh 2: Menampilkan teks 5 kali

```cpp
// Program C++ untuk menampilkan teks 5 kali

#include <iostream>

using namespace std;

int main() {
    for (int i = 1; i <= 5; ++i) {
        cout <<  "0x3n0! " << endl;
    }
    return 0;
}
```

Output

```
0x3n0!
0x3n0!
0x3n0!
0x3n0!
0x3n0!
```

Berikut adalah cara kerja program ini

|looping |	Variable| 	i <= 5 |	Tindakan
|:---|:--|:--|:--
1 |	`i = 1` |	`true` |	`0x3n0!` diprint dan `i` ditingkatkan menjadi `2`.
ke-2 |	`i = 2` |	`true` |	`0x3n0!` diprint dan `i` ditingkatkan menjadi `3`.
ke-3 |	`i = 3` |	`true` |	`0x3n0!` diprint dan `i` ditingkatkan menjadi `4`.
4th |	`i = 4` |	`true` |	`0x3n0!` diprint dan `i` ditingkatkan menjadi `5`.
tanggal 5 |	`i = 5` |	`true` |	`0x3n0!` diprint dan `i` ditingkatkan menjadi `6`.
tanggal 6 |	`i = 6` |	`false` |	Loop dihentikan

### Contoh 3: Temukan jumlah n Angka Asli pertama

```cpp
// Program C++ untuk mencari jumlah n angka asli pertama
// integer positive seperti 1,2,3 dan dikenal sebagai Angka asli

#include <iostream>

using namespace std;

int main() {
    int angka, jumlah;
    jumlah = 0;

    cout << "Masukkan sebuah integer positive: ";
    cin >> angka;

    for (int i = 1; i <= angka; ++i) {
        jumlah += i;
    }

    cout << "Jumlah = " << jumlah << endl;

    return 0;
}
```

Output

```cpp
Masukkan sebuah integer positive: 10
Jumlah = 55
```

Dalam contoh di atas, kita memiliki dua variable `angka` dan `jumlah`. NSjumlah variable ditugaskan dengan `0` dan variable `angka` ditetapkan dengan nilai yang diberikan oleh user.


Perhatikan bahwa kita telah menggunakan `for` loop.

```cpp
for(int i = 1; i <= angka; ++i)
```

Di Sini,

- int `i = 1`: menginisialisasi variabel `i`
- `i <= angka:` menjalankan `loop` selama `i` kurang dari atau sama dengan angka
- `++i`: meningkatkan variable `i` dengan `1` di setiap iterasi

Kapan `i` menjadi `11`, `condition` adalah `false` dan jumlah sama dengan `0 + 1 + 2 + ... + 10`.

## Ranged Based for Loop
Di C++11, for loop berbasis rentang baru diperkenalkan untuk bekerja dengan collection seperti **array** dan **vektor**. Syntaxnya adalah:

```cpp
for (variable : collection) {
    // body dari loop
}
```

Di sini, untuk setiap nilai dalam `collection`, perulangan for dieksekusi dan nilainya ditetapkan ke variable.

### Contoh 4: range-based for Loop

```cpp
#include <iostream>

using namespace std;

int main() {
  
    int angka_array[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  
    for (int n : angka_array) {
        cout << n << " ";
    }
  
    return 0;
}
```

Output

```cpp
1 2 3 4 5 6 7 8 9 10
```

Dalam program di atas, kita telah mendeklarasikan dan menginisialisasi sebuah `int` array bernama `angka_array`. Ini memiliki 10 item.

Di sini, kita telah menggunakan range-based `for` loop untuk mengakses semua item dalam `array`.

## C++ Infinite for loop
Jika `condition` dalam a `for` loop selalu `true`, itu berjalan selamanya (sampai memori penuh). Sebagai contoh,

```cpp
// infinite for loop
for(int i = 1; i > 0; i++) {
    // block dari code
}
```
Dalam program di atas, `condition` selalu `true` yang kemudian akan menjalankan code untuk waktu yang tidak di tentukan.
