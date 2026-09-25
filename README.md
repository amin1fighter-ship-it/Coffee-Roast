# Coffee Roast Lab

**A pocket roast lab for people who care about the curve.**

Log a roast while it happens. See the curve, the RoR, the phases. Know whether you landed Specialty, Espresso, or Omni — not from a guess, from the numbers you just recorded.

نرم‌افزار روست برای قهوه‌دوست‌های تخصصی. همه چیز روی گوشی می‌ماند. حساب ابری نمی‌خواهد. فقط روست، تحلیل، کاپ، موجودی.

[![version](https://img.shields.io/badge/version-0.4.20-6F4E37)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![build](https://img.shields.io/github/actions/workflow/status/amin1fighter-ship-it/Coffee-Roast/android-build.yml?branch=main&label=Android%20Build)](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)
[![platform](https://img.shields.io/badge/Android-8%2B-3DDC84)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![data](https://img.shields.io/badge/data-local%20first-2E8B57)](https://github.com/amin1fighter-ship-it/Coffee-Roast)

**v0.4.20** · versionCode `42000` · schema `7`  
Source: [`CoffeeRoast-v0.4.20-source.zip`](CoffeeRoast-v0.4.20-source.zip)  
Signed APK: [Actions → latest successful run → artifacts](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)

---

## Why it exists

Most roasting software is built for a laptop next to a 15 kg machine.  
This one is built for a phone next to a home or sample roaster.

You charge the beans. You tap **Charge**. You mark turning point, dry end, first crack, drop. Fan and heater changes go on the same timeline. When you drop, the app tells you the development ratio, the phase split, the weight loss — and which style you actually roasted, not only which style you intended.

---

## A roast, start to finish

1. Pick a green bean from inventory (stock is reserved automatically).
2. Choose a **target style**: Specialty (Filter), Espresso, or Omni.
3. See a **suggested drop range** from density and process (naturals sit a little cooler).
4. Roast live. The chart draws BT, ET, reference curve, and RoR. The notification clock keeps running if you leave the screen.
5. Log temperatures on the interval *and* off-grid (a sample at 4:15 stays at 4:15).
6. Mark **TP → DE → FC → SC → Drop** in order.
7. After drop: weight loss, DTR, dry / Maillard / development percentages, and **achieved style** from the curve.
8. Score the cup later. Rest the batch. Export if you want.

---

## What you get

### Live roast
- Monotonic timer (`elapsedRealtime`) so a lock-screen or timezone change does not jump the clock
- Bean temperature and optional environment temperature
- Rate of rise, ETA toward dry-end / first-crack / drop targets
- Fan and heater strip on the same chart
- Resume a roast that is still in progress

### Analysis
- Development time ratio
- Phase percentages (dry, Maillard, development)
- Achieved style heuristic from DTR + drop temperature
- Suggested drop °C from green density + process
- Reference curve overlay from a previous roast

### Inventory
- Green beans: origin, process, variety, altitude, supplier, stock grams
- Roasted inventory with resting days
- Cupping scores (SCA-style attributes)
- Dashboard: counts, averages, recent batches

### Tools
- Weight / density helpers
- Charge and brew calculators
- °C / °F and grams / other units in settings
- Backup and restore (ZIP)
- Import a legacy roast by hand
- Artisan-style TSV / CSV / PDF export from a finished roast

---

## Privacy, by design

Nothing leaves the phone unless you export it.

| File | Role |
|---|---|
| `coffeeroast_data.json` | Live database |
| `coffeeroast_data.json.bak` | Last good copy |
| `coffeeroast_recovery_*.json` | Emergency dump if a write fails |

Writes go temp → backup → main, then the file is parsed again to prove it is valid.  
Numbers that are not finite never go into JSON (Android `org.json` rejects `NaN`).  
If a file exists but cannot be read, it is **left alone** — the app will not invent an empty database over your history.

---

## Build a release APK

This repo is a **source zip + GitHub Action**, not a full Gradle tree in git.

1. Place one file in the repo root: `CoffeeRoast-v0.4.20-source.zip` (or any newer `CoffeeRoast-*-source.zip`).
2. Push to `main`.
3. The workflow [`.github/workflows/android-build.yml`](.github/workflows/android-build.yml) unpacks it, runs unit tests, and signs a release APK.

Repo secrets:

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

Stack: **minSdk 26 · targetSdk 35 · JDK 17 · Gradle 8.9 · Kotlin**

---

## Project layout (inside the zip)

```
app/src/main/java/com/amin1fighter/coffeeroast/
  MainActivity.kt      UI and roast flow
  RoastChartView.kt    Live curve (BT / ET / REF / RoR)
  RoastMath.kt         RoR, DTR, phases, style, drop range
  Storage.kt           JSON persistence, backup, recovery
  Models.kt            Beans, sessions, scores, settings
```

Single activity, no cloud, no ads, no account.

---

Made for the bench next to the roaster.  
Charge. Log. Drop. Taste. Repeat.
