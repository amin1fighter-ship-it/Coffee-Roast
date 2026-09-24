# Coffee Roast Lab 0.4.3

A local-first Android roast logging and analysis app for specialty coffee.

## 0.4.3

This release turns the original manual logger into a roast-management system.

### Live roast
- Persistent in-progress sessions: leaving the app no longer loses a roast.
- Monotonic elapsed time (`elapsedRealtime`) instead of wall-clock time.
- Keep-screen-on during live roasting.
- Persistent notification when the app is backgrounded.
- Haptic feedback for TP / DE / FC / DROP.
- Manual BT/ET sampling at any elapsed time.
- Configurable logging interval.
- Turning Point detection/saving.
- Dry End, First Crack and Drop markers.
- Live RoR, low-RoR warning and ETA heuristics for DE/FC.
- Fan/heater change log.

### Analysis
- RoR and Delta RoR.
- Smoothing-ready chart engine.
- Phase percentages and DTR.
- Current roast vs reference/previous roast overlay.
- Reference roast per bean.
- Artisan TSV export.
- CSV export.
- PDF roast report with chart.

### Beans & inventory
- Edit/delete beans.
- Supplier, purchase date, price, harvest year, altitude, variety and storage location.
- Green stock tracking.
- Roasted inventory and resting-day tracking.
- Pre-roast blend percentage builder.

### Cupping
- SCA-style tasting fields:
  Fragrance, Flavor, Aftertaste, Acidity, Body, Balance, Sweetness,
  Clean Cup, Uniformity and Overall.
- 100-point total.

### Dashboard/tools
- Average weight loss.
- Average DTR.
- Cupped-roast count and average score.
- Per-bean roast counts and stock.
- Green-weight calculator.
- Brew ratio calculator.
- g/oz converter.
- Charge-temperature heuristic.
- Stopwatch.

### Data safety
- Schema versioning and migration path.
- Atomic JSON writes.
- Backup/restore ZIP.
- Raw JSON export.
- Local crash-log sharing.
- RoastMath unit tests.
- No network/database required.

### UI
- Light/dark/system theme.
- °C/°F and g/oz settings.
- Android 15 / target SDK 35.
- FileProvider export support.

## Deliberately not included
Thermocouple/Bluetooth thermometer integration is intentionally excluded from this release, as requested. The temperature source remains manual BT/optional ET.

## Build

CI uses Gradle 8.9 + JDK 17 and produces a signed release APK when the four signing secrets exist:

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

Release version: `0.4.3` / versionCode `40300`.
