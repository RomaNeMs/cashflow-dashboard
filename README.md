# Forecasted Monthly Cashflow

Single-page app hosted on GitHub Pages. **This repository contains no financial data.**

- The page is locked by a passcode; it decrypts a small vault (AES-GCM / PBKDF2) holding the API access key.
- All data — including reference data (payroll base/history, vendor definitions and history) — lives in a private Google Sheet, reached through an Apps Script JSON API that rejects requests without the key.
- The Apps Script source is **not** in this repo (it contains the key). The reference copy is kept outside the repo.

## Data safety
- Saves are blocked until the server copy has loaded; a timestamp check refuses saves that would overwrite a newer copy from another device.
- If the server is unreachable at load, the app opens read-only.
- The server keeps one snapshot per day (Backups tab); the browser keeps the last 5 local backups; Save → Export All Data downloads a full JSON.

## Moving to another Google account
1. Open the data Sheet → **File → Make a copy** (signed in to the new account). The script is inside the Sheet and is copied with it.
2. In the copy: **Extensions → Apps Script → Deploy → New deployment** (Web app · Execute as: Me · Who has access: Anyone). Copy the `/exec` URL.
3. In the app: **Save → Change server**, paste the URL. If the new server is empty, the app offers to copy your current data to it.
