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
1. Browse through the subkeys until you find one with a value containing the
   name of the blank entry
1. Delete it
1. Reopen Windows Explorer

### Change next screenshot number
1. Open Registry Editor
1. Navigate to
   HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer
1. Edit `ScreenshotIndex`

### Custom shell folder locations
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell
Folders

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
> what if you  
> wanted to delete a file  
> but Windows said  
> **This action can't be completed because the file is open in another program**

1. Download and launch [Process
   Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
1. Hit Ctrl + F (or go to the **Find** menu and select **Find Handle or
   DLL...**)
1. Type in at least part of the filename and hit **Search**
1. For each process locking the file in question,
    1. Select the search results entry, which will highlight the process in the
       main window
    1. Switch to the main window
    1. Hit the delete key (or right-click the entry and select **Kill Process**)

Now you should be able to do whatever you wanted to with said file

### Install HEVC codec
Along with the
[easy to find paid HEVC codec](https://www.microsoft.com/en-us/p/hevc-video-extensions/9nmzlz57r3t7),
Microsoft offers a
[hidden away free HEVC codec](https://www.microsoft.com/en-us/p/hevc-video-extensions-from-device-manufacturer/9n4wgh0z6vhq)
that has your hardware manufacturer foot the HEVC licensing bill.

### Edit the Power User Menu (Win + X)
The Power User Menu is located at `%LocalAppData%\Microsoft\Windows\WinX`. Its
subfolders (named `Group1`, `Group2`, etc.) correspond to the groups of
shortcuts separated by horizontal bars. The lower the number, the lower it
appears on the menu. You can add and remove groups, and numbers don't have to be
consecutive.

Shortcuts that get added will be ignored unless they have a 4-byte hash (of data
that includes application path, arguments, and "do not prehash links.  this
should only be done by the user."). There's a command-line tool called hashlnk
[[executable]](https://github.com/riverar/hashlnk/blob/master/bin/hashlnk_0.2.0.0.zip)
[[source]](https://github.com/riverar/hashlnk) to add this hash to a shortcut.

Shortcuts are listed in alphabetical order of their filenames. However, this can
be different from the filename shown in File Explorer. The `desktop.ini` file in
group folders can set display names that show in both File Explorer and the
Power User Menu, in the format `filename=Display Name`. You can also customize
the display name using the shortcut's comment field. This overrides
`desktop.ini` for the name that gets displayed in the Power User Menu, but won't
affect what's displayed in File Explorer.

The Power User Menu, like much of Windows, supports *access keys*, which are
keys you can press to activate a menu item, indicated by underlined letters in
the label. To add an access key to your shortcut, add `&` before the letter you
wish to be the access key in either `desktop.ini` or the shortcut comment. If
more than one shortcut in the Power User Menu (across groups) shares the same
access key, pressing the access key will toggle between them instead of
launching (which you can do with Enter instead).

In order to see any changed you make to the Power User Menu shortcuts, you will
need to restart `explorer.exe`, which is easy enough to do with Task Manager or
PowerShell:
```powershell
Stop-Process -Name explorer
```

### Edit spellcheck dictionary
Navigate to `%APPDATA%\Microsoft\Spelling` and edit the `Default.dic` file under
the appropriate language.

### Turn Num Lock on/off at startup
On:
```powershell
Set-ItemProperty -Path 'Registry::HKU\.DEFAULT\Control Panel\Keyboard' -Name "InitialKeyboardIndicators" -Value "2"
```

Off:
```powershell
Set-ItemProperty -Path 'Registry::HKU\.DEFAULT\Control Panel\Keyboard' -Name "InitialKeyboardIndicators" -Value "0"
```
