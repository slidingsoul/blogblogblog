---
date: '2026-01-26T12:27:52+07:00'
title: 'picoCTF - So Meta'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/19
- Title: So Meta
- Tags: Medium, Forensics, picoCTF 2019
- Author: Kevin Cooper/Danny
- _Started: 19 July 2025_
- _Solved: 19 July 2025_
- Description: Find the flag in this picture.

It is the same as [this problem](../picoctf-canyousee/) and [this one](../picoctf-information/) but instead of encoded in base64, it's hidden in plain sight

```
strikingsoul@ramones:~/Downloads$ exiftool pico_img.png 
ExifTool Version Number         : 12.76
File Name                       : pico_img.png
Directory                       : .
File Size                       : 109 kB
File Modification Date/Time     : 2026:01:26 12:29:49+07:00
File Access Date/Time           : 2026:01:26 12:29:49+07:00
File Inode Change Date/Time     : 2026:01:26 12:29:49+07:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Artist                          : picoCTF{s0_m3ta_9a8b5aa1}
Image Size                      : 600x600
Megapixels                      : 0.360
```

The flag is `picoCTF{s0_m3ta_9a8b5aa1}`