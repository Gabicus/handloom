# Handloom

A hand-woven instrument. Sing into your mic and play effects, harmonies and folk voices with your hands in the air, via the camera. Inspired by Imogen Heap's Mi.Mu gloves and jaida_quinn's MediaPipe → Ableton harmonizer reel.

- **Phone mode:** one hand in front of the camera, plus a touch pad for your other thumb. Up to 4 loop layers.
- **Computer mode:** two hands, the full rack, thread (mod-matrix) editor, 4 weather LFOs, sound-library uploads, MIDI CC/notes out to a DAW, 8 loop layers, and takes recorded to file.

Everything runs in the browser. Camera and mic never leave the device.

**Play it:** https://gabicus.github.io/handloom/
**Android app:** https://github.com/Gabicus/handloom/releases/latest/download/handloom.apk

## Layout

- `web/`: the whole app (one `index.html` plus a PWA manifest, service worker and icons). Pushing to `main` deploys it to Pages.
- `.github/workflows/android.yml`: wraps `web/` in a Capacitor shell, bundles Tone.js, MediaPipe and the hand model so it runs offline, and publishes `handloom.apk` as a release.

### Stable APK signature (optional)
Each build signs with a fresh debug key unless you add one, so installing a newer APK over an older one fails ("app not installed"). Uninstall first, or add a key once:
```bash
keytool -genkeypair -keystore hl.keystore -storepass android -alias androiddebugkey -keypass android -keyalg RSA -keysize 2048 -validity 10000 -dname "CN=Handloom"
base64 -w0 hl.keystore | gh secret set ANDROID_DEBUG_KEYSTORE_B64 -R Gabicus/handloom
```

## Deploy your own copy to GitHub Pages

1. Create a new **public** repo, e.g. `handloom`.
2. Put the `web/` folder and `.github/` in the repo.
3. Repo → **Settings → Pages** → Source: **GitHub Actions**.
4. After about a minute it's live at `https://<you>.github.io/handloom/`.

Or from a terminal with the GitHub CLI:

## iPhone / iPad
Open the Pages link in Safari, then Share → **Add to Home Screen**. Camera, mic and hand tracking work in Safari.

## Install on a PC

Open the Pages URL in Chrome or Edge, then click the **install** icon in the address bar (or menu → *Install Handloom*). It gets its own window and start-menu icon, and works offline after the first load.

## Tips

- **Wear headphones.** The mic goes through the effects live. If you have to use speakers, turn on *Speaker mode* in Settings.
- **For Ableton** (like the reel): Settings → Enable MIDI → pick a loopMIDI or IAC port. Each thread sends a CC (number set per thread) and voices send notes on channel 1.
- Default hand signs (desktop): left ✊ = record/stop a loop layer, left ✌ = undo, left 👍 = freeze, right 🤘 = next preset. Phone: 👍 = record, ✌ = undo, 🤘 = next. All of them can be remapped in Threads.
- Keyboard: Space loop · Z undo · ←/→ presets · F freeze · M mic · 1–0 toggle effects.
- Presets you save can be exported as JSON (⇅) and shared.

## Libraries

Tone.js 15.1.22 and MediaPipe Tasks Vision 0.10.35 (both from jsDelivr), plus Google's hand_landmarker model.
