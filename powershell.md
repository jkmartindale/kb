## powershell

### Change file's "Date Modified"
You'll most likely provide a date in `YYYY,MM,DD` or `YYYY,MM,DD,HH,MM,SS` format, but you can use any [DateTime constructor](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.-ctor).
```powershell
(Get-Item '.\path\to.item').LastWriteTime = New-Object DateTime 2019,10,27, 21,24,56
```

### Get Dell Service Tag
```powershell
(Get-WmiObject win32_SystemEnclosure).SerialNumber
```
