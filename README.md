# Zoe's Source

An [AltStore Classic](https://altstore.io) source. The catalog lives in
**`source.json`**; its hosted raw URL is what people add in AltStore:

```
https://raw.githubusercontent.com/zobeez/zoes-source/main/source.json
```

**AltStore → Browse → Sources → +**, then paste that URL.

## How this is organized

This **public** repo hosts everything AltStore needs to fetch: the catalog
(`source.json`), each app's `icon.png` + screenshots, and each app's `.ipa`
(attached to a GitHub Release here). App source code lives in separate, private
repos — AltStore only needs the public asset URLs, which all live here.

| App | Bundle ID | Assets (in this repo) |
| --- | --- | --- |
| Hex Code Getter | `io.altstore.hexcodegetter` | `icon.png`, `screenshots/`, Release `v1.0` → `HexCodeGetter-1.0.ipa` |

## Adding another app

1. Build the app's unsigned `.ipa` and attach it to a GitHub **Release** in this
   repo (use a unique tag, e.g. `app2-v1.0`).
2. Commit that app's icon + screenshots here (e.g. under `app2/`).
3. Append a new object to the `apps` array in `source.json` pointing at those
   URLs (same shape as the existing entry). Optionally add its bundle ID to
   `featuredApps`.
4. Commit `source.json`. AltStore picks it up on its next refresh.

## Shipping an update to an existing app

Prepend a new entry to that app's `versions` array (newest first) with a new
`version`, `date`, `downloadURL`, and `size`, then commit. AltStore detects the
update from the changed `version` string, so it must increase every release.
