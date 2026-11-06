# Freefall Club Altimeter (free)

A skydiver's altimeter for FiveM: a dial on screen while you fall, audible alerts at break-off, pull and hard
deck, and a logbook of every jump for each character.

Made by a skydiving coach.

## Features
- **Altimeter dial HUD.**
  - Feet or metres, height above the ground (as set at a dropzone) or above sea level.
  - Red and yellow zones.
  - Four screen positions and adjustable size.
- **Audible alerts** in freefall: three beeps at break-off, a long tone at pull, and a fast alarm at the hard deck
  until your canopy opens. Heights are configurable.
- **Jump logbook** (`/logbook`): exit and deploy heights, freefall and canopy time, top speed, and how it ended
  (landed, cutaway, or incident).
- Shows automatically in freefall, and in an aircraft once you're high enough with a parachute on.
- Works with **Freefall Club Wingsuit** and **Freefall Club Jet Wing**: wingsuit flights are tracked and logged too.
- **Frameworks:** Qbox, QBCore and ESX are detected automatically, or it runs standalone (the logbook then uses the
  player's license).

## Requirements
- [ox_lib](https://github.com/overextended/ox_lib)
- [oxmysql](https://github.com/overextended/oxmysql) (the `dz_jumps` table is created on first start)

## Install
1. Put the `dz_altimeter` folder in your server's `resources` folder.
2. Add it to `server.cfg` after ox_lib and oxmysql:
   ```
   ensure oxmysql
   ensure ox_lib
   ensure dz_altimeter
   ```
3. Restart the server.

## Commands
| Command | What it does |
|---|---|
| `/altimeter` | Show or hide the HUD (players can also bind a key) |
| `/logbook` | Open your jump logbook |
| `/dzjump` | Admins: go up 1,500 m with a parachute to test |

## Config highlights (`config.lua`)
- `Config.Units` (ft or m), `Config.AltitudeMode` (agl or msl), `Config.Position`, `Config.Scale`.
- `Config.Alerts`: heights and sounds. `Config.AlertVolume`.
- `Config.RedZone` and `Config.YellowZone`, `Config.DialMax`.
- `Config.Framework`: `auto`, or force `qbx`, `qb`, `esx` or `standalone`.
- Text is in `locales/en.json`. Copy it to add a language.

(c) Samavik Studio. Free to use on your servers. Do not resell.
