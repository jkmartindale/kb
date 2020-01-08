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
1. Within the `Personalization` key, create a new DWORD value called `NoLockScreen` set to 1

### Copy command-line output to clipboard
Just pipe it to `clip`, e.g.
```cmd
echo "ok this is epic" | clip
```

### Find which process locked a file
what if you  
wanted to delete a file  
but Windows said  
**This action can't be completed because the file is in use by an application**

1. Download and launch [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
1. Hit Ctrl + F (or go to the **Find** menu and select **Find Handle or DLL...**)
1. Type in at least part of the filename and hit **Search**
1. For each process locking the file in question,
    1. Select the search results entry, which will highlight the process in the main window
    1. Switch to the main window
    1. Hit the delete key (or right-click the entry and select **Kill Process**)

Now you should be able to do whatever you wanted to with said file
