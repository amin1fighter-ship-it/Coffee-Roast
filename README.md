# Coffee Roast

Android app for logging your own fluid-bed roasts: green bean inventory,
per-bean batch numbering, an editable 30-second BT/optional-ET log grid, real-time
RoR with a low-energy warning, live phase-timing prediction, fan/heater
change log tagged by temperature, phase percentages, weight loss, a
numbered BT/ET/RoR chart with share/export, and a density-based drop-temp
suggestion.

## Screens

- Home -> Roast section / Green Bean section
- Green Bean: list + add (name, origin, process, stock in grams)
- Roast home: history list + "start new roast"
- New roast setup: pick bean -> auto-assigns a global roast number and a
  per-bean batch number; enter green weight, optional density (g/L),
  starting fan/heater
- Live roast: elapsed timer, a BT/ET row auto-appears every 30s and stays
  editable any time (so a slow or mistyped entry is never lost), live RoR
  (warns below 10 C/min), a live estimate of when dry-end / first crack
  will be reached (linear projection from current RoR - clearly labeled as
  an estimate), a rule-of-thumb suggested drop range from density+process,
  fan/heater change log (tagged with the BT at the moment of change),
  Dry-End / First-Crack marker buttons, End Roast button
- Summary: roasted weight entry -> weight loss %, drying/Maillard/development
  phase %, numbered BT/ET/RoR chart, actual drop BT vs. the suggested range,
  and a "Share / export chart" button (system share sheet, PNG)

## Data

Stored locally as JSON in the app's private storage
(`filesDir/coffeeroast_data.json`). No network access, no external database.

## Build

CI is at `.github/workflows/android-build.yml`. It builds the Gradle project directly and produces a **signed release APK**
(not debug), and uploads it as a downloadable Actions artifact named
`CoffeeRoast-release-apk`.

versionCode auto-increments from `GITHUB_RUN_NUMBER`, so every build
installs as an update over the previous one - as long as the signing key
stays the same. Required repository secrets:

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

## Not yet built

- Artisan-compatible TSV export, legacy text import, and optional ET logging
- Editing or deleting a saved bean or roast after the fact
- The dry-end/first-crack predictions and the drop-temp suggestion are
  rule-of-thumb heuristics, not validated formulas - treat them as a
  reference point, not an instruction.
