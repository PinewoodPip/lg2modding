# Ships
Custom ships go in the `Ships` folder.

## Example
A tanky, slow-moving ship with 2 automatic abilities.

```json
{
	"stringId": "testship",
	"nameKey": "ship.example",
	"speed": 30,
	"baseDmg": 2,
	"baseHp": 80,
	"dmgGrowth": 1,
	"hpGrowth": 20,
	"baseCost": 8000,
	"costMultiplier": 1.03,
	"baseUpgradeCost": 4000,
	"upgradeCostMultiplier": 1.03,
	"shopIndex": 1,
	"deathSound": 19,
	"sprite": "ship_1.png",
	"automaticAbilities": [
		"summon_ability",
		"spiral_ability"
	]
}
```

## Properties
As with all modded content, the `stringId` field is essential.

- `nameKey`: string, the [text key](custom-text.md) to use for the name of the ship. The description uses this same key suffixed with `.desc`. 
- `purchasable`: boolean, determines if the ship appears in the fleet menu and can be bought. Defaults to true.
- `speed`: number, the movement speed of the ship. The Wasp's speed is 180. Defaults to 50.
- `orbitRadius`: number, determines how far away from the center of the "combat ring" the ship orbits. The Wasp has this set to 120. Default is 100.
- `size`: number, determines how many particles to spawn when this ship is destroyed. Defaults to 1.
    - `0`: Small, 2 particles
    - `1`: Medium, 3 particles
    - `2`: Large, 6 particles
- `baseDmg`: number, the base damage this ship deals. Defaults to 3 (Wasp's value).
- `baseHp`: number, the base HP of the ship. Defaults to 40 (Wasp's value).
- `automaticAbilities`: list of string IDs of the abilities the ship will automatically use. Use to define the automatic attack(s).
- `activeAbility`: string, the ID of the active ability of the ship - the one used when the player clicks on the ship.
- `shopIndex`: number, determines the position of the ship in the fleet shop menu. Lower indexes get placed higher.
- `hpGrowth`: number, the amount of HP the ship gains with each level after the first one.
- `dmgGrowth`: number, the amount of extra damage the ship gains with each level after the first one.
- `turningSpeed`: number, the ship's turning speed in degrees/s while the ship is not moving on the "combat ring". Used by the Wolf.
- `baseCost`: number, the base metal cost to buy the ship.
- `costMultiplier`: number, multiplies base cost for every level after 1. The formula therefore being `baseCost * costMultiplier^(level - 1)`
- `baseUpgradeCost`: number, the base cost of upgrading the ship.
- `upgradeCostMultiplier`: number, multiplies the base upgrade cost for every level after 1. The formula is `baseUpgradeCost * (upgradeCostMultiplier^(level + 1) / (upgradeCostMultiplier - 1));`
- `sprite`: string, the [sprite](sprites.md) filename for the ship.
- `deathSound`: number, sound to play upon the ship's death. See [sounds enumeration](enums.md#sounds).
    