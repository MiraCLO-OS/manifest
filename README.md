# MiraCLO manifest

The repo manifest for **MiraCLO**, a CodeLinaro-based Android 17 ROM built on Paranoid Android (AOSPA) Calcite.

| | |
| --- | --- |
| Branch | `calcite` (Android 17) |
| Base | [AOSPA](https://github.com/AOSPA) Calcite |
| Devices | `marble` (POCO F5 / Redmi Note 12 Turbo) |
| Changes | See [CHANGELOG.md](CHANGELOG.md) |

## Requirements

- 64-bit Linux, Ubuntu 22.04 or newer recommended
- 32 GB RAM or more (64 GB preferred)
- 400 GB or more of free SSD space
- Git and `repo` installed, with your Git name and email configured

## Get the source

```bash
mkdir -p ~/miraclo && cd ~/miraclo
repo init -u https://github.com/MiraCLO-OS/manifest -b calcite --git-lfs --depth=1
repo sync -c -j16 --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
```

Device repositories for `marble` (device, kernel, vendor and HALs) are synced automatically during `lunch` from `vendor/aospa/products/marble/beans.xml`.

If a later `repo sync` fails with `invalid upstream ... ^1` on the manifest, unshallow it once:

```bash
git -C .repo/manifests fetch --unshallow origin
```

## Build

```bash
./rom-build.sh marble -t userdebug -z
```

| Flag | Meaning |
| --- | --- |
| `-t userdebug` / `-t user` | Build type: `userdebug` for testing, `user` for public releases |
| `-z` | Also produce a fastboot image zip |
| `-i` | Clean old images first (after changing kernel, build type or keys) |
| `-s <dir>` | Sign with release keys from `<dir>` |
| `-v beta` / `-v stable` | Release build: names the zip with the release number and codename from `vendor/aospa/target/product/version.mk` (e.g. `MiraCLO-1.0-beta1-Aurora-…`) |

Output zips are written to the root of the source tree:

| File | Use |
| --- | --- |
| `MiraCLO-<ver>-<variant>-marble-<date>-gapps.zip` | Flash from recovery |
| `MiraCLO-<ver>-<variant>-marble-<date>-gapps-image.zip` | Flash with `fastboot update` |
| `…-signed-target_files.zip` | Build package for incremental OTAs; not for flashing |

## Signed builds

Official MiraCLO builds are signed with the maintainer's private release keys, which are **never** stored in any repository. Your own builds should use your own keys:

```bash
./rom-build.sh marble -t user -v beta -z -s ~/.android-certs
```

## MiraCLO-maintained repositories

| Path | Repository | Why it is forked |
| --- | --- | --- |
| `vendor/aospa` | `android_vendor_aospa` | Branding, version, build script, boot animation, wallpaper |
| `frameworks/base` | `android_frameworks_base` | SystemUI Quick Settings: ColorOS style, media card |
| `packages/apps/Settings` | `android_packages_apps_Settings` | MiraCLO version, QS style setting |
| `packages/apps/ParanoidSystemUI` | `android_packages_apps_Paranoid_SystemUI` | Refresh-rate tile cleanup |
| `packages/apps/Launcher3` | `android_packages_apps_Launcher3` | ColorOS (stacked) recents style |
| `hardware/xiaomi` | `android_hardware_xiaomi` | Dolby build fix |

Every other repository comes unchanged from AOSPA or `aospa-shadedark`.

## Credits

[Paranoid Android (AOSPA)](https://github.com/AOSPA), [ShadeDark6](https://github.com/aospa-shadedark), [Pzqqt](https://github.com/Pzqqt), [The LineageOS Project](https://github.com/LineageOS), [CodeLinaro](https://www.codelinaro.org/) and the Android Open Source Project.
