# Freefall Club Wingsuit

A realistic wingsuit for FiveM. Put the suit on, walk to the edge of a building or cliff, jump, and you dive
head-first into flight. Glide, dive, flare, carve turns, then pull your parachute.

Made by a skydiving coach: the flight model is tuned to real wingsuit numbers.

## Features
- **Real wingsuit flight.** The physics are driven by angle of attack:
  - Glide ratios from 0.5:1 (full dive, about 300 km/h) to 3:1 (best glide).
  - Turns cost height.
  - A flare climbs only if you've built speed: 20–50 m after a dive, and none from a slow glide.
  - Energy is conserved, so there's no infinite climbing.
- **Jump exits.** Stand at an edge and press Space: you leap off one foot and dive into flight. Walking or falling
  off anything 40 m+ high works too.
- **A full suit you can see.** Inflated arm and leg wings with rib seams, worn from the moment you put it on, standing
  or flying, and visible to other players. Colours are in the config.
- **11 tested BASE exits** with map blips: the Maze Bank Tower roof, the Mile High Club tower, Mount Chiliad cliffs,
  Mount Josiah over Raton Canyon, a bridge tower and more. Every exit was test-jumped.
- **Parachute** on F (or left mouse) at any time.
- **Chase camera** with the mouse wheel to zoom, and a live HUD showing glide ratio and speeds.
- **Inventory item support** (ox_inventory, Qbox, QBCore, ESX) or a simple `/wingsuit` command.
- **Standalone:** works with any framework, or none. Only needs `ox_lib`.
- **Light:** about 0.13 ms per visible suit while one is on screen, near zero otherwise.

## Requirements
- GTA V **Legacy** game build (FiveM Asset Escrow is not available on Enhanced yet).
- [ox_lib](https://github.com/overextended/ox_lib)

## Install
1. Put the `dz_wingsuit` folder in your server's `resources` folder.
2. Add it to `server.cfg` **after** ox_lib:
   ```
   ensure ox_lib
   ensure dz_wingsuit
   ```
3. Restart the server.

## How to fly
| Key | Action |
|---|---|
| `/wingsuit` (or use the item) | Put the suit on or take it off |
| Space at an edge | Jump off and dive into flight |
| W / S | Dive / flare |
| A / D | Turn (bank) |
| F or left mouse | Open the parachute |
| Mouse wheel | Camera distance |

Players can rebind F in *Settings > Key Bindings > FiveM*.

## Exits
The exits are in `Config.TestExits.exits` and appear on the map (`Config.ExitBlips`). Admins can teleport to one
with `/wsexit <number>`. To let every player use it, set `restricted = false`. You can add your own exits: stand on
the edge, facing the drop, and copy your position and heading. A good exit has a near-vertical first 50–100 m,
as in real BASE.

## Inventory item (optional)
Set `Config.Item.enabled = true` (item name `wingsuit` by default).

**ox_inventory**: add this to `ox_inventory/data/items.lua`:
```lua
['wingsuit'] = {
    label = 'Wingsuit',
    weight = 3500,
    stack = false,
    close = true,
    description = 'Use to put it on or take it off.',
    client = { export = 'dz_wingsuit.toggle' },
},
```
**Qbox / QBCore / ESX** (without ox_inventory): add an item called `wingsuit` the usual way for your framework.
The script registers it as usable.

## Config highlights (`config.lua`)
- `Config.Suit.colours`: main, panel and trim colours (RGB).
- `Config.Flight`: the flight model. The defaults are tuned; change with care.
- `Config.MinStartHeight`: how high a fall has to be before the suit takes over.
- `Config.Exit`: the jump exit (leap speed, dive time).
- `Config.Camera`, `Config.DeployKey`, `Config.SpeedUnits` (mph or km/h).

## For developers
Exports (client): `exports.dz_wingsuit:toggle()`, `exports.dz_wingsuit:isWearing()`,
`exports.dz_wingsuit:isFlying()`.
While flying, the player's state bag `dzFlight` is `'wingsuit'`. The Freefall Club Altimeter uses this to log
wingsuit jumps in the logbook.

## Works well with
- **Freefall Club Altimeter** (free): an altimeter HUD with audible alerts and a jump logbook.
- **Freefall Club Jet Wing**: take off from standing and fly at jet speed.

Wearing one rig takes the other off.

## Support
See the store page for the support link. Please include your framework, your server build and any F8 errors.

(c) Samavik Studio. Licensed for use on servers you own or run. Do not redistribute or resell.
