# Freefall Club Jet Wing

A jet-powered wing for FiveM, inspired by the real jet-wing pilots. Jump to take off from standing, hover like
a drone, then tilt forward into jet flight at about 330 km/h (435 km/h with boost). Land gently on your feet,
or open the parachute.

## Features
- **Vertical take-off from standing.** Jump and you climb into a hover. Step off anything high and the engines catch you.
- **Drone-like hover.** Lean to move, let go to stop, climb and descend on an auto-throttle, turn on the spot.
- **Plane-style jet flight.**
  - **Controls:** A/D bank; S pulls (pull in a bank to tighten the turn); W pushes.
  - **Hands off:** the wing holds its line.
  - **Physics:** engine thrust fades with speed, so the top speed is real, not capped.
- **Boost, smoke trails, fuel** (10 minutes at full power), and **engine sound made in code** (no audio files).
- **A drawn carbon wing** with four turbines, glowing nozzles and jet exhaust, visible to other players.
- **Landing:** touch down gently and you step out. Hit something fast and it is fatal. The parachute is on F.
- **Inventory item support** (ox_inventory, Qbox, QBCore, ESX) or a simple `/jetwing` command.
- **Standalone:** works with any framework, or none. Only needs `ox_lib`.
- **Light:** about 0.13 ms per visible wing.

## Requirements
- GTA V **Legacy** game build (FiveM Asset Escrow is not available on Enhanced yet).
- [ox_lib](https://github.com/overextended/ox_lib)

## Install
1. Put the `dz_jetwing` folder in your server's `resources` folder.
2. Add it to `server.cfg` **after** ox_lib:
   ```
   ensure ox_lib
   ensure dz_jetwing
   ```
3. Restart the server.

## How to fly
| Key | Hover | Jet flight |
|---|---|---|
| Space (on the ground) | Take off | |
| W / S | Move forward / back; hold W to go into jet flight | Push / pull |
| A / D | Turn on the spot | Bank and turn |
| Space / Ctrl | Climb / descend | Throttle up / down |
| Shift | Boost | Boost |
| J | Engines on / off | |
| H | Smoke trails | Smoke trails |
| F | Parachute | Parachute |
| Mouse wheel | Camera distance | Camera distance |

Throttle right back in jet flight and you drop into a hover once you slow down. Players can rebind J, F and H in
*Settings > Key Bindings > FiveM*. `Config.InvertPitch` swaps W and S in jet flight.

## Inventory item (optional)
Set `Config.Item.enabled = true` (item name `jetwing` by default).

**ox_inventory**: add this to `ox_inventory/data/items.lua`:
```lua
['jetwing'] = {
    label = 'Jet Wing',
    weight = 9000,
    stack = false,
    close = true,
    description = 'Use to put it on or take it off.',
    client = { export = 'dz_jetwing.toggle' },
},
```
**Qbox / QBCore / ESX** (without ox_inventory): add an item called `jetwing` the usual way for your framework.
The script registers it as usable.

## Config highlights (`config.lua`)
- `Config.Wing`: colours (black and blue by default) and where the wing sits on the back.
- `Config.Flight`: the flight model (thrust, top speed, hover and jet handling). The defaults are tuned.
- `Config.FuelSeconds`, `Config.Keys`, `Config.Camera`, `Config.SpeedUnits` (mph or km/h).

## For developers
Exports (client): `exports.dz_jetwing:toggle()`, `exports.dz_jetwing:isWearing()`,
`exports.dz_jetwing:isFlying()`.
The player's state bag `dzJetwing` is `'equipped'` or `'flying'`.

## Works well with
- **Freefall Club Altimeter** (free): an altimeter HUD with audible alerts and a jump logbook.
- **Freefall Club Wingsuit**: BASE jump from buildings and cliffs.

Wearing one rig takes the other off.

## Support
See the store page for the support link. Please include your framework, your server build and any F8 errors.

(c) Samavik Studio. Licensed for use on servers you own or run. Do not redistribute or resell.
