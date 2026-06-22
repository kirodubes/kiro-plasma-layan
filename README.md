<p align="center">
  <img src="kiro.jpg" alt="Kiro" width="220" />
</p>

# kiro-plasma-layan

Kiro's **Kiro Layan** Plasma global theme — a clean, flat/material look (KDE Store #3 by
downloads), packaged as ready-to-pick Global Themes for the Kiro Plasma edition.

Everything ships under a `Kiro-` namespace, so it **coexists with the upstream Layan
theme** — install the real `layan-kde-theme-git` / `layan-cursors-git` alongside it
without any file conflict.

## What it ships

The Global Theme you select in **System Settings → Appearance → Global Themes**:
**Kiro Layan** (dark), pulling in its full set of layers, plus a **Kiro Layan Solid**
Aurorae/Kvantum extra.

| Layer | Path | Notes |
|---------------------|------------------------------------------|------------------------------|
| Plasma desktop theme | `/usr/share/plasma/desktoptheme/Kiro-Layan` | panels, widgets, popups |
| Global theme (look-and-feel) | `/usr/share/plasma/look-and-feel/com.kiroproject.Layan` | the dark variant |
| Window decorations | `/usr/share/aurorae/themes/Kiro-Layan{,-solid}` | Aurorae titlebars |
| Color scheme | `/usr/share/color-schemes/Kiro-Layan.colors` | application colours |
| Kvantum themes | `/usr/share/Kvantum/Kiro-{Layan,LayanSolid}` | Qt app styling |
| Kvantum default selection | `/etc/skel/.config/Kvantum/kvantum.kvconfig` | new users get `Kiro-Layan` |
| SDDM login theme | `/usr/share/sddm/themes/Kiro-Layan` | the login screen (Plasma 6) |
| Cursors | `/usr/share/icons/Kiro-Layan-{,white-,border-}cursors` | bundled Layan cursors |

**Icons:** the theme uses **Tela**, so the package depends on `tela-icon-theme`.
Layan is Plasma-6 native — no metadata conversion needed.

## Install

```bash
sudo pacman -S kiro-plasma-layan
```

Then open **System Settings → Appearance → Global Themes** and apply **Kiro Layan**.
New users get the Kiro Layan Kvantum theme for Qt apps automatically; existing users can
pick it in **Kvantum Manager**.

## Heritage

Based on [vinceliuice/Layan-kde](https://github.com/vinceliuice/Layan-kde) and
[vinceliuice/Layan-cursors](https://github.com/vinceliuice/Layan-cursors), GPL-3.0. The
verified-working global-theme files were captured from a configured Plasma test box (the
KDE-Store release), with the light variant / Kvantum / SDDM added from the git repo. See
[UPSTREAM.md](./UPSTREAM.md) for exact sources and refresh notes.
