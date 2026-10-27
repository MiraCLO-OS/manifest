# MiraCLO changelog

Every change made to MiraCLO, newest first. Each entry says **what** changed, **where** (repository and commit) and **why**, so the project can be rebuilt or understood without anyone's memory.

Format: `repository @ commit — summary`

---

## 1.0 Beta 1 "Aurora" — 2026-10-27

First public MiraCLO release. `user` build, signed with MiraCLO release keys. Can be dirty-flashed over the 1.0 unofficial test build (same keys).

### Quick Settings — new optional ColorOS style
Settings › Display › Quick settings › **QS style: Default | ColorOS**. Default is the stock layout with circular tiles.

- `android_frameworks_base` — "SystemUI: Match QS tile and icon bubble sizes to target design": tile height 80dp, toggle bubble 62dp (Default style circles)
- `android_frameworks_base` — "SystemUI: Add MiraCLO (ColorOS-style) Quick Settings tile style" and "Refine MiraCLO QS style towards ColorOS": glass tiles, ColorOS blue/green, light and dark aware
- `android_frameworks_base` — "SystemUI: Add MiraCLO (ColorOS-style) Quick Settings layout": Wi-Fi + mobile data, media + tall brightness and volume sliders, Bluetooth + ringer switch, round tiles below
- `android_frameworks_base` — "SystemUI: Use ColorOS 17 proportions in MiraCLO ColorOS QS style": 66dp tiles, 46dp bubbles, 16dp gaps
- `android_frameworks_base` — "SystemUI: Colour the MiraCLO ringer switch by sound mode": ring blue, vibrate orange, silent red
- `android_frameworks_base` — "SystemUI: Smooth the MiraCLO QS expand and collapse": no tile morphing, QS no longer scrolls in portrait so a swipe up always collapses it, 3 rows of round tiles per page
- `android_frameworks_base` — "SystemUI: Restore the top spacing of the MiraCLO ColorOS QS"
- `android_frameworks_base` — "SystemUI: Turn the MiraCLO brightness icon orange at full brightness"
- `android_frameworks_base` — "SystemUI: Let the MiraCLO ColorOS QS scroll in landscape"
- `android_frameworks_base` — "SystemUI: Feed the MiraCLO media card from the media pipeline": square media card (app icon, title, artist, previous / play-pause / next) built from MediaDataManager, so it works with legacy media controls
- `android_packages_apps_Settings` — "Settings: Add MiraCLO Quick Settings style switch" and "Turn MiraCLO QS switch into a QS style chooser"

### Recents — new optional ColorOS style
Home settings › Recents › **Recents style: Default | ColorOS**.

- `android_packages_apps_Launcher3` — "Launcher3: Add ColorOS (stacked) recents style": older tasks tucked behind the focused one, newer tasks on top; swipe-up, quick switch and launch animations stay in sync
- `android_packages_apps_Launcher3` — "Launcher3: Keep the stock app chip in the ColorOS recents style"

### Branding
- `android_vendor_aospa` — "MiraCLO: Use the HD branding pack boot animation and wallpaper": PSP's boot animation (logo draws once, then holds) and *Planetary* default wallpaper
- `android_vendor_aospa` — "MiraCLO: Name release builds, starting with Beta 1 "Aurora"": zips named `MiraCLO-1.0-beta1-Aurora-marble-<date>`
- `android_packages_apps_Settings` — "Settings: Show MiraCLO version on the Android version page" (replaces "Paranoid Android version") and "Show the MiraCLO release name"
- `.github` — new organisation banner

### Infrastructure
- `manifest` — `packages/apps/Launcher3` now uses the MiraCLO-OS fork

### Notes
- `adb remount` is refused on MiraCLO because the bootloader state is spoofed for Play Integrity. Test SystemUI, Settings or launcher changes on a `userdebug` build by bind-mounting the signed APK over the one in `/system_ext/priv-app/` and running `stop && start`; a reboot removes the overlay.

---

## 1.0 (unofficial test) — 2026-10-26

First MiraCLO build, signed with MiraCLO release keys. Booted and tested on `marble`.

### Branding
- `android_vendor_aospa @ 915d809` — Version set to `1.0`; zips renamed from `aospa-*` to `MiraCLO-*` (`target/product/version.mk`, `build.sh`)
- `android_vendor_aospa @ 8b68f4e` — Build number shows `MiraCLO-<version>`; adds `ro.aospa.miraclo.version` property (`version.mk`)
- `android_packages_apps_Settings @ ca1453b` — "MiraCLO version" row in Settings › About phone, read from `ro.aospa.miraclo.version` (new `MiraCLOVersionPreferenceController`)
- `android_vendor_aospa` — Builder name set to `MiraCLO` (`build.sh` exports `BUILD_USERNAME` / `BUILD_HOSTNAME`)
- `android_vendor_aospa @ d15766d` — MiraCLO boot animation (all resolutions) and *Nero* default wallpaper

### Removed
- `android_vendor_aospa` — ParanoidHub (OTA updater) removed from the build: it only checks AOSPA's servers, which have no MiraCLO builds

### Quick Settings
- `android_frameworks_base @ 5611432fb` — `common_tile_default_tile_height` 72dp → 86dp so icon tiles become circles on `marble` (tile radius is already height / 2)
- `android_packages_apps_Paranoid_SystemUI @ 4effbc2` — AOSPA's refresh-rate tile removed in favour of the CLO one; both registered the same `refresh_rate` key and Dagger refused the duplicate

### Build fixes (upstream bugs)
- `android_hardware_xiaomi @ f513532` — Added missing `DropdownMenu` / `DropdownMenuItem` imports in `DolbySettingsScreen.kt`; upstream commit "Dolby: Add icons for Dolby profiles" did not compile

### Infrastructure
- `manifest` — Uses MiraCLO-OS forks for `vendor/aospa`, `frameworks/base`, `packages/apps/Settings`, `packages/apps/ParanoidSystemUI`
- `android_vendor_aospa @ 98c496b` — `products/marble/beans.xml` points `hardware/xiaomi` at the MiraCLO-OS fork
- Release keys generated (`CN=PSP`), backed up offline. Never committed.

### Base
- AOSPA Calcite (Android 17), from `aospa-shadedark/manifest` as of 2026-10-26
- `marble` device, vendor and kernel trees from `aospa-shadedark` (synced through `beans.xml`)
