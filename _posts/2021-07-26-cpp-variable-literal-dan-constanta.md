---
title: C++ Variable Literal dan constanta
author: Eno
date: 2021-07-26 00:00:00 +0000
categories: [Programming CPP, CPP Introduction, C++ variable Literal dan Constanta]
image: /assets/img/programming/CPP/C++.png
tags: [Programming, C++, variable, Literal, constanta, Integers, Floating-point Literals, Escape Sequences, String Literal]
---
![Desktop View](/assets/img/programming/CPP/C++.png)

Dalam tutorial ini, kita akan belajar tentang variable, literal, dan Const dalam C++ dengan contoh.

## C++ variable 
Dalam pemrograman, variable adalah wadah (area penyimpanan) untuk menampung data.

Untuk menunjukkan area penyimpanan, setiap variableharus diberi nama unik (identifier). Sebagai contoh,

```cpp
int usia = 14;
```
Di Sini, `usia` adalah variable dari `int` tipe data, dan kami telah menetapkan nilai integer 14 untuk itu.

> Catatan: `int` tipe data menunjukkan bahwa variable hanya bisa menampung integers. Demikian pula, kita dapat menggunakan double tipe data jika kita harus menyimpan decimal dan exponential.

Kita akan belajar tentang semua tipe data secara rinci dalam tutorial berikutnya.

Nilai variable dapat diubah, maka nama **variable**.

```cpp
int usia = 14;   // usia 14
usia = 17;       // usia 17
```
## Aturan untuk penamaan variable
- Nama variable hanya boleh memiliki huruf, angka, dan garis bawah _.
- Nama variable tidak boleh diawali dengan angka.
- Nama variable tidak boleh dimulai dengan karakter huruf besar.
- Nama variable tidak boleh berupa kata kunci . Misalnya, int adalah kata kunci yang digunakan untuk menunjukkan integer.
- Nama variable dapat dimulai dengan garis bawah. Namun, itu tidak dianggap sebagai praktik yang baik.
> Catatan: Kita harus mencoba memberi nama yang bermakna pada variable. Sebagai contoh,nama depan adalah nama variable yang lebih baik daripada fn.

## C++ Literal
Literal adalah data yang digunakan untuk mewakili nilai tetap. Mereka dapat digunakan langsung dalam code. Contoh: `1`, `2.5`, `'c'`dst.

Di sini, `1`, `2.5` dan `'c'`adalah literal. Mengapa? Anda tidak dapat menetapkan nilai yang berbeda untuk istilah ini.

Berikut daftar literal yang berbeda dalam pemrograman C++.

### Integers
Integer adalah literal numeric (terkait dengan angka) tanpa bagian pecahan atau exponential. Ada tiga jenis literal integer dalam pemrograman C:

- decimal (basis 10)
- octal (basis 8)
- hexadecimal (basis 16)

Sebagai contoh:

```cpp
Decimal: 0, -9, 22 dst
Octal: 021, 077, 033 dst
hexadecimal: 0x7f, 0x2a, 0x521 dll
```
Dalam pemrograman C++, octal dimulai dengan `0`, dan hexadecimal dimulai dengan `0x`.

### Floating-point Literals
Floating-point Literals adalah literal numeric yang memiliki bentuk pecahan atau bentuk exponential. Sebagai contoh:

- `-2.0`

- `0.0000234`

- `-0.22E-5`

> Catatan: *`E-5 = 10-5`*

### karakter
karakters literal dibuat dengan melampirkan satu karakter di dalam tanda kutip tunggal. Misalnya: `'a'`, `'m'`, `'F'`, `'2'`,`'}'`dst.

### Escape Sequences
Terkadang, perlu menggunakan karakter yang tidak bisa diketik atau memiliki arti khusus dalam pemrograman C++. Misalnya, baris baru (enter), tab, tanda tanya, dll.

Untuk menggunakan karakter ini, sequence runner digunakan.

|Escape Sequences|karakters
|:---|:--
`\b` |	Backspace
`\f` |	Form feed
`\n` |	Newline
`\r` |	Return
`\t` |	Horizontal tab
`\v` |	Vertical tab
`\\` |	Backslash
`\'` |	Single quotation mark
`\"` |	Double quotation mark
`\?` |	Question mark
`\0` |	Null karakter

### String Literal
Literal string adalah urutan karakter yang diapit oleh tanda kutip ganda. Sebagai contoh:

|Escape order|karakter
|:---|:--
`"0x3n0"` |	string const
`""` |	null string const
`" "` |	string const enam spasi
`"x"` |	string const memiliki karakter tunggal
`"Bumi itu bulat\n"` |	print string dengan baris baru

Kita akan belajar tentang string secara rinci dalam tutorial string C++.

## C++ Constanta 
Dalam C++, kita dapat membuat variable yang nilainya tidak dapat diubah. Untuk itu, kami menggunakan kata kunci `const`. Berikut ini contohnya:

```cpp
const int LIGHT_SPEED = 299792458;
LIGHT_SPEED = 2500 // Error! LIGHT_SPEED is a constant.
```
Di sini, kita telah menggunakan kata kunci `const` untuk mendeklarasikan sebuah const bernama `LIGHT_SPEED`. Jika kita mencoba mengubah nilai `LIGHT_SPEED`, kita akan mendapatkan kesalahan.

const juga dapat dibuat menggunakan `#define` preprocessor directive.
