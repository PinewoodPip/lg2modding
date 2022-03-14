# Boosts
Boosts define the effects of upgrades and food items. Every upgrade and food item from the base game uses them, meaning any effects that you see in the game can be used in your own mod.

A single boost can contain multiple effects to apply; for example, the Eldritch Burger food gives production multipliers to 4 different buildings, at the same time.

The game keeps track of all your upgrade multipliers, ship stat increases, unlocks, etc. by merging all your owned boosts into one. Owning an upgrade or a food item applies its boost. In the case of food, it's applied as many times as the amount of the food you have.

There are 3 base types of boost properties:

- Numeric (double-type), which are simply **added together** to calculate the final value, and (in nearly all cases) accept negative values. These all default to 0.
- Binary/Flags (boolean-type), used for unlocking features. These can only be added, and not removed. For example, the Galaxy Map is unlocked if any owned boost sets the `galaxyMap` property to `true`.
- Other, specialized structures with parameters, such as `ResourceProductionBoost`, which gives a multiplier bonus to the production of a specific resource, optionally making it scale with some other game statistic.

## Boost properties
This section lists all properties you can include in a boost, and their in-game effect.

**Unless otherwise specified, multiplier and percentage values are fractional and additive. That means that '1.5' will equal a +150% multiplier in-game, and combined with another boost that adds '2.5', will result in a +400% multiplier.**

Note that "all production", unless otherwise specified, does not affect energy nor candy production.

### Numeric boosts

- `strangeAsteroidPotency`: increases the effects of Strange Asteroids. Each unit (1) is equivalent to upgrading a Scanner by one level. Strange Asteroid effects have a base value, and a scaled value that is multiplied by the Strange Asteroid Potency.
- `candyEffectMultiplier`: adds multiplier to the candy multiplier. Ex. a value of 0.01 will make each candy grant 2% production. Note that candy is multiplicative with all other calculations.
- `allProductionMultiplier`: adds multiplier to the production of all **non-energy** buildings. Note that there are buildings which are unaffected by production multipliers.
- `asteroidProductionMultiplier`: adds multiplier to **all** resources gained from clicking asteroids.
- `flatEnergy`: adds a flat amount of energy.
- `synergyMultiplier`: adds a multiplier for the effects of synergies. Ex. a value of `0.5` will make numeric synergies 50% stronger. Chunk quirks are unaffected.
- `candyGainMultiplier`: adds a multiplier to the amount of candy you gain upon ascending.
- `offlineProductionMultiplier`: adds a multiplier to offline production. Offline production is capped at 100%. Negative offline production does nothing.
- `baseAsteroidValue`: adds extra base metal to asteroid production.
- `keyboardStrastMultiplier`: adds a multiplier to the chance of Strange Asteroids appearing while mining with the keyboard.
- `activeProductionMultiplier`: adds a multiplier to all production while you're not idling. You're considered idle if you haven't made any input outside of moving the mouse in the last few minutes, modifiable with the `idlingMinutesThreshold` boost.
- `xpScannerScaling`: adds a multiplier to XP production for each level of the Scanner building that you have.
- `buildingCostsRefund`: refunds a percentage of the metal spent on a building (including its level upgrades) when you demolish it. Capped at 100% of the metal spent.
- `strastChanceMultiplier`: adds a multiplier to the chance of Strange Asteroids appearing.
- `baseStrastChance`: adds to the base chance of a Strange Asteroid appearing. The base chance is 1% (0.01) in the vanilla campaign (set in the [default boost](campaigns.md#default-boost)).
- `productionMultiplierPerUniqueBuilding`: adds a multiplier to all production for each unique building type currently owned.
- `allProductionPerStrast`: adds a multiplier to all production for each Strange Asteroid destroyed (total), up to a cap defined of +100%.
- `lunchboxDoublingChance`: adds a chance to gain 2x lunchboxes from a conquest.
- `allProductionPerNode`: adds a multiplier to all production for each galaxy map node conquered in the current ascension.
- `strastCooldownFlatReduction`: reduces the "cooldown" of Strange Asteroids by a flat amount of seconds. For each Strange Asteroid clicked, the chance of finding additional ones is reduced for a certain amount of seconds, with the penalty scaling down linearly as the cooldown approaches 0.
- `idleProductionMultiplier`: adds a multiplier to all production while you're idling.
- `productionOnMissedStrast`: gives X seconds of resource production whenever a Strange Asteroid despawns without having been collected.
- `allBuildingsOwnedProduction`: adds a multiplier to all production if you own every type of building. Does not exclude buildings you currently cannot obtain.
- `obstacleSpawnMultiplier`: adds a multiplier to the amount of obstacles that spawn in each chunk.
- `randomUnavailableBuildingsCount`: makes a certain amount of buildings unavailable to be built in the next ascension. Cannot affect buildings marked as "essential" (see the `essentialBuildings` boost).
- `chunkQuirkMultiplier`: adds a multiplier to the effect of quantifiable chunk quirks.
- `startingUpgrades`: causes you to start the next ascension with a number of randomly picked upgrades already unlocked, from upgrades that you owned in the previous ascension. Ascension, multi-choice, guild and league upgrades are excluded.
- `keepUpgrades`: allows you to pick a number of owned upgrades to keep for the next ascension. Multi-choice, league and guild upgrades are excluded.
- `lunchboxT1Chance`: adds a chance for Basic-tier 1 recipe foods to appear in lunchboxes.
- `lunchboxT2Chance`: adds a chance for Advanced-tier recipe foods to appear in lunchboxes.
- `lunchboxT3Chance`: adds a chance for Gourmet-tier recipe foods to appear in lunchboxes.
- `spawnBudget`: adds to the "point budget" of spawning enemies in fights. A higher budget means more enemies per fight. Stronger enemies cost more points to spawn. This also works on pre-defined encounters, by placing random enemies from the faction of the last ship to have been spawned from the encounter. Capped at +14.
- `strastEffectDurationMultiplier`: adds a multiplier to the duration of Strange Asteroid effects.
- `resourceConversion`: increases the exchange rate for converting fuel to experience at the Administrative Chamber - a feature unlocked if the player's total boost has this boost above 0. `0.5` equals +50% exchange rate.
- `defaultEnergyRequirement`: the base amount of energy required for optimal production. Ex. setting this to `10` will require the player to have 10 more energy for buildings to stay at 100% efficiency.
- `defaultEnergy`: the base amount of energy the player gets, which is unaffected by other multipliers. In the vanilla campaign, this is set to `1` in the [default boost](campaigns.md#default-boost).
- `strangeAsteroidChanceCooldown`: the pseudo-cooldown between strange asteroids appearing. After activating a strange asteroids, the chance to find the next one scales linearly from 0 to your regular chance as this cooldown ticks down. This penalty is stackable.
- `guild1Perk`: affects the strength of the Scavenger guild's perk.
- `guild2Perk`: affects the strength of the Scientist guild's perk.
- `guild3Perk`: affects the strength of the Trader guild's perk.
- `idlingMinutesThreshold`: affects the time (in minutes) inactivity requirement for the game to consider the player to be idling.
- `energyFormulaLeniency`: affects the formula for production efficiency from energy. Higher numbers cause it to switch to a harsher curve later.
- `healthpackConstant`: the multiplier for healing received from healing packs.

#### Ship/combat boosts

- `combatExperienceMultiplier`: adds multiplier for the experience gained after winning a space fight.
- `shipDamageMultiplier`: damage multiplier for all player ships.
- `shipHealingMultiplier`: multiplier for all healing received by player ships **from abilities**. Does not affect health packs.
- `shipHealthMultiplier`: multiplier for the maximum health of all player ships.
- `shipFullHpDamageMultiplier`: increases damage dealt by player ships at 100% HP.
- `shipDodgeChance`: adds a chance for incoming damage to be negated.
- `shipScenarioHealing`: heals a % of each ship's health upon winning a fight.
- `lowHpDR`: adds incoming damage reduction to ships below 25% health.
- `shipDamageBoostOnAllyDeath`: adds a multiplier to player ship damage when an allied, non-summon ship dies, until the end of the expedition.
- `shipHealthMultiplierPerUniqueShip`: adds a multiplier to ship maximum health based on the amount of unique ship types in the fleet upon starting an expedition, until the end of it.
- `shipRegularResistance`: adds a % of "regular-type" incoming damage that is resisted.
- `healthpackHealing`: adds a multiplier to the healing received from health packs.
- `randomUnavailableShipsCount`: makes a certain amount of purchasable ships unavailable to be bought in the next ascension. The starting ship cannot be affected by this.
- `healthpackIntervalMultiplier`: adds a multiplier to the cooldown between health packs spawning.
- `galaxyMapInfluence`: adds a flat amount of "influence" to the current galaxy map. Influence is normally gained after each conquered node, and is used to scale enemy level.
- `fleetCooldown`: increases the cooldown for deploying ships.
- `fleetSize`: increases the amount of ships you can deploy in a fleet. Does not support negative values!

#### Discounts

Discount boosts are additive with each other and a flat %, with the exception of the building discount, which follows a diminishing returns formula.

- `differentGuildDiscount`: adds a discount to guild-exclusive upgrades, if the upgrade's associated guild is different from the one you were in the previous ascension.
- `previousUpgradesDiscount`: adds a discount to upgrades that have been bought in previous ascensions.
- `buildingCostsReduction`: adds a `(buildingCostsReduction / (buildingCostsReduction + 1))` discount to the price of building buildings.

### Flags
- `idleStrastBoost`: increases the chance of finding Strange Asteroids, if you haven't collected one in over 15 minutes. Scales over the spawn of 20 minutes, up to a 2.5x chance multiplier.
- `keyboardClicking`: allows you to collect asteroids on-screen by jamming on your keyboard. Applies a penalty to Strange Asteroid chance while in use (see the `keyboardStrastMultiplier` boost).
- `cookingTier1`: allows you to cook Basic-tier recipes.
- `cookingTier2`: allows you to cook Advanced-tier recipes.
- `cookingTier3`: allows you to cook Gourmet-tier recipes.
- `synergiesTier1`: enables Basic-tier synergies.
- `synergiesTier2`: enables Advanced-tier synergies.
- `synergiesTier3`: enables Legendary-tier synergies.
- `flurryClicking`: allows you to click to fire additional bullets when using Flurry-type abilities.
- `ascension`: enables the Ascension button.
- `chunkQuirks`: enables chunk quirks.
- `galaxyMap`: enables the Galaxy map button, and deploying fleets.
- `combatAbilities`: enables combat abilities for your ships.
- `combatExperienceScaling`: multiplies XP gained from combat based on your achievement completion. Having X% of all achievements unlocked equals an X% increase in XP gained.
- `lunchboxes`: enables getting lunchboxes from conquests.
- `endlessCombat`: enables fighting in the space wilderness.
- `showLunchboxHint`: does nothing. Used by lunchboxes to display a "Click to open" hint.
- `headstart`: causes the closest connected node to the galaxy map's starting point to start nearly-fully conquered (with only one fight remaining).
- `strastLunchbox`: causes you to gain a lunchbox when you activate Strange Asteroids while already under the effect of another.
- `buyAllUpgrades`: enables the "buy all upgrades from this tier" button in the upgrades menu.
- `multiSelect`: enables multi-selecting buildings with shift+click.
- `multiCasting`: allows you to have all ships of one type fire their abilities at once by shift+clicking the ability.
- `loadouts`: enables saving and buying fleet loadouts.
- `galaxyMapQueue`: enables you to queue up locations to conquer on the galaxy map by right clicking nodes. If the queue is not empty and you have a loadout save when you lose, you will automatically try to deploy a new fleet of that loadout once the deployment cooldown runs out.
- `autoHealthpacks`: enables automatically collecting health packs, right before they would normally despawn.

### Other fields
The following boosts use more complex structures; you need to be careful to follow their format. You do not need to include all the sub-properties they have. Unmentioned ones will be set to a default value (almost always 0/false).

Most of these are lists, meaning you can stack multiple instances of their effect onto a single boost. This is useful in case you want to, for example, create an upgrade that increases both metal and experience production, by different amounts.

#### resourceProductionBoosts
A list of boosts which modify the production of a specific resource.

Example: increases experience production by 100%, +1% per achievement unlocked, +5% per synergy active, +5% per building owned, +2% per food cooked, and +1% for each click in the last minute.
```json
"resourceProductionBoosts": [
		{
			"resourceId": 1,
			"multiplier": 1,
			"multiplierPerAchievement": 0.01,
			"multiplierPerSynergy": 0.05,
			"multiplierPerBuilding": 0.05,
			"multiplierPerFoodCookedTotal": 0.02,
			"multiplierPerClick": 0.01
		}
	],
```

Properties:

- `resourceId`: number, the ID of the resource to apply the effects to. See [resources enumeration](enums.md#resources)
- `multiplier`: number, an unconditional multiplier for the resource's production.
- `multiplierPerAchievement`: number, adds a multiplier to the resource's production for each achievement level owned.
- `multiplierPerSynergy`: number, adds a multiplier for each synergy active.
- `multiplierPerBuildings`: number, adds a multiplier for each building owned.
- `multiplierPerFoodCooked`: number, adds a multiplier for each food item cooked in the current Ascension.
- `multiplierPerFoodCookedTotal`: number, adds a multiplier for each food item cooked across all Ascensions.
- `multiplierPerClick`: number, adds a multiplier for each asteroid click in the last minute.

#### multiplicativeResourceProductionBoosts
Similar to a `ResourceProductionBoost`, but increases production multiplicatively instead of adding to an existing multiplier.

Example:

Doubles metal production and halves experience production.
```json
"multiplicativeResourceProductionBoosts": [
		{"resource": 0, "multiplicativeBoost": 2},
        {"resource": 1, "multiplicativeBoost": 0.5},
	],
```

Properties:

- `resourceId`: number, the ID of the resource to apply the effects to. See [resources enumeration](enums.md#resources)
- `multiplicativeBoost`: number, the multiplier. Ex. '2' equals 2x.

#### multiplicativeAllProductionBoosts
Similar to `multiplicativeResourceProductionBoosts`, but affects "all production". That is, all resource production except candy and energy.

Example:

Halves all resource production.
```json
"multiplicativeAllProductionBoosts": [
		{"multiplicativeBoost": 0.5}
	],
```

Properties:

- `multiplicativeBoost`: number, the multiplier. '2' equals 2x.

#### buildingProductionBoosts
A list of boosts to specific buildings.

Example:

Increases Metal Mine's base production by 1 metal, reduces energy consumption by 50% and multiplies their overall production by 2x.
```json
"buildingProductionBoosts": [
		{
			"buildingId": "metal_mine",
			"baseProduction": 1.0,
			"multiplier": 0.0,
			"energyConsumptionMutliplier": -0.5,
			"multiplicativeBoost": 2.0
		}
	],
```

Properties:

- `buildingId`: string, the ID of the building to apply the effects to. Leave as "" to affect all buildings. See [building types](enums.md#buildings).
- `affectAll`: boolean, same effect as setting `buildingId` to an empty string.
- `baseProduction`: number, increases the base resource production of the building by a flat amount.
- `multiplier`: number, adds to the multiplier of the building's production.
- `energyConsumptionMultiplier`: number, adds to the multiplier for the building's energy consumption. Ex. 0.5 makes the build use up 50% more energy.
- `extraBuildingLimit`: number, increases the building's building placement limit, if it has one set.

#### shipBoosts
A list of boosts to specific player ships.

Example:

Gives the Wasp 100% more health (additive, as is the case with all boosts unless otherwise specified) and makes its active ability shoot 2 more bullets.

```json
"shipBoosts": [
		{
			"shipId": "wasp",
			"healthMultiplier": 1.0,
			"abilityShotgunBullets": 2
		}
	],
```

Properties:

- `shipId`: string, the ID of the ship this effect applies to. See [ship types](enums.md#ships). Needs to be prefixed with your mod ID and an underscore to reference your custom ships.
- `affectAllShips`: boolean, if true, this set of boosts will apply to all ships.
- `healthMultiplier`: number, adds to the multiplier of the ship's maximum health.
- `damageMultiplier`: number, adds to the multiplier of the ship's damage.
- `abilityShotgunBullets`: integer, adds an amount of extra bullets fired for Shotgun-type abilities.
- `abilityExplosionRadiusBoost`: number, increases the radius of AoE attacks.
- `abilityShotgunAngle`: number, increases the firing angle of Shotgun-type abilities.
- `accurate`: boolean, if true, the ship will never fail accuracy checks*.
- `healingDoT`: number, heals the ship by a percentage of its health every 5 seconds.
- `critChance`: number, adds a chance to deal critical hits with attacks. Critical hits get a multiplier applied to them, 3x by default.
- `fleetUniqueHealthMultiplier`: number, adds to the ship's health multiplier for each unique ship type in the fleet at the start of an expedition.
- `fleetUniqueDamageMultiplier`: number, adds to the ship's damage multiplier for each unique ship type in the fleet at the start of an expedition.
- `dodgeAtFullHealth`: number, adds dodge chance when the ship is at full health. Dodging an attack completely negates its damage and any other effects of the hit.
- `cooldownPercentageReduction`: number, reduces the cooldown of **active** abilities by a percentage.
- `volatileDamageForQuickFight`: number, adds to the ship's damage multiplier if the previous fight was completed in less than 10 seconds. Does not stack, and is removed after a battle that did not meet the criteria.
- `comebackChance`: number, adds a chance for the ship to be healed to full health instead of dying, once per expedition.
- `healingOnAbility`: number, heals ships that use their active ability for a fraction of their maximum health.
- `damageMultiplierPerEnemy`: number, adds to the ship's damage multiplier for each enemy present at the start of a fight.

*Abilities that are marked as "homing" have a chance to not home into the target and instead deviate by a few degrees. This chance is determined by the speed of the attacker and the target. Slower ships have a lesser chance to fire homing projectiles onto faster ships.

### shipMultiplicativeHealthBoosts and shipMultiplicativeDamageBoosts
Multiplies a ship's maximum health and damage respectively.

Example: doubles health of all player ships, and halves the damage of wasps.
```json
	"shipMultiplicativeHealthBoosts": [{"shipId": "", "multiplicativeBoost": 2}],
	"shipMultiplicativeDamageBoosts": [{"shipId": "wasp", "multiplicativeBoost": 0.5}],
```

Properties:

- `shipId`: string, the ID of the ship to affect. Needs to be prefixed with your mod ID and an underscore to reference your custom ships. If empty, will affect all ships.
- `multiplicativeBoost`: number, the multiplier.

#### buildingUnlocks
A list of buildings that the boost unlocks for construction. See [building types](enums.md#buildings).

Example:

Unlocks the Metal Mine and Academy buildings.
```json
    "buildingUnlocks": ["metal_mine", "academy"],
```

#### shipUnlocks
A list of ships that the boost unlocks for the player. See [ship types](enums.md#ships). Remember that your own ships must be prefixed with your mod ID and an underscore!

Example:

Unlocks the Tortoise and a custom ship.
```json
    "shipUnlocks": ["porcupine", "pip_example_mod_whale"],
```

#### strastEffects
A list of Strange Asteroid effects that the boost unlocks. See [strast types](enums.md#strange-asteroid-types).

Example: unlocks the Gambler's asteroid (the one that randomizes production for X seconds)
```json
    "strastEffects": ["randomized_production"],
```

#### completeSynergyTierBoosts

Adds to the all production multiplier when all synergies of a specified tier are active. See [synergy tier IDs](enums.md#synergy-tiers).

Example: adds 100% all production if all basic synergies are active, and +200% if all advanced synergies are active.
```json
"completeSynergyTierBoosts": [
		{"tier": 1, "multiplier": 1},
		{"tier": 2, "multiplier": 2}
	],
```

Properties:
- `tier`: number, the synergy tier to require. See [synergy tier IDs](enums.md#synergy-tiers).
- `multiplier`: number, adds to the all production multiplier if all synergies from the tier are active.

#### playtimeProductionBoosts
Adds to the all production multiplier, based on how much time has elapsed since you started your playthrough.

Example: adds +1% fuel production for each minute since you started playing, up to +300%.
```json
"playtimeProductionBoosts": [
		{
			"resource": 4,
			"increment": 0.01,
			"interval": 60,
			"maximum": 3
		}
	],
```

#### synergyBoosts
Makes a specific synergy stronger.

Example: makes Tunnel System synergies 100% more powerful.
```json
"synergyBoosts": [
		{
			"id": 0,
			"multiplier": 1
		}
	],
```

Properties:

- `id`: number, the ID of the synergy to affect. See [synergy IDs](enums.md#synergies).
- `multiplier`: number, adds to the multiplier of the synergy's effect.

#### guildBoosts
Adds a multiplier to all production for each time you join a specific guild.

Example: adds +150% all production for each time you join the Scavenger guild.
```json
"guildBoosts": [
		{
			"id": 0,
			"multiplierPerJoin": 1.5
		}
	],
```

Properties:
- `id`: number, the ID of the guild to use for the effect. See [guild IDs](enums.md#guilds).
- `multiplierPerJoin`: number, adds to the all production multiplier for each time you joined the guild.

#### leagueBoosts
Similar to a `GuildBoost`, but for leagues! Wow!

Example: adds +50% to all production for each time you've joined the Schemist league.
```json
"leagueBoosts": [
		{
			"id": 1,
			"multiplierPerJoin": 0.5
		}
	],
```

Properties:
- `id`: number, the ID of the league to use for the effect. See [league IDs](enums.md#leagues).
- `multiplierPerJoin`: number, adds to the all production multiplier for each time you joined the league.

#### strastBoosts
Makes a specific Strange Asteroid effect stronger.

Example: makes the Gambler's asteroid 100% stronger.
```json
"strastBoosts": [
		{
			"stringId": "randomized_production",
			"multiplier": 1
		}
	],
```

Properties:
- `stringId`: string, the ID of the Strange Asteroid effect to affect. See [Strange Asteroid effect IDs](enums.md#strange-asteroid-effects).
- `multiplier`: number, adds to the multiplier of the effect's strength. This is a separate multiplier from the scaling gained from Scanner levels.

#### synergyScalingExclusions
A list of Synergies to exclude from scaling with any boosts that increase their strength. This affects all boosts, not just the one this is included in. Chunk quirks are unaffected. See [synergy IDs](enums.md#synergies).

Example: makes Unlucky Luck, Spectroscopy and Fractal Matter unable to gain bonuses from boosts that would scale them.
```json
    "synergyScalingExclusions" = [17, 9, 22],
```

#### clickingExtraResourceBoosts
Increases the resources you gain from clicking asteroids by a percentage of your production per second.

Example: makes asteroids give +1% of your Metal production, per Metal Mine built.
```json
    "clickingExtraResourceBoosts": [
		{
			"id": 0,
			"multiplier": 0.01,
			"buildingAmountScaling": "metal_mine"
		}
	],
```

#### essentialBuildings
A list of buildings that cannot be made unavailable by the `randomUnavailableBuildingsCount` boost.

Example: the vanilla list of essential buildings.
```json
    "essentialBuildings": ["metal_mine", "academy", "pumpjack", "research_lab", "scanner", "solar_panel"],
```

#### delayedCandyBoosts
Adds to the multiplier of candy gained upon ascending, for each real-life day elapsed since your last ascension.

Example: increases candy gained from ascending by +100% for each day elapsed, up to +200%.
```json
	"delayedCandyBoosts": [
		{
			"multiplier": 1,
			"daysCap": 2
		}
	],
```

Properties:
- `multiplier`: number, the multiplier added for each day elapsed.
- `daysCap`: number, the maxmimum amount of days this effect stacks for.

#### previousGuildBoosts
Adds to the all production multiplier if your previous guild was the one specified.

Example: increases all production by 50% if your previous guild was the Scientist guild.
```json
	"previousGuildBoosts": [
		{"id": 1, "multiplier": 0.5}
	],
```

Properties:
- `id`: number, the ID of the guild to require. See [guild IDs](enums.md#guilds).
- `multiplier`: number, adds to the all production multiplier if your previous guild was the one specified in this effect.

#### overflowedEnergyProductionBoosts
Adds to the all production multiplier, scaling with the amount of excess energy that you have (energy over your required amount for optimal building production).

Example: adds +1% to all production for each 1 energy over your optimum amount, up to +100%.
```json
"overflowedEnergyProductionBoosts": [
		{
			"multiplier": 0.01,
			"additiveCap": 1
		}
	],
```

Properties:
- `multiplier`: number, adds to the all production multiplier for each point of excess energy.
- `additiveCap`: number, the cap to the multiplier you can get from this effect.

#### upgradeUnlocks
A list of upgrades to unlock upon the boost being first applied, or upon ascending. Only works as a boost for upgrades, not food items. Used in the vanilla game for the ascension upgrades that make you start with buildings already unlocked, by unlocking their upgrades (so as to hide them from the upgrades screen).

**To reference your own upgrades, you must prefix them with your mod ID and an underscore.**

Example: unlocks the upgrade that allows building academies.
```json
	"upgradeUnlocks": ["academy_unlock"],
```

