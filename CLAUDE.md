# kiro-plasma-layan — Project Claude Instructions

## Overview
The **Layan** Plasma global theme for the Kiro Plasma edition — a clean flat/material
look. Ships Layan (dark) + Layan Light as Global Themes, plus a Layan Solid Aurorae/Kvantum
extra. Sibling to [[kiro-plasma-sweet]] and [[kiro-plasma-nord]].

## Current state
- Source repo: `~/KIRO/kiro-plasma-layan` (payload under `usr/`, Kvantum default `etc/skel`).
- Build recipe: `~/KIRO-PKG-BUILD-APPS/kiro-plasma-layan`.
- Sources: Plasma-test-box Store install (dark) + vinceliuice/Layan-kde (light/Kvantum/SDDM)
  + vinceliuice/Layan-cursors. See [UPSTREAM.md](./UPSTREAM.md).

## Patterns / things to know
- **Plasma 6 native** — no metadata conversion (unlike kiro-plasma-nord). Both look-and-feel
  variants and desktopthemes ship `metadata.json` as-is.
- **Dark variant is captured from the working Store install**, not a raw git copy: the AUR
  build failed because a naive copy skips the `desktoptheme/common/`→variant overlay. The
  Store files are pre-merged. If refreshing the dark desktoptheme from git, do the overlay.
- **Icons are Tela** (deliberate — upstream's pairing). Recipe depends on `tela-icon-theme`.
  Defaults reference `Tela`; do NOT repoint to neo-candy.
- **No defaults edits** — `Tela` (dep) and `Layan-white-cursors` (bundled) are satisfied.
- Cursors bundled: `Layan-cursors`, `Layan-white-cursors` (the one defaults use), `-border`.
- Kvantum default for new users: `etc/skel/.config/Kvantum/kvantum.kvconfig` → `theme=Layan`.
- SDDM from `sddm/6.0/` only (Plasma 6); `sddm/5.0/` excluded. konsole excluded.
- Mixed delivery: payload → `/usr/share`, Kvantum selection → `/etc/skel`. PKGBUILD copies both.
- **Test on the Plasma test box** — dark is a regression check (works from Store); confirm
  Layan Light (git-sourced) also applies.
