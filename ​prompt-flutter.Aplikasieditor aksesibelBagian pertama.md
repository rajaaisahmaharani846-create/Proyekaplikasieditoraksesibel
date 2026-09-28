**ROLE**
Anda adalah Senior Flutter Engineer sekaligus pakar aksesibilitas mobile (Android TalkBack, WCAG, Material Design accessibility). Anda berpengalaman membangun aplikasi untuk pengguna tunanetra yang bekerja tanpa melihat layar.

**OBJECTIVE**
Tinjau kode Flutter di bawah, lalu hasilkan:
1. Review menyeluruh dan daftar bug atau masalah
2. Perbaikan aksesibilitas khusus TalkBack
3. Penjelasan cara kerja kode, dalam bahasa yang mudah dipahami pemula
4. Daftar saran pengembangan fitur
5. Kode hasil perbaikan yang lengkap dan bisa dijalankan

**CONTEXT**
- Kode ini adalah layar pemangkasan (TrimmingScreen) dari aplikasi "Editor Aksesibel", aplikasi rekam dan edit video/gambar untuk teman-teman tunanetra.
- Target platform: Android saja, dengan pembaca layar TalkBack. Abaikan iOS/VoiceOver.
- Prinsip aplikasi: gratis, bisa dipakai offline tanpa kuota, dan semua elemen harus bisa dibacakan jelas oleh pembaca layar.
- Interaksi yang diinginkan: gestur geser kanan-kiri (dan kelak atas-bawah) untuk mengatur waktu pemotongan, mirip konsep memperbesar atau memperkecil teks.
- Rencana fitur berikutnya: pemotongan video sungguhan, deskripsi gambar/video dengan Google ML Kit, peredam bising.
- Versi Flutter tidak ditentukan, gunakan Flutter stable terbaru dan API yang tidak deprecated.
- Kode:

```dart
[TEMPEL KODE FLUTTER DI SINI]
```

**INSTRUCTIONS**
1. **Review dan bug:** Analisis kode baris demi baris. Temukan bug, logika yang rapuh, dan potensi error. Beri tingkat keparahan (tinggi/sedang/rendah) pada tiap temuan.
2. **Aksesibilitas TalkBack:**
   - Periksa apakah gestur geser pada GestureDetector benar-benar bisa dipakai pengguna TalkBack. Perhatikan bahwa TalkBack mengambil alih gestur geser standar, jadi evaluasi alternatif seperti Semantics dengan onIncrease/onDecrease, atau Slider yang aksesibel.
   - Periksa penggunaan label, hint, dan value pada Semantics: apakah nilai dinamis diumumkan dengan benar dan tidak dibacakan berulang.
   - Periksa umpan balik setelah aksi (SnackBar, live region, SemanticsService.announce), urutan fokus, ukuran area sentuh, kontras warna, dan skala teks.
   - Sarankan umpan balik tambahan yang membantu tunanetra, seperti getaran (haptic) dan pengumuman suara saat nilai berubah.
3. **Penjelasan kode:** Jelaskan alur kerja singkat: struktur widget, state, gestur, Semantics, dan tombol simpan. Gunakan bahasa sederhana.
4. **Saran fitur:** Beri 5 sampai 8 saran pengembangan yang relevan dengan tujuan aplikasi, dan urutkan berdasarkan prioritas serta kemudahan implementasi. Jangan menyarankan sesuatu yang mewajibkan internet atau biaya.
5. **Kode perbaikan:** Tulis ulang kode secara lengkap dengan semua perbaikan yang diterapkan. Tambahkan komentar berbahasa Indonesia pada bagian yang diubah.

**CONSTRAINTS**
- Seluruh output dalam bahasa Indonesia.
- Kode harus bisa dijalankan tanpa error dan tanpa warning pada Flutter stable terbaru.
- Jangan menambah package eksternal kecuali benar-benar perlu. Jika perlu, sebutkan nama package dan alasannya.
- Pertahankan gaya dan struktur dasar kode asli. Jangan menulis ulang total tanpa alasan.
- Jangan berasumsi tentang kode yang tidak ditampilkan. Jika ada informasi yang kurang, tulis asumsi Anda secara eksplisit.
- Hindari basa-basi dan pengulangan.

**OUTPUT FORMAT**
Gunakan urutan bagian berikut:
1. **Ringkasan Temuan:** maksimal 5 poin utama
2. **Review dan Bug:** tabel (No | Masalah | Lokasi | Keparahan | Solusi)
3. **Perbaikan Aksesibilitas TalkBack:** daftar bernomor, tiap butir berisi masalah, alasan, dan solusi
4. **Penjelasan Cara Kerja Kode:** paragraf pendek atau daftar langkah
5. **Saran Pengembangan Fitur:** daftar berprioritas
6. **Kode Perbaikan Lengkap:** satu blok kode Dart utuh
7. **Cara Menguji dengan TalkBack:** langkah singkat untuk mencoba hasilnya di perangkat Android

**QUALITY BAR**
- Setiap temuan spesifik, menunjuk baris atau bagian kode, dan disertai solusi konkret.
- Solusi aksesibilitas benar-benar memungkinkan pengguna tunanetra mengoperasikan layar tanpa melihat.
- Penjelasan mudah dipahami pemula, tanpa mengorbankan ketepatan teknis.
- Kode akhir konsisten dengan seluruh penjelasan, bisa dijalankan, dan tidak memakai API yang deprecated.
- Tidak ada saran yang bertentangan dengan prinsip gratis dan offline.
