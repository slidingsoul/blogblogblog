+++
date = '2025-06-18T00:17:11+07:00'
draft = true
title = 'Home Lab Revamp'
tags = ['indonesia', 'it']
+++
## Dibuat di Surga
Aku memutuskan untuk merombak _setup_ home-lab ku. Kenapa? Karena ada banyak conflict antara service yang berjalan. Aku mencoba memasang Pi-Hole untuk eksperimen DNS dan _Ad-Blocker_ tapi ternyata itu conflict dengan Apache Web Server. Aku tidak mau mematikan Apache karena FreshRSS, Nextcloud berjalan di atas itu. 

Alasan yang kedua adalah aku ingin melakukan ekspansi untuk _storage_. Thinkpad X260 serverku sekarang memiliki "hanya" 128 GB. Aku berencana untuk membuat SMB dan memindahkan banyak film dari PC-ku (sekitar 87.7 GB, 56 film) untuk ditonton dengan streaming via Jellyfin. _Kenapa engga streaming pakai website biasa aja?_ Jawabannya karena ada risiko bakal patah-patah. Aku juga berencana melakukan banyak hal seperti mendownload otomatis film via _torrent_ ke serverku jadi aku tidak perlu menyalakan PC-ku dan menunggu proses _download_ selesai. 

_Post_ ini adalah bentuk dari dokumentasi dalam proses perombakan ini.

## X260
Mari kenalan dulu sama _lappy_ yang bakal kuoprek. Dia akan kuberi nama, "RENNER" yang artinya pelari (dari bahasa Jerman) dan nama itu bersifat palindrom (dibaca dibalik tetap RENNER). Dia adalah Thinkpad X260 yang kubeli 27 Desember 2021. Waktu itu aku ada di kampung halaman, cuma punya PC dan PC-ku ada di kota aku kuliah😢. Karena mati bosan aku memutuskan untuk membeli laptop yang "murah". Berikut penampakan si doi.

![](./komuk.jpg)

### Sejarah X260
Sedikit _flashback_, Aku kurang puas dengan _layout_ _keyboard_ Jepang-nya. Jadi aku beli lagi keyboard khusus untuk _layout_ US, tapi karena aku terlalu tengil jadi keycap untuk _backspace_ jadi lepas dan aku engga tahu cara benerinnya.

![](./keyboard-us.jpg)

Setelah beberapa bulan beli, aku kembali kuliah dan laptop ini jadi tidak terpakai. Aku memutuskan untuk meminjamkannya ke sahabatku. Setelah dipakai beberapa semester, laptopnya rusak...keyboard-nya ngetik sendiri sama ada beberapa _keys_ yang tidak berfungsi. Sudah tertekan tetapi dia tidak mau merespon. Sahabatku beli laptop baru dan kembaliin si RENNER.

Aku kira aku masih bisa pakai RENNER sebagai laptop (bisa dibawa ke warkop). Tapi setelah aku coba ganti _keyboard_ ke Jepang lagi ternyata masalahnya di konektor😫. Bisa sih pakai _keyboard_ eksternal tapi yang aku ga suka itu _ghost click_ nya, tiba-tiba bisa ngespam YYYYYYYYYYYYYYYYYYYYYYYYYY tiada aliran elektron tiada tekanan jari manusia.

### Kondisi

I/O keyboard ini cukup lengkap, di bagian kanan ada

![](./kanan.jpg)

- _Audio combo jack_
- _USB A 3.0_ (support _Always on_)
- _SD Card Reader_
- _Port RJ45_
- _Kensington Lock_
- _Slot SIM card_ (aku cukup takjub dengan adanya ini, soalnya ini cuma ada di laptop kelas bisnis)


Di bagian kiri ada

![](./kiri.jpg)

- _DC jack_
- _HDMI port_
- _Mini Display Port_
- 2 _USB A 3.0_

Namun sayangnya ada sedikit masalah di skrup bagian kanannya. Skrupnya tidak mampu melekatkan bodi atas dan bawah sehingga ada sedikit celah seperti ini

![](./skrup_rusak.gif)

RENNER masih bisa nyala dan bisa kugunakan sebagai bahan _homelab_, aku bersyukur untuk itu.

Ini adalah spesifikasi hardware singkat dari RENNER

![](./neofetch.png)

Sedikit tambahan kalau RENNER sebenarnya punya slot M.2 SATA tapi engga kepake dan untuk _booting_ dia pakai SSD SATA 2.5 _inch_ 128 GB.

## Memilih OS

Sebelumnya, aku menggunakan Lubuntu 24 untuk OS _homelab_ ku. Saat itu aku belum tahu tentang Proxmox. Sebuah OS yang memungkinkan virtualisasi VM dan Container. Dengan Proxmox aku tidak perlu takut dengan terjadinya _conflict_ seperti yang aku ceritakan sebelumnya. Aku kenal Proxmox dari [video ini](https://youtu.be/cMVcclMkp7g?si=o5Eu6_09dNmtT5gg&t=443). Saatnya kita mulai instalasi

1. Aku kunjungi situs resminya dan memilih Proxmox VE (_Virtual Environment_) untuk di-download. Pada waktu aku menulis ini, aku sedang menunggu prosesnya selesai.
2. Ambil _flashdisk_ engga kepake trus buat jadi _bootable_ USB dengan ISO yang baru di-download. Di sini aku pakai Rufus
![alt text](image.png)

Aku kaget karena aku dapet _warning_ kalau bakal pakai DD image (aku engga tahu apa itu, dan rasanya sejauh ini aku buat _Bootable_ USB) engga pernah pakai itu

![alt text](image-1.png)

Setelah kucari ternyata [ini bedanya](https://github.com/pbatard/rufus/issues/843)
Oke...dan pas aku klik ternyata aku engga bisa akses USB-nya dan USB-nya jadi 2 partisi

![alt text](image-2.png)

Dan aku juga engga bisa akses F: dan G: (kedua partisi USB itu)
![alt text](image-3.png)

Jawabannya juga ada [di sini](https://github.com/pbatard/rufus/issues/843)
> But this can also be one of the drawbacks, as it means you will usually find that you cannot access the content of your USB any longer after it has been created.
Itu menjelaskan kenapa.
3. Sekarang aku perlu colok aja USB ini ke RENNER dan install Proxmox-nya. Aku udah lihat [video tutorial ini](https://www.youtube.com/watch?v=_u8qTN3cCnQ) dan kelihatannya tidak begitu buruk.

## Proxmox Setup
Jadi langsung saja aku masuk ke _boot option_ dan memilih _flashdisk_ untuk di-_boot_

![](./boot_option.jpeg)

Lalu aku disuguhkan Welcome Screen yang langsung kupilih _graphical installation_

![](./welcome.jpeg)

Seperti instalasi _software_ lainnya aku juga disuguhkan EULA

![](./eula.jpeg)

Setelah itu aku diminta untuk memilih _harddisk_ instalasi dan aku melihat tombol _options_

![](./harddisk.jpeg)

Oke di menu ini ada beberapa size yang bisa kita tentukan, penjelasan dari hdsize, minroot, swapsize, minfree, dan maxvz dapat ditemukan [di sini](https://www.reddit.com/r/Proxmox/comments/1bpfiaj/question_about_disk_sizes/)

Kurang lebih artinya begini
- hdsize: ukuran dari harddisk yang ingin digunakan untuk **semua** partisi
- swapsize: kapasitas memori swap (_virtual memory_) untuk partisi ini
- minroot: ukuran dari partisi OS
- minfree: ukuran dari harddisk yang tidak boleh digunakan
- maxvz: ukuran untuk disk VM, dan kawan-kawan

Aku biarkan kosong saja

Lalu aku ditunjukkan halaman untuk konfigurasi jaringan

![](./network_example.jpeg)

Aku coba cari-cari tentang apa itu _hostname_, ternyata [bisa aku awur](https://forum.proxmox.com/threads/hostname-fqdn-huh.63667/), yang penting masuk saja. Berikut adalah konfigurasiku

![](./network.jpeg)

Akhirnya aku ditunjukkan ringkasan tentang Proxmox yang kubuat dan ini hasilnya

![](./summary.jpeg)

Dan setelah reboot, aku bisa login. Dan _seharusnya_ aku bisa akses Proxmox dari IP address port 8006

![](./login.jpeg)

Dan saat kucoba akses 192.168.18.78:8006, lihat apa yang terjadi

![alt text](./timed_out.jpg)

Saat aku coba `ping` juga tidak dapat sampai

![alt text](./ping_failed.jpg)

Lalu aku sadar...aku belum menghubungkannya ke Wi-Fi, bruh. Setelah aku mencari-cari aku menemukan [situs ini](https://www.x88.in/proxmox-with-wifi) dan aku langsung edit `/etc/network/interfaces` dengan menambahkan `wpa-essid` dan `wpa-psk` menjadi seperti ini

![](./config.jpeg)

Dan setelah aku reboot dan aku coba ping 1.1.1.1 ternyata masih tidak bisa. Aku coba ping PC-ku juga tidak bisa😔. Setelah sekian lama mencari ternyata menggunakan Wi-Fi tidak disarankan

> Avoid using WLAN if possible, it has several technical limitations making it not really suitable as single interface of a hyper-visor like PVE. 

Oke...aku memutuskan untuk berhenti di sini karena aku tidak punya kabel LAN.