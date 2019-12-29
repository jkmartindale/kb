# Windows

### Shortcut to Windows Store app
Open the Applications folder, by typing `shell:AppsFolder` into the Windows
Explorer address bar or the Run dialog.

### Get Dell Service Tag
Run this in PowerShell:
```powershell
(Get-WmiObject win32_SystemEnclosure).SerialNumber
```

### Remove blank Devices and Drives entry
1. Open Registry Editor
1. Navigate to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace
1. Browse through the subkeys until you find one with a value containing the name of the blank entry
1. Delete it
1. Reopen Windows Explorer

### Change next screenshot number
1. Open Registry Editor
1. Navigate to HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer
1. Edit `ScreenshotIndex`

### Custom shell folder locations
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

### Skip lock screen
1. Open Registry Editor
1. Navigate to HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows
1. Create a new key `Personalization` if it doesn't already exist
1. Within the `Personalization` key, create a new DWORD value called `NoLockScreen` set to 1.
