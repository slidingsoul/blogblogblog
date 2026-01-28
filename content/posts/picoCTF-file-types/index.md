---
date: '2026-01-27T10:35:10+07:00'
title: 'picoCTF - File types'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/268
- Title: File types
- Tags: Medium, Forensics, picoCTF 2022
- Author: Geoffrey Njogu
- _Started: 17 July 2025_
- _Solved: 17 July 2025_
- Description: 
> This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can. You can download the file from [here](https://artifacts.picoctf.net/c/82/Flag.pdf).

This one was quite complicated. Insteas of a pdf file, the file was actually a shar file

```
strikingsoul@ramones:~/Downloads/filetype$ file Flag.pdf 
Flag.pdf: shell archive text
```

```
strikingsoul@ramones:~/Downloads/filetype$ sh Flag.pdf
x - created lock directory _sh00046.
x - extracting flag (text)
x - removed lock directory _sh00046.
strikingsoul@ramones:~/Downloads/filetype$ ls
flag  Flag.pdf
strikingsoul@ramones:~/Downloads/filetype$ file flag
flag: current ar archive
strikingsoul@ramones:~/Downloads/filetype$ ar -x flag 
strikingsoul@ramones:~/Downloads/filetype$ ls
flag  Flag.pdf
strikingsoul@ramones:~/Downloads/filetype$ file flag 
flag: cpio archive; device 234, inode 37435, mode 100644, uid 0, gid 0, modified Thu Mar 16 01:40:19 2023, 510 bytes "flag"
strikingsoul@ramones:~/Downloads/filetype$ mkdir extracted
strikingsoul@ramones:~/Downloads/filetype$ cd extracted/
strikingsoul@ramones:~/Downloads/filetype/extracted$ cpio -iv < ../flag 
flag
2 blocks
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag 
flag: bzip2 compressed data, block size = 900k
strikingsoul@ramones:~/Downloads/filetype/extracted$ bunzip2 flag
bunzip2: Can't guess original name for flag -- using flag.out
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag.out 
flag.out: gzip compressed data, was "flag", last modified: Thu Mar 16 01:40:19 2023, from Unix, original size modulo 2^32 328
strikingsoul@ramones:~/Downloads/filetype/extracted$ gunzip flag.out
gzip: flag.out: unknown suffix -- ignored
strikingsoul@ramones:~/Downloads/filetype/extracted$ ls
flag.out
strikingsoul@ramones:~/Downloads/filetype/extracted$ mv flag.out flag.gz
strikingsoul@ramones:~/Downloads/filetype/extracted$ gunzip flag.out
gzip: flag.out.gz: No such file or directory
strikingsoul@ramones:~/Downloads/filetype/extracted$ gunzip flag.gz
strikingsoul@ramones:~/Downloads/filetype/extracted$ ls
flag
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag 
flag: lzip compressed data, version: 1
strikingsoul@ramones:~/Downloads/filetype/extracted$ lunzip flag 
strikingsoul@ramones:~/Downloads/filetype/extracted$ ls
flag.out
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag.out 
flag.out: LZ4 compressed data (v1.4+)
strikingsoul@ramones:~/Downloads/filetype/extracted$ mv flag.out flag.lz4
strikingsoul@ramones:~/Downloads/filetype/extracted$ lz4 -d flag.lz4 
Decoding file flag 
flag.lz4             : decoded 264 bytes 
strikingsoul@ramones:~/Downloads/filetype/extracted$ ls
flag  flag.lz4
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag
flag: LZMA compressed data, non-streamed, size 253
strikingsoul@ramones:~/Downloads/filetype/extracted$ unlzma flag
unlzma: flag: Filename has an unknown suffix, skipping
strikingsoul@ramones:~/Downloads/filetype/extracted$ mv flag flag.lzma
strikingsoul@ramones:~/Downloads/filetype/extracted$ unlzma flagunlzma: flag: No such file or directory
strikingsoul@ramones:~/Downloads/filetype/extracted$ unlzma flag.lzma
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag
flag: lzop compressed data - version 1.040, LZO1X-1, os: Unix
strikingsoul@ramones:~/Downloads/filetype/extracted$ mv flag flag.lzo
strikingsoul@ramones:~/Downloads/filetype/extracted$ lzop -d flag.lzo
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag
flag: lzip compressed data, version: 1
strikingsoul@ramones:~/Downloads/filetype/extracted$ lunzip flag
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag
flag: cannot open `flag' (No such file or directory)
strikingsoul@ramones:~/Downloads/filetype/extracted$ ls
flag.lz4  flag.lzo  flag.out
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag.out
flag.out: XZ compressed data, checksum CRC64
strikingsoul@ramones:~/Downloads/filetype/extracted$ mv flag.out flag.xz
strikingsoul@ramones:~/Downloads/filetype/extracted$ unxz flag.xz
strikingsoul@ramones:~/Downloads/filetype/extracted$ file flag
flag: ASCII text
strikingsoul@ramones:~/Downloads/filetype/extracted$ cat flag
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f39353063346665657d0a
strikingsoul@ramones:~/Downloads/filetype/extracted$ cat flag | xxd -r -p
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee}
```

Basically, the file was archived using layering. There's the layer and the step
1. shar (or shell archive), use `sh` command to run the file. If there was an error, install `sharutils` package
2. ar, use `ar -x` command to extract
3. cpio, make a new directory, cd to that new directory and run `cpio -iv < ../flag`
4. bzip2, use `bunzip2` command to extract
5. gzip, use `gunzip` command to extract, append .gz to the file extension if there was an error
5. lzip, use `lunzip` command to extract, install `lunzip` package if there was an error
6. lz4, use `lz4 -d` command to decode, install `lz4` package if there was an error
7. lzma, use `unlzma` command to extract
8. lzop, use `lzop -d` command to decode, append .lzo to the file extension
9. lzip
10. xz, use `unxz` command to extract, append .xz to the file extension
12. Convert the flag content from hex to plain text

Here's the final flag `picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee}`
