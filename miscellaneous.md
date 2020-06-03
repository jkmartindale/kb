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

### Spotify search syntax
Spotify supposedly supports literal searches with quotes, though Spotify will
still treat quoted content as a substring.

Spotify has traditional Boolean operators OR, AND (+), and NOT (-), with AND
being the default (because it's no longer 1998).

**&** is treated as a literal, so don't search for a song by multiple artists
with `artist1 & artist2`, just remove the `&`.

Spotify supports a number of search operators, some no longer documented. For
passing content with spaces to an operator, use quotes (e.g. `genre:"Rock &
Roll"`).

| Operator  | Description |
| --------- | ----------- |
| `album:`  | Album name |
| `artist:` | Artist name |
| `label:`  | Record label |
| `genre:`  | [List of genres](http://everynoise.com/everynoise1d.cgi?scope=all) |
| `isrc:`   | International Standard Recording Code |
| `tag:new` | "Recently added" |
| `track:`  | Track name |
| `upc:`    | Universal Product Code |
| `year:`   | Year or year range |

### Telegram: find replies
Search for `#m`. You can filter to a single conversation but you can't filter by
sender or additional keywords.

### Twitter search operators
| Operator | Finds tweets... |
| -------- | --------------- |
| bruh moment | containing both "bruh" and "moment" |
| "bruh moment" | containing the exact phrase "bruh moment" |
| bruh OR moment | containing either "bruh" or "moment" or both |
| bruh -moment | containing "bruh" but not "moment |
| #bruhmoment | containing the hashtag #bruhmoment |
| from:jkmartindale | sent from [@jkmartindale](https://twitter.com/jkmartindale) |
| to:jkmartindale | sent as a reply to @jkmartindale |
| @jkmartindale | replying to or mentioning @jkmartindale |
| near:"New York" | sent near New York |
| within:15mi | within a 15-mile radius (requires near:) |
| since:2017-01-17 | sent on or after 2017-01-17 |
| until:2023-01-17 | sent before 2020-01-17 |
| :) | with positive sentiment |
| :( | with negative sentiment |
| filter:hashtags | with at least one hashtag |
| filter:images | containing photos or "GIFs" (filter:twimg is an alias) |
| filter:links | containing links or media |
| filter:media | containing photos, video, or "GIFs" |
| filter:mentions | mentioning or replying to anyone |
| filter:native_video | containing videos uploaded directly to Twitter |
| filter:periscope | containing Periscope URLs |
| filter:safe | that are not marked as potentially sensitive content |
| filter:verified | sent from verified accounts |
| filter:videos | containing uploaded video or links to videos |
| filter:vine | containing a link to a Vine |
| lang:und | in an unidentified language [[list of supported languages]](https://developer.twitter.com/en/docs/tweets/search/guides/premium-operators) |
| url:jkmartindale | with URLs containing "jkmartindale" |
| source:"Twitter for HomePod" | sent from the client "Twitter for HomePod" (not standalone) |

`?` is officially an operator for finding questions but it seems to be based on
literal matching of a question mark, not intent analysis.

`-filter:retweets` is supposed to filter out retweets, though retweets no longer
show up in search results. `filter:retweets` matches "RT" anywhere in the tweet.

According to Twitter documentation `filter:images` matches links identified as
photos, but this is no longer the case.

### youtube-dl
List available formats for a video
```
youtube-dl -F https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Extract the best audio and convert it if needed
```
youtube-dl -f bestaudio -x --audio-format flac https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
