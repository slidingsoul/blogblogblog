---
date: '2025-12-30T10:56:32+07:00'
title: 'picoCTF - Tapping'
draft: false
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/21
- Title: Tapping
- Tags: Medium, Cryptography, picoCTF 2019
- Author: DANNY
- _Started: 27 July 2025_
- _Solved: 27 July 2025_
- Description: Theres tapping coming in from the wires.
Additional details will be available after launching your challenge instance.

I started the instance, and copied this `nc` command snippet.

![alt text](image.png)

The host returned this information.

```
buddyhearto-picoctf@webshell:~$ nc fickle-tempest.picoctf.net 53806
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. -.-. ----. .---- ..-. -.... ..--- ----- -.... } 
```

In primary school, I used to memorize _morse code_, but now I can just use online translator at this point. This is the first part before `{`
![alt text](image-1.png)
And this is the part encapsulated within `{}`
![alt text](image-2.png)

The final flag is

```PICOCTF{M0RS3C0D31SFUNC91F6206}```