# Build and install OHLI Social Client v3.7.4

## Build APK
1. Extract the ZIP.
2. Upload the **contents** of this extracted folder to the root of the GitHub repository (the repository root should contain `settings.gradle`, `app/`, `.github/`, and `tools/`).
3. Open GitHub → Actions → **Build OHLI Social Client APK** → Run workflow.
4. Wait for the workflow to finish. Download artifact `OHLI-Social-Client-APK-v3.7.4` and install `app-debug.apk`.
5. The app label is `OHLI Social`; package ID remains `com.ohli.social.client`, so v3.7.4 is intended as an update to v3.7.2. Keep the OHLI server APK (`com.rk.server`) installed separately.

## First diagnostics on Vivo Android Oreo
1. Sign in once and allow OHLI to remain active.
2. Open OHLI Social → Pengaturan → Chat & perangkat → **Diagnostik perangkat**.
3. Check `webViewProvider` and `webViewVersion`; update Android System WebView/Chrome from Play Store if the provider is old or unavailable, then restart the phone.
4. Press **Tes notifikasi** in the diagnostics dialog. This test is local and does not need the server.
5. Check `syncServiceRunning` and the endpoint fields `lastMessagesHttp`, `lastCallsHttp`, and `lastSocialHttp`.
6. Use **Izinkan aktivitas latar belakang** and also allow OHLI in Vivo's Auto-start / background power settings if those menus are present.
7. Test incoming chat while OHLI is in the background (press Home; do not Force stop). Test calls and LIVE with a second phone.

## How to interpret endpoint diagnostics
- `200 · OK`: endpoint returned JSON successfully.
- `404`, `401`, `403`, `5xx`, `-1`, or a JSON parse / HTML response: the background poller is not receiving a valid API response. The public website host must route `/api/*` to the actual running backend.
- A local test notification appearing proves Android notification channels can display alerts; it does not prove the server API or push path works.

## Known infrastructure requirements
- The ZIP includes the Android client and the existing local backend source, but the client APK does not run that backend service.
- This source tree does not include Netlify Functions, `_redirects`, or `netlify.toml` to proxy `/api/*`. Static Netlify hosting alone cannot run this app's chat/call database API.
- The 7-second foreground-service poll is best effort while Android allows the service to run. It cannot continue after Force stop and may be stopped by OEM power controls. True WhatsApp-like background delivery requires an FCM Firebase project (`google-services.json`), sender credentials stored only on the backend, and a backend push sender.
- WebRTC calls and LIVE need TURN relay for networks where STUN/direct peer connection is insufficient. No TURN secret is embedded in this client.
- This source has passed static checks only. The APK still needs a GitHub Actions build and installation/real-device testing on Vivo.
