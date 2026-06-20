<p align="center">
  <img src="kiro.jpg" alt="Kiro" width="220" />
</p>

# kiro-plasma-layan

Kiro's **Layan** Plasma global theme — a clean, flat/material look (KDE Store #3 by
downloads), packaged as ready-to-pick Global Themes for the Kiro Plasma edition.

## What it ships

Global Themes you select in **System Settings → Appearance → Global Themes**:
**Layan** (dark) and **Layan Light**, each pulling in its full set of layers, plus a
**Layan Solid** Aurorae/Kvantum extra.

| Layer | Path | Notes |
|---------------------|------------------------------------------|------------------------------|
| Plasma desktop theme | `/usr/share/plasma/desktoptheme/Layan{,-light}` | panels, widgets, popups |
| Global themes (look-and-feel) | `/usr/share/plasma/look-and-feel/com.github.vinceliuice.Layan{,-light}` | the two variants |
| Window decorations | `/usr/share/aurorae/themes/Layan{,-light,-solid}` | Aurorae titlebars |
| Color schemes | `/usr/share/color-schemes/{Layan,LayanLight}.colors` | application colours |
| Kvantum themes | `/usr/share/Kvantum/{Layan,LayanSolid}` | Qt app styling |
| Kvantum default selection | `/etc/skel/.config/Kvantum/kvantum.kvconfig` | new users get `Layan` |
| SDDM login themes | `/usr/share/sddm/themes/Layan{,-light}` | the login screen (Plasma 6) |
| Cursors | `/usr/share/icons/Layan-{,white-,border-}cursors` | bundled Layan cursors |

**Icons:** the theme uses **Tela** (and Tela-circle), so the package depends on
`tela-icon-theme`. Layan is Plasma-6 native — no metadata conversion needed.

## Install

```bash
sudo pacman -S kiro-plasma-layan
```

Then open **System Settings → Appearance → Global Themes** and apply **Layan** or
**Layan Light**. New users get the Layan Kvantum theme for Qt apps automatically;
existing users can pick it in **Kvantum Manager**.

## Heritage

Based on [vinceliuice/Layan-kde](https://github.com/vinceliuice/Layan-kde) and
[vinceliuice/Layan-cursors](https://github.com/vinceliuice/Layan-cursors), GPL-3.0. The
verified-working global-theme files were captured from a configured Plasma test box (the
KDE-Store release), with the light variant / Kvantum / SDDM added from the git repo. See
[UPSTREAM.md](./UPSTREAM.md) for exact sources and refresh notes.
