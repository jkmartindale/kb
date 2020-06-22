# Steam

### Remove a game from your account
Sometimes hiding a game from your library isn't enough to hide the sin.

1. Find the game in your Steam library
1. Click on **Support**
1. Select **I want to permanently remove this game from my account**
1. Confirm that you want to lose access to everything in the package the game came in and click on **Ok, remove the listed games from my account permanently**

If you change your mind and want the game back,
1. Find the support page for the game
    1. Go to the [Games and Applications](https://help.steampowered.com/en/wizard/HelpWithGame) section of Steam support and search for the game.
    1. If it doesn't show up, the game might have been delisted from Steam. Search for the game on [SteamDB](https://steamdb.info/) and make note of the `appid`, then navigate to https://help.steampowered.com/en/wizard/HelpWithGame/?appid=, adding the `appid` to the end of the URL
1. Select **It's not in my library**
1. Select **Restore the previously removed package to my account**

Just like removing a game, adding a game back to your account will restore everything in the package.

### See how much money you've given to Gabe Newell
https://help.steampowered.com/en/accountdata/AccountSpend

### Extract Steam TOTP secret
This method requires Steam Authenticator to be installed and activated on an Android device with root access.

Open `/data/data/com.valvesoftware.android.steam.community/files/Steamguard-*/` as a JSON file. The `uri` property contains an `optauth://` URI including the secret.

If you have a `sed` installed (e.g. from Busybox), you can run this with an on-device terminal emulator or `adb shell` to get the `optauth://` URI:
```shell
sed 's/\\\//\//g; s/.*"\(otpauth\:[^"]*\).*/\1\n/' /data/data/com.valvesoftware.android.steam.community/files/Steamguard-*
```
