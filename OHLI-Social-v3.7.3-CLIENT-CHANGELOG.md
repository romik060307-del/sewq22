# OHLI Social Client v3.7.3 — Media, Audio & Notification Diagnostics

## Pembaruan source
- Mempertahankan identitas paket `com.ohli.social.client` dan origin Netlify.
- Menambahkan diagnostik perangkat yang bisa dibuka dari Pengaturan → Chat & perangkat → Diagnostik perangkat: versi Android, provider/versi Android System WebView, izin kamera/mikrofon, status notifikasi/channel, status layanan sync, dan hasil HTTP polling `/api/messages`, `/api/calls`, serta `/api/notifications`. Tidak menampilkan token atau nomor akun.
- Menambahkan fallback `getUserMedia` dengan constraints sederhana untuk WebView lama/perangkat yang gagal pada constraints ideal; dipakai untuk panggilan, LIVE host, dan LIVE peserta.
- Menurunkan target LIVE default ke 640×480 / 20 fps (720p tetap tersedia) untuk mengurangi kegagalan kamera dan tekanan memori.
- Menambahkan AudioManager mode komunikasi/audio focus Android saat VC/LIVE aktif dan mengembalikannya saat selesai.
- Menambahkan pemeriksaan dan pencatatan asal permintaan izin WebView serta hasil izin Android. Hanya HTTPS origin OHLI yang dipercaya.
- Menambahkan kanal notifikasi aktivitas sosial selain pesan dan panggilan.
- Mencatat hasil API polling agar endpoint yang 404/401/HTML dapat dibedakan dari masalah izin notifikasi.
- Menonaktifkan menu konteks native WebView ketika tekan-lama tepat pada gambar/video agar tidak membuka operasi gambar besar yang berpotensi membebani perangkat. Tekan-lama pada elemen lain tidak dicegat.

## Batas yang tetap berlaku
- Polling 7 detik tetap foreground-service fallback, bukan push FCM. Force Stop, Doze, dan pembatasan autostart/baterai Vivo dapat menghentikan atau menunda polling. FCM memerlukan Firebase project/app config dan endpoint pengirim server yang belum tersedia di source ini.
- Panggilan/LIVE memerlukan server signaling online dan ICE connectivity; source saat ini hanya memiliki STUN publik, belum ada TURN ber-kredensial. Karena itu panggilan lintas NAT/jaringan belum dapat dijamin.
- Netlify static site tidak otomatis menyediakan API. Endpoint `/api/*` harus benar-benar diproxy ke backend OHLI. Diagnostik baru akan menunjukkan status endpoint secara konkret pada HP.
- Fallback media mengatasi constraints/provider lawas, tetapi tidak dapat menggantikan Android System WebView/Chrome yang terlalu lama atau rusak.
- APK belum dibangun/diinstal pada Vivo; source checks bukan pengganti uji perangkat nyata.
