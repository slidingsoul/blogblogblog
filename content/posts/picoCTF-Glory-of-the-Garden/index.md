---
date: '2026-01-27T09:21:34+07:00'
title: 'picoCTF - Glory of the Garden'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/44
- Title: Glory of the Garden
- Tags: Easy, Forensics, picoCTF 2019
- Author: jedavis/Danny
- _Started: 15 July 2025_
- _Solved: 15 July 2025_
- Description: 
> This file contains more than it seems. Get the flag from [garden.jpg](https://challenge-files.picoctf.net/c_fickle_tempest/19722024edeecca10f263776ab05c8b1235b136dcf25aa6e976d3860513ffcd5/garden.jpg).

After downloading the file, I checked the hexdump value using `xxd` command.

```
strikingsoul@ramones:~/Downloads$ xxd garden.jpg | tail
00230500: d9f9 9f63 4b2b c1e5 daf2 7b59 db49 4ba3  ...cK+....{Y.IK.
00230510: f43e b881 5e30 1060 8030 47d6 bacb 58cb  .>..^0.`.0G...X.
00230520: 1046 07b5 7216 df7e 5ff7 c576 363f ebab  .F..r..~_..v6?..
00230530: b70d 18ce 3ccd 6a7e 6b8d af56 b579 39ca  ....<.j~k..V.y9.
00230540: eeef 53ae 8620 31b8 751f 9514 f7fb cff5  ..S.. 1.u.......
00230550: a2bb bdac 9687 98e4 d3b2 e87f ffd9 4865  ..............He
00230560: 7265 2069 7320 6120 666c 6167 3a20 7069  re is a flag: pi
00230570: 636f 4354 467b 6d6f 7265 5f74 6861 6e5f  coCTF{more_than_
00230580: 6d33 3374 735f 7468 655f 3379 3337 6664  m33ts_the_3y37fd
00230590: 6538 3839 317d 0a                        e8891}.
```

Voila, here's the a flag: `picoCTF{more_than_m33ts_the_3y37fde8891}`. To make copy-pasting easier, `strings` command can also be used

```
strikingsoul@ramones:~/Downloads$ strings garden.jpg | tail -n 1
Here is a flag: picoCTF{more_than_m33ts_the_3y37fde8891}
```