## android

### Useful Downloads
- [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools), because nobody wants to download Android Studio just for adb/fastboot
- [Universal ADB Drivers](https://adb.clockworkmod.com/)

### Extract Steam TOTP Secret
Open `/data/data/com.valvesoftware.android.steam.community/files/Steamguard-*/` as a JSON file. The `uri` property contains an `optauth://` URI including the secret.
