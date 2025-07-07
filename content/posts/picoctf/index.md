+++
date = '2025-07-07T12:02:41+07:00'
draft = true
title = 'PicoCTF'
tags = ['english', 'it']
+++
## Flag
Here's my write-up of my solutions when I try to solve some of PicoCTF's problems. You can use `Ctrl+F` to search. I will try my best to explain my thought process. I actually solved some of them but I want to document my solution so that people know. The flag will be in the form of picoCTF{flag}.

## Easy
I'll try to solve the easy ones.
### DISKO 1, 7 July 2025
We're challenged to find the flag in a disk image. To download the disk image, we use `wget` command and put in the url.

![alt text](image.png)

As we can see, the disk image is in the format of `dd.gz` to it's compressed in a gzip format. First, I think we should try to unzip it.

![alt text](image-1.png)

And I happened to know that we can use `strings` command to find human-readable string in a byte-type file

![alt text](image-2.png)
### Fantasy CTF, 7 July 2025
First, I tried to run the command provided.

![alt text](image-3.png)

I was shown a story...I'll try to follow along. And after trials and errors, it gives me the flag

![alt text](image-4.png)

### RED, 7 July 2025

So I downloaded the `red.png` and checked the metadata

![alt text](image-5.png)

What? A poem? I tried to list all capital letters which gave me "CHECK LSB". I searched for "lsb in image" and DuckDuckGo returned results about Least Significant Bit

![alt text](image-6.png)

I went to Cyberchef and put `Extract LSB` to my recipe. From the hint, `Red?Ged?Bed?Aed?` it's provided that the color pattern is RGBA

![alt text](image-7.png)

I noticed that from the output there's a repeating pattern. I suspect that it's a Base64

![alt text](image-8.png)
### rust fixme 1, WIP
I downloaded the file using wget and extracted it using gunzip and tar

![alt text](image-9.png)

![alt text](image-10.png)

OK, but first we have to install Rust, just follow the instruction from [this page](https://www.rust-lang.org/tools/install)

![alt text](image-11.png)

Great, the errors are display. Now it's time to edit. I added a semicolon, corrected "return" statement, and fixed println. Unfortunately my VM in homelab ran out of memory and I had to fix reboot it. We're back to VM in my PC because well...my homelab has insufficient RAM (To be continued).