# stopmotionmoviemaker.com

Marketing and support site for Stop Motion Movie Maker, the iPhone and iPad app for making stop-motion movies with toys, puppets and clay. Static HTML with no build step and no third-party requests, served by GitHub Pages at **https://stopmotionmoviemaker.com**. The app itself lives in `stopmotion-camera` (Xcode project).

## About Stop Motion Movie Maker

A stop-motion movie studio inspired by children's-museum puppet stations: simple enough for an 8-year-old, deep enough for a grown-up who wants to go all out.

- **Capture.** Five big buttons (Snap, Oops, Play, Ghost, Done), a ghost of the last picture (onion skin), and a camera that locks focus, exposure and white balance after the first picture so frames don't flicker. Speeds: 🐢 6, 🐇 12, 🚀 24 pictures a second. Done, pressed twice, saves the movie to Photos and starts a new one.
- **Auto Snap.** Takes the picture once everything holds still and no hand is in the picture (Vision, on the device). Never takes the same picture twice.
- **Decorate.** Words and speech bubbles, stickers (Pro), 54 sound effects, 9 songs, voice-over, My Songs (Files, the Music app, Share and AirDrop), 11 color looks, an opening title, and "The End" or rolling credits.
- **Big screen and buttons.** A TV or monitor over HDMI or AirPlay shows the stage while the phone is the remote. Keyboards, button boxes (F13–F17), foot pedals, game controllers including the Xbox Adaptive Controller, camera remotes, volume buttons, Camera Control and AirPods. Museum mode plus Guided Access for unattended stations.
- **Studio mode.** Manual camera, time-lapse, shooting on twos, frame editor, timeline, keyframes, transitions, video import, 4K/HEVC export and project backups.
- **Stop Motion Pro.** One-time purchase: 1080p HD and 4K, no "Made with Stop Motion Movie Maker" badge, stickers, adding photos, animated GIFs. Free movies save at 720p with the badge.
- **Privacy.** No account, ads, analytics, tracking or third-party code; the app makes no network connections of its own. The full picture is in `privacy.html`.

Requires iOS 26 or iPadOS 26 or later. Made by CaLa Studios LLC. Questions go to support@calastudios.app.

## Pages

| Path | File | Purpose |
| --- | --- | --- |
| `/` | `index.html` | Landing page |
| `/support` | `support.html` | FAQ and contact; the App Store listing's Support URL |
| `/privacy` | `privacy.html` | Privacy policy; the App Store listing's Privacy Policy URL, and the address for `AppLinks.privacyPolicy` in the app |
| `/404` | `404.html` | Not-found page |

GitHub Pages serves `support.html` at `/support` (and `/support.html`), so the extensionless URLs work as-is. Terms of Use link to Apple's [Standard EULA](https://www.apple.com/legal/internet-services/itunes/dev/stdeula/); there is no terms page here.

`privacy.html` adds an `embedded` class to `<html>` when it detects it is inside an iframe and hides its header and footer, so the policy alone can be embedded elsewhere.

## Layout

- `assets/css/site.css` – the one stylesheet, shared by every page. Light only, like the app's kid screens. Colors are the hex values from the app's `Theme.swift`: Cream `#FFF8E7` canvas, Ink `#2B2350` text, Night `#1B1A3A` bands, and the seven candy colors with one job each (Grass Snap, Tomato Oops, Sky Play, Grape Ghost, Sunny Done, Bubblegum Edit, Tangerine). Grape is the only candy color used for text (5.3:1 on cream). Buttons are drawn as the app's candy buttons, on a lip that is the app's `shaded(-0.3)` of their color.
- `assets/js/site.js` – mobile nav, scroll reveal, footer year. No dependencies.
- `assets/img/` – app icon sizes (`icon-*`, from the app's `AppIcon.png`), raw device screens (`screen-*.webp`), two crops of the camera stage (`stage.webp`, clean; `autosnap-hand.webp`, with Auto Snap waiting for a hand), Apple's App Store badge (for launch, see below) and `og-image.jpg` for link previews.
- `assets/fonts/` – Nunito, subset to Latin with weights 500–900 as one variable WOFF2 (SIL OFL, license alongside). The font stack puts `ui-rounded` first, so Safari on Apple devices uses SF Pro Rounded, the app's own typeface, and only other browsers download Nunito.
- The five button glyphs (camera, back arrow, play, dashed circle, check) are an inline SVG sprite at the top of `index.html`, drawn after the app's SF Symbols. The "come alive!" sticker and the free-movie badge follow `Watermark.swift`: rainbow letters on a navy face over a rainbow lip, tilted 3°.
- `sitemap.xml`, `robots.txt`, `site.webmanifest` – the usual metadata.
- `CNAME` – `stopmotionmoviemaker.com`, so the custom domain survives redeploys.
- `.nojekyll` – tells Pages to publish the files as they are.

## Updating

Edit the HTML, commit to `main`, push. Pages redeploys in about a minute.

Feature copy follows the build that is live in the App Store, not what is in development. The counts on the landing page (54 sound effects, 9 songs, 11 looks) come from the app's `Resources/sounds.json` and the `Look` enum in `Model/Timeline.swift`; update them when those change. The privacy policy describes an app that collects nothing and makes no network connections, asks for the camera, the microphone (voice-over only), add-only Photos and Media & Apple Music (adding a song from the Music app), and imports through the system photo and file pickers; change the policy and its effective date before a change to any of that ships.

To regenerate images: the screens come from the Simulator, which uses the app's simulated camera, with the debug launch arguments from the app's README, for example `xcrun simctl launch booted app.calastudios.stopmotion-camera -ResetLibrary YES -SeedProject demo -OpenScreen capture` (then `-OpenScreen editor`, `-Autopilot credits`, `-OpenTool titles`, `-OpenTool music -SeedSongs YES`, `-Autopilot autosnap`). They are iPhone 17 Pro Max screenshots (1320×2868) resized to 600 wide and encoded with `cwebp -q 82`. `og-image.jpg` is a 1200×630 HTML composition rendered with headless Chrome.

### When the App Store listing goes live

1. Replace each `<span class="store-soon" data-store>…</span>` (two in `index.html`) with the official badge:
   ```html
   <a class="badge-link" href="https://apps.apple.com/app/idAPP_ID"><img src="/assets/img/app-store-badge.svg" alt="Download on the App Store" width="162" height="54"></a>
   ```
2. Point every "Get the app" button (`href="#download"` / `href="/#download"`) at the same App Store URL, and change the CTA's "coming soon" line.
3. Add `<meta name="apple-itunes-app" content="app-id=APP_ID">` to `index.html` for Safari's Smart App Banner, and `downloadUrl`, `installUrl` and `offers` to its JSON-LD.
4. Add an "App Store" link to each page's footer.
5. Swap the raw device screens for the App Store screenshots once they exist, if they tell the story better.
