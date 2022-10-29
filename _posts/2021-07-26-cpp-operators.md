---
title: C++ Operators
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, C++ Operators]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, variable, Divisi, Arithmetic, Integers, Floating-point, Tambah, Modul, Assignment, Relational, Bitwise, Logical]
---

![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang berbagai jenis operator di C++ dengan contoh. Dalam pemrograman, operator adalah symbol yang beroperasi pada nilai atau variable.

Operator adalah symbol yang melakukan operasi pada variable dan nilai. Misalnya, `+` adalah operator yang digunakan untuk penjumlahan, sedangkan `-` adalah operator yang digunakan untuk pengurangan.

Operator dalam C++ dapat diklasifikasikan menjadi 6 jenis:

- Arithmetic Operators
- Assignment Operators
- Relational Operators
- Logical Operators
- Bitwise Operators
- Operators Lainnya

## 1. C++ Operator Arithmetic 
Operator aritmatika digunakan untuk melakukan operasi Arithmetic pada variabel dan data. Sebagai contoh,

```cpp
a + b;
```

Di sini, operator `+` digunakan untuk menambahkan dua variable `A` dan `B`. Demikian pula ada berbagai operator Arithmetic lainnya di C++.

|Operator |	Operasi
|:---|:--
`+` |	Tambahan
`-` |	Pengurangan
`*` |	Perkalian
`/` |	Divisi
`%` |	Operasi Modul (Sisa setelah pembagian)

### Contoh 1: Operator Arithmetic

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    a = 7;
    b = 2;

    // print jumlah a dan b
    cout << "a + b = " << (a + b) << endl;

    // print selisih a dan b
    cout << "a - b = " << (a - b) << endl;

    // print hasil kali a dan b
    cout << "a * b = " << (a * b) << endl;

    // print pembagian a dengan b
    cout << "a / b = " << (a / b) << endl;

    // print sisa bagi dari a oleh b
    cout << "a % b = " << (a % b) << endl;

    return 0;
}
```

Output

```cpp
a + b = 9
a - b = 5
a * b = 14
a / b = 3
a% b = 1
```

Di sini, operator `+`, `-` dan `*` menghitung penambahan, pengurangan, dan perkalian masing-masing seperti yang kita harapkan.

## C++ Operator Divisi `/`

Perhatikan operasi `(a / b)` dalam program. oprator `/` adalah operator divisi.

Seperti yang dapat kita lihat dari contoh di atas, jika sebuah integer dibagi dengan integer lainnya, kita akan mendapatkan hasil bagi. Namun, jika pembagi atau divisi adalah bilangan floating-point, kita akan mendapatkan hasilnya dalam decimal.

```cpp
Dalam C++,

7/2 adalah 3
7.0 / 2 adalah 3.5
7 / 2.0 adalah 3.5
7.0 / 2.0 adalah 3.5
```

## C++ Operator Sisa Bagi `%`

Operator Sisa bagi `%` menghitung sisanya. Ketika `a = 9` dibagi dengan `b = 4`, sisanya adalah **`1`**.

> **Catatan: Operator % hanya dapat digunakan dengan Integer.**

## C++ Operator Penambahan dan pengurangan `+` `-`
C++ juga menyediakan operator Penambahan dan pengurangan : `++` dan `--` masing - masing.

- `++` meningkatkan nilai operator sebesar 1
- `--` berkurang 1

Sebagai contoh,

```cpp
int num = 5;

// operator tambah
++num;  // 6
```

Di sini, code ++ num; menambahkan nilai 1 num.

### Contoh 2: Operator Penambahan dan pengurangan

```cpp
// Bekerja di operator penambahan dan pengurangan

#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 100, result_a, result_b;

    // menambah a dengan 1 dan menyimpan hasilnya di result_a
    result_a = ++a;
    cout << "result_a = " << result_a << endl;


    // mengurangi b dengan 1 dan menyimpan hasilnya di result_b 
    result_b = --b;
    cout << "result_b = " << result_b << endl;

    return 0;
}
```

Output

```cpp
result_a = 11
result_b = 99
```

Dalam program di atas, kita telah menggunakan operator `++` dan `--` sebagai awalan `(++a dan --b)`. Namun, kita juga dapat menggunakan operator ini sebagai postfix `(a++ dan b--)`.

## 2. C++ Operators Assignment 
Dalam C++, operator Assignment digunakan untuk menetapkan nilai ke variable. Sebagai contoh,

```cpp
// assign 5 ke a
a = 5;
```

Di sini, kita telah menetapkan nilai 5 ke sebuah variable.

Operator |	Contoh |	Setara dengan
|:---|:--|:--
`=` |	`a = b;` |	`a = b;`
`+=` |	`a += b;` |	`a = a + b;`
`-=` |	`a -= b;` |	`a = a - b;`
`*=` |	`a *= b;` |	`a = a * b;`
`/=` |	`a /= b;` |	`a = a / b;`
`%=` |	`a %= b;` |	`a = a % b;`

### Contoh 3: Operator Assignment

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;

    // 2 ditugaskan ke a
    a = 2;

    // 7 ditugaskan ke b
    b = 7;

    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "\nSetelah a += b;" << endl;

    // menugaskan jumlah a dan b ke a
    a += b;  // a = a +b
    cout << "a = " << a << endl;

    return 0;
}
```

Output

```cpp
a = 2 
b = 7 

Setelah a += b; 
a = 9
```

## 3. C++ Operators Relational
Operator Relational digunakan untuk memeriksa hubungan antara dua operan. Sebagai contoh,

```cpp
// memeriksa apakah a lebih besar dari b
a > b;
```

Di sini, `>` adalah operator relasional. yang memeriksa apakah `a` lebih besar dari `B` atau tidak.

Jika relasinya **`true`**, ia mengembalikan `1` sedangkan jika hubungan itu **`false`**, ia mengembalikan `0`.

|Operator |	Berarti |	Contoh
|:---|:--|:--
`==` |	Adalah sama dengan |	`3 == 5` memberi kita **false**
`!=` |	Tidak sebanding dengan |	`3 != 5` memberi kita **true**
`>` |	Lebih besar dari |	`3 > 5` memberi kita **false**
`<` |	Kurang dari |	`3 < 5` memberi kita **true**
`>=` |	Lebih dari atau sama dengan |	`3 >= 5` beri kami **false**
`<=` |	Kurang dari atau Sama Dengan |	`3 <= 5` memberi kita **true**

### Contoh 4: C++ Operator Relasional

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    a = 3;
    b = 5;
    bool result;

    result = (a == b);   // false
    cout << "3 == 5 adalah " << result << endl;

    result = (a != b);  // true
    cout << "3 != 5 adalah " << result << endl;

    result = a > b;   // false
    cout << "3 > 5 adalah " << result << endl;

    result = a < b;   // true
    cout << "3 < 5 adalah " << result << endl;

    result = a >= b;  // false
    cout << "3 >= 5 adalah " << result << endl;

    result = a <= b;  // true
    cout << "3 <= 5 adalah " << result << endl;

    return 0;
}
```

Output

```cpp
3 == 5 adalah 0 
3 != 5 adalah 1 
3 > 5 adalah 0 
3 < 5 adalah 1 
3 >= 5 adalah 0 
3 <= 5 adalah 1
```

Catatan : Operator relasional digunakan dalam pengambilan keputusan dan perulangan atau dikenal dengan looping.

## 4. C++ Logical Operators
Operator logika digunakan untuk memeriksa apakah **true atau **false**. Jika ekspresinya true, ia mengembalikan `1` sedangkan jika ekspresinya false , ia mengembalikan `0`.

|Operator |	Contoh |	Berarti
|:---|:--|:--
|`&&` |	ekspresi1 **&&** ekspresi2 |	logical **AND**. true hanya jika semua operan true.
|`| |` |	ekspresi1 **`| |`** ekspresi2 |	logical **OR**. true jika setidaknya salah satu operan benar.
`!` |	! ekspresi |	Logical **NOT**. true hanya jika operan false.

Dalam C++, operator logika biasanya digunakan dalam pengambilan keputusan. Untuk lebih memahami operator logika, mari kita lihat contoh berikut,

```cpp
Suppose,
a = 5
b = 8

Then,

(a > 3) && (b > 5) mengevaluasi ke true
(a > 3)  && (b < 5) mengevaluasi ke false

(a > 3) || (b > 5) mengevaluasi ke true
(a > 3) || (b < 5) mengevaluasi ke true
(a < 3) || (b < 5) mengevaluasi ke false

!(a < 3) mengevaluasi ke true
!(a > 3) mengevaluasi ke false
```

### Contoh 5: Logical Operators

```cpp
#include <iostream>
using namespace std;

int main() {
    bool result;

    result = (3 != 5) && (3 < 5);     // true
    cout << "(3 != 5) && (3 < 5) is " << result << endl;

    result = (3 == 5) && (3 < 5);    // false
    cout << "(3 == 5) && (3 < 5) is " << result << endl;

    result = (3 == 5) && (3 > 5);    // false
    cout << "(3 == 5) && (3 > 5) is " << result << endl;

    result = (3 != 5) || (3 < 5);    // true
    cout << "(3 != 5) || (3 < 5) is " << result << endl;

    result = (3 != 5) || (3 > 5);    // true
    cout << "(3 != 5) || (3 > 5) is " << result << endl;

    result = (3 == 5) || (3 > 5);    // false
    cout << "(3 == 5) || (3 > 5) is " << result << endl;

    result = !(5 == 2);    // true
    cout << "!(5 == 2) is " << result << endl;

    result = !(5 == 5);    // false
    cout << "!(5 == 5) is " << result << endl;

    return 0;
}
```

Output

```cpp
(3 != 5) && (3 < 5) adalah 1 
(3 == 5) && (3 < 5) adalah 0 
(3 == 5) && (3 > 5) adalah 0 
(3 != 5) || (3 < 5) adalah 1 
(3 != 5) || (3 > 5) adalah 1 
(3 == 5) || (3 > 5) adalah 0 
!(5 == 2) adalah 1 
!(5 == 5) adalah 0
```

Penjelasan program operator logical

- `(3 != 5) && (3 < 5)` mengevaluasi ke **`1`** karena kedua operan `(3 != 5)` dan `(3 < 5)` yang **`1`** (true).
- `(3 == 5) && (3 < 5)` mengevaluasi ke **`0`** karena operan `(3 == 5)` adalah ***`0`*** (false).
- `(3 == 5) && (3 > 5)` mengevaluasi ke **`0`** karena kedua operan `(3 == 5)` dan `(3 > 5)` yang **`0`** (false).
- `(3 != 5) || (3 < 5)` mengevaluasi ke **`1`** karena kedua operan `(3 != 5)` dan `(3 < 5)` yang **`1`** (true).
- `(3 != 5) || (3 > 5)` mengevaluasi ke **`1`** karena operan `(3 != 5)` adalah **`1`** (true).
- `(3 == 5) || (3 > 5)` mengevaluasi ke **`0`** karena kedua operan `(3 == 5)` dan `(3 > 5)` yang **`0`** (false).
- `!(5 == 2)` mengevaluasi ke **`1`** karena operan `(5 == 2)` adalah **`0`** (false).
- `!(5 == 5)` mengevaluasi ke **`0`** karena operan `(5 == 5)` adalah **`1`** (true).

## 5. C++ Operators Bitwise
Dalam C++, operator bitwise digunakan untuk melakukan operasi pada bit individu. hanya dapat digunakan bersama `char` dan type `int` data.

|Operator |	Keterangan
|:---|:--
`&` |	Binary AND
`|` |	Binary OR
`^` |	Binary XOR
`~` |	Komplemen Binary Satu
`<<` |	Shift Binary ke Kiri
`>>` |	Shift Binary Kanan

Untuk mempelajari lebih lanjut, kunjungi operator bitwise C++ .

## 6. C++ Operators Lainnya
Berikut daftar beberapa operator umum lainnya yang tersedia di C++. Kita akan mempelajarinya di tutorial selanjutnya.

|Operator |	Keterangan |	Contoh
|:---|:--|:--
`sizeof` |	mengembalikan ukuran type data |	`sizeof(int); // 4`
`?:` | 	mengembalikan nilai berdasarkan kondisi |	`string result = (5 > 0) ? "even" : "odd"; // "even"`
`&` |	mewakili alamat memori operan |	`&num; // address of num`
`.` |	mengakses anggota variable struct atau object class |	`s1.marks = 92;`
`->` |	digunakan dengan pointer untuk mengakses class atau variable struct |	`ptr->marks = 92;`
`<<` |	mencetak nilai keluaran |	cout `<< 5;`
`>>` |	mendapatkan nilai input |	`cin >> num;`
