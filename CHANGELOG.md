# MiraCLO changelog

Every change made to MiraCLO, newest first. Each entry says **what** changed, **where** (repository and commit) and **why**, so the project can be rebuilt or understood without anyone's memory.

Format: `repository @ commit — summary`

---

## Unreleased

### Quick Settings
- `android_frameworks_base @ 5663d10ee` — Tile and icon-bubble sizes matched to the target design: `common_tile_default_tile_height` 86dp → 80dp (icon tiles become centred circles ~92% of the column), `common_tile_default_toggle_target_size` 56dp → 62dp (even ~9dp ring around the wide-tile bubble). Tested on `marble` with a SystemUI-only build.

### Planned
- Quick Settings: brightness bar above the tiles, as in the target design
- Quick Settings: optional ColorOS-style layout with a toggle in Settings › Display (design: "MiraCLO Quick Settings" mockup)

### Notes
- `adb remount` is refused on MiraCLO because the bootloader state is spoofed for Play Integrity. Test SystemUI builds by bind-mounting the signed APK, `.odex` and `.vdex` over `/system_ext/priv-app/ParanoidSystemUI/` and running `stop && start`; a reboot removes the overlay. Screenshots may fail until reboot when testing this way.

---

## 1.0 (unofficial test) — 2026-10-27

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
