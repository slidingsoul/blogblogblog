---
date: '2026-01-26T12:17:10+07:00'
title: 'picoCTF - CanYouSee'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/408
- Title: CanYouSee
- Tags: Easy, Forensics, picoCTF 2024, browser_webshell_solvable
- Author: Mubarak Mikail
- _Started: 15 July 2025_
- _Solved: 15 July 2025_
- Description: How about some hide and seek? Download this file here. 

After downloading the file, I unzipped it.

```
strikingsoul@ramones:~/Downloads$ unzip unknown.zip 
Archive:  unknown.zip
  inflating: ukn_reality.jpg 
```

The archived file contains only one .png file. This is the image

![alt text](ukn_reality.jpg)

Looks cool! First, I used exiftool to check the image

```
strikingsoul@ramones:~/Downloads$ exiftool ukn_reality.jpg 
ExifTool Version Number         : 12.76
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:03:12 07:05:57+07:00
File Access Date/Time           : 2026:01:26 12:19:44+07:00
File Inode Change Date/Time     : 2026:01:26 12:18:41+07:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4
```

Focus on the attribution URL, it looked like it's a base64 encoded message

```
strikingsoul@ramones:~/Downloads$ echo cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg== | base64 --decode
picoCTF{ME74D47A_HIDD3N_d8c381fd}
```

Well, it was! Here's the flag

`picoCTF{ME74D47A_HIDD3N_d8c381fd}`

I got to remember to check file metadata for any info while doing forensics.