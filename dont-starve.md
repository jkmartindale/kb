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

### List all players
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
