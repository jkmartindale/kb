## Change file's "Date Modified"
```powershell
# YYYY, MM, DD
# or YYYY, MM, DD, HH, MM, SS
(Get-Item '.\path\to.item').LastWriteTime = New-Object DateTime 2019,10,27, 21,24,56
```
