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

## Split string on a string
`String.Split()` works on just a single character, but the [`-Split` operator](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_split) uses regular expressions by default.

### Remove line from files
```powershell
Get-ChildItem "path\to\folder" -Filter *.htm | 
Foreach-Object {
    $content = Get-Content $_.FullName # Temp variable needed to prevent simultaneous access
    $content | Select-String -SimpleMatch 'String you want to remove' -NotMatch | Set-Content $_.FullName
}
```

You can also swap `-SimpleMatch` with `-Pattern` if you want to use regular expressions.

### View function source code
```powershell
${function:Get-FileHash}
```
`Function:` is a virtual volume full of strings.

### Remove a property from an object
Let's say we have this object:
```powershell
$demo = [PSCustomObject] @{
    Foo="foo"
    Bar="bar"
}
```

It looks like this when we output it:
```
PS> $demo

Foo Bar
--- ---
foo bar
```

To remove the property:
```powershell
$a.PSObject.Properties.Remove("Bar")
```

Now it's gone:
```powershell
$demo
```
```
Foo
---
foo
```

However if a custom type was set on this object, that can (but not always) override what gets shown with Get-Output:
```powershell
 $demo.PSObject.TypeNames.Insert(0, "System.String")
 $demo
```
```
@{Foo=foo}
```
```powershell
$demo.PSObject.TypeNames.Insert(0, "Microsoft.Powershell.Utility.FileHash")
$demo
```
```
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
```
Sometimes output is deferred to something lower in the types stack:
```powershell
$demo.PSObject.TypeNames.Insert(0, "System.IO.File")
$demo
```
```
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
```
Sometimes it isn't:
```powershell
$demo.PSObject.TypeNames.Insert(0, "System.String")
$demo
```
```
@{Foo=foo}
```
Sometimes it forgets again:
```powershell
$demo.PSObject.TypeNames.Insert(0, "System.IO.File")
$demo
```
```
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
```

If late binding gets in the way you're better off making a custom object.
