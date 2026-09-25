# Coffee Roast Lab 0.4.14

A local-first Android roast logging and analysis app for specialty coffee.

## 0.4.14

### Fixes
- Live chart legend no longer overlaps (chip-style BT / ET / REF / RoR).
- Fan & Heater control strip taller and clearer.
- Temperature log keeps every manual sample (e.g. 4:15) even when it is not on the 30s grid; rows rebuild correctly after leave/return.
- Live notification clock keeps ticking while the app is in the background or on the home screen.
- Suggested drop temperature range restored (density + process).
- Pre-roast style choice: Specialty / Espresso / Omni.
- Post-roast achieved style from DTR + drop BT.

### From 0.4.13
- Monotonic elapsedRealtime timer, live recovery, stock restore, °C/°F conversion, marker order, Second Crack, schema 7.

## Build

CI uses Gradle 8.9 + JDK 17. Upload `CoffeeRoast-v0.4.14-source.zip` to the repo root (or keep the Gradle project at root).

Version `0.4.14` / versionCode `41400`.
