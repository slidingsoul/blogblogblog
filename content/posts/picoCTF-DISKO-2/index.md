---
date: '2026-01-27T09:22:23+07:00'
title: 'picoCTF - DISKO 2'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/506
- Title: DISKO 2
- Tags: Medium, Forensics, picoGym Exclusive
- Author: Darkraicg492
- _Started: 15 July 2025_
- _Solved: 15 July 2025_
- Description: 
> Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone! Download the disk image [here](https://artifacts.picoctf.net/c/539/disko-2.dd.gz).

This one is similar to [DISKO1](../picoctf-disko-1/) with extra steps.

After downloading and inflating, I checked the disk image using `fdisk -l`

```
strikingsoul@ramones:~/Downloads$ fdisk -l disko-2.dd 
Disk disko-2.dd: 100 MiB, 104857600 bytes, 204800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x8ef8eaee

Device      Boot Start    End Sectors Size Id Type
disko-2.dd1       2048  53247   51200  25M 83 Linux
disko-2.dd2      53248 118783   65536  32M  b W95 FAT32
```

According to the description, I had to grab the linux partition.

```
strikingsoul@ramones:~/Downloads$ dd if=disko-2.dd of=flag.dd bs=512 skip=2048 count=51200
51200+0 records in
51200+0 records out
26214400 bytes (26 MB, 25 MiB) copied, 0.0801104 s, 327 MB/s
```

if denotes input file, of is output file, bs is block size (normally 512kB), we skip to the starting sector of Linux which is 2048 and count for 51200 sectors.

After that, I could just use `strings` command

```
strikingsoul@ramones:~/Downloads$ strings flag.dd | grep CTF
picoCTF{4_P4Rt_1t_i5_90a3f3d1}
Generate CTF debug information at default level.
MIIEogIBAAKCAQEA7UtSJPeCTF+m2SQKy+sT3XRGb8oQMr+QRSkicJvjY7xkDUdI
```

The flag is `picoCTF{4_P4Rt_1t_i5_90a3f3d1}`