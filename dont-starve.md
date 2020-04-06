# Don't Starve

### Curio rarity
The Trade Inn only works for rarities below <span
style="font-wight:bold;color:#BD4646">Elegant</span> and nothing with a
**Woven** modifier.

| Rarity | Drop Rate | Marketable? |
| ------ | --------- | ----------- |
| <span style="font-weight:bold;color:#B7D2D9">Common</span> | 52.7% | Unless Event/Seasonal |
| <span style="font-weight:bold;color:#415078">Classy</span> | 26.0% | Unless Event/Seasonal |
| <span style="font-weight:bold;color:#68457C">Spiffy</span> | 13.0% | Unless Event/Seasonal |
| <span style="font-weight:bold;color:#BA74A5">Distinguished</span> | 6.0% | Unless Event/Seasonal |
| <span style="font-weight:bold;color:#BD4646">Elegant</span> | 2.3% | Unless Event/Seasonal |
| <span style="font-weight:bold;color:#A2C46F">Loyal</span> | N/A | No |
| <span style="font-weight:bold;color:#6CC17B">Timeless</span> | N/A | No |
| <span style="font-weight:bold;color:#B49400">Event</span> | N/A | No |
| <span style="font-weight:bold;color:#007A4D">Proof of Purchase</span> | N/A | No |
| <span style="font-weight:bold;color:#E8971E">Reward</span> | N/A | No |
| <span style="font-weight:bold;color:#EE5D40">Heirloom</span> | N/A | Yes |

### Selecting players
If you just want to target yourself, you can use `ThePlayer`. Otherwise, you'll
need to index the `AllPlayers` array. You can figure out which player is at
which index with:
```lua
c_listAllPlayers()
```

### Set stats
```lua
c_sethealth(percent)
c_sethunger(percent)
c_setmoisture(percent)
c_setsanity(percent)
c_settemperature(degrees)
```

Or if you prefer to constantly regenerate your hunger:
```lua
c_maintainall(ThePlayer)
c_maintainhealth(ThePlayer)
c_maintainhunger(ThePlayer)
c_maintainmoisture(ThePlayer)
c_maintainsanity(ThePlayer)
c_maintaintemperature(ThePlayer)
```

If you want to stop your cheaty regeneration:
```lua
c_cancelmaintaintasks(ThePlayer)
```

Or if you hate getting your sanity, hunger, and health drained when being
attacked, you can use:
```lua
c_godmode(ThePlayer)
```

And if you want to max out your stats as well, use this:
```lua
c_supergodmode(ThePlayer)
```

Both God Mode and Super God Mode are toggled with those commands. While in
either mode you can't change your stats.

### Move to player
Using the `AllPlayers` index from `c_listAllPlayers()`:
```lua
c_goto(AllPlayers[index])
```
