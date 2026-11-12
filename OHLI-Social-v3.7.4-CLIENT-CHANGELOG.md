# OHLI Social Client v3.7.4 — diagnostics and media compatibility

## Changes
- Keeps the OHLI client package ID `com.ohli.social.client`; the app label remains OHLI Social.
- Adds endpoint diagnostics for `/api/messages`, `/api/calls`, and `/api/notifications` (HTTP status and latest response state).
- Adds device diagnostics for Android version, WebView provider/version, runtime camera/microphone permission, notification permission/channel state, foreground sync state, and the last WebView media permission/error. Tokens and phone numbers are not shown.
- Adds a local test notification so Android notification-channel delivery can be separated from server/API delivery.
- Adds user-invoked battery-optimization exclusion settings for more reliable foreground polling on OEM Android builds. This is not a force-stop bypass.
- Adds social notification polling and makes first-poll delivery alerts include only recent items, avoiding old notification floods.
- Uses legacy `getUserMedia` fallback for supported older WebView builds in chat calls and LIVE participant joining.
- Applies Android communication audio mode before microphone capture and restores it after failed capture/end of call or LIVE.
- Suppresses image/video long-press context menus in the Android client to reduce accidental heavy media actions.

## Important limitations
- Polling every 7 seconds is foreground-service best effort. It may stop after Force stop, OEM task killing, network restriction, or device reboot; FCM requires Firebase project configuration and a backend push sender.
- Online messaging, message delivery receipts, notifications, call signaling, and LIVE require the Netlify domain to proxy `/api/*` to a live backend. The source ZIP does not contain Netlify redirects/functions or a deployable always-on backend.
- Camera/microphone access requires a compatible Android System WebView provider and a trusted HTTPS origin. Diagnostics records the actual provider and permission grant.
- Peer-to-peer calls and LIVE can still fail on restrictive networks until a TURN relay is configured on the backend. Do not put TURN credentials into the public client source.
- The source has not been compiled into an APK or installed on a Vivo device in this environment.
