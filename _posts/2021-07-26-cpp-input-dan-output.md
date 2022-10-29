---
title: C++ Input dan Output
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, Input dan Output]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, Input, output, string output, string Input, Characters Output, Integer Input, Integer Output, Multiple Inputs, cin, cout, num]
---
![Window shadow](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar menggunakan object `cin` untuk mengambil input dari user, dan object `cout` untuk menampilkan output kepada user dengan contoh.

## C++ Output
Dalam C++, `cout` mengirimkan output yang diformat ke perangkat output standar, seperti layar. Kami menggunakan object `cout` bersama dengan operator `<<` untuk menampilkan output.

### Contoh 1: string output

```cpp
#include <iostream>
using namespace std;

int main() {
    // print string yang diapit tanda kutip ganda
    cout << "Ini Pemrograman C++++";
    return 0;
}
```

Output

```cpp
Ini Pemrograman C++++
```

Bagaimana cara kerja program ini?

- pertama-tama menyertakan `iostream` file header yang memungkinkan menampilkan output.
- `cout` object ditentukan dalam `std` namespace. Untuk menggunakan `std` namespace, menggunakan pernyataan `using namespace std;`.
- Setiap program C++ dimulai dengan fungsi `main()`. ekesekusi code dimulai dari awal fungsi `main()`.
- `cout` adalah object yang mencetak string di dalam tanda kutip `" "`. Hal ini diikuti oleh operator `<<`.
- `return 0;` adalah "status keluar" dari fungsi `main()`. Program diakhiri dengan pernyataan ini, namun pernyataan tidak wajib.

> **Catatan: Jika kita tidak menyertakan pernyataan `using namespace std;`, kita perlu menggunakan `std::cout` sebagai ganti `cout`.
> Ini adalah metode yang disukai karena menggunakan `std` namespace dapat menimbulkan masalah.
> Namun, kita telah menggunakan `std` namespace dalam tutorial untuk membuat code lebih mudah dibaca.**

```cpp
#include <iostream>

int main() {
    // string yang tanda kutip ganda
    std::cout << "Ini Pemrograman C++++";
    return 0;
}
```

### Contoh 2: Output Angka dan Character

Untuk mencetak variable angka dan Character, kita menggunakan object `cout` yang sama tetapi tanpa menggunakan tanda petik.

```cpp
#include <iostream>
using namespace std;

int main() {
    int num1 = 70;
    double num2 = 256.783;
    char ch = 'A';

    cout << num1 << endl;    // print integer
    cout << num2 << endl;    // print double
    cout << "character: " << ch << endl;    // print char
    return 0;
}
```

Output

```cpp
70
256.783
Character: A
```

> Catatan:
manipulator `endl` digunakan untuk menyisipkan baris baru. Itu sebabnya setiap output ditampilkan di baris baru.
operator `<<` dapat digunakan lebih dari sekali jika kita ingin mencetak variable yang berbeda, string dan sebagainya dalam sebuah pernyataan tunggal. 

Sebagai contoh:

```cpp
C++cout << "character: " << ch << endl;
```

## C++ Input
Dalam C++, `cin` mengambil input yang diformat dari perangkat input standar seperti keyboard. menggunakan object `cin` bersama dengan operator `>>` untuk mengambil input.

### Contoh 3: Input/Output Integer

```cpp
#include <iostream>
using namespace std;

int main() {
    int num;
    cout << "Masukkan sebuah integer: ";
    cin >> num;   // mangambil input
    cout << "num adalah: " << num;
    return 0;
}
```

Outpput

```cpp
Masukkan sebuah integer: 70
num adalah: 70
```

Dalam program, menggunakan
`cin >> num;`
untuk menerima input dari user. Input disimpan dalam variable `num`. menggunakan operator `>>` dengan `cin` untuk mengambil input.

> **Catatan: Jika kita tidak menyertakan pernyataan `using namespace std;` kita perlu menggunakan `std::cin` sebagai ganti `cin`**.

## C++ Mengambil Banyak Input

```cpp
#include <iostream>
using namespace std;

int main() {
    char a;
    int num;

    cout << "Masukkan characters dan integers: ";
    cin >> a >> num;

    cout << "Character: " << a << endl;
    cout << "Number: " << num;

    return 0;
}
```

Output

```cpp
Masukkan characters dan integers: F
23
characters: F
number: 23
```
