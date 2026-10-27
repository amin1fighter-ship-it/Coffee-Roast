# Coffee Roast Lab

**A pocket roast lab. Not a roast judge.**

Log the curve while it happens. See the phases, the RoR, and how the drum answered when you moved the fan or the heater. Choose what the coffee was *for* — Filter, Omni, or Espresso — and let the cup decide whether it worked.

نرم‌افزار رست برای قهوه‌دوست‌هایی که کنار دستگاه کار می‌کنند. داده روی گوشی می‌ماند. اپ از روی نمودار حکم «این اسپرسو است» یا «این bake است» نمی‌دهد؛ الگوی مشاهده‌شده را توصیف می‌کند و فنجان را جدا نگه می‌دارد.

[![version](https://img.shields.io/badge/version-0.6.0-6F4E37)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![build](https://img.shields.io/github/actions/workflow/status/amin1fighter-ship-it/Coffee-Roast/android-build.yml?branch=main&label=Android%20Build)](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)
[![platform](https://img.shields.io/badge/Android-8%2B-3DDC84)](https://github.com/amin1fighter-ship-it/Coffee-Roast)
[![data](https://img.shields.io/badge/data-local%20first-2E8B57)](https://github.com/amin1fighter-ship-it/Coffee-Roast)

**v0.6.0** · versionCode `60000` · schema `9`  
Source: [`CoffeeRoast-v0.6.0-source.zip`](CoffeeRoast-v0.6.0-source.zip)  
Signed APK: [Actions → latest successful run → artifacts](https://github.com/amin1fighter-ship-it/Coffee-Roast/actions)

---

## What it is

A local-first Android app for home and sample roasting.

You charge the beans, mark turning point, dry end, first crack, and drop, and the chart keeps bean temperature, optional environment temperature, rate of rise, and every fan and heater change on one timeline. After the roast, the lab separates four questions that are easy to mix up:

| Layer | Question | Who answers |
|---|---|---|
| Brew intent | Filter, Omni, Espresso, or Other? | You, before the roast. Never inferred from DTR or drop temperature. |
| Roast degree | How far did the color and mass go? | A reference level you set, plus a weight-loss *indication*. Not a color meter, and not a style label. |
| Development | What did the curve do after first crack? | Time, DTR, and the post-crack RoR pattern. Descriptive only. |
| Cup | Did it actually taste right? | Cupping scores, kept apart from the curve. |

Omni is a brew intent — coffee meant to work across methods — not a synonym for “medium roast.”

---

## A roast, start to finish

1. Pick a green bean. Stock is reserved when the roast starts.
2. Set **brew intent** (Filter / Espresso / Omni / Other) and a **reference roast level**.
3. Optionally see a **working drop range** from green density and process. It is a machine aid, not a universal rule.
4. Roast live. The notification clock keeps running if you leave the screen.
5. Log temperatures on the interval and off the grid. A point at 4:15 stays at 4:15.
6. Mark **TP → DE → FC → SC → Drop**, in order. You can edit or remove them later.
7. After drop: weight loss, phase split, density, thermal response, and development notes — each in its own language.
8. Score the cup. Rest the batch. Export if you want.

A saved **roast plan** can apply time-based fan and heater steps (`4:30 fan 12`, `6:00 heater 8`). Lines written as a bean-temperature target stay as reference text. This app does not drive roaster hardware.

---

## What you actually see

### Live roast
- Monotonic timer (`elapsedRealtime`), so a lock screen does not jump the clock
- Bean temperature, optional environment temperature, RoR, ETA toward your targets
- Fan and heater strip on the same chart
- Resume a roast that is still in progress

### After the roast
- Dry / Maillard / development as a **description of the profile**, not a classifier
- Development time, DTR, and a post-crack pattern such as “late-stage RoR flattening” — never “underdeveloped” or “baked” as a verdict
- Thermal response: RoR before and after a fan or heater change. RoR is a temperature slope, not joules inside the bean
- Green and roasted density. Bulk density is not treated as true bean-volume expansion; expansion is estimated only when you mark the reading as particle/true density
- Edit weights, notes, events, and the fan/heater history after the roast is finished
- Reference curve from an earlier roast of the same bean

### Around the roastery
- Green-bean stock: origin, process, variety, altitude, supplier
- Roasted inventory and resting days
- Cupping scores
- Dashboard and calculators
- Four palettes: Dark Roast, Light Lab, Forest, Ember
- Backup and restore, legacy roast import
- Artisan-style TSV, CSV, dashboard CSV, PDF, and JSON

---

## What it will not claim

- It will not infer Filter, Omni, or Espresso from weight loss, DTR, or drop temperature.
- It will not treat heater level `15` as a unit of energy.
- It will not turn a long Maillard phase, by itself, into “baked.”
- It will not use a fixed clock (“dry end before four minutes”) as a universal law. Your roaster, charge, and batch size set the baseline.
- Phase percentages describe the curve. They do not name the brew method.

A hypothesis stays a hypothesis until the cup agrees.

---

## Privacy

Nothing leaves the phone unless you export it.

| File | Role |
|---|---|
| `coffeeroast_data.json` | Live database |
| `coffeeroast_data.json.bak` | Last good copy |
| `coffeeroast_recovery_*.json` | Kept if a write fails |

Writes go through a temp file, then a backup, then the main file, and the result is parsed again before it is trusted. Values that are not finite never go into JSON. If a file exists but cannot be read, it is left alone — the app will not invent an empty database over your history.

Schema **9**. Older files migrate on load, including the old `specialty` intent (now Filter) and missing fan/heater events at 0:00. Roast plans live in app preferences, not in the roast schema.

---

## Build a release APK

This repo is a **source zip + GitHub Action**.

1. Keep one `CoffeeRoast-*-source.zip` in the repo root.
2. Push to `main`.
3. [`.github/workflows/android-build.yml`](.github/workflows/android-build.yml) unpacks it, runs tests, and signs a release APK.

Secrets: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

**minSdk 26 · targetSdk 35 · JDK 17 · Gradle 8.9 · Kotlin**

```
app/src/main/java/com/amin1fighter/coffeeroast/
  MainActivity.kt      screens and roast flow
  RoastChartView.kt    live curve
  RoastMath.kt         RoR, phases, density, thermal response
  Storage.kt           JSON, backup, schema 9
  Models.kt            beans, sessions, scores
```

Single activity. No cloud. No ads. No account.

---

Made for the bench next to the roaster.  
Charge. Log. Drop. Taste. Repeat.
