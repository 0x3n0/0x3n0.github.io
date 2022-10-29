---
title: C++ Data Types
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, Data Types]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, type Data Dasar, int, float, double, Character, wchar_t, bool, void, modifiers, Turunan]
---
![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang type data dasar seperti `int`, `float`, `char`, dll dalam pemrograman C++.

Dalam C++, type data adalah deEnotion untuk variable. Untuk menentukan jenis dan ukuran data yang terkait dengan variable. Sebagai contoh,

```cpp
int usia = 13;
```

Di Sini, `usia` adalah variable type int. Artinya, variable hanya dapat menyimpan Integer baik 2 atau 4 byte.

## C++ Data type Dasar
Tabel di bawah ini menunjukkan type data dasar, artinya, dan ukurannya (dalam byte):

|type data |Berarti | (dalam Byte) |
|:---|:--|:-
`int` |	Integer |	2 atau 4
`float` |	floating-point |	4
`double` |	Double Floating Point |	8
`char` |	Character	| 1
`wchar_t` |	Wide Character |	2
`bool` |	Boolean	| 1
`void` |	Empty |	0

Sekarang, mari kita bahas type data fundamental ini secara lebih rinci.

### C++ int
Kata kunci `int` digunakan untuk menunjukkan Integer.
Ukurannya biasanya 4 byte. Artinya, dapat menyimpan nilai dari **-2147483648** hingga **2147483647**.

Sebagai contoh,

```cpp
int gaji = 85000;
```

### C++ float dan double
- `float` dan `double` digunakan untuk menyimpan bilangan floating-point (decimal dan eksponensial).
- Ukurannya `float` adalah 4 byte dan ukurannya `double` adalah 8 byte. Oleh karena itu, `double` memiliki dua kali presisi `float`.

Sebagai contoh

```cpp
float area = 64.74;
double volume = 134.64534;
```
Seperti disebutkan di atas, kedua type data ini juga digunakan untuk eksponensial. Sebagai contoh,

```cpp
double distance = 45E12    // 45E12 adalah sama dengan 45*10^12
```

### C++ Character 
- Kata kunci `char` digunakan untuk Character.
- Ukurannya adalah 1 byte.
- Character dalam C++ diapit di dalam tanda kutip tunggal ' '.

Sebagai contoh

```cpp
char test = 'h';
```
> **Catatan: Dalam C++, nilai integer disimpan dalam `char` variable dari.**

### C++ wchar_t
- Character lebar `char_t` mirip dengan chartype data, kecuali ukurannya 2 byte, bukan 1.
- digunakan untuk mewakili Character yang membutuhkan lebih banyak memori untuk mewakilinya daripada satu char.

Sebagai contoh
```cpp
wchar_t test = L'ם'  // menyimpan character Hebrew;
```

Perhatikan huruf L sebelum tanda petik.

> **Catatan: Ada juga dua type character ukuran tetap lainnya `char16_t` dan `char32_t` diperkenalkan di C++ 11.**

### C++ bool
- `bool` type data memiliki salah satu dari dua kemungkinan nilai: `true` atau `false`.
- Boolean digunakan dalam pernyataan dan loop conditional 

Sebagai contoh

```cpp
bool cond = false;
```
### C++ void
- Kata  kunci`void` menunjukkan tidak adanya data. Itu berarti "tidak ada" atau "tidak ada nilai".
- Kita akan menggunakan void ketika kita belajar tentang fungsi dan pointer.

> **Catatan: Kami tidak dapat mendeklarasikan variable void bertype.**

## C++ Type Modifiers
selanjutnya dapat memodifikasi beberapa type data dasar dengan menggunakan `modifier` type. Ada 4 jenis pengubah di C++.

- 1 `signed`
- 2 `unsigned`
- 3 `short`
- 4 `long`

Kita dapat memodifikasi type data berikut dengan modifiers di atas:

- `int`
- `double`
- `char`

## Daftar Type Data yang Di modifikasi C++

| Type data |	Ukuran (Byte) |	Berarti
|:---|:--|:--
`signed int` |	4 |	digunakan untuk bilangan bulat (setara dengan `int`)
`unsigned int` |	4 | 	hanya dapat menyimpan bilangan bulat positif
`short` |	2 |	digunakan untuk integer kecil (range **-32768** hingga **32767**)
`unsigned short` |	2 |	digunakan untuk bilangan bulat positif kecil (range **0** hingga **65.535**)
`long` |	setidaknya 4 |	digunakan untuk integer besar (setara dengan `long int`)
`unsigned long` |	4 |	digunakan untuk positive integer besar atau 0 (setara dengan `unsigned` `long int`)
`long long` |	8 |	digunakan untuk integer yang sangat besar (setara dengan `long long` `int`).
`unsigned long long` |	8 |	digunakan untuk integer positive yang sangat besar atau 0 (setara dengan `unsigned long long int`)
`long double` |	12 |	digunakan untuk bilangan floating-point besar
`signed char` |	1 |	digunakan untuk karakter (rentang dijamin  **-127** hingga **127**)
`unsigned char` |	1 |	digunakan untuk karakter (rentang **0** hingga **255**)

Mari kita lihat beberapa contoh.

```cpp
long b = 4523232;
long int c = 2345342;
long double d = 233434.56343;
short d = 3434233; // error! dari range
unsigned int a = -5;    // error! hanya dapat menyimpan angka positive atau 0
```

## Type Data Turunan
Type data yang diturunkan dari type data dasar adalah type turunan. Misalnya: `array`, `pointer`, `function type`, `structures`, dll.

Kita akan belajar tentang type data turunan di tutorial selanjutnya.
