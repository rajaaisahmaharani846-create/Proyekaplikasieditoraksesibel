**PROMPT FINAL — SIAP DIEKSEKUSI**

**ROLE**
Anda adalah Senior Android Developer sekaligus Accessibility Engineer, ahli dalam Kotlin native, Jetpack Compose, TalkBack/screen reader compliance, dan integrasi Google ML Kit (Image Labeling, Object Detection, Text Recognition).

**OBJECTIVE**
Bangun aplikasi Android bernama **"Editor Aksesibel"** — editor rekaman & gambar yang sepenuhnya dapat dioperasikan tanpa melihat layar oleh pengguna tunanetra, gratis, dan berfungsi offline (tanpa kuota internet).

**CONTEXT**
- Pengguna akhir: penyandang tunanetra, mengandalkan TalkBack/screen reader untuk seluruh navigasi.
- Semua interaksi harus punya konfirmasi suara (TTS) di setiap aksi.
- Rekomendasi platform: **Android native (Kotlin + Jetpack Compose)** — dipilih karena dukungan aksesibilitas Compose paling matang, integrasi ML Kit paling langsung (library resmi Google), dan performa offline lebih stabil dibanding cross-platform untuk kasus ini.
- Model bisnis: 100% gratis untuk pengguna, tanpa biaya bulanan; hanya ada biaya satu kali (~Rp400.000) untuk publikasi ke Play Store di tahap akhir.

**INSTRUCTIONS**
1. Setup proyek Android (Kotlin, Jetpack Compose, minSdk yang mendukung TalkBack penuh), dengan nama aplikasi "Editor Aksesibel" pada `app_name` dan metadata Play Store.
2. Implementasikan **Deskripsi Gambar**: pindai gambar dengan ML Kit Image Labeling/Object Detection → bacakan hasil via TextToSpeech ("Di gambar terlihat: ...").
3. Implementasikan **Deskripsi Video**: ekstrak frame per interval waktu, jalankan ML Kit per frame, susun ringkasan per rentang menit → bacakan via TTS.
4. Implementasikan **Pemangkasan/Pemotongan Video**: kontrol geser (swipe naik/turun/kiri/kanan) untuk menandai titik mulai & selesai, dengan umpan balik suara real-time menyebutkan detik saat ini; tombol "Hapus Bagian Ini" dan "Simpan Hasil" dengan konfirmasi suara.
5. Implementasikan **Peredam Bising**: proses audio track video untuk mengurangi noise (gunakan library noise suppression yang tersedia offline di Android, mis. built-in AudioEffects/NoiseSuppressor API).
6. Pastikan SEMUA elemen UI (tombol, slider, status) memiliki `contentDescription` yang jelas dan teruji dengan TalkBack.
7. Gunakan navigasi berbasis fokus linear yang mudah diikuti lewat swipe TalkBack standar (bukan gesture custom yang bentrok dengan gesture TalkBack).
8. Struktur kode modular: pisahkan modul `mlkit-description`, `video-editor`, `audio-denoise`, `accessibility-ui`.

**CONSTRAINTS**
- Tidak boleh ada fitur yang mewajibkan koneksi internet untuk versi pertama.
- Tidak boleh ada gesture custom yang bentrok dengan gesture navigasi TalkBack bawaan Android.
- Setiap aksi destruktif (hapus bagian rekaman) wajib ada konfirmasi suara sebelum eksekusi final.
- Gunakan hanya library gratis/open-source atau API bawaan Android (ML Kit on-device, bukan versi cloud berbayar).

**OUTPUT FORMAT**
Hasilkan dalam urutan: (1) struktur folder proyek, (2) kode lengkap per modul dimulai dari `mlkit-description`, (3) kode `video-editor` dengan swipe-trim, (4) kode `audio-denoise`, (5) checklist pengujian aksesibilitas TalkBack untuk tiap layar.

**QUALITY BAR**
Kode harus bisa di-build langsung tanpa error, setiap layar lulus audit aksesibilitas (Accessibility Scanner Android), dan setiap interaksi suara terasa natural bagi pengguna tunanetra saat diuji langsung.
