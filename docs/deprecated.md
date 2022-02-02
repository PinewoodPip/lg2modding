
If you've found this page, it means you are worthy of reading up about juicy functionality that never quite saw the light of the day. Below are numerous moddable properties that are unused by the game, most having been scrapped sometime during development. 

I chose not to make them inaccessible in modding, however, their use is discouraged as most of them likely are no longer functional and may have adverse effects (read: crashing or scripting failures). This page mainly serves as an easter egg, and a tribute to tcrf.net.

# Boosts
- `multipleCombats`: flag, allows you to deploy multiple fleets at once, to different locations. Scrapped somewhat in the middle of the game's development as there was little reason for the player to be able to do this, and would've caused balancing headaches to the lead designer. Likely does not function properly ever since the fleet cooldown was added. The area in the bottom left of the screen would have one button per fight active, and the "minimap" would allow for switching between them, as well as buttons on the fight interface itself.

# Ships
- `isPlayerShip`: boolean, determines if the ship is an ally or an enemy. Defaults to true. All enemy ships have this at false, and it's what determines their alignment. Since you currently cannot mod in new enemies, this property is not shown on the ships page.
- `faction`: numeric, from 0 to 4. Determines which faction the ship belongs to (player, angel, insectoid, dpf or warden). Not mentioned for the same reason as above.
- `isBoss`: boolean, makes the ship a valid enemy to spawn in "boss fights" (last fight of each node, every 20 nodes in endless)
- `spawningValue`: number, how many 'spawning credits' this ship costs as an enemy. A combat scenario with a budget of 3 points could spawn a ship with a spawningValue of 0.5 6 times.
- `onDeathAbility`: string, the ability the ship casts when it dies. Can only be a `SummonSuicide`-type ability, with the ship being the one to suicide, not the summons. Used by the Swarm enemies. Not mentioned in the regular docs as its functionality was not quite versatile enough.

# Abilities
- `isPassive`: makes an ability never usable.
- `needsTarget`: boolean, if true the ability will not be usable if there's no valid target. Used by the Wolf's active ability.
- `needsMovementTarget`: boolean, if true the ability will not be usable unless the caster has an active "ability target". Used by the Wolf's active ability.