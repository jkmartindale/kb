# ZTE Axon 7

### Recoveries
Bootstacks and recoveries are linked, so make sure you don't mix them up.

- [TWRP (official)](https://twrp.me/zte/zteaxon7.html) gets updates first, but doesn't have device-specific tools built in
- [TWRP Oki Labs Mod](https://forum.xda-developers.com/axon-7/development/recovery-twrp-3-2-3-0l-labs-mod-zte-t3841978) (Oreo Bootstack) has a few integrated scripts, but behind on TWRP updates and doesn't support ADB on the B12 encryption version

### TWRP Oki Labs Mod
- **iEDL Backup:** creates a flashable ZIP backup compatible with both recovery and EDL mode (or MiFlash)
- **Deep Wipe:** low level wipe of a partition including corresponding eMMC portions
- **Storage Backup/Restore:** works with backups of internal storage to `/external_sd/TWRP/BACKUPS`
- **Treble PARTY:** creates a vendor partition for use with Treble ROMs or removes it for use with legacy ROMs
- **Expand OS:** expands vendor and system partitions
- **Remove Msg.:** removes the unlocked bootloader message, **doesn't currently seem to work**
- **Unlock PW:** remove lock screen security
- **Unlock Google:** remove Google account binding

### Pixel Experience (Unofficial)
Device-specific ROM based on AOSP and special GApps. **Doesn't support encryption.**

1. Use [PARTY](https://forum.xda-developers.com/axon-7/development/tool-party-v0-1-vendor-partition-t3831517) to create a vendor partition if one doesn't already exist
1. Wipe system, data, cache, and Dalvik/ART cache
1. Install the LineageOS 15 Universal bootstack by DrakenFX if you have a different bootstack
1. Flash the corresponding modem if you haven't already
1. Re-flash your desired recovery if the bootstack flash overwrote it
1. Flash [Pixel Experience](https://forum.xda-developers.com/axon-7/development/rom-pixel-experience-t3953999) (which comes with GApps)
1. Flash [Magisk](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445) if you want it
1. Reboot

## Remove unlocked bootloader warning
1. Peruse [runninghamster's Android File Host files](https://androidfilehost.com/?w=files&flid=299186)
1. Flash `patch_unlock.zip`
1. Flash `Axon7_Stock_Logo_Blue.zip` if you'd like an alternate boot logo with a blue Axon 7 logo
1. Flash `Axon7_Stock_Logo.zip` when you change your mind and prefer just the ZTE logo
