# Coffee Roast Lab 0.4.13

A local-first Android roast logging and analysis app for specialty coffee.

## 0.4.13

Stability and correctness release over the 0.4.x line.

### Fixes
- **Monotonic live timer**: elapsed time uses `SystemClock.elapsedRealtime` (no drift on sleep or wall-clock changes).
- **Live roast recovery**: incomplete sessions auto-open on launch; home shows Resume button.
- **Green stock safety**: reserved at start; restored when an incomplete roast (or its bean) is deleted.
- **Temperature units**: storage always °C; display and input convert for °F.
- **Marker order validation**: TP → DE → FC → SC → DROP chronology enforced.
- **Second Crack** marker supported end-to-end (live, chart, export, PDF).
- **Activity Result API** for backup restore (no deprecated `onActivityResult`).
- **Phase math** consistent from charge (t=0).
- Chart height tuned for phones; dark-mode chart colors improved.
- Schema version **6** with migration for older data files.
- Version numbers unified: `0.4.13` / versionCode `41300`.

### Live roast
- Persistent in-progress sessions.
- Keep-screen-on during live roasting.
- Persistent notification when backgrounded.
- Haptic feedback for TP / DE / FC / SC / DROP.
- Manual BT/ET sampling; configurable logging interval.
- Live RoR, low-RoR warning, ETA heuristics.

### Analysis
- RoR and Delta RoR; chart smoothing.
- Phase percentages and DTR.
- Reference overlay; Artisan TSV / CSV / PDF export.

### Beans & inventory
- Full bean metadata; green stock; roasted remaining + rest days.
- Safe delete with stock restore for incomplete work.

### Cupping
- SCA-style 10 fields, 100-point total.

### Data safety
- Atomic JSON writes, `.bak`, write-block if corrupt.
- Backup/restore ZIP; raw JSON export; crash log share.
- Unit tests for RoastMath.

### UI
- Light / dark / system theme.
- °C/°F and g/oz.
- Android 15 / target SDK 35.

## Deliberately not included
Thermocouple/Bluetooth thermometer integration is intentionally excluded. Temperature entry remains manual.

## Build

CI builds from the committed Gradle project at the repo root (preferred), or from the newest `CoffeeRoast-*-source.zip` if present.

Requires secrets:

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

Release version: `0.4.13` / versionCode `41300`.
