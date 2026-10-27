**ROLE**
Anda adalah Senior Flutter Engineer sekaligus pakar aksesibilitas mobile (Android TalkBack), berpengalaman mengintegrasikan `image_picker` dan `google_mlkit_image_labeling` (offline) ke aplikasi Flutter untuk pengguna tunanetra.

**OBJECTIVE**
Tinjau kode `ImageDescriptionScreen` di bawah ini, lalu hasilkan versi perbaikan yang: (1) bebas bug, (2) terhubung ke implementasi nyata `image_picker` + `google_mlkit_image_labeling` menggantikan simulasi `Future.delayed`, dan (3) sepenuhnya aksesibel untuk TalkBack. Tentukan juga posisi terbaik layar ini dalam struktur navigasi proyek.

**CONTEXT**
- Aplikasi "Editor Aksesibel": alat rekam/edit video dan gambar untuk teman-teman tunanetra, gratis, berjalan offline, semua interaksi harus terbacakan oleh TalkBack.
- Proyek sudah memiliki `TrimmingScreen` (pemangkasan video via gestur geser).
- Dependensi yang tersedia:

```yaml
image_picker: ^1.0.7
google_mlkit_image_labeling: ^0.12.0
```
- Kode saat ini (`ImageDescriptionScreen`) masih simulasi: `_scanImage()` hanya menunggu 2 detik lalu menampilkan teks hasil statis via `Future.delayed`, belum benar-benar memanggil galeri/kamera atau model ML Kit.
- Target platform: Android saja, TalkBack.
- Kode:

```dart
[TEMPEL KODE ImageDescriptionScreen DI SINI]
```

**INSTRUCTIONS**
1. **Review dan bug:** Temukan semua bug dan kode janggal, termasuk ekspresi tidak masuk akal `ElevatedButton.styleFrom != null ? ElevatedButton(...) : Container()` (selalu true, harus dihapus jadi widget langsung), lalu identifikasi masalah lain (pengelolaan state saat widget di-dispose di tengah proses async, dsb). Beri tingkat keparahan pada tiap temuan.
2. **Integrasi nyata image_picker + ML Kit:**
   - Ganti `_scanImage()` simulasi dengan alur nyata: `ImagePicker().pickImage()` (tawarkan sumber kamera atau galeri) → buat `InputImage` dari file hasil → proses dengan `ImageLabeler` (`ImageLabelerOptions` default, on-device, bukan cloud) → gabungkan label hasil menjadi kalimat deskripsi yang enak didengar.
   - Tangani `ImageLabeler.close()`/`dispose()` agar tidak bocor memori.
   - Tangani kondisi gagal: pengguna membatalkan pemilihan gambar, izin kamera/galeri ditolak, gambar gagal diproses.
   - Pastikan proses tetap berjalan tanpa internet; jelaskan secara singkat bagaimana memastikan ini (model bundel on-device).
3. **Aksesibilitas TalkBack:**
   - Perbaiki penggunaan `Semantics` pada kotak hasil: saat ini `hint` dipakai untuk menampung hasil deskripsi, padahal `hint` bukan tempat yang tepat untuk konten dinamis utama — gunakan `value` atau umumkan perubahan via `SemanticsService.announce`/live region agar TalkBack otomatis membacakan hasil baru tanpa pengguna harus menavigasi ulang.
   - Pastikan status "Memindai..." dan hasil akhir diumumkan otomatis, bukan hanya berubah secara visual.
   - Pastikan tombol pilih sumber gambar (kamera/galeri) punya label dan hint yang jelas, termasuk saat dialog pemilihan sumber muncul.
   - Pastikan `CircularProgressIndicator` punya label aksesibel ("Sedang memindai gambar") agar tidak diam saja bagi TalkBack.
4. **Posisi layar dalam navigasi:** Sarankan apakah layar ini sebaiknya berdiri sendiri dan dinavigasikan dari `TrimmingScreen` (misalnya via tab atau tombol navigasi), atau digabung jadi satu layar. Berikan alasan singkat berdasarkan alur pengguna tunanetra (kesederhanaan navigasi, jumlah langkah, kejelasan konteks).
5. **Sebutkan asumsi:** Jika ada struktur proyek yang tidak diketahui (routing, nama file), nyatakan asumsi secara eksplisit.

**CONSTRAINTS**
- Seluruh output dalam bahasa Indonesia.
- Kode harus bisa dijalankan tanpa error/warning di Flutter stable terbaru, tanpa API deprecated.
- Jangan gunakan ML Kit berbasis cloud dengan alasan apa pun; proses harus 100% offline.
- Jangan menambahkan dependensi lain kecuali benar-benar diperlukan, dan jelaskan alasannya jika ditambahkan.
- Pertahankan gaya dan struktur dasar kode asli selama tidak bertentangan dengan perbaikan yang diminta.
- Hindari basa-basi dan pengulangan.

**OUTPUT FORMAT**
1. **Ringkasan Temuan:** maksimal 5 poin utama
2. **Review dan Bug:** tabel (No | Masalah | Lokasi | Keparahan | Solusi)
3. **Rencana Integrasi ML Kit:** daftar langkah teknis singkat
4. **Perbaikan Aksesibilitas TalkBack:** daftar bernomor (masalah → alasan → solusi)
5. **Rekomendasi Posisi Layar dalam Navigasi:** 1 paragraf singkat beserta alasan
6. **Kode Perbaikan Lengkap:** satu blok kode Dart utuh, dengan komentar berbahasa Indonesia pada bagian penting
7. **Cara Menguji dengan TalkBack:** langkah singkat di perangkat Android

**QUALITY BAR**
- Setiap temuan spesifik, menunjuk baris/bagian kode, dengan solusi konkret.
- Integrasi ML Kit benar-benar offline dan fungsional, bukan simulasi.
- Semua status (memindai, hasil, error) dibacakan otomatis oleh TalkBack tanpa aksi tambahan dari pengguna.
- Kode akhir konsisten, lengkap, bisa langsung dijalankan.
- Rekomendasi navigasi didasarkan pada kemudahan penggunaan oleh tunanetra, bukan preferensi estetika semata.
