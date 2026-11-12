# Test Plan v3.7.3

1. Build APK melalui GitHub Actions; pastikan artifact bernama `OHLI-Social-Client-APK-v3.7.3`.
2. Login pada Vivo Oreo, keluar dengan Home (jangan Force Stop), lalu periksa notifikasi ongoing OHLI.
3. Buka Pengaturan OHLI → Diagnostik perangkat. Pastikan versi WebView terdeteksi, permission kamera/mikrofon true, `syncServiceRunning` true, dan status HTTP untuk `/api/messages`, `/api/calls`, `/api/notifications` tampil.
4. Dari HP lain kirim pesan; pastikan timestamp/count polling berubah dan notifikasi Android masuk.
5. Coba notifikasi aktivitas sosial dan balasan inline.
6. Coba VC audio, VC video, LIVE host, LIVE viewer, kamera depan/belakang. Jika gagal, diagnostik harus memuat nama error, kemampuan media, dan provider/version WebView.
7. Uji tekan-lama foto/video, scroll, dan buka gambar besar beberapa kali.
8. Tutup dengan Home, kirim pesan dari perangkat kedua, lalu pastikan pesan masih diterima. Force Stop tidak termasuk jaminan polling; FCM dibutuhkan untuk keandalan saat proses dibunuh.
