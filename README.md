# All-in-One ICT Indicator (Pine Script v5)

A TradingView indicator that combines several ICT (Inner Circle Trader) concepts in one script.

## Features

**Sessions and time**
- Killzone boxes for Asia, London, NY AM, London Close and NY PM, with session highs and lows, labels and optional break alerts
- ICT macro windows: London 1/2, NY AM 1/2/3, NY Lunch, NY PM and NY Last Hour. Daylight saving is detected automatically, and times can be shown in UTC, New York time or your own time zone
- Day-of-week labels, vertical timestamp lines and "True Day Open" and other opening-price lines

**Key price levels**
- Previous day, week, month and quarter high, low and midpoint
- Current-year high and low
- Daily, weekly, monthly, quarterly and yearly opens
- Monday range, previous 4H levels, and London, New York and Asia session ranges
- Nearby levels can be merged into one combined label
- Standard and right-anchored display styles

**Imbalances and gaps**
- Multi-timeframe Fair Value Gaps (5m, 15m, 1H, 4H, 1D, 1W) with consequent encroachment (CE) lines, mitigation options and labels
- Current-timeframe FVG boxes
- New Week Opening Gap (NWOG) and New Day Opening Gap (NDOG), with optional CE lines, price labels and Event Horizon
- RTH gap: the gap between the 4:15pm close and the 9:30am New York open (4pm on SPY), with a midline and labels

**HTF candles**
- Higher-timeframe candles drawn to the right of the chart (up to six timeframes), with remaining-time countdown, interval labels and a custom daily open
- FVG and volume-imbalance detection between HTF candles, and optional trace lines back to the HTF open, high, low and close

**Market structure**
- Short-term and intermediate swing high and low markers

**Extras**
- Chart watermark with title and symbol/timeframe info

## Installation
1. Open the Pine Editor in TradingView.
2. Paste the contents of `ICT_All_in_One_HTF_Candles.pine`.
3. Click **Add to chart**.

## Notes
- Written in Pine Script v5. It imports the `cryptonnnite/helpers/1` library for the NWOG/NDOG gap code.
- Session times default to GMT-5 (New York). Change the time zone in the settings if you trade from another region.
- This is a charting tool only, not financial advice.

## Credits and license
This script merges and adapts work from:
- **ICT All-in-One v1.2** by @projjalroy
- **ICT HTF Candles** by @fadizeidan (ported from Pine v6 to v5)
- **RTH/ETH gap indicator** by @twingall
- **cryptonnnite/helpers** library for the opening-gap code

Released under the **Mozilla Public License 2.0**, matching the source scripts. Check each original author's terms before publishing.
