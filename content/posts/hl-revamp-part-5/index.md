+++
date = '2025-06-27T11:20:23+07:00'
draft = false
title = 'Home Lab Revamp Part 5'
tags = ['indonesia', 'homelab']
+++
## Pengantar
Saya masih membutuhkan bantuan SFTP dan FileZilla untuk memindahkan film-film yang ada di harddisk PC ke harddisk dari Renner atau lebih tepatnya Aurelia (container untuk Jellyfin). Rencana awalnya saya ingin membuat skrip untuk mengautomatisasi pengunduhan film, jadi saya tinggal memasukkan URL sebagai argumen yang bisa langsung terunduh di Aurelia tanpa perlu membiarkan PC saya menyala untuk menunggu unduhan selesai. Namun, ternyata ada beberapa film yang unduhannya dijaga oleh CAPTCHA. Untuk itu saya masih perlu membuktikan bahwa saya adalah manusia (😬) sebelum mengunduh. 

Oleh karena itu untuk mempermudah pemindahan dan juga unduhan. Saya ingin mengatur Server Message Block atau SMB pada Aurelia. SMB memungkinkan adanya Drive baru yang bisa saya akses di section network pada File Explorer Windows, jadi sewaktu saya mengunduh, saya bisa langsung browse ke drive itu dan mengunduhnya langsung ke Aurelia. Saya tidak perlu mengunduh di PC dahulu, dan memindahkannya ke Aurelia via SFTP.

![alt text](image.png)

## Konfigurasi
Saya menemukan [tutorial](https://www.atlantic.net/vps-hosting/how-to-create-samba-share-on-ubuntu/) yang menunjukkan cara untuk konfigurasi dan saya ikuti.

Sewaktu saya ingin start service untuk smbd dan nmbd, saya mendapat error tetapi jika saya mengecek statusnya ternyata sudah running. Saya telan saja itu

![alt text](image-1.png)

Instead of following the tutorial editing smb.conf, saya memutuskan untuk memodifikasinya sedikit menjadi seperti ini

![alt text](image-2.png)

`
[Private]
comment = film share
path = /mnt/storage/
browseable = yes
guest ok = yes
writable = yes
valid users = @samba
`

Setelah itu saya membuat group baru bernama samba dan menambahkan jello ke group samba

![alt text](image-3.png)

Namun saat saya coba mengatur access list dari /mnt/storage saya mendapatkan permission denied, padahal sudah root.

![alt text](image-4.png)

Oke setelah menjalankan command di bawah ini

![alt text](image-5.png)

Saatnya saya coba hubungkan File Explorer ke Samba

Klik kanan di bagian Network lalu klik Map Network Drive, dan kita mendapatkan pop-up seperti ini

![alt text](image-6.png)

Yang perlu saya masukkan adalah abjad dari drive dan IP Address serta private dengan format sebagai berikut

`\\{ip-address}\private`

![alt text](image-7.png)

Lalu kita diminta memasukkan username dan juga password dari samba yang sudah kita atur dengan smbpasswd tadi

![alt text](image-8.png)

## Hasil

![alt text](image-9.png)

Saya bisa mengakses /mnt/storage yaitu harddisk yang saya beli kemarin via SMB. Bahkan file-nya bisa saya akses dengan baik

![alt text](image-10.png)

![alt text](image-11.png)

YESS!

Sekarang mari kita coba untuk pindahkan 1 folder

![alt text](image-12.png)

ke folder "Enggres"

![alt text](image-13.png)

Speed-nya bakal agak lama karena mengikuti speed dari jaringan rumah saya, which is fineee

OK, ini prosesnya sudah selesai dan memakan waktu sekitar 10 sampai 12 menit dengan kecepatan 5 MB/s

![alt text](image-14.png)

Sekarang karena ini ada di folder "Enggres" dan saya belum setup folder itu di Jellyfin, saya akan tunjukkan setupnya bagaimana

Di interface Jellyfin, kita pergi ke setting, klik libraries lalu klik pilihan dropdown pertama

![alt text](image-16.png)

Klik add media library

![alt text](image-15.png)

Masukan tipe konten dan namanya

![alt text](image-17.png)

*Ini yang paling penting*. Klik folder dan masukkan path yang betul. Untuk kasus ini adalah /mnt/storage/enggres

![alt text](image-18.png)

Dan akhirnya, Fight Club sudah dideteksi sama Jellyfin

![alt text](image-19.png)

![alt text](image-20.png)

## Kesimpulan
Saya sekarang bisa dengan mudah drag'n'drop dari File Explorer ke PC dengan SMB dan kalau saya mau download di PC saya bisa langsung browse ke SMP jadi tidak perlu pakai FileZilla untuk SFTP lagi. Thank you yang sudah baca, ciao.