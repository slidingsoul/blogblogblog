---
date: '2025-12-30T15:59:19+07:00'
title: 'Greatest Common Denominator'
tags: ["math", "indonesia"]
---

Ketika, aku masih jadi mahasiswa yang punya tujuan dan semangat tinggi untuk mendapatkan nilai tinggi, aku diberikan satu tantangan yaitu kuis. Well, kita diberi sedikit headstart dalam wujud "kisi-kisi". Aku baru mengenal "kisi-kisi" akan sangat berguna di masa perkuliahan dan rasanya aku sudah ketergantungan dengan konsep yang bernama "kisi-kisi" ini, sampai-sampai aku bakal enggan belajar kalau tidak diberi kisi-kisi.

Kuis waktu itu adalah kuis pertamaku di masa kuliah, dan untuk soal yang pertama, kita diberikan kisi-kisi tentang menjadi FPB (GCD) dan KPK (LCF). Aku mau kita fokus ke FPB karena ini konsep yang cukup penting, jadi FPB atau Faktor Persekutuan TerBesar adalah bilangan bulat paling besar yang membagi habis kedua/ketiga/ke-x bilangan. Semisal nih

$$ gcd(10, 45) $$

Kalau kamu udah cukup tokcer ngitungnya, pasti langsung tahu jawabannya itu 5, tapi kalau kamu masih belajar, kita pecah dulu jadi bentuk perkalian bilangan prima

$$ 10 = 2 \times 5 \newline 45 = 3 \times 3 \times 5 $$

Oke, langsung ketemu jadinya 5, tapi itu cara SD sih. Waktu itu, aku diminta buat nulis kode cara menjadi FPB dari 2 angka. Sebagai mahasiswa ilmu komputer, kita belajar ke suatu metode mencari FPB yang namanya Algoritma Euclid. Aku kasi tahu oret-oretannya dulu, trus aku jelasin per baris

$$
45 = 10 \times q_1 + r_1
\newline
45 = 10 \times 4 + 5
\newline
q_1 = 4
\newline
r_1 = 5
$$

$$
10 = 5 \times q_2 + r_2
\newline
10 = 5 \times 2 + 0 \newline
q_1 = 2 \newline
r_1 = 0
$$

Oke, kita cek blok pertama dulu deh, yang buat cari $q_1$ dan $r_1$, pertama kita taruh angka yang terbesar (dalam kasus ini 45, atau kita sebut greater), di ruas kiri dan angka yang kecil di ruas kanan ("lesser"), lalu kalikan dengan sebuah angka $q$ dan tambahkan dengan sebuah angka $r$. Trus kita cari tuh aja angka-angkanya, gimana caranya? Well, kita bisa pakai bantuan komputer buat itu. Di Python, ada floor division `//` dan juga module operator `%`

```
>>> 45 // 10
4
>>> 45 % 10
5
```

Nah, setelah itu pindahin angka yang sekarang di $q$ ke ruas kiri, dan jadikan gantikan $ 10 $ menjadi $r$ sekarang yaitu $5$. Lalu, kita pindah ke blok kedua, 10 sekarang di ruas kiri, 5 di ruas kanan dan kita cari $q$ dan $r$ yang kedua.

```
>>> 10 // 5
2
>>> 10 % 5
0
```

Oke, kita udah ketemu sampai $ r = 0 $ nih, akhirnya kita bisa stop dan anggap "greater" yang sekarang itu sebagai gcd-nya.

$$ gcd(10, 45) = 5 $$

Itulah konsep dari Algoritma Euclid. Kalau mau dibuat kode di python, bakal seperti ini

```
def find_gcd(a, b):
  greater = 0
  lesser = 0
  if (a > b):
    greater = a
    lesser = b
  elif (a < b):
    greater = b
    lesser = a
  else:
    return a
  while lesser > 0:
    q = greater // lesser
    r = greater % lesser
    greater = lesser
    lesser = r
  return greater
```

Oke, santai dulu, kode ini belum final, kita masih bisa improve beberapa bagian, perhatikan di bagian greater dan lesser itu. Bisa dijadikan seperti ini

```
def find_gcd(a, b):
  if (a == b):
    return a
  greater, lesser = (a,b) if (a > b) else (b,a)
  while lesser > 0:
    q = greater // lesser
    r = greater % lesser
    greater = lesser
    lesser = r
  return greater
```

Lalu, kalau kalian perhatikan, $q% itu engga terpakai sama sekali, bisa dibuang.

```
def find_gcd(a, b):
  if (a == b):
    return a
  greater, lesser = (a,b) if (a > b) else (b,a)
  while lesser > 0:
    r = greater % lesser
    greater = lesser
    lesser = r
  return greater
```

Aku mau kalian tahu kodeku dari yang spageti sampai ke "mendingan" supaya kalian tahu kalau orang engga langsung jadi pinter. Kode yang ditulis engga bakal langsung jadi clean (kecuali kalian udah tokcer). Kalau engga bisa, jangan langsung nyerah dan langsung cari solusi orang lain dengan searching Google atau tanya AI, berusahalah sedikit lagi.

Sekarang tantangannya adalah, kode yang kutulis ini bisa dibuat versi rekursif. Iya iya, kalau kalian searching dari Google udah langsung ditunjukkan yang versi rekursif kok, tapi ini versiku

```
def rec_find_gcd(a, b):
  if (a == b) or b == 0:
    return a
  return rec_find_gcd(b, a % b)
```

Nah, dari sini mungkin kalian bingung, "Lho, kok ga ada greater dan lesser-nya?". Jawabannya adalah, sebenernya greater dan lesser itu engga ngaruh sih. Kita coba runtut pakai konsepnya dulu, tapi 10 dan 45-nya dibalik

$$
10 = 45 \times q_1 + r_1
\newline
10 = 45 \times 0 + 10
\newline
q_1 = 0
\newline
r_1 = 10
$$

$$
45 = 10 \times q_2 + r_2
\newline
45 = 10 \times 4 + 5
\newline
q_2 = 4
\newline
r_2 = 5
$$

Terlihat familiar kan?

$$
10 = 5 \times q_3 + r_3
\newline
10 = 5 \times 2 + 0 \newline
q_3 = 2 \newline
r_3 = 0
$$

See? Jadinya kalau kebalik di awal, itu bakal secara otomatis dibenerin di step selanjutnya. Oleh karena itu versi yang looping bisa dijadikan seperti ini

```
def find_gcd(a, b):
  if (a == b):
    return a
  while b > 0:
    r = a % b
    a = b
    b = r
  return a
```

Jadi lebih clean lagi kan? Oke deh, have a good one!