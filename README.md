# ICT All-in-One (V1.3) — TradingView Indicator

**All-in-One-ICT + RTH Gap + HTF Candles + CISD** is a single Pine Script v6 overlay that puts the most commonly used ICT (Inner Circle Trader) concepts on one chart: killzones, session pivots, macro windows, opening prices, HTF levels, FVGs, opening gaps, HTF candles and a liquidity-gated CISD signal.

> **Pine Script:** v6 · **Type:** Overlay indicator · **File:** `ICT_All_in_One_V1_3_CISD_v6_switches.pine`
> **Author:** [@projjalroy](https://www.tradingview.com/u/projjalroy/) · **License:** Mozilla Public License 2.0

---

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Feature Details](#feature-details)
- [Settings Reference](#settings-reference)
- [Alerts](#alerts)
- [Performance Notes](#performance-notes)
- [Version Notes](#version-notes)
- [Credits](#credits)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## Features

| Module | What it does |
|---|---|
| **Killzones** | Boxes for Asia, London, NY AM, London Close (NY Lunch) and NY PM, with editable session times |
| **Killzone Pivots** | Session high/low lines and labels that extend until broken (or a cutoff time), with optional break alerts |
| **ICT Macros** | London, NY AM 1–3, NY Lunch, NY PM and NY Last Hour macro windows, with automatic DST detection |
| **Opening Prices** | True Day Open plus three extra configurable opening-price lines |
| **Timestamps** | Up to four vertical time markers |
| **DWM Open** | Daily / Weekly / Monthly opens, separators and day-of-week labels |
| **Levels** | 4H, Daily, Weekly, Monthly, Quarterly, Yearly, Monday range and FX session (London / New York / Tokyo) open, previous H/L and mid |
| **HTF FVGs** | Fair Value Gaps from up to 6 higher timeframes, with mitigation handling |
| **Chart-TF Imbalance** | Fair Value Gaps on the current chart timeframe |
| **Swing Points** | Swing high/low circles with intermediate swing highlighting |
| **NWOG / NDOG** | New Week and New Day Opening Gaps, with optional C.E. (Consequent Encroachment) line |
| **RTH Gap** | Regular-trading-hours gap boxes and midlines (4:15 pm close → 9:30 am NY open) for index futures |
| **HTF Candles** | Higher-timeframe candles drawn beside the chart, with auto-alignment by chart timeframe |
| **CISD** | Change-in-State-of-Delivery signals, restricted to killzones and gated by HTF liquidity |
| **Watermark** | Customisable title, subtitle and symbol/timeframe info |

Every section starts with a **✔ SHOW … (master switch)** tick so you can turn whole modules on or off in one click.

---

## Installation

1. Open [TradingView](https://www.tradingview.com/) and open the **Pine Editor** (bottom panel).
2. Create a new indicator and paste the contents of `ICT_All_in_One_V1_3_CISD_v6_switches.pine`.
3. Click **Save**, then **Add to chart**.

The script imports a helper library (`cryptonnnite/helpers/1`), which TradingView loads automatically when you add the script to a chart.

---

## Quick Start

1. Set **Settings → Timezone** to the timezone your sessions are defined in (default `GMT-5`). Note that GMT offsets are **not** adjusted for Daylight Saving Time.
2. Use an intraday chart. Session drawings are hidden on timeframes **greater than or equal to** *Timeframe Limit* (default `30`).
3. Turn modules on or off with their **✔ SHOW** master switches.
4. If the chart feels slow, lower **Drawing Lookback (bars)** (see [Performance Notes](#performance-notes)).

---

## Feature Details

### Killzones & Pivots
Five configurable sessions, each with its own on/off tick, label, time range and colour:

| Session | Default time (in selected timezone) |
|---|---|
| Asia | 20:00 – 00:00 |
| London | 02:00 – 05:00 |
| NY AM | 07:00 – 10:00 |
| London Close | 11:00 – 12:00 |
| NY PM | 13:30 – 16:00 |

Each session can draw a box, a high line and a low line with labels (e.g. `LO.H`, `NYAM.L`). Lines keep extending until price breaks them or the **Drawing Cutoff Time** (default `1200-1201`) is reached. Per-session **Alerts** fire when a pivot is broken.

### ICT Macros
Macro windows for London, NY AM 1/2/3, NY Lunch, NY PM and NY Last Hour. Time handling is selectable (`UTC`, `Session Local Time` or `Your Time Zone`), with built-in DST detection. Optional range-time and macro labels (`LDN 1`, `NY AM 1`, …).

### Opening Prices, Timestamps & DWM Open
- **Opening Price:** True Day Open (`00:00`) enabled by default; three more lines (`06:00`, `10:00`, `14:00`) available.
- **Timestamps:** four vertical lines (`00:00`, `08:00`, `10:00`, `12:00` by default).
- **DWM Open:** Daily, Weekly and Monthly opens with optional separators and day-of-week labels.

### Levels
Opens, previous high/low and previous mid for **4H, Daily, Weekly, Monthly, Quarterly, Yearly**, plus the **Monday range** and **FX session ranges**. Supports shorthand labels (`PDH`, `PDL`, `PWH`, …), merged labels for overlapping levels, and *Standard* or *Right Anchored* display.

### HTF FVGs & Imbalance
- **HTF FVGs:** up to six timeframes, each with its own colours and maximum count; mitigated FVGs can be shown/hidden.
- **Imbalance:** current-timeframe FVG boxes with configurable colour, transparency and length.

### NWOG / NDOG
New Week and New Day Opening Gaps with C.E. line, label placement and the number of previous gaps to keep.

### RTH Gap
Standard RTH gap (4:15 pm close → 9:30 am New York open) and an optional High-Low gap, each with midline and label. Intended for index futures (ES, NQ, YM); boxes only appear on **15-minute or lower** timeframes.

### HTF Candles
Draws higher-timeframe candles next to the chart. With **Auto HTF by chart timeframe** enabled, the timeframes are chosen for you:

| Chart TF | HTF candles shown |
|---|---|
| M1 | 15m › 4H › 1W |
| M3 | 30m › 12H |
| M5 | 1H › 1D |
| M15 | 4H › 1W |
| M30 | 12H |
| H1 | 1D |
| H4 | 1W |

On any other chart timeframe, the manual HTF 1–6 settings are used.

### CISD (Change in State of Delivery)
A CISD signal prints when:

1. A **delivery series** (consecutive same-direction candles, minimum length configurable) is followed by a close **beyond the open of the last opposite series**,
2. the move happens **inside an enabled killzone** (optional), and
3. **HTF liquidity** was taken beforehand — an HTF FVG take/retest and/or an HTF swing sweep, depending on the *Liquidity gate* setting.

Signals are drawn as `CISD ▲` / `CISD ▼` labels with a dashed line at the broken level, tagged with the liquidity source that qualified them.

**Liquidity gate options**
- `Auto (FVG if in range, else swing)` — default
- `FVG only`
- `FVG or swing`

**FVG take/retest trigger options:** `Zone edge touched`, `CE (50%) reached`, `Fully filled (wick)`.

---

## Settings Reference

### General
| Setting | Default | Description |
|---|---|---|
| Session Drawing Limit | 3 | Number of sessions of drawings kept per type |
| Timeframe Limit | 30 | Drawings are hidden on timeframes ≥ this value |
| Timezone | GMT-5 | Timezone used for killzone / open / timestamp sessions |
| Drawing Cutoff Time | 1200-1201 | Highs/lows stop extending after this time |
| Drawing Lookback (bars) | 1000 | Limits swing labels and small FVG boxes to recent bars (performance) |

### CISD
| Setting | Default | Description |
|---|---|---|
| Show CISD | On | Master toggle |
| Print only inside killzones | On | Uses the killzones enabled in the Killzones group |
| Use HTF FVG | On | Allow HTF FVGs as liquidity |
| Use HTF swing highs / lows | On | Allow HTF swing sweeps as liquidity |
| Also use the indicator's own swing points | Off | Adds chart-TF swing points as extra liquidity |
| Auto HTF alignment by chart timeframe | On | Uses the HTF table above |
| Manual swing TF 1 / 2 / 3 | 4H / 1D / 1W | Used when auto alignment is off or not applicable |
| HTF swing pivot bars (left/right) | 2 | Pivot strength for HTF swings |
| Liquidity gate | Auto | See above |
| FVG take / retest trigger | Zone edge touched | See above |
| Drop an FVG after a candle closes through it | On | Invalidates filled FVGs |
| FVG "in range" distance (× daily ATR) | 1.0 | How close price must be to an HTF FVG |
| Setup expiry (chart bars) | 30 | Max bars between liquidity take and CISD |
| Min candles in delivery series | 2 | Minimum series length |
| Max CISD marks kept on chart | 40 | Older marks are deleted |

---

## Alerts

| Alert | Description |
|---|---|
| `CISD Bullish` | Bullish CISD confirmed (killzone + HTF liquidity) |
| `CISD Bearish` | Bearish CISD confirmed (killzone + HTF liquidity) |
| Pivot break alerts | Per killzone, enable **Alerts** in the *Killzone Pivots* group, then create an alert on the indicator using *Any alert() function call* |

To create an alert: **Add alert → Condition: this indicator → choose the alert → Create**.

---

## Performance Notes

This build is tuned to stay within TradingView's script execution limits, including on the free plan:

- `request.security` calls were merged into tuples (about 46 → 17).
- HTF candles and HTF FVG zones are drawn only on the last bar.
- Swing labels and small FVG boxes are limited to the **Drawing Lookback** window.
- Macro text strings are cached.

If you ever see a *"script takes too long to execute"* error, lower **Drawing Lookback (bars)** or switch off modules you do not use.

---

## Version Notes

**V1.3 (Pine v6, CISD build)**
- Converted from Pine v5 to **v6** (session flags are real booleans; `array_peek` split so bool arrays return `false` instead of `na`).
- Added **master switches** to every section.
- Added the **CISD** module (killzone-only, HTF FVG take/retest + HTF swing sweep gating).
- Added **auto HTF alignment** by chart timeframe for HTF candles and CISD.
- Performance rework (merged security calls, last-bar drawing, lookback window).

---

## Credits

- **RTH Gap** module merged from [@twingall](https://www.tradingview.com/u/twingall/)'s indicator, with identifiers renamed to avoid clashes.
- Uses the TradingView library `cryptonnnite/helpers/1`.
- ICT concepts are the work of Michael J. Huddleston (Inner Circle Trader). This project is an unofficial tool and is not affiliated with him.

---

## Disclaimer

This indicator is for **educational and informational purposes only**. It is not financial advice and does not guarantee results. Trading involves substantial risk of loss. Always do your own research and test on a demo account first.

---

## License

This source code is subject to the terms of the [Mozilla Public License 2.0](https://mozilla.org/MPL/2.0/).

© [@projjalroy](https://www.tradingview.com/u/projjalroy/)
