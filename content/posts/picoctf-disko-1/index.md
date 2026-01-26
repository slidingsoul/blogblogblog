---
date: '2026-01-26T10:11:29+07:00'
title: 'picoCTF - DISKO 1'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/505
- Title: DISKO 1
- Tags: Easy, Forensics, picoGym Exclusive
- Author: Darkraicg492
- _Started: 7 July 2025_
- _Solved: 7 July 2025_
- Description: Can you find the flag in this disk image? Download the disk image here. 

After downloading a file, it appeared to be a gzipped disk image (dd.gz) file. First, I unzipped it

```
gunzip disko-1.dd.gz
```

and then from the hint, it seems like I could use `strings` command and filter the result using grep

```
strings disko-1.dd | grep CTF
```

`picoCTF{1t5_ju5t_4_5tr1n9_e3408eef}`