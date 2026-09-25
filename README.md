# Coffee Roast Lab

Local-first Android app for logging and analyzing coffee roasts.

**Current version: `0.4.20`** · versionCode `42000`

Source zip: [`CoffeeRoast-v0.4.20-source.zip`](CoffeeRoast-v0.4.20-source.zip)

Latest CI: [Android Build](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions) — signed release APK is uploaded as an artifact.

## What it does

- Live roast timer with bean-temp / env-temp log, RoR, fan & heater changes
- Markers: Turning Point, Dry End, First Crack, Second Crack, Drop
- Roast style: Specialty / Espresso / Omni at start, then achieved style from DTR + drop temp
- Suggested drop range from density + process
- Green bean stock, roasted inventory / resting, cupping scores
- Dashboard, calculators, °C/°F, backup / restore, Artisan-style export
- Data stays on the phone (`coffeeroast_data.json` + `.bak` + recovery files)

## Persistence (the important part)

Saves never write `NaN`/`Infinity` (Android `org.json` forbids them — that was the bug that made new roasts disappear).

- Write path: temp file → backup → main file, then parse-verify
- Load path: main → `.bak` → recovery snapshots
- If a file exists but cannot be parsed, it is **kept**, not overwritten with an empty database

## Build

1. Put the latest `CoffeeRoast-v*-source.zip` in the repo root (only one zip needed).
2. Push to `main`.
3. GitHub Actions (`android-build.yml`) extracts the zip, runs unit tests, and builds a **signed** release APK.

Requires secrets: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

- minSdk 26 · targetSdk 35 · JDK 17 · Gradle 8.9

## Schema

Local JSON schema version **7**. Older files migrate on load.
