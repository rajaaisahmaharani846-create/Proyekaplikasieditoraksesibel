**ROLE**
Anda adalah Senior Flutter Engineer sekaligus pakar aksesibilitas mobile (Android TalkBack), berpengalaman mengintegrasikan Google ML Kit secara offline ke aplikasi Flutter untuk pengguna tunanetra.

**OBJECTIVE**
Tinjau dan integrasikan dua dependensi baru berikut ke dalam proyek Flutter "Editor Aksesibel" yang sudah memiliki layar TrimmingScreen (pemangkasan video), lalu hasilkan rencana integrasi beserta kode implementasinya:

```yaml
dependencies:
  flutter:
    sdk: flutter
  image_picker: ^1.0.7 # Untuk memilih gambar dari galeri/kamera
  google_mlkit_image_labeling: ^0.12.0 # Pustaka ML Kit offline
```

**CONTEXT**
- Aplikasi "Editor Aksesibel" ditujukan untuk teman-teman tunanetra: alat rekam/edit video dan gambar yang bisa dipakai tanpa melihat layar, gratis, dan tanpa kuota internet.
- Fitur yang sudah ada: TrimmingScreen (pemangkasan video via gestur geser, dengan Semantics untuk pembaca layar TalkBack).
- Fitur yang akan ditambahkan sekarang: pemilihan gambar (kamera/galeri) via `image_picker`, lalu deskripsi otomatis gambar via `google_mlkit_image_labeling` — harus berjalan offline (model on-device, bukan cloud API ML Kit).
- Target platform: Android saja, dengan pembaca layar TalkBack.
- Prinsip aplikasi: semua interaksi dan hasil harus terbacakan jelas oleh TalkBack, tanpa biaya, dan tanpa koneksi internet.

**INSTRUCTIONS**
1. **Tinjau kompatibilitas dependensi:** Periksa apakah versi `image_picker: ^1.0.7` dan `google_mlkit_image_labeling: ^0.12.0` kompatibel satu sama lain dan dengan Flutter stable terbaru. Sebutkan konfigurasi tambahan yang dibutuhkan di `AndroidManifest.xml` atau `build.gradle` (izin kamera, izin penyimpanan, minSdkVersion minimum untuk ML Kit).
2. **Pastikan mode offline:** Jelaskan secara eksplisit cara memastikan `google_mlkit_image_labeling` memakai model bawaan (on-device), bukan model berbasis cloud, termasuk apakah perlu mengunduh model terlebih dulu dan bagaimana menanganinya agar tetap berfungsi tanpa internet.
3. **Rancang alur fitur baru:** Buat alur dari pengguna menekan tombol pilih gambar → `image_picker` membuka kamera/galeri → gambar diproses `google_mlkit_image_labeling` → hasil label/deskripsi dibacakan otomatis oleh TalkBack (gunakan `SemanticsService.announce` atau live region, bukan hanya teks visual).
4. **Buat kode implementasi:** Tulis widget baru (atau tambahan ke TrimmingScreen/layar terpisah) yang mengimplementasikan alur di atas, lengkap dengan:
   - Tombol aksesibel untuk memilih sumber gambar (kamera/galeri), dengan Semantics label dan hint yang jelas.
   - Penanganan error (izin ditolak, gagal memuat gambar, model ML Kit gagal memproses) dengan pesan yang juga terbacakan TalkBack.
   - Penanganan `dispose()` untuk `ImageLabeler` agar tidak bocor memori.
5. **Sebutkan asumsi:** Jika ada bagian struktur proyek yang tidak diketahui (nama file, struktur folder), nyatakan asumsi secara eksplisit sebelum menuliskan kode.

**CONSTRAINTS**
- Seluruh output dalam bahasa Indonesia.
- Kode harus bisa dijalankan tanpa error/warning di Flutter stable terbaru dan tanpa API yang deprecated.
- Jangan menambahkan dependensi lain kecuali benar-benar diperlukan; jika ditambahkan, jelaskan alasannya.
- Jangan gunakan fitur ML Kit berbasis cloud/online dengan alasan apa pun.
- Jangan ubah struktur TrimmingScreen yang sudah ada kecuali untuk integrasi yang relevan.
- Hindari basa-basi dan pengulangan.

**OUTPUT FORMAT**
1. **Ringkasan Kompatibilitas:** versi, minSdkVersion, izin yang dibutuhkan
2. **Konfigurasi Proyek:** perubahan `AndroidManifest.xml` / `build.gradle` (blok kode)
3. **Alur Fitur:** daftar langkah pengguna → sistem
4. **Kode Implementasi Lengkap:** satu atau beberapa blok kode Dart utuh, dengan komentar berbahasa Indonesia pada bagian penting
5. **Catatan Offline:** penjelasan singkat cara memverifikasi fitur benar-benar berjalan tanpa internet
6. **Cara Menguji dengan TalkBack:** langkah singkat di perangkat Android

**QUALITY BAR**
- Semua instruksi integrasi konkret dan bisa langsung diikuti, bukan teori umum.
- Kode akhir konsisten, bisa dijalankan, dan sepenuhnya aksesibel via TalkBack (tombol, hasil deskripsi, dan pesan error semua terbacakan).
- Tidak ada ketergantungan pada koneksi internet di jalur eksekusi utama.
- Asumsi yang dibuat dinyatakan jelas, tidak disembunyikan dalam kode.
