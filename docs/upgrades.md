# Upgrades
Upgrades are defined in the `Upgrades` folder. An upgrade only defines the name, price, tiering and other metadata; the actual effects that it grants to the player are defined through a [boost](boosts.md).

## Example
This example is a tier 2 upgrade that costs 5k metal and 200 Experience.

```json
{
	"referenceName":"Panel upgrade 2",
	"mutualExclusivityGroup": "",
	"boostId": "test_upgrade_boost",
	"stringId":"test_upgrade",
	"name": "upgrade.test_upgrade_1",
	"isAscensionUpgrade": false,
	"important": true,
	"sprite": "test_sprite.png",
	"tier": 2,
	"costs": {
		"metal": 5000,
        "experience": 200,
	},
}
```

## Properties
Like with all modded content, the `stringId` field is mandatory. Additionally, for them to do anything for the player, you must include a `boostId` property, with the ID of the [boost](boosts.md) to grant.

The resource cost of the upgrade is defined through the `costs` property, with a special structure:

```json
"costs": {
		"metal": 5000,
        "experience": 200
	},
```

The following are the IDs of the resources to use for `costs`:
- `"metal"`
- `"experience"`
- `"candy"` (only works for Ascension upgrades)
- `"energy"` (not deducted; if used, the upgrade will be unpurchasable unless you have excess energy equal or greater than the 'cost')
- `"fuel"`

Other properties:
- `name`: string, the [text key](custom-text.md) to use for the name of the upgrade. The description and flavour text use this same key suffixed with `.desc` and `.flavour` respectively. Note that by default, the description of an upgrade is automatically generated from its boost. If you provide your own description, it will be used instead. You can use this to reword boosts with ugly/verbose descriptions.
- `displayIndex`: number, higher amounts cause the upgrade to be displayed further on the end of each tier in the upgrades menu.
- `tier`: number, the upgrade's tier, as shown in the upgrades menu. Upgrades with a negative tier are hidden from the upgrades menu, but still obtainable through other means (such as conquest).
- `important`: boolean, if true, the upgrade will flash red in the upgrades menu, and always have a `<!>` over it, and will show that same badge over the upgrades menu button on the sidebar until it is bought. It will also go into a special tier in the upgrades menu.
- `guildRestriction`: number, restricts this upgrade to players of a specific guild. Values:
    - `-1`: default, no guild restriction.
    - `0`: Scavenger guild
    - `1`: Scientist guild
    - `2`: Trader guild
- `mutualExclusivityGroup`: string. Upgrades with the same `mutualExclusivityGroup` cannot be bought together. Once one is bought, the others become hidden from the upgrades menu (but may still be obtained through other means).
- `sprite`: string, the [sprite](sprites.md) filename.