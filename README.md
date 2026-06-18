# BOTC — Download page

A tiny static site (GitHub Pages) that hands people the BOTC app: an **iOS** App Store
link and a **direct Android `.apk`** download, each with a scannable QR code. Players scan
the QR shown on screen, land here, and tap to install.

This repo is **public** (so free GitHub Pages can serve it). It contains **no app source
code** — that lives in the private repo. Nothing here is secret.

## The only file you edit: `config.js`

```js
window.BOTC_CONFIG = {
  iosUrl: '',      // your unlisted App Store link (added after App Review)
  androidUrl: '',  // direct link to the .apk
  supportEmail: 'you@example.com',
}
```

Fill the URLs, commit, push. The page regenerates the QR codes and buttons automatically.
A URL left as `''` shows a tidy **"Coming soon"** state for that platform — so you can ship
the page before either store link exists.

## Enable GitHub Pages

Repo **Settings → Pages → Build and deployment → Source: "Deploy from a branch"**, branch
`main`, folder `/ (root)`. Save. Your page goes live at
`https://noltechas.github.io/botc-download/` within a minute.

(The empty `.nojekyll` file tells Pages to serve everything as-is.)

## Hosting the Android APK

The Android button downloads an `.apk` file directly. Easiest place to host it is a
**GitHub Release on this repo** (Releases → Draft a new release → attach the `.apk`):

```
https://github.com/noltechas/botc-download/releases/latest/download/botc.apk
```

Put that URL in `androidUrl`. Re-upload the asset (same filename) each time you ship a new
build and `latest/download/...` keeps working.

> Build the APK from the app repo with: `eas build -p android --profile production-apk`,
> then download it from the EAS build page and attach it to a Release here.

## The iOS link

You get the App Store URL only **after** the app is approved and you've turned on
**Unlisted distribution** in App Store Connect. Until then, leave `iosUrl` empty. The full
walkthrough is in the app repo's `PUBLISHING.md`.

## Files

| File | Purpose |
|---|---|
| `index.html` | The download page. |
| `privacy.html` | Privacy policy (required for App Review — link it in App Store Connect). |
| `config.js` | **Edit this** — the two URLs + support email. |
| `vendor/qrcode.min.js` | QR generator ([qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator), MIT). |
| `assets/app-icon.png` | App icon shown on the page. |
| `.nojekyll` | Serve files verbatim on GitHub Pages. |
