# Windows

### Useful utilities
- [EdgeDeflector](https://github.com/da2x/EdgeDeflector) - redirect web searches
  from Windows Search to your preferred browser instead of Edge
- [HEVC
  codecs](https://www.microsoft.com/en-us/p/hevc-video-extensions-from-device-manufacturer/9n4wgh0z6vhq)
  free from Microsoft, just hidden
- [Sandboxie](https://www.sandboxie.com/DownloadSandboxie) - lightweight
  sandbox, especially good for analyzing application installers

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

### Start tiles for desktop apps
Start tiles for desktop apps are defined in
`appname.VisualElementsManifest.xml`, where `appname` is the filename your tile
points to, without the extension. This works for `appname.exe` but also things
like `appname.txt` or whatever you want. Store it next to the shortcut target.
If there are any errors in the XML, the entire file is ignored.

The XML looks like this:
```xml
<Application xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <VisualElements
        BackgroundColor="#FF0000"
        ForegroundText="light"
        ShowNameOnSquare150x150Logo="on"
        Square70x70Logo="path\to\something.png"
        Square150x150Logo="path\to\something.png"
    />
</Application>
```

All attributes are required except `Square150x150Logo` and `Square70x70Logo`.

`BackgroundColor` also applies to the background of the application icon shown
in **All Apps**. It can be an RGB hex string or one of these predefined
constants:
- black
- silver
- gray
- white
- maroon
- red
- purple
- fuchsia
- green
- lime
- olive
- yellow
- navy
- blue
- teal
- aqua

`ForegroundText` is either "light" or "dark"

`ShowNameOnSquare150x150Logo` is either "on" or "off"

Tile image constraints:
- You must define no images or both, defining just one is an error
- Maximum dimensions of 1024x1024
- Maximum file size of 200 KB
- Extension of .gif, .jpg, .jpeg, or .png

To see the new tile, update the shortcut file. Changing its date modified is
enough:
```powershell
(ls "$env:ProgramData\Microsoft\Windows\Start Menu\Programs\appname.lnk").LastWriteTime = Get-Date
```

### Override DPI scaling for system apps
System applications don't provide a **Compatibility** tab in their properties
window and ignore keys in `HKCU\Software\Microsoft\Windows
NT\CurrentVersion\AppCompatFlags\Layers`.

The easiest approach to overriding DPI scaling is to make a new subkey
`HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution
Options\executable.exe`, where `executable.exe` is the filename of the
executable (duh). Add a DWORD value called `dpiAwareness` with the data `0`, and
Windows will now scale the application. This registry key is primarily for
attaching a debugger to an executable no matter how it's run, but it can change
a few other aspects of how the executable runs like Exploit Guard mitigation
options or, thankfully, DPI scaling.

This will apply to every executable with that filename, so in the rare case that
doesn't work out for you, you can use an external application manifest. First,
you'll want to find the old manifest, which can be easily done by opening the
executable in a text editor. The manifest is embedded as plain text so it's easy
to spot:
```xml
□M□U□I□<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!-- Copyright (c) Microsoft Corporation -->
<assembly 
    xmlns="urn:schemas-microsoft-com:asm.v1" 
    xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
    manifestVersion="1.0"
    >
<assemblyIdentity
    version="5.1.0.0"
    processorArchitecture="amd64"
    name="Microsoft.Windows.Help.HH"
    type="win32"
/>
<description>Microsoft HTML Help Executable</description>

<trustInfo xmlns="urn:schemas-microsoft-com:asm.v3">
    <security>
        <requestedPrivileges>
            <requestedExecutionLevel
                level="asInvoker"
                uiAccess="false"
            />
        </requestedPrivileges>
    </security>
</trustInfo>
    <asmv3:application>
        <asmv3:windowsSettings xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
            <dpiAware>true</dpiAware>
        </asmv3:windowsSettings>
    </asmv3:application>
</assembly>
```

Copy the manifest into an XML file called `filename.exe.manifest` and change the
`<dpiAware>` tag to `false`. Save it next to the original executable.

In order for Windows to recognize the external manifest, open
`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\SideBySide`. Make a new DWORD
value called `PreferExternalManifest` with the data `1`.
