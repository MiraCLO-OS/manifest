# MiraCLO changelog

Every change made to MiraCLO, newest first. Each entry says **what** changed, **where** (repository and commit) and **why**, so the project can be rebuilt or understood without anyone's memory.

Format: `repository @ commit — summary`

## 1.0 Beta 2 "Aurora" — 30-10-2026

`user` build, signed with MiraCLO release keys. Dirty-flash over Beta 1.

### Dynamic Island (new)
- ColorOS 17-style Dynamic Island around the front camera
- Own settings page: Settings › Notifications › Dynamic Island
- Music and video with controls, album-art glow and recent players
- Incoming and ongoing calls with Answer and Decline
- Timers and stopwatch from Clock, with a "Time's up" card
- Screen recording with countdown, timer and Stop
- Live updates for navigation, rides and deliveries
- Progress for downloads, Quick Share and recordings
- Charging, earbuds battery, ringer mode and low battery alerts
- Up to 3 activities at once as pills beside the camera
- Tap to open a card; swipe and hold gestures
- Optional haptics, touch glow and ambient glow
- Hides inside its own app, on the lock screen and in full-screen apps
- Replaces the status bar chip and pop-up for the same activity
- Status bar trims to clock and battery when pills need room
- Paused music leaves after 10 minutes (optional)
- Every activity and behaviour can be turned off

### Liquid Glass (new)
- Clear glass look, chosen per place in Settings › Display › Liquid Glass
- For Quick Settings, notifications, island cards, island pills, volume panel and power menu
- Lock screen and pop-up notifications stay solid for readability
- With Liquid Glass off, the dark ColorOS Quick Settings is solid, with no blur

### Volume panel (new)
- One UI-style panel: slim edge slider that opens to every volume
- Ringer mode, media output and sound settings in the panel
- Follows Material You colours and Liquid Glass
- Android's panel is one switch away in Settings

### About phone (redesigned)
- ColorOS-style banner with your wallpaper, MiraCLO version and an Update button
- Device name and maintainer first, every other detail in matching cards

### Quick Settings
- Smaller music buttons in the ColorOS style

### Status bar
- Network speed on one line, in the status bar font

### MiraCLO kernel (new)
- Own kernel, "aurora", built from MiraCLO-OS source
- Linux 5.10.269 with the October 2026 security patch
- BBR network congestion control by default
- Larger zram (60% of RAM, up to 6 GB) keeps more apps in memory
- 128 KB read-ahead for quicker app launches
- Short touch boost on the performance cores for smoother scrolling
- Root as separate recovery zips: KernelSU, KernelSU-Next and SukiSU-Ultra, each with SUSFS

### Base
- Updated to CLO LA.QSSI.17.0.r1-12300
- Newer CLO Wi-Fi, Bluetooth, telephony, frameworks and build components
- MiraCLO is now independent: every repository lives in the MiraCLO-OS organisation

### Branding
- New boot animation
- Shorter, clearer texts across all MiraCLO settings
- About banner in MiraCLO brand colours

### Fixes
- YouTube Music pill appears right away after minimising
- Tapping a side pill opens its own card
- Screen-record chip no longer shows over the island
- Island timers, recent players and card buttons fixed
- QS play button fixed

### Known issues
- Some banking apps (for example Kotak 811) report a security threat

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
