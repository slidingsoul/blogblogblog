---
date: '2026-01-28T13:52:18+07:00'
title: 'picoCTF - basic-mod1'
tags: ["ctf"]
draft: true
---

- URL: https://play.picoctf.org/practice/challenge/253
- Title: basic-mod1
- Tags: Medium, Cryptography, picoCTF 2022
- Author: WILL HONG
-  _Started: 24 July 2025_
-  _Solved: 24 July 2025_
- Description:
> We found this weird message being passed around on the servers, we think we have a working decryption scheme. Download the message [here](https://artifacts.picoctf.net/c/129/message.txt). Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore. Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)