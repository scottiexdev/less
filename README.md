# Less

A tiny, private web app to cut down on nicotine and alcohol. Count your pouches or cigarettes, log your drinks in units, set daily and weekly limits, and watch the trend.

**Live:** https://scottiexdev.github.io/less/

## Features

- **Pick what you track**: the first screen asks "Less of what?" (pouches, cigarettes, alcohol, vaping); only those get a tab. Change it later in *Settings* (the button next to the date).
- **Money saved**: enter the price of a can, a pack, an alcohol unit or a vape refill and how much you used before (pre-filled from a quit plan). If you roll your own, tick *I roll my own* and enter what you spend on tobacco, papers and filters and every how many days you buy them. Saved = (before − logged) × price, every day since a start date, per tracker and in total.
- **Measures**: drink volumes in ml, litres or US fl oz. Alcohol is always counted in UK units.
- **Alcohol**: tap a drink (pint, can, glass of wine, spirit…) or enter ml and % ABV, and it is converted to UK units (ml × % ÷ 1000). Daily and weekly (Monday–Sunday) limits, with a warning as soon as either is reached. Mark dry days and see them counted over 30 days.
- **Pouches and cigarettes** modes, each with its own counter and daily limit
- **Vaping**: log ⅓, ½ or a full tank of liquid; the limit is refills per week (Monday–Sunday), and a quit plan lowers it half a refill at a time. Less follows one quit plan at a time.
- **Strength in mg** per pouch (from the can) or per cigarette, so you also get total mg per day
- **30-day charts**: units per day against your limit, and total nicotine mg per day
- **Quit plan**: on first launch (or from the *Plan* panel) enter how many you use a day and the date you want to stop by. The app lowers the daily limit in a straight line down to 0 on that date and shows each day's target on a calendar next to what you logged. You can skip it.
- **Fix past days**: pick a day with the arrows or the date picker above the counter, or tap a bar in *This week* or a day on the plan calendar, and adjust it with +1 / −
- 7-day averages and week-over-week change
- **Installable** and works offline
  - Android (Chrome): menu → *Add to Home screen* / *Install app*
  - iPhone / iPad (Safari): Share → *Add to Home Screen*. Do this on iOS: Safari may clear data of websites you haven't opened for 7 days, the installed app keeps it.
- Light and dark theme

## Privacy

Less is published by **ScottieLabs**, the data controller under the GDPR. Contact: scottiexdev@gmail.com. The full notice is in the app (*Privacy*, at the bottom of the page).

- **What you log never leaves the device.** There is no server and no account. Everything is stored in your browser's `localStorage`. ScottieLabs never receives it.
- **No third parties on load.** No cookies, no analytics, no ads. Fonts (SIL Open Font License, see `fonts/OFL.txt`) and images are served from this site.
- **Hosting:** GitHub Pages logs visitors' IP addresses, as any web server does ([GitHub privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)).
- **Android app:** the daily reminder is scheduled on the phone; nothing is sent. Tips go through Google Play. The app loads its files from the phone, not from GitHub.
- **Donations** go through PayPal only when someone taps Donate or scans the QR code.
- **Backups:** use **Export backup** from time to time: clearing browser data or uninstalling the browser deletes your history. **Import backup** merges a backup file back in.

## Notes on the numbers

- Pouch mg is the amount printed on the can, not what your body absorbs (usually less).
- The cigarette default is 1 mg, roughly what a smoker absorbs per cigarette. Adjust it if you want.
- Treat the mg chart as a trend line, not a precise comparison between pouches and cigarettes.

## Support

If this helps you cut down, you can buy me a coffee: [Donate with PayPal](https://www.paypal.com/qrcodes/managed/c189142f-aba7-441a-ac65-a644cdb7b9a0?utm_source=consweb_more)

## Run it yourself

It's plain HTML, CSS and JavaScript with no build step. Serve the folder with any static server, for example `python3 -m http.server`, or fork the repo and turn on GitHub Pages (Settings → Pages → Deploy from branch → `main` / root).

## Android app

The same `index.html` runs inside a native shell made with [Capacitor](https://capacitorjs.com) (`android/`, `capacitor.config.json`, app id `com.scottielabs.less`). In the app:

- **Daily reminder** (Settings → Reminder): a local notification the phone schedules by itself, no server. It doesn't ask for the exact-alarm permission, so Android may deliver it a few minutes late.
- **Tips instead of donations**: no PayPal link, because Google Play doesn't allow paying the developer outside its billing. The Support section offers three Play Billing tips, each unlocking a badge (🌱 Seed, 🌿 Sprout, 🌳 Tree). They're one-time products, so each can be bought once and the badges come back after a reinstall. To turn them on, create in Play Console → *Monetize → In-app products* three products with ids `tip_seed`, `tip_sprout`, `tip_tree` and the prices you want (for example 1, 3 and 5 €). Until they exist the buttons stay greyed out. Play only shows them in a build installed from a Play track (internal testing is enough), not in the debug APK.
- Android's back button closes the open sheet before leaving the app. There's no service worker: the files are inside the app.
- The app's data is separate from the website's: use Export and Import backup to move it. Android's cloud backup is off (`allowBackup="false"`), so the data stays on the phone.

**Builds:** the *Android* workflow in GitHub Actions runs on every pull request and push to `main`. It always uploads `less-debug-apk`, which you can install on a phone to try (allow installing from unknown sources). When the upload key secrets exist it also uploads `less-release-aab`, the signed bundle for the Play Console. Each run's number is the `versionCode`.

**Upload key** (once, on your computer; keep the file and passwords safe, you need them for every update):

```bash
keytool -genkeypair -keystore less-upload.jks -alias upload -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 less-upload.jks   # on macOS: base64 -i less-upload.jks
```

Then in the repo, Settings → Secrets and variables → Actions, add `ANDROID_KEYSTORE_BASE64` (the base64 output), `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS` (`upload`) and `ANDROID_KEY_PASSWORD`.

**Building locally:** `npm ci && npm run sync` copies the web files into `www/` and then into the Android project; open `android/` in Android Studio. After changing `index.html`, run `npm run sync` again.

## Setting up the donation link

The *Support Less* section at the bottom of the app shows `donate-qr.png` (a PayPal QR code) and a button to the same link, `DONATE_URL` near the top of the script in `index.html`. To use your own, replace the image and the URL; an empty `DONATE_URL` hides the section. Once someone has logged 7 days, a popup asks for a donation every 2 weeks (a month after "Ask me next month", 3 months after they tap Donate); that choice is stored in `less-donate`, outside the backup.

## Counting visitors

Off by default. To see roughly how many people use the app, create a free site at [GoatCounter](https://www.goatcounter.com) (no cookies, no personal data) and put its code in `const GOATCOUNTER = "";` in `index.html`. Only the page visit is counted, never what anyone logs. Visits while offline aren't counted.

## License

MIT
