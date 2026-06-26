# Changelog

## 2026.06.22 — Remove Layan Light variant; fix broken panel clock

### What Changed
- **Removed the Layan Light variant entirely** — the package is now dark-only. Deleted the
  light look-and-feel, desktoptheme, Aurorae decoration, color scheme, and SDDM theme. Dark
  Layan + the Layan Solid Aurorae/Kvantum extra + cursors are unchanged.
- **Fixed the broken panel clock.** The dark Layan layout referenced the panel applet
  `org.kde.plasma.splitdigitalclock` — a third-party plasmoid that is not shipped by the
  package, not a dependency, and not installed on target systems, leaving a broken/empty
  clock. Repointed to the stock `org.kde.plasma.digitalclock`, matching every other
  kiro-plasma theme. (The light layout had the same bug but was removed in this release.)

### Technical Details
- Deleted source dirs/files: `look-and-feel/com.kiroproject.Layan-light`,
  `desktoptheme/Kiro-Layan-light`, `aurorae/themes/Kiro-Layan-light`,
  `color-schemes/Kiro-LayanLight.colors`, `sddm/themes/Kiro-Layan-light`. The PKGBUILD
  installs via a blanket `cp -a usr`, so removing the files drops them from the package — no
  recipe install lines to change. The light bits were self-contained; nothing in the dark
  theme referenced them.
- Clock: changed `"plugin"` at the panel clock entry from `org.kde.plasma.splitdigitalclock`
  to `org.kde.plasma.digitalclock`; dropped the split-clock-specific `spinboxHorizontalPercentage`
  Appearance key (stock applet has no such config); kept stock-valid `displayTimezoneAsCode`
  and `use24hFormat`. JS re-validated with `node --check`.
- PKGBUILD `pkgdesc` updated to dark-only (`pkgrel` auto-bumped by `build-data.sh`).
- Docs updated: README.md, UPSTREAM.md (with a re-add note), project CLAUDE.md.

### Files Modified
- Removed: `usr/share/plasma/look-and-feel/com.kiroproject.Layan-light/`,
  `usr/share/plasma/desktoptheme/Kiro-Layan-light/`,
  `usr/share/aurorae/themes/Kiro-Layan-light/`,
  `usr/share/color-schemes/Kiro-LayanLight.colors`,
  `usr/share/sddm/themes/Kiro-Layan-light/`
- `usr/share/plasma/look-and-feel/com.kiroproject.Layan/contents/layouts/org.kde.plasma.desktop-layout.js`
- `README.md`, `UPSTREAM.md`, `CLAUDE.md`
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-layan/PKGBUILD`

## 2026.06.20 — Kvantum default via install scriptlet (no packaged kvconfig)

### What Changed
- Stopped shipping a packaged `kvantum.kvconfig`. The Kvantum selection is now written by a
  pacman **install scriptlet** to `/etc/skel/.config/Kvantum/kvantum.kvconfig` (`theme=Kiro-Layan`)
  on install/upgrade. This removes the shared-file clash on that path (with `kiro-kvantum` and
  the other kiro-plasma themes) — they all coexist now; last-installed theme wins, falling back
  to `kiro-kvantum`'s `ArcDark` baseline.

### Technical Details
- Removed the `etc/` payload entirely (it held only the Kvantum selection); the PKGBUILD no
  longer copies `etc/`. Added `install=kiro-plasma-layan.install` (`post_install`/`post_upgrade`)
  and `depends+=('kiro-kvantum')` so the overwritten baseline stays package-owned and the
  override is deterministic. Dropped `conflicts=('kiro-kvantum')` (no longer needed).

### Files Modified
- Removed `etc/skel/.config/Kvantum/kvantum.kvconfig` (+ empty `etc/`)
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-layan/PKGBUILD` — drop `cp etc`, add `install=` + `kiro-kvantum` dep, drop conflicts
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-layan/kiro-plasma-layan.install` — new scriptlet

## 2026.06.20 — rename theme identity to Kiro namespace (coexist with upstream Layan)

### What Changed
- Renamed every shipped theme identity from the upstream `Layan` name into a `Kiro-`
  namespace so the package **coexists with the upstream Layan theme + cursors** — a user
  can install `layan-kde-theme-git` / `layan-cursors-git` alongside this without any pacman
  file conflict — and so System Settings shows honest **Kiro Layan** / **Kiro Layan Light**
  labels.
- Internal identifiers (folders, `Id`, `__aurorae__svg__` token, `ColorScheme`, Kvantum
  dirs, SDDM `Theme-Id`, `.colors` filenames, cursor dirs) → hyphenated `Kiro-Layan*` /
  `com.kiroproject.Layan*`. Visible Global Theme names are the spaced **Kiro Layan** forms.

### Technical Details
- Look-and-feel `com.github.vinceliuice.Layan{,-light}` → `com.kiroproject.Layan{,-light}`
  (both `metadata.json` and legacy `metadata.desktop` Id+Name). Desktoptheme, aurorae
  (incl. `*rc`), Kvantum (incl. dual `*Dark` configs/svgs), SDDM, color schemes, and the
  three cursor themes all prefixed `Kiro-`.
- SDDM `Main.qml` carried **absolute self-paths** (`/usr/share/sddm/themes/Layan…`) — these
  were repointed to the renamed dirs.
- Cross-references repointed: look-and-feel `defaults` (`cursorTheme`/`ColorScheme`/
  `__aurorae__svg__`/`plasmarc name`) and `etc/skel` Kvantum `theme=Kiro-Layan`. External
  icon refs (`Tela`/`Tela-circle`) unchanged.
- PKGBUILD: dropped `conflicts=(layan-kde-theme-git layan-cursors-git)` and bumped `pkgrel`.

### Files Modified
- Renamed all theme dirs/files under `usr/share/{plasma,aurorae,color-schemes,Kvantum,sddm,icons}` to `Kiro-Layan*`
- Look-and-feel `contents/defaults`, SDDM `Main.qml`, `etc/skel/.config/Kvantum/kvantum.kvconfig` — repointed
- `README.md`, `CLAUDE.md` — Kiro Layan naming + coexistence note
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-layan/PKGBUILD` — drop upstream conflicts, bump pkgrel

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
