---
date: '2025-09-01T11:05:37+07:00'
title: 'Password Management'
draft: true
tags: ['indonesia', 'homelab']
---
Dulu, pas gue masih kecil, akun gue sedikit. Paling juga akun email dan Facebook. Gue ga terlalu memusingkan tentang password karena gue bisa inget (dulu bahkan gue pakai 1 password di banyak akun). Fast forward ke 2025, zaman berubah. Gue udah punya banyak akun online service mulai dari social media (IG, LinkedIn, Bluesky, Hardcover, Letterboxd), MOOC (Udemy, Coursera), E-Commerce (Tokopedia, Shopee), dan masih banyak lagi. Gue udah jadi cyber-security aware sekarang dan menganggap bahwa password harus beda di antara 1 akun dengan yang lainnya agar ketika 1 akun _compromised_, yang lain tetap bisa aman.

Dan gue pun bingung. Gimana caranya supaya gue bisa store password dengan aman? Ada beberapa cara yang pernah gue dulu lakukan dan gue harap elu engga melakukan hal yang sama
1. Simpen 1 file yang namanya passwords.txt atau passwords.md yang isinya nama akun dan passwordnya. Jangan sampai file ini terupload ke internet, simpan aja di local. This was a bad practice karena bisa aja ada shoulder-surfer atau perangkat gue kena bajak.
2. Pakai Anki (yes, that cursed weeb software) untuk mengingat password dengan menjadikannya suatu deck. This was also a bad practice karena essentially sama kayak nomor 1 dan gue tetep aja kelupaan buat password di akun-akun yang jarang gue pake tetapi secara tiba-tiba butuh.

Itu yang buruknya ya, sekarang gue kasi tahu cara yang bagus dan gue saranin elu tiru.
1. Pakai password manager. Gue dulu pakainya Bitwarden. Jadinya gue buat akun di situ, set email sama master password, dan import semua passwords gue. Semua passwordnya bakal di-encrypt dan butuh master password untuk encrypt itu.

Menggunakan Bitwarden sangat memudahkan hidup gue dan membuat gue merasa lebih aman. Namun, di sisi lain gue masih pengen supaya password gue engga bertebaran di internet dan dipegang oleh satu entitas. Oleh karena itu sekarang gue pakai KeePassXC. Prinsip kerjanya sama kayak Bitwarden tapi local. Semua password gue sekarang disimpen di 1 database (.kdbx).

Namun ada saat di mana gue butuh password itu di perangkat lain. File .kdbx itu sekarang ada di laptop dan bisa aja gue butuh aksesnya di komputer atau HP ketika bepergian. Tentu gue udah punya solusinya yaitu pakai Syncthing. Kalau misalnya gue mau pergi, gue tinggal sync aja file-nya di HP gue. Di komputer gue juga udah pasti nyalain Syncthing pas startup. Homelab server gue juga nge-serve Syncthing-nya 24/7 (kecuali kalau ada pemadaman listrik).

Gue merasa lebih aman karena password gue engga bertebaran di internet lagi dan bisa menambahkan fungsi ke Homelab gue.