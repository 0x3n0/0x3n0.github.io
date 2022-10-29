---
title: C++ Type Conversion
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, Type Conversion]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, Implicit, Explicit, style casting, Function Casting, Conversion Operators, static cast, dynamic_cast, const cast, reinterpret cast]
---
![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang dasar-dasar conversion type C++ dengan contoh.

C++ memungkinkan kita untuk mengconversi data dari satu type ke type lainnya. Ini dikenal sebagai type conversion.

Ada dua jenis type conversion di C++.

- Implicit Type Conversion
- type conversion (juga dikenal sebagai Type Casting)

## Implicit Type Conversion
type Conversion yang dilakukan secara otomatis oleh compiler dikenal sebagai type conversion implisit. Jenis Conversion ini juga dikenal sebagai konversi otomatis.

Mari kita lihat dua contoh konversi tipe implisit.

### Contoh 1: Konversi Dari int ke double

```cpp
// Bekerja dari implicit type-conversion

#include <iostream>
using namespace std;

int main() {
   // menetapkan nilai int ke num_int
   int num_int = 9;

   // mendeklarasikan variable type ganda
   double num_double;
 
   // implicit conversion
   // menetapkan nilai int ke variable ganda
   num_double = num_int;

   cout << "num_int = " << num_int << endl;
   cout << "num_double = " << num_double << endl;

   return 0;
}
```

Output

```cpp
num_int = 9 
num_double = 9
```

Dalam program, menetapkan data `int` ke `double` variable.

```cpp
num_double = num_int;
```

Di sini, nilai `int` secara otomatis dikonversi oleh double compiler sebelum ditetapkan ke to `num_double` variable. Ini adalah contoh type conversion implisit.

### Contoh 2: conversi Otomatis dari double ke int

```cpp
// Bekerja dari Implicit type-conversion

#include <iostream>
using namespace std;

int main() {

   int num_int;
   double num_double = 9.99;

   // implicit conversion
   // menetapkan nilai ganda ke variable int
   num_int = num_double;

   cout << "num_int = " << num_int << endl;
   cout << "num_double = " << num_double << endl;

   return 0;
}
```

Output

```cpp
num_int = 9 
num_double = 9,99
```

Dalam program, telah menetapkan data `double` ke variable `int`.

```cpp
num_double = num_int;
```

Di sini, nilai double secara otomatis dikonversi oleh int compiler sebelum ditetapkan ke to variable `num_int`. Ini juga merupakan contoh type conversion implisit.

> Catatan: Karena `int` tidak dapat memiliki bagian decimal, num setelah titik decimal terpotong dalam contoh di atas.

## Kehilangan Data Selama conversion (Narrowing Conversion)
Seperti yang telah kita lihat dari contoh di atas, conversi dari satu type data ke type data lainnya rentan kehilangan data. Ini terjadi ketika data dari type yang lebih besar diconversi ke data dari type yang lebih kecil.

![Desktop View](/assets/img/programming/CPP/C++2.png)

## C++ Explicit Conversion
Saat user secara manual mengubah data dari satu jenis ke jenis lainnya, ini dikenal sebagai Conversion eksplisit. Jenis Conversi ini juga dikenal sebagai type casting.

Ada tiga cara utama di mana kita dapat menggunakan Conversi eksplisit dalam C++:

- C-style type casting (also known as cast notation)
- Function notation (dikenal sebgai type casting)
- Type conversion operators

## C-style Type Casting

Seperti namanya, jenis ini casting disukai oleh **bahasa pemrograman C**. Hal ini juga dikenal sebagai **cast notation**.

Syntax untuk style ini adalah:

```cpp
(data_type)expression;
```

Sebagai contoh,

```cpp
// menginisialisasi variable int
int num_int = 26;

// mendeklarasikan variabel ganda
double num_double;

// conversi dari int ke double
num_double = (double)num_int;
```

### Function-style Casting
Kita juga dapat menggunakan fungsi seperti notasi untuk mentransmisikan data dari satu type ke type lainnya.

Syntax untuk style ini adalah:

```cpp
data_type(expression);
```

Sebagai contoh,

```cpp
// menginisialisasi variable int
int num_int = 26;

// mendeklarasikan variable ganda
double num_double;

// conversi dari int ke double
num_double = double(num_int);
```

### Contoh 3: Type Casting

```cpp
#include <iostream>

using namespace std;

int main() {
    // menginisialisasi variable ganda
    double num_double = 3.56;
    cout << "num_double = " << num_double << endl;

    // C-style conversion dari double ke int
    int num_int1 = (int)num_double;
    cout << "num_int1   = " << num_int1 << endl;

    // function-style conversion dari double ke int
    int num_int2 = int(num_double);
    cout << "num_int2   = " << num_int2 << endl;

    return 0;
}
```

Output

```cpp
num_double = 3,56 
num_int1 = 3 
num_int2 = 3
```

menggunakan **C style type conversion** dan **function-style casting** untuk type conversi dan menampilkan hasilnya. Karena mereka melakukan tugas yang sama, keduanya memberi kita output yang sama.

### Type Conversion Operators
Selain dua jenis ini, C++ juga memiliki empat operator untuk jenis conversi. Mereka dikenal sebagai Type Conversion Operators:

- `static_cast`
- `dynamic_cast`
- `const_cast`
- `reinterpret_cast`
