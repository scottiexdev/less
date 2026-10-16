# Nicotine Tracker

A tiny, private web app to cut down on nicotine. Count your pouches or cigarettes each day, set a daily limit, and watch the trend.

**Live:** https://scottiexdev.github.io/tracker/

## Features

- **Pouches and cigarettes** modes, each with its own counter and daily limit
- **Strength in mg** per pouch (from the can) or per cigarette, so you also get total mg per day
- **30-day charts**: units per day against your limit, and total nicotine mg per day
- **Quit plan**: on first launch (or from the *Plan* panel) enter how many you use a day and the date you want to stop by. The app lowers the daily limit in a straight line down to 0 on that date and shows each day's target on a calendar next to what you logged. You can skip it.
- **Fix past days**: pick a day with the arrows or the date picker above the counter and adjust it with +1 / −
- 7-day averages and week-over-week change
- **Installable** and works offline
  - Android (Chrome): menu → *Add to Home screen* / *Install app*
  - iPhone / iPad (Safari): Share → *Add to Home Screen*. Do this on iOS: Safari may clear data of websites you haven't opened for 7 days, the installed app keeps it.
- Light and dark theme

## Privacy

There is no server and no account. Everything is stored in your browser's `localStorage` on your device. Use **Export backup** from time to time: clearing browser data or uninstalling the browser deletes your history. **Import backup** merges a backup file back in.

## Notes on the numbers

- Pouch mg is the amount printed on the can, not what your body absorbs (usually less).
- The cigarette default is 1 mg, roughly what a smoker absorbs per cigarette. Adjust it if you want.
- Treat the mg chart as a trend line, not a precise comparison between pouches and cigarettes.

## Support

If this helps you cut down, you can buy me a coffee: [Support this app](DONATE_LINK_HERE)

## Run it yourself

It's plain HTML, CSS and JavaScript with no build step. Serve the folder with any static server, for example `python3 -m http.server`, or fork the repo and turn on GitHub Pages (Settings → Pages → Deploy from branch → `main` / root).

## Setting up the donation link

Open `index.html`, find `const DONATE_URL = "";` near the top of the script and paste your page (Ko-fi, Buy Me a Coffee, PayPal.me, GitHub Sponsors). The "Support this app" link appears in the footer only when it's set. Replace `DONATE_LINK_HERE` above with the same URL.

## License

MIT
