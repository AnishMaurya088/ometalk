# Ometalk

Ometalk is an anonymous random chat MVP with text chat and browser-to-browser video calling.

## Features

- Random matching for text or video chat, with optional shared interests
- Real-time messages and typing indicator using Socket.IO
- WebRTC video/audio with camera and microphone controls
- Tap or click either video preview to make it the main view
- Leave and report actions
- Password-protected admin dashboard at `/admin` with live user, connection, and report aggregates

## Tech stack

- Node.js and Express
- Socket.IO
- WebRTC
- HTML, CSS, and browser JavaScript

## Run locally

Install dependencies and start the server:

```sh
npm ci
npm start
```

The app uses port `3000` by default and reads the optional `PORT` environment variable. Camera and microphone access require localhost or HTTPS.

To enable the admin dashboard, set `ADMIN_PASSWORD` in the process environment. Use a strong value of at least 16 characters; never commit the real password. The example values in `.env.example` are placeholders and are not loaded automatically.

PowerShell example:

```powershell
$env:ADMIN_PASSWORD = "replace-with-your-own-strong-password"
npm start
```

## Render deployment

The included `render.yaml` can be used to create a Render Blueprint from this repository. Set `ADMIN_PASSWORD` as a secret in the Render service environment before using `/admin`.

The admin dashboard stores only aggregate daily counts in `data/admin-metrics.json`. Free hosting filesystems may be temporary, so use a persistent disk or database if those counts must survive host restarts and redeploys.

## Limitations

- The 18+ checkbox is not identity or age verification.
- Reports are aggregate counts only; there is no review queue or moderation workflow yet.
- WebRTC currently uses public STUN servers. A TURN service is needed for reliable calls across restrictive networks.
- This is an early MVP and should not be treated as a fully moderated public chat service.