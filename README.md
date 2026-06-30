# Zoe's Source

An [AltStore Classic](https://altstore.io) source. The catalog lives in
**`source.json`**; its hosted raw URL is what people add in AltStore:

```
https://raw.githubusercontent.com/zobeez/zoes-source/main/source.json
```

**AltStore → Browse → Sources → +**, then paste that URL.

## How this is organized

This repo holds **only the catalog** (`source.json`). Each app keeps its own
repo, which hosts that app's `.ipa` (as a GitHub Release), icon, and
screenshots. `source.json` links out to those URLs — they can live in any repo.

| App | Repo | Assets |
| --- | --- | --- |
| Hex Code Getter | [`zobeez/hex-code-getter`](https://github.com/zobeez/hex-code-getter) | icon + screenshots committed to the repo; `.ipa` attached to a Release |

## Adding another app

1. Create the app's own repo; commit its `icon.png` + screenshots and attach
   its `.ipa` to a GitHub Release.
2. Append a new object to the `apps` array in `source.json` pointing at that
   app's URLs (same shape as the existing entry). Optionally add its bundle ID
   to `featuredApps`.
3. Commit `source.json`. AltStore picks it up on its next refresh.

## Shipping an update to an existing app

Prepend a new entry to that app's `versions` array (newest first) with a new
`version`, `date`, `downloadURL`, and `size`, then commit. AltStore detects the
update from the changed `version` string, so it must increase every release.
