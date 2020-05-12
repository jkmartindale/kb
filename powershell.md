# PowerShell

### Change file's "Date Modified"
You'll most likely provide a date in `YYYY,MM,DD` or `YYYY,MM,DD,HH,MM,SS` format, but you can use any [DateTime constructor](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.-ctor).
```powershell
(Get-Item '.\path\to.item').LastWriteTime = New-Object DateTime 2019,10,27, 21,24,56
```

### Hash a file
```powershell
(Get-FileHash '.\ngl-pretty-sus.rar' -Algorithm MD5).Hash
```
Where `.\ngl-pretty-sus.rar` is the filepath to the file to hash. Algorithms supported are SHA1, SHA256, (default), SHA384, SHA512, and MD5.
