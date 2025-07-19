+++
date = '2025-07-14T22:27:28+07:00'
draft = false
title = 'PicoCTF'
tags = ['english', 'it']
+++
## **SPOILER**
I don't recommend you read this article before you _actually_ try to solve some of the problems! Try your best first dude. You won't learn anything if you just jump to the answer without any thinking.

## Flag
Here's my write-up of my solutions when I try to solve some of PicoCTF's problems. You can use `Ctrl+F` to search. I will try my best to explain my thought process. I actually solved some of them but I want to document my solution so that people know. The flag will be in the form of picoCTF{flag}.

I'll try to solve the easy ones.

## IN RANDOM ORDER

### DISKO 1, Started and Finished 7 July 2025
We're challenged to find the flag in a disk image. To download the disk image, we use `wget` command and put in the url.

![alt text](image.png)

As we can see, the disk image is in the format of `dd.gz` to it's compressed in a gzip format. First, I think we should try to unzip it.

![alt text](image-1.png)

And I happened to know that we can use `strings` command to find human-readable string in a byte-type file

![alt text](image-2.png)
### Fantasy CTF, Started and Finished 7 July 2025
First, I tried to run the command provided.

![alt text](image-3.png)

I was shown a story...I'll try to follow along. And after trials and errors, it gives me the flag

![alt text](image-4.png)

### RED, Started and Finished 7 July 2025

So I downloaded the `red.png` and checked the metadata

![alt text](image-5.png)

What? A poem? I tried to list all capital letters which gave me "CHECK LSB". I searched for "lsb in image" and DuckDuckGo returned results about Least Significant Bit

![alt text](image-6.png)

I went to Cyberchef and put `Extract LSB` to my recipe. From the hint, `Red?Ged?Bed?Aed?` it's provided that the color pattern is RGBA

![alt text](image-7.png)

I noticed that from the output there's a repeating pattern. I suspect that it's a Base64

![alt text](image-8.png)
### rust fixme 1, Started 7 July 2025, Finished 9 July 2025
I downloaded the file using wget and extracted it using gunzip and tar

![alt text](image-9.png)

![alt text](image-10.png)

OK, but first we have to install Rust, just follow the instruction from [this page](https://www.rust-lang.org/tools/install)

![alt text](image-11.png)

Great, the errors are displayed. Now it's time to edit. I added a semicolon, corrected "return" statement, and fixed println. Unfortunately my VM in homelab ran out of memory and I had to fix reboot it. We're back to VM in my PC because well...my homelab has insufficient RAM.

I'm back, let's continue. From my little programming experience (C mainly), I had to make sure that every line ends with semicolon (;), if we want to exit from a function use "return". For the println part, I searched and found that I had to use curly braces ({}). To compile, execute `cargo build` in the working directory and the compiled file is in `./target/debug`.

![alt text](image-12.png)

### rust fixme 2, Started 9 July 2025
First, the spadework just like _rust fixme 1_

![alt text](image-13.png)

I like to build/compile the project and then see the errors.

![alt text](image-14.png)

And from the errors we got the hint. I fixed some of them. Another error.

![alt text](image-15.png)

(To be continued)

### Binary Search, Started and Finished 9 July 2025

I immediately ssh'ed to the instance. I had to guess a number ranging from 1 to 1000 under 10 guesses. Hinted from the title, I had to add the upper range and lower range and divide it by 2, effectively doing a Binary Search.

![alt text](image-16.png)

Now we do between 1 and 500

![alt text](image-17.png)

Fast forward, it took me 10 guesses, whew

![alt text](image-18.png)

### WebDecode, Started and Finished 9 July 2025

I was given a website and I had to find it using web inspector just like the detail of the problem suggested. I tried inspecting `index.html` and found nothing. But something caught my eye in `about.html`

![alt text](image-19.png)

Yeah it must be base64 again.

![alt text](image-20.png)

### Ph4nt0m 1ntrud3r, Started and Finished 14 July 2025

I was given a PCAP file and it's about network traffic. I didn't know a damn thing about it but from my conscience I knew it has something to do with Wireshark. So I opened it in Wireshark.

![alt text](image-21.png)

From the hint, it's all about time so I sorted it by time and starts decoding the last part of each payload _from the bottom_ and I got this

![alt text](image-22.png)

And it's suspiciously a base64 and I decoded it with cyberchef and got the flag

![alt text](image-23.png)

### Verify, Started and Finished 14 July 2025

I ssh'ed into the server and utilized the hints. Now I know that checksum and SHA256 is used the verify integrity of a file.

`sha256sum ./checksum.txt ./files/*`

Now I can view all the checksum from all files now I have to find one with the correct checksum, a file which checksum matches the content of checksum.txt. Grep to the rescue

![alt text](image-24.png)

### Scan Surprise, Started and Finished 15 July 2025

I just downloaded the zip, extracted it, and scan the flag.png using online scanner

![alt text](image-25.png)

### Secret of the Polyglot, Started and Finished 15 July 2025

I downloaded the .pdf file and from the description `they're getting conflicting information on what type of file it is` I checked using `file` command.

![alt text](image-26.png)

I decided to copy the file and changed the file extension.

![alt text](image-27.png)

### CanYouSee, Started and Finished 15 July 2025

I downloaded the .zip file and extracted it, the result is a single .png file named "ukn_reality". My instinct says to check the metadata.

![alt text](image-28.png)

Another base64!

![alt text](image-29.png)

### information, Started and Finished 15 July 2025

Similar to the previous "CanYouSee" but now it's in the license field

![alt text](image-30.png)

![alt text](image-31.png)

### Glory of the Garden, Started and Finished 15 July 2025

The spadework is similar to _information_ but this time I used "To Hexdump" in Cyberchef and use the image as input

![alt text](image-32.png)

### DISKO 2, Started and Finished 15 July 2025

I downloaded the disk and checked it using `fdisk -l` command

![alt text](image-33.png)

From the challenge description, it looked like the flag is in the Linux partition so I extracted it using dd command

![alt text](image-34.png)

if denotes input file, of is output file, bs is block size (normally 512kB), we skip to the starting sector of Linux which is 2048 and count for 51200 sectors.

### flags are stepic, Started and Finished 16 July 2025

I started the instance and checked the hint...okay so I had to use my geography knowledge for this one :P. And I found this flag

![alt text](image-35.png)

There's no nation named Upanzi and it's actually a research network in Africa by CMU :\). I downloaded the image and found that I had to use a python library called "Stepic" to decrypt the message. Here's my script

![alt text](image-36.png)

![alt text](image-37.png)

### Event-Viewing, Started and Finished 16 July 2025

I downloaded the .evtx file and browsed a little bit to gain knowledge :P. Eventually I found [this site](https://exploit-notes.hdks.org/exploit/windows/forensics/windows-xml-eventlog/)

I parsed the event log to .xml instead of .txt

![alt text](image-38.png)

There were about 8000 records and from the description I had to find 3 correct records. I'm kind of damned. From the description I knew that there should be an event ID associated with program installation. I searched a bit and [found 11707](https://learn.microsoft.com/en-us/answers/questions/983008/eventid-that-logs-software-installation-on-worksta). And just below the first 11707 (the next record), I found the first part of the flag, encoded in base64

![alt text](image-39.png)

I decided to change the search (Ctrl+F) query to `Totally_Legit_Software` and after some clicking found the second part. 

![alt text](image-40.png)

I changed the search query to `shutdown` and finally found the third part!

![alt text](image-41.png)

### Find and Open, Started and Finished 16 July 2025

This one is kind of tricky...no, very tricky. I imported the .pcap file to WireShark and found this suspicious packet

![alt text](image-42.png)

![alt text](image-43.png)

And all I had to do was to put half of the flag as password to extract flag.zip

![alt text](image-44.png)

### File types, Started and Finished 17 July 2025

This one is troublesome. Flag.pdf can't be opened by normal pdf viewer

![alt text](image-45.png)

Actually it's a .shar file

![alt text](image-46.png)

I extracted it and the flag is still nested. Here's the plan, I'll show you my terminal and explain it afterwards.

![alt text](image-47.png)

![alt text](image-48.png)

![alt text](image-49.png)

![alt text](image-50.png)

![alt text](image-51.png)

![alt text](image-52.png)

![alt text](image-53.png)

![alt text](image-54.png)

FINALLY!

![alt text](image-55.png)

![alt text](image-56.png)

So basically the flag is nested and compressed many times to different format each time. What I did is extracted it to the purest form. I opened this many tabs to find the commands ROFL.

![alt text](image-57.png)

### Enhance!, Started and Finished 18 July 2025

I downloaded the image and used Firefox, found this

![alt text](image-58.png)

### extensions, Started and Finished 19 July 2025

Just change the extension from .txt to .png dude. You also can check using file command.

![alt text](image-59.png)

### So Meta, Started and Finished 19 July 2025

I just...checked the metadata

![alt text](image-60.png)

### What Lies Within, Started and Finished 19 July 2025

This time I used Cyberchef and from the image I immediately knew it was a stego.

![alt text](image-61.png)

### St3g0, Started and Finished 19 July 2025

Similar to what lies within.

![alt text](image-62.png)

