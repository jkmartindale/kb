# Miscellaneous Software

### KeePass Field References
Fields in one entry can reference fields in other entries, such as when two
services might have differing usernames but the same password (thanks,
university LDAP). Field references can keep multiple fields in sync.

The general format:
```
{REF:<FieldCode>@<SearchCode>:<SearchString>}
```

`FieldCode` and `SearchCode` are one-letter codes corresponding to the following
fields:

| Code | Field |
| ---- | ----- |
| T    | Title |
| U    | Username |
| P    | Password |
| A    | URL |
| N    | Notes |
| I    | UUID |
| O    | Custom Field (`SearchCode` only) |

`FieldCode` specifies which field to fetch and `SearchCode` and `SearchString`
specify which record to fetch from.

For example, my Office 365 entry has a password value of `{REF:P@T:University of Oklahoma}`,
which references the password of the entry with the title "University of Oklahoma".

### youtube-dl
List available formats for a video
```
youtube-dl -F https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Extract the best audio and convert it if needed
```
youtube-dl -f bestaudio -x --audio-format flac https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
