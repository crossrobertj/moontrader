🌙 Moontrader
Buy or sell, based on the moon.
Moontrader is a self-contained, single-file HTML trading signal dashboard that derives buy/sell recommendations from lunar cycles and a lightweight astrological scoring engine. No server, no build step, no API keys — open the file in a browser and it runs.
Vibecoded by Robert James Cross.

Features

Live lunar signal — Displays the current moon phase, illumination percentage, age in days, and a BUY / SELL / WAIT recommendation with a 0–100 confidence score.
Astrological scoring engine — Combines moon phase bias, lunar declination, lunar latitude, planetary retrograde pressure, cardinal-ingress windows, and Moon-to-planet aspects (conjunct, trine, square, opposite) into a single market score.
Interactive chart — A dual-axis Chart.js graph overlays the buy/sell signal bars against the moon illumination curve for any selected time range.
Time range selector — View signals across four granularities: Year (12 monthly points), Month (30 daily points), Week (7 daily points), Day (24 hourly points).
Date picker — Navigate to any date from year 1000 to year 3000 and see the historical or future signal.
Timezone support — PST, EST, UTC, and CET offsets are supported; all calculations shift accordingly.
Rich chart tooltips — Hover any bar to see the exact moon phase, signal action, summary, top scoring factors, active retrograde planets, and Moon aspects at that moment.
No dependencies to install — All libraries (Tailwind CSS, Chart.js, Google Fonts) are loaded from CDN at runtime.


How to Run

Download Moontrader.html.
Open it in any modern browser (Chrome, Firefox, Safari, Edge).
That's it.

An internet connection is required on first load to fetch Tailwind CSS, Chart.js, and the Inter / Space Grotesk fonts from their CDNs. After the initial paint the page is fully functional offline.

Signal Algorithm
The engine runs entirely in client-side JavaScript. For a given date and timezone:

Moon phase is computed from a known New Moon epoch (January 6, 2000 18:14 UTC) using the synodic month (29.53058867 days). This yields phase name, illumination, and age.
Planetary positions are calculated using NASA JPL mean orbital elements for Mercury through Pluto, propagated via Julian centuries from J2000. Geocentric longitude and retrograde status (negative daily velocity) are derived for each body.
Moon longitude is approximated via a fast linear formula anchored to J2000.
Aspects are checked between the Moon and each planet at four angles — conjunction (0°, ±6° orb), square (90°, ±5°), trine (120°, ±5°), and opposition (180°, ±6°). The six tightest aspects are kept.
Scoring starts at 50 and applies weighted adjustments:
FactorWeightPhase bias (per phase)−28 to +30Positive lunar declination+4Negative lunar declination−4Positive lunar latitude+2Negative lunar latitude−2Cardinal ingress window (±3 days of equinox/solstice)−12Mercury retrograde−8Mars retrograde−10Saturn retrograde−6Venus / Uranus retrograde−5Jupiter retrograde−4Neptune / Pluto retrograde−34+ simultaneous retrogrades−6Moon trine / conjunct Jupiter+7Moon trine / conjunct Venus+5Moon square / opposite Saturn, Mars, or Uranus−8Moon hard aspect to Mercury retrograde−6

Final signal: score ≥ 60 → BUY TODAY (green); score ≤ 40 → SELL TODAY (red); otherwise → WAIT (amber). An active cardinal-ingress window overrides borderline buy signals (40–64) to WAIT. The score is clamped to [12, 88].


UI Sections
SectionDescriptionHomeCurrent signal card with moon emoji, phase name, illumination, action label, summary text, and score bar.GraphFull live dashboard with date picker, timezone selector, range selector, signal card, and Chart.js dual-axis chart.
Navigation is handled client-side with no page reloads.

Tech Stack
LibraryVersionPurposeTailwind CSSCDN (play)Utility-first stylingChart.js4.4.1Dual-axis bar + line chartInterGoogle FontsBody typefaceSpace GroteskGoogle FontsLogo / heading typeface
All JavaScript is vanilla ES2020+ with no framework.

Disclaimer
Moontrader is a creative / experimental tool. The signals are generated from astrological heuristics and are not financial advice. Past lunar correlations with market behavior are not guaranteed to repeat. Trade responsibly.
