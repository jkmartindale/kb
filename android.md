# Android

### Useful Links
- [Edify reference](https://source.android.com/devices/tech/ota/nonab/inside_packages)
  (scripting language used by `update-binary`)
- [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools),
  because nobody wants to download Android Studio just for adb/fastboot
- [Universal ADB Drivers](https://adb.clockworkmod.com/)

### Favorite Magisk Modules
- [Foxy Boot](https://github.com/Magisk-Modules-Repo/foxy-boot) - replaces the
  boot animation with kernel ring buffer skid porn
- [Magisk Direct Share Disabler](https://github.com/AndroPlus-org/magisk-module-direct-share-disabler) -
  Removes the annoying "direct share" menu that makes the share sheet take ages
  to load
- [Smali Patcher](https://forum.xda-developers.com/apps/magisk/module-smali-patcher-0-7-t3680053) -
  hides mock location status, disables screenshot blocking, disables APK
  signature verification, disables the high volume warning, and bypasses Samsung
  KNOX

### Force reset PIN
Assuming the device isn't encrypted, deleting `locksettings.db` is sufficient.

With `adb`:
```sh
adb shell su -c "rm /data/system/locksettings.db*"
```

If a custom recovery is installed, you likely can find your own way to delete
`locksettings.db` without needing `adb` access.

If the device is encrypted but you have `fastboot` access, you can wipe user
data as a last resort:
```sh
fastboot erase userdata
```

### Extract Steam TOTP Secret
This requires root access.

Open `/data/data/com.valvesoftware.android.steam.community/files/Steamguard-*/`
as a JSON file. The `uri` property contains an `optauth://` URI including the
secret.

If you have a `sed` installed (e.g. from Busybox), you can run this with an
on-device terminal emulator or `adb shell` to get the `optauth://` URI:
```shell
sed 's/\\\//\//g; s/.*"\(otpauth\:[^"]*\).*/\1\n/' /data/data/com.valvesoftware.android.steam.community/files/Steamguard-*
```
