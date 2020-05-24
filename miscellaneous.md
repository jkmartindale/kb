# Miscellaneous

### KeePass field references
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

### Office phone activation
Office likes to say that **Telephone activation is no longer supported for your
product.** Rude and wrong. Sucks that phone activation is the only way to
transfer an Office license.

In the United States, call [+1 (866) 421-7141](tel:+1-866-421-7141).

For other countries, see the Office KB article ["Telephone activation is no longer supported for your product" error when activating Office](https://support.office.com/en-us/article/-telephone-activation-is-no-longer-supported-for-your-product-error-when-activating-office-9b016cd2-0811-4cb3-b896-5a6a13177713).

Don't bother with the smartphone option the phone system offers. All it does is
text a link (VoIP numbers unsupported) to a webpage that asks you to type in the
numbers on your screen. You could do the same thing over the phone in the same
amount of time.

### youtube-dl
List available formats for a video
```
youtube-dl -F https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Extract the best audio and convert it if needed
```
youtube-dl -f bestaudio -x --audio-format flac https://www.youtube.com/watch?v=dQw4w9WgXcQ
```