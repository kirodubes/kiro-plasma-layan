# Upstream references — kiro-plasma-layan

Everything needed to refresh this theme from upstream in the future.

## Sources

| Component | Source | Notes |
|---------------------------|------------------------------------------|----------------------------|
| Dark global theme (verified) | **Plasma test box** KDE-Store install, `~/.local/share/` | captured because the AUR build failed but the Store version works |
| Kvantum, SDDM | https://github.com/vinceliuice/Layan-kde @ `master` (`a0b6a49`) | git supplement |
| Cursors | https://github.com/vinceliuice/Layan-cursors @ `master` (`b8c4689`) | bundled |

- **Author:** vinceliuice · **License:** GPL-3.0 (upstream `LICENSE` carried in).
- **Plasma 6:** Layan is already P6-native (`metadata.json`, `X-Plasma-APIVersion 2`,
  fallback `org.kde.breeze.desktop`). **No P5→P6 conversion needed.**

## Why the dark variant comes from the test box, not git

The AUR package failed; the KDE-Store version works. The Store-installed
`desktoptheme/Layan` already has the shared `plasma/desktoptheme/common/` SVGs **merged
into the variant dir** — a naive git copy that skips that overlay produces a broken
desktoptheme (the likely AUR failure). The captured Store files are already merged.

## What was copied (source → install path)

From the test box (`~/.local/share/`):
| Source | Installed to |
|------------------------------|----------------------------------------|
| `plasma/look-and-feel/com.github.vinceliuice.Layan` | `usr/share/plasma/look-and-feel/` |
| `plasma/desktoptheme/Layan` (common already merged) | `usr/share/plasma/desktoptheme/` |
| `aurorae/themes/Layan` | `usr/share/aurorae/themes/` |
| `color-schemes/Layan.colors` | `usr/share/color-schemes/` |

From `vinceliuice/Layan-kde`:
| Source | Installed to |
|------------------------------|----------------------------------------|
| `aurorae/themes/Layan-solid` | `usr/share/aurorae/themes/` |
| `Kvantum/{Layan,LayanSolid}` | `usr/share/Kvantum/` |
| `sddm/6.0/Layan` | `usr/share/sddm/themes/` |

> **Layan Light removed (2026.06.22):** the light variant (look-and-feel
> `com.kiroproject.Layan-light`, `desktoptheme/Kiro-Layan-light`,
> `aurorae/Kiro-Layan-light`, `color-schemes/Kiro-LayanLight.colors`,
> `sddm/Kiro-Layan-light`) is no longer shipped. If re-adding it, pull the light
> look-and-feel + `desktoptheme/Layan-light` (overlay `common/` first) + `sddm/6.0/Layan-light`
> from `vinceliuice/Layan-kde`.

From `vinceliuice/Layan-cursors`: `dist`→`icons/Layan-cursors`,
`dist-border`→`icons/Layan-border-cursors`, `dist-white`→`icons/Layan-white-cursors`.

## Intentionally NOT copied
- `sddm/5.0/` — Plasma-5 only (Kiro is Plasma 6).
- konsole — none upstream; Kiro ships `kiro-plasma-konsole`.

## Refresh gotchas
1. **Re-capture the dark variant from the working Store install**, not a raw git copy —
   or, if copying the dark desktoptheme from git, overlay `desktoptheme/common/` into
   `desktoptheme/Layan/` first.
2. **No defaults edits** — the look-and-feel defaults reference `Tela` icons (external
   dep `tela-icon-theme`) and `Layan-white-cursors` (bundled). Both satisfied as-is.

Kiro-only file (not upstream — leave as is on refresh):
- `etc/skel/.config/Kvantum/kvantum.kvconfig` → `[General] theme=Layan`

## Verify on the Plasma test box
Layan (dark) is a regression check (already works from the Store); confirm it appears and
applies in System Settings → Global Themes.
