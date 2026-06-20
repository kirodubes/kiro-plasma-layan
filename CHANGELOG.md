# Changelog

## 2026.06.20 — initial package

### What Changed
- New repo: **kiro-plasma-layan**, the **Layan** Plasma global theme for the Kiro Plasma
  edition (Layan is #3 most-downloaded global theme on the KDE Store). Ships **Layan** and
  **Layan Light** as full Global Themes plus a **Layan Solid** Aurorae/Kvantum extra.
- Combined the layers: 2 desktopthemes + 2 look-and-feel + 3 Aurorae + 2 color schemes +
  Kvantum (Layan, LayanSolid) + 2 SDDM themes (Plasma 6) + bundled Layan cursors.
- **Dark variant captured from the verified-working KDE-Store install** on the Plasma test
  box (the AUR build failed; the Store version works). Its `desktoptheme/Layan` already has
  the shared `common/` SVGs merged — the likely AUR failure was a copy skipping that overlay.
- **No Plasma-6 metadata conversion needed** — Layan is already P6-native (`metadata.json`,
  `X-Plasma-APIVersion 2`). Light variant / Kvantum / SDDM / cursors added from git.
- **Icons:** uses Tela → depends on `tela-icon-theme` (no defaults edit).
- **Default Kvantum selection** via `/etc/skel/.config/Kvantum/kvantum.kvconfig` (`theme=Layan`).

### Technical Details
- Sources: Plasma-test-box Store install (dark global theme),
  [vinceliuice/Layan-kde](https://github.com/vinceliuice/Layan-kde) `a0b6a49` (light,
  Kvantum, SDDM 6.0), [vinceliuice/Layan-cursors](https://github.com/vinceliuice/Layan-cursors)
  `b8c4689`. Full mapping in [UPSTREAM.md](./UPSTREAM.md).
- License: GPL-3.0.
- Recipe depends on `tela-icon-theme`, `kvantum`, `sddm`; copies `usr/` + `etc/`.

### Files Modified
- usr/share/plasma/look-and-feel/com.github.vinceliuice.Layan{,-light} (new)
- usr/share/plasma/desktoptheme/Layan{,-light} (new)
- usr/share/aurorae/themes/Layan{,-light,-solid}, color-schemes/{Layan,LayanLight}.colors (new)
- usr/share/Kvantum/{Layan,LayanSolid}, sddm/themes/Layan{,-light} (new)
- usr/share/icons/Layan-{,white-,border-}cursors (new)
- etc/skel/.config/Kvantum/kvantum.kvconfig (new)
- README.md, CHANGELOG.md, CLAUDE.md, UPSTREAM.md, LICENSE, up.sh, setup.sh, kiro.jpg, .gitignore (new)
