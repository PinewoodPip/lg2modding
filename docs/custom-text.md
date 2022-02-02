# Custom Text
Many modded items have fields for in-game names and descriptions; these fields use keys, which point to the actual text in files in the `Language` folder.

For now, only one language is supported (`en.xml`), thus all your strings should go there.

The format is the following:

```json
<lang>

	<lines area="myarea">
		<line key="upgrade.test_upgrade_1">Modded Upgrade</line>
        <line key="upgrade.test_upgrade_1.flavor">this really do be the customized lifestyle</line>
	</lines>

</lang>
```

The `areas` are for organization only, they have no special meaning nor should they be referenced anywhere. What matters are the `<line>` elements, each of them holding one string.

The example is used for the [upgrade](upgrades.md) in the example mod. Most items only have one text field (the name), with the description and flavour text being that same key suffixed with `.desc` and `.flavour` respectively. **Note that upgrades and food generate their descriptions automatically from their boost by default. If you include a `.desc` key for them, the string will be used instead of the boost description.**

## Ability Parameters
The descriptions for abilities support formatting the string with values from the ability itself. For example, `{cooldown}` in the text is replaced with the ability's `cooldown` property.

Supported properties:

- `{cooldown}`: `cooldown`
- `{charges}`: `charges`
- `{duration}`: `duration`
- `{statuseffectduration}`: the duration of the first status effect the ability applies.
- `{fractionhealing}`: `fractionHealing`, only for `healing`-type abilities
- `{spreadangle}`: `spreadAngle`, only for `shotgun`-type abilities
- `{bulletamount}`: `bulletAmount`, only for `shotgun`-type abilities
- `{maxSummons}`: `maxSummons`, only for `summon`-type abilities
- `{summonedship}`: the name of the summoned ship for `summon`-type abilities

For `bulletDetonation`-type abilities, you can prefix these with `boundability.` (ex. `{boundability.cooldown}`) to pull properties from the bound ability instead.