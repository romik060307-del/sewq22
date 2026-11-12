# OHLI Social Client v3.7.4 — test plan

1. Build `:app:assembleDebug` in GitHub Actions; confirm APK installs over v3.7.2 under package `com.ohli.social.client`.
2. Open Settings → Chat & perangkat → Diagnostik perangkat. Confirm Android/WebView version, notification enabled state, sync running, and endpoint HTTP results.
3. Press **Tes notifikasi**. If absent, fix Android app/channel permission first. If visible, Android notification delivery works and API/polling becomes the next suspect.
4. Enable **Izinkan aktivitas latar belakang** and OEM Auto-start/background run for OHLI, then press Home (do not Force stop). From a second phone send a new message. Check message notification, reply action, and sender delivered tick.
5. Verify endpoint diagnostics show HTTP 200 + JSON for `/api/messages`, `/api/calls`, and `/api/notifications`. HTTP 404/HTML means the Netlify `/api/*` route is not connected to backend; configure the real backend/proxy.
6. On HTTPS site, run voice and video calls from two devices. If diagnostic shows CAMERA/AUDIO resource denied or no WebView `getUserMedia`, update Android System WebView/Chrome. If media permission passes but ICE fails, configure TURN.
7. Test LIVE host preview, participant join, local/remote audio, and both cameras.
8. Long-press images/videos in chat and feed; confirm no native context menu/crash. Verify ordinary tap, image preview and zoom remain usable.
9. Close app normally / swipe Recents and test background notification. Separately test Force stop; no app can promise polling after a user force-stops it.
