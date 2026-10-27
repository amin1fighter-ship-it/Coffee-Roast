# Coffee Roast Lab

**A roast lab that fits in a pocket.**

Log a roast while it is happening. Keep the curve, the controls, the inventory, and the cup in one place. The app describes what the profile did. It does not declare that a roast “is espresso” or “is baked.”

نرم‌افزار رست برای کنار دستگاه. همهٔ داده روی گوشی می‌ماند. هدف دم‌آوری را خودت انتخاب می‌کنی؛ برنامه از روی DTR یا دمای دراپ حدس نمی‌زند.

[![version](https://img.shields.io/badge/version-0.6.0-6F4E37)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![build](https://img.shields.io/github/actions/workflow/status/amin1fighter-ship-it/Coffee-Roast/android-build.yml?branch=main&label=Android%20Build)](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)
[![platform](https://img.shields.io/badge/Android-8%2B-3DDC84)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![data](https://img.shields.io/badge/data-local%20first-2E8B57)](https://github.com/amin1fighter-ship-it/Coffee-Roast)

**v0.6.0** · versionCode `60000` · local schema `9`  
Source: [`CoffeeRoast-v0.6.0-source.zip`](CoffeeRoast-v0.6.0-source.zip)  
Signed APK: [Actions → latest successful run → artifacts](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)

---

## How a roast is read

Four questions stay separate. Mixing them is how a log turns into a bad verdict.

| Layer | What it is | Where it comes from |
|---|---|---|
| Brew intent | Filter, Espresso, Omni, or Other | Chosen before charge. Historical imports can stay **Not recorded**. |
| Reference roast level | Very Light through Very Dark | Chosen by you, then compared with weight loss as a *working band*, not a color measurement. |
| Development | Time after first crack, DTR, late RoR | Observed. DTR alone is never a quality score. |
| Cup | Fragrance through overall, notes | Cupping, after the roast. |

Omni means “meant for more than one brew method.” It is not a synonym for medium.

Phase percentages (dry, Maillard, development) describe the shape of the curve. They do not name the brew method.

---

## Live roast

- Charge with bean, green weight, optional density, starting fan and heater, charge bean temperature, and roaster name.
- Green stock is reserved when the roast starts, and put back if the save fails or the roast is deleted.
- Monotonic clock (`elapsedRealtime`). Leaving the app does not freeze the roast or the notification.
- Screen stays on during a live roast. Back goes home; the roast keeps running and can be resumed.
- Live readout: bean temperature, environment temperature, RoR, and ETA to your dry-end, first-crack, and drop targets. ETA uses the median RoR of the last 30 / 60 / 90 seconds.
- Low-RoR warning when the slope falls under the limit you set.
- Temperature log on your interval (default 30 s), plus any off-grid point. A sample at 4:15 stays at 4:15, and every past point can be edited.
- Markers, in order: Turning Point, Dry End, First Crack, Second Crack, Drop. Existing markers can be edited or removed. Out-of-order times are rejected.
- Fan and heater changes, each with time, level (0–100), and bean temperature.
- Roast notes during the roast.
- Drop asks for the final bean temperature, then saves.

### The chart

One canvas, built so the labels do not collide:

- Bean temperature, environment temperature, and up to a reference curve
- Rate of rise on the same plot, with its own right-hand axis
- Event lines for TP, DE, FC, SC, and Drop, each on its own lane
- A fan / heater strip under the time axis (`F12`, `H8`, …)
- Smoothing of 1, 3, or 5 samples on the summary chart
- °C or °F on the axis; storage stays in Celsius

---

## After the drop

The summary is a lab sheet, not a stamp.

- Weight loss, and whether it sits inside the reference band for the roast level you chose. Those bands are broad working ranges (for example light 12–15%, medium 15–19%). They are not an industry standard and not a substitute for color.
- Dry / Maillard / development split.
- Working drop range from green density and process (naturals and honeys shift the hint). Shown only as a machine aid.
- Post-roast density: bulk or particle/true, with measurement age. The screen suggests repeating a personal protocol around 24 hours. It does not claim ISO compliance.
- Density retention and reduction. Volume expansion is estimated only for particle/true density. Bulk density is never treated as bean-volume expansion.
- Thermal observations: environment-temperature coverage, and the RoR change in the 60 seconds after each fan or heater move. RoR is a slope, not energy. Heater level 15 is not “15 units of heat.”
- Development observations: duration, DTR, end-of-development RoR, and a pattern such as “late-stage RoR flattening” or “RoR remains measurable.” No “underdeveloped” or “baked” label.
- Edit green weight, roasted weight, starting fan and heater, and notes after the fact. Events and the control history can be added, edited, deleted, and re-sorted.
- Cupping on the ten usual attributes, in a scrollable form so Save stays reachable. Total is out of 100.
- Resting days and remaining roasted weight.
- Reference overlay from another roast of the same coffee.
- Delete returns the reserved green stock.

---

## Roast plan

Write the profile before you charge.

- Saved on the phone, separate from the roast database.
- Lines like `4:30 fan 12` and `6:00 heater 8` can be applied onto the open roast.
- Lines aimed at a bean temperature stay as reference text. They are not triggered automatically.
- The app does not control roaster hardware.

---

## The rest of the roastery

**Green beans.** Name, origin, process, variety, altitude, supplier, price, harvest, storage location, notes, and stock in grams.

**Roasted inventory.** Remaining weight and a simple rest clock: still resting, or in the peak window.

**Dashboard.** Roast count, average weight loss, average DTR, cupped count and average score, and stock per bean. Export the table as CSV.

**Tools.**

- Green weight needed for a target roasted weight and expected loss
- Brew ratio (cups, dose, water)
- Independent stopwatch
- Grams ↔ ounces
- Charge-temperature heuristic from batch weight, density, and a base charge — labeled as a heuristic, not a recipe
- Pre-roast blend builder (percentages should add to 100)

**Settings.** °C/°F and g/oz for display. Log interval. Targets for dry end, first crack, drop, and the low-RoR warning. Default rest days. Four palettes: Dark Roast, Light Lab, Forest, Ember. Dialogs follow the palette so a light phone theme does not wash out the forms.

**Import.** A finished roast can be entered by hand. If you did not record an intent, it stays **Not recorded** instead of quietly becoming Filter.

---

## Export

| Export | What you get |
|---|---|
| Artisan TSV | Time, BT, ET, and named events |
| Roast CSV | The temperature log |
| Dashboard CSV | One row per roast: weights, loss, densities, level, intent, DTR, development, score |
| PDF | A shareable report of that roast |
| Backup ZIP | The whole database |
| Raw JSON | The file the app actually stores |

Share goes through the Android share sheet.

---

## Data

Nothing is uploaded unless you export it.

| File | Role |
|---|---|
| `coffeeroast_data.json` | The live database |
| `coffeeroast_data.json.bak` | The last copy that parsed |
| `coffeeroast_recovery_*.json` | Kept when a write fails |

A save writes a temp file, keeps the previous good copy, then replaces the main file and reads it back. `NaN` and infinities are never written. If a file is present but cannot be parsed, it is left in place — the app will not overwrite your history with an empty database.

Schema **9** migrates older files, including the old `specialty` intent (now Filter) and missing fan/heater points at 0:00.

From Backup you can also force a save and read the storage report, or share a crash log if one was written.

---

## Build

The repo is a source zip plus a GitHub Action.

1. Keep one `CoffeeRoast-*-source.zip` in the root.
2. Push to `main`.
3. [`.github/workflows/android-build.yml`](.github/workflows/android-build.yml) unpacks it, runs the unit tests, and signs a release APK.

Secrets: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

**minSdk 26 · targetSdk 35 · JDK 17 · Gradle 8.9 · Kotlin** · one activity, no cloud account.

```
app/src/main/java/com/amin1fighter/coffeeroast/
  MainActivity.kt      every screen
  RoastChartView.kt    the live curve
  RoastMath.kt         RoR, phases, density, thermal response
  Storage.kt           JSON, backup, schema 9
  Models.kt            beans, sessions, cupping, settings
```

---

Charge. Log. Drop. Taste. Then decide — not the other way around.
