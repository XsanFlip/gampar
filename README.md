GAMPAR - Multi Protocol RFID Converter

GAMPAR (Ghosted Access Multi-protocol Proximity And RFID) adalah sebuah tool berbasis web yang dirancang untuk mengonversi nomor kartu desimal (DEC-10) dari sistem ZKTeco menjadi format Heksadesimal (HEX) 5-byte yang kompatibel dengan Flipper Zero untuk emulasi kartu RFID EM4100.

✨ Fitur Utama

    Konversi Instan: Mengubah nomor kartu ZKTeco (Wiegand 26-bit) menjadi beberapa format output secara cepat.

    Output untuk Flipper Zero: Menghasilkan kode Heksadesimal 10-digit yang siap digunakan untuk fitur "Manual Add" pada Flipper Zero (RFID 125kHz).

    Rincian Data Wiegand: Menampilkan hasil kalkulasi Facility Code (FC) 8-bit dan Card ID 16-bit.

    Sepenuhnya Sisi Klien: Dibangun dengan HTML dan JavaScript murni. Tidak ada data yang dikirim ke server, menjamin privasi dan kecepatan.

    Desain Responsif: Tampilan antarmuka yang modern dan dapat menyesuaikan diri dengan berbagai ukuran layar, dari desktop hingga perangkat mobile.

    Salin-ke-Papan Klip: Fungsionalitas sekali klik untuk menyalin hasil konversi dengan mudah.

    Validasi Input: Sistem validasi untuk memastikan input adalah angka yang valid dan berada dalam rentang maksimum standar Wiegand 26-bit.

⚙️ Alur Kerja Teknis

Skrip ini mereplikasi logika konversi protokol Wiegand 26-bit yang umum digunakan pada sistem kontrol akses. Berikut adalah alur kerja teknisnya dari input hingga output:

    Input Pengguna:

        Pengguna memasukkan nomor kartu ke dalam kolom input. Nomor ini biasanya berupa representasi desimal 10 digit dari data mentah kartu.

        JavaScript menangani event submit pada formulir untuk memulai proses tanpa me-reload halaman.

    Validasi Input (JavaScript):

        Skrip pertama-tama memeriksa apakah input tidak kosong dan hanya berisi angka (/^\d+$/.test(rawInput)).

        Selanjutnya, input dikonversi menjadi tipe data integer. Skrip kemudian memvalidasi apakah nilai desimal tersebut tidak melebihi batas maksimum untuk data 24-bit dalam standar Wiegand 26-bit, yaitu 16,777,215.

        Jika validasi gagal, sebuah pesan kesalahan akan ditampilkan secara dinamis.

    Proses Kalkulasi Inti:

        Jika input valid, skrip melanjutkan ke logika konversi utama:

            Facility Code (FC): Nilai desimal dibagi dengan 65536 (2¹⁶) dan dibulatkan ke bawah (Math.floor(decimalValue / 65536)). Ini mengisolasi 8 bit pertama dari data.

            Card ID: Sisa bagi dari nilai desimal dengan 65536 (decimalValue % 65536) dihitung. Ini mengisolasi 16 bit terakhir.

            Wiegand Raw Hex (3-Byte): Nilai desimal asli dikonversi menjadi string heksadesimal, diubah menjadi huruf besar, dan diberi padding nol di depan hingga mencapai 6 karakter (.toString(16).toUpperCase().padStart(6, '0')).

            Flipper Zero Hex (5-Byte): Skrip menambahkan prefix tetap 1600 ke hasil Wiegand Raw Hex 3-byte. Prefix ini umum digunakan untuk format kartu EM4100.

    Menampilkan Hasil (Manipulasi DOM):

        Setelah semua nilai dihitung, skrip menyisipkan hasilnya ke dalam elemen-elemen HTML yang sudah disiapkan di dalam kontainer output.

        Kontainer hasil, yang awalnya disembunyikan (display: none atau class="hidden"), kemudian ditampilkan untuk menunjukkan hasil konversi kepada pengguna.

🚀 Cara Menggunakan

Karena aplikasi ini sepenuhnya mandiri, Anda hanya perlu:

    Kloning repositori ini atau unduh file gampar_converter.html.

    Buka file gampar_converter.html langsung di peramban web modern apa pun (Chrome, Firefox, Safari, Edge, dll.).

    Aplikasi siap digunakan.

⚠️ Disclaimer

Aplikasi ini ditujukan untuk tujuan edukasi, riset keamanan, dan pengembangan. Pengguna bertanggung jawab penuh atas penggunaan alat ini. Selalu patuhi hukum dan etika yang berlaku.

Dibuat oleh XsanLahci.
