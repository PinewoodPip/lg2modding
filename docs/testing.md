# Testing your mod

Testing your creations is essential to the process of modding. This page gives you hints on how to be more efficient with the process.

## Log output
The `modding.log` file in your save directory logs errors related to modding - these are mostly related to malformatted data in the json files. If the game or your mod doesn't work properly, you should check this file for troubleshooting. It pinpoints the problematic files.

## Cheat console
By creating a file named `ilovepip.txt` in your save directory, you'll be able to access the console ingame by pressing the `\`` (tilde) key, from which you can enter numerous commands to speed up testing content.

The following commands exist. `{}` denote required parameters, `[]` denote optional ones.

`addres {metal | xp | candy | fuel} {amount}`

Adds an amount of a resource.

`setres {metal | xp | candy | fuel | energy} {amount}`

Sets a resource's amount.

`sethangarspace {amount}`

Sets the base amount of ships that you can deploy to fights.

`maxenergy`

Forces energy to stay at the 'optimal' amount. Enter again to toggle off.

`idle {minutes}`

Gives you `{minutes}` worth of resource production.

`unlockbuildings`

Unlocks all buildings for construction.

`unlockships`

Unlocks all ships, including modded ones.

`skipfleetcd`

Removes the current cooldown for deploying a new fleet.

`strast [id]`

Next asteroid to spawn will be strange. If a strast id is provided, it will be of that type (even if not unlocked).

`pipmode`

The holy grail cheat:

- Allows you to buy most things without needing the resources
- Unlocks the Galaxy map, combat abilities and Ascension
- Calls the `maxenergy`, `unlockbuildings` and `unlockships` commands
- Unlocks all lore logs
- Changes the default boost to the testing one (TODO elaborate)