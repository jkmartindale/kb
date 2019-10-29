# Android

### Useful Downloads
- [SDK PlatformTools](https://developer.android.com/studio/releases/platform-tools),
  because nobody wants to download Android Studio just for adb/fastboot
- [Universal ADB Drivers](https://adb.clockworkmod.com/)

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
