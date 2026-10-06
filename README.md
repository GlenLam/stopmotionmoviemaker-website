# stopmotionmoviemaker.com

Marketing and support site for Stop Motion Movie Maker, the iPhone and iPad app for making stop-motion movies with toys, puppets and clay. Static HTML with no build step and no third-party requests, served by GitHub Pages at **https://stopmotionmoviemaker.com**. The app itself lives in `stopmotion-camera` (Xcode project).

## About Stop Motion Movie Maker

A stop-motion movie studio inspired by children's-museum puppet stations: simple enough for an 8-year-old, deep enough for anyone who wants to go all out.

- **Capture.** Five big buttons (Snap, Oops, Play, Ghost, Done), a ghost of the last picture (onion skin), and a camera that locks focus, exposure and white balance after the first picture so frames don't flicker. Speeds: 🐢 6, 🐇 12, 🚀 24 pictures a second. Done, pressed twice, saves the movie to Photos and starts a new one.
- **Auto Snap.** Takes the picture once everything holds still and no hand is in the picture (Vision, on the device). Never takes the same picture twice.
- **Decorate.** Words and speech bubbles, 54 sound effects, an opening title, and "The End" or rolling credits. With Pro: stickers, 9 songs and My Songs (Files, the Music app, Share and AirDrop), voice-over, 11 color looks, and video clips.
- **Big screen and buttons.** A TV or monitor over HDMI or AirPlay shows the stage while the phone is the remote. Keyboards, button boxes (F13–F17), foot pedals, game controllers including the Xbox Adaptive Controller, camera remotes, volume buttons, Camera Control and AirPods. Museum mode plus Guided Access for unattended stations.
- **Studio mode.** Manual camera, time-lapse, shooting on twos, frame editor, timeline, keyframes, transitions, video import, 4K/HEVC export and project backups.
- **Stop Motion Pro.** One-time purchase: 1080p HD and 4K, no "Made with Stop Motion Movie Maker" badge, music, voice-overs, stickers, looks, video clips, adding photos, animated GIFs. Free movies save at 720p with the badge.
- **Privacy.** No account, ads, analytics, tracking or third-party code; the app makes no network connections of its own. The full picture is in `privacy.html`.

Requires iOS 26 or iPadOS 26 or later. Made by CaLa Studios LLC. Questions go to support@calastudios.app.

## Pages

| Path | File | Purpose |
| --- | --- | --- |
| `/` | `index.html` | Landing page |
| `/how-to-make-a-stop-motion-movie` | `how-to-make-a-stop-motion-movie.html` | Step-by-step guide, written for search (see below) |
| `/support` | `support.html` | FAQ and contact; the App Store listing's Support URL |
| `/privacy` | `privacy.html` | Privacy policy; the App Store listing's Privacy Policy URL, and the address for `AppLinks.privacyPolicy` in the app |
| `/404` | `404.html` | Not-found page |

GitHub Pages serves `support.html` at `/support` (and `/support.html`), so the extensionless URLs work as-is. Terms of Use link to Apple's [Standard EULA](https://www.apple.com/legal/internet-services/itunes/dev/stdeula/); there is no terms page here.

`privacy.html` adds an `embedded` class to `<html>` when it detects it is inside an iframe and hides its header and footer, so the policy alone can be embedded elsewhere.

## Layout

- `assets/css/site.css` – the one stylesheet, shared by every page. Light only, like the app's kid screens. Colors are the hex values from the app's `Theme.swift`: Cream `#FFF8E7` canvas, Ink `#2B2350` text, Night `#1B1A3A` bands, and the seven candy colors with one job each (Grass Snap, Tomato Oops, Sky Play, Grape Ghost, Sunny Done, Bubblegum Edit, Tangerine). Grape is the only candy color used for text (5.3:1 on cream). Buttons are drawn as the app's candy buttons, on a lip that is the app's `shaded(-0.3)` of their color.
- `assets/js/site.js` – mobile nav, scroll reveal, footer year. No dependencies.
- `assets/img/` – app icon sizes (`icon-*`, from the app's `AppIcon.png`), the six App Store screenshots in listing order (`shot-0N-*.webp`, the gallery), the camera and editor screens behind them (`screen-*.webp`, the hero's phones), the toy-set photo as the clean stage (`stage.webp`), the Auto Snap screen's stage with a hand in it (`autosnap-hand.webp`), Apple's App Store badge and `og-image.jpg` for link previews.
- `assets/fonts/` – Nunito, subset to Latin with weights 500–900 as one variable WOFF2 (SIL OFL, license alongside). The font stack puts `ui-rounded` first, so Safari on Apple devices uses SF Pro Rounded, the app's own typeface, and only other browsers download Nunito.
- The five button glyphs (camera, back arrow, play, dashed circle, check) are an inline SVG sprite at the top of `index.html`, drawn after the app's SF Symbols. The "come alive!" sticker and the free-movie badge follow `Watermark.swift`: rainbow letters on a navy face over a rainbow lip, tilted 3°.
- `sitemap.xml`, `robots.txt`, `site.webmanifest` – the usual metadata.
- `CNAME` – `stopmotionmoviemaker.com`, so the custom domain survives redeploys.
- `.nojekyll` – tells Pages to publish the files as they are.

## Updating

Edit the HTML, commit to `main`, push. Pages redeploys in about a minute. Pages tells browsers to keep files for 10 minutes, so every page links the stylesheet as `site.css?v=YYYYMMDD`: **when `site.css` changes, bump that date on all five pages** (add a letter for a second change the same day), or visitors can get new HTML with the old styles.

Feature copy follows the build that is live in the App Store, not what is in development. The counts on the landing page (54 sound effects, 9 songs, 11 looks) come from the app's `Resources/sounds.json` and the `Look` enum in `Model/Timeline.swift`; update them when those change. The privacy policy describes an app that collects nothing and makes no network connections, asks for the camera, the microphone (voice-over only), add-only Photos and Media & Apple Music (adding a song from the Music app), and imports through the system photo and file pickers; change the policy and its effective date before a change to any of that ships.

To regenerate images: everything comes from the v1.0 App Store set, so the site shows what the listing shows. The `shot-*` files are the listing's 6.5″ iPhone screenshots (1242×2688), resized to 720 wide. The `screen-*` files and the two stage crops come from the raw sources behind them (`source/app-screens/` and `source/photos/toy-set.png` in the App Store working folder): 1320×2868 screens resized to 600 wide, and 16:9 crops at 800×450 (`autosnap-hand.webp` is the stage of `autosnap.png`, x 36–1284, y 648–1350). All are encoded with `cwebp -q 82`. When the screenshots change, swap the `shot-*` files and their alt text together. `og-image.jpg` is a 1200×630 HTML composition (site.css, the icon, the headline and the two `screen-*` phones) rendered with headless Chrome.

### The how-to guide and search

`how-to-make-a-stop-motion-movie.html` is the page meant to bring in search traffic: "how to make a stop motion movie", "stop motion on iPhone", "stop motion ideas for kids", "why does my stop motion flicker" and the like. Its title, description, H1 and URL carry the main phrase; the frame-rate table, six steps, tips, ideas and six questions answer the related ones directly, in under 800 words. Keep it short: each step is one card with at most one picture. Step numbers come from a CSS counter on the `<ol>`, so headings stay clean in search results and reader views. Its JSON-LD has `BreadcrumbList`, `Article`, `HowTo` and `FAQPage`; the `HowTo` steps and the FAQ answers repeat the visible text, so **change both together**, and bump `dateModified`, the visible "Updated" date and its `sitemap.xml` `lastmod` when the content changes. Every page links to it from the nav ("How to") and footer, and the home page's How it works and Support's first-movie answer link to it in context. App facts in it (speeds, buttons, Auto Snap, Pro) follow the same rule as the rest of the site: the live build.

Search Console (Google) and Bing Webmaster Tools should both have `https://stopmotionmoviemaker.com/sitemap.xml` submitted, and a new page can be sent for indexing from Search Console's URL Inspection.

### App Store

The app went live on October 6, 2026: https://apps.apple.com/us/app/stop-motion-movie-maker/id6815898667 (app ID `6815898667`, free with Stop Motion Pro as an in-app purchase). That URL is behind both App Store badges and the "Get the app" button on every page, and in each page's footer; `index.html` also carries it in the Smart App Banner (`apple-itunes-app`) and its JSON-LD. If the listing's URL changes, update it everywhere at once.
