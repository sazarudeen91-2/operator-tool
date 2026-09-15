# Operator Tools — Installable Web App (PWA)

This folder is your original Operator Tools app (Lab Micro Entry, Centrifuge,
Chemical Cal, Data Collection Forms) turned into an installable app that
works on both Android and iOS, with no app store needed.

## What changed from the original file
- Added `manifest.json` + `icons/` so it can be "installed" to a home screen
  like a real app.
- Added `sw.js` (a service worker) so it opens fast and keeps working with a
  weak/no connection after the first visit.
- Fixed the Lab Micro Entry tool's saving: it used to save data using
  a Claude-only API (`window.storage`) that only exists inside Claude's
  artifact preview. It now saves to the browser's own `localStorage`
  instead, so reports are saved **on that device only** — nothing is
  shared between phones/tablets. (The Centrifuge tool already had this
  fallback built in; Chemical Cal doesn't save anything, so it needed
  no change.)

## How to put this on the internet (required for install)
Phones can't "install" a website straight from your computer's file system —
it needs to be served over `https://`. Any static host works, for example:
- **Netlify Drop**: go to app.netlify.com/drop and drag this whole folder in.
  You'll get a live `https://…netlify.app` link in seconds, free.
- **GitHub Pages**, **Cloudflare Pages**, or your own web server also work —
  just make sure `index.html`, `manifest.json`, `sw.js`, and the `icons/`
  folder all stay in the same folder together, at the site's root.

## How to install it on a phone once it's hosted
**Android (Chrome):** open the link → tap the ⋮ menu → "Add to Home screen" /
"Install app".

**iPhone/iPad (Safari):** open the link → tap the Share icon → "Add to Home
Screen". (This must be done in Safari — Chrome on iOS can't install PWAs.)

Once installed, it opens full-screen with its own icon, exactly like a
native app.

## Good to know
- Saved Lab Micro Entry reports live in that browser's storage on that one
  device. Uninstalling the app, clearing site data, or switching browsers
  will lose them — there's no cloud backup with this version.
- PDF/Excel export and the Google Fonts still need internet the first time
  they're used per device (they load from cdnjs/Google Fonts); the service
  worker caches them afterwards so exports keep working offline later.
- The "Data Collection Forms" tab still links out to your existing
  Microsoft Forms — that part is unchanged.

## If you later want a true native app (Play Store / App Store binary)
This same code can be wrapped with a tool like **Capacitor** to produce a
real Android `.apk`/`.aab` and an iOS Xcode project — say the word and I'll
set that project up. You'd need Android Studio (for the Play Store build)
and a Mac with Xcode + an Apple Developer account (for the App Store build)
to finish and submit it.
