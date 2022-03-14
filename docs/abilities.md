# Abilities
Abilities refer both to the active abilities of ships, as well as their automatic weapons. They are defined in the `Abilities` folder.

Aside from the mandatory `stringId` field, abilities must also define an `archetype`. The archetype defines the behaviour of the ability, each of them having additional properties specific to them.

The words "user ship" and "caster" here refer to the ship using the ability.

## Common properties
These properties can be set on any ability.

- `icon`: string, the [sprite](sprites.md) filename for the ability icon.
- `abilityNameTranslationKey`: string, the [text key](custom-text.md) for the ability's name. Shown when you hover over a ship in the fleet menu that has this ability as an active.
- `abilityDescriptionTranslationKey` string, the [text key](custom-text.md) for the ability's description. Shown when you hover over a ship in the fleet menu that has this ability as an active. Supports parameters, see the [text docs](custom-text.md#ability-parameters).
- `target`: number, determines who this ability is *aimed* at.
    - `-1`: None; the projectile will be fired straight towards where the ship is pointing.
    - `0`: Enemies of the caster (the ability's user)
    - `1`: Allies of the caster
    - `2`: Same as -1, but allows the projectile to hit the ship that created it, as well as allies (useful for healing abilities)
- `charges`: number, the maximum amount of charges the ability can store. An ability can be used so long as it has charges remaining. Defaults to `1`.
- `cooldown`: number, the time between the ability's charges being restored. Defaults to `0.2`.
- `firingDelay`: number, a minimum delay between charges of the ability being usable.
- `onlyReloadAtNoCharges`: boolean. If `false`, 1 charge of the ability will be replenished every `cooldown` seconds. If `true`, all charges will be replenished after `cooldown` seconds once charges reach 0. Use `true` to create weapons that reload their whole clip at once. Defaults to `true`.
- `canBeAutoFired`: boolean, determines if the ship can use this ability automatically. Use `false` for active abilities.
- `manuallyAimed`: boolean, determines if the ability should be aimed with the player's cursor.
- `duration`: number, the duration of the ability. If >0, the ability is considered a durative ability; by default, no other abilities can be used alongside a durative ability until its duration ends.
- `ignoreShipBusyState`: boolean, if true, the ability will be usable even while the ship is using a durative ability.
- `hitAllies`: boolean, if true, the ability will be able to hit allies of the caster.
- `hitSelf`: boolean, if true, the ability will be able to hit the caster.
- `setAimingCursor`: boolean, if true, the cursor will be set to a crosshair when using the ability, if it is a durative one.
- `useSound`: number, the sound to play when the ability is used. See [sounds enumeration](enums.md#sounds).
- `statusesApplied`: list of status effects to apply to the target, with the following structure:
```
    "statusesApplied": [
        {
            "id": 1,
            "duration": 5
        }
    ],
```

Where `id` is the ID of the status effect, and `duration` is the duration in seconds. Available status effects are:

- `0`: "Guardian Angel"; multiplies damage taken by `0.6`, and redirects that portion to the ship that applied the status as unresistable damage. Used by the Tortoise.
- `1`: Disarm; prevents the ship from using any abilities.
- `2`: Shielded; multiplies damage taken by `0.25`.
- `3`: Reflect; causes most projectiles that were to hit the ship to be reflected back to their caster. Reflected projectiles are always homing.

## Archetypes
The `archetype` field of an ability defines its behaviour. The available archetypes are the following:

### projectile

Projectile abilities create projectiles that move across the screen, and land hits upon colliding with a valid target. Multiple other archetypes are based on it, inheriting its properties:

- `dmgMultiplier`: number, the multiplier for the ability's damage. Ex. `1.5` will deal 150% of the ship's damage.
- `damageType`: number, the type of damage the ability deals. See [damage type enumeration](enums.md#damage-types).
- `homingByDefault`: boolean, if true, the projectile will home into its target, unless it missed*. Defaults to `true`.
- `travelSpeed`: number, the speed of the projectile. Default is `100`.
- `unmissable`: boolean, if true, the ability will not miss if it's also set to be homing.
- `projectileRendererScale`: number, a multiplier for the scale of the projectile. Defaults to `1`.
- `piercing`: boolean, if true, the projectile will not be deleted upon landing a hit and will instead turn into a non-homing projectile (if it was homing) and continue travelling in a straight line, possibly hitting additional targets.
- `hitCooldown`: number, the duration (in seconds) that must pass before a ship can be hit again by the same projectile. Used for piercing projectiles. Defaults to `0.2`.
- `lifetime`: number, the duration (in seconds) that this projectile can exist for before disappearing. Defaults to `10`.
- `explodeAtCursor`: boolean, if true, the projectile will pass through any targets and only explode at the position the cursor was on when it was cast. Only intended to be used for active player abilities.
- `firingAngle`: number, offsets the aiming direction of the projectile, in degrees. Normally projectiles are fired towards their target; this property lets you add a degree offset.
- `impactSound`: number, the sound the projectile will make upon landing a hit. See [sounds enumeration](enums.md#sounds).
- `projectileSpriteOverride`: string, the [sprite](sprites.md) filename for the projectile.

*Abilities that are marked as "homing" have a chance to not home into the target and instead deviate by a few degrees. This chance is determined by the speed of the attacker and the target. Slower ships have a lesser chance to fire homing projectiles onto faster ships.

### shotgun
Shotgun abilities fire multiple projectiles at once. They inherit properties from the `projectile` archetype.

Specific properties:

- `bulletAmount`: number, amount of projectiles to fire.
- `spreadAngle`: number, the random deviation, in degrees, for each projectile fired. Ex. `180` means the projectiles can deviate 90 degrees in either direction from where the ability is aimed.

### summon
Summon-type abilities summon a ship when used. Summons are temporary ships that do not return to your fleet after finishing an expedition. Used by the Queen ship.

Specific properites:

- `summonedShip`: string, the ID of the ship to summon. See [ship types](enums.md#ships). To use your custom ships, you must prefix their ID with your mod ID and an underscore.
- `summonRadius`: number, the radius (centered on caster) within which the ship is summoned.
- `maxSummons`: number, the ability will do nothing if the caster already has this amount of summons, or more, regardless of what ability they came from.

### spiral
Spiral-type abilities fire bullets around the caster, with each shot being offset by a few degrees from the last one. Used by some enemies (like angels) in the base game. **Inherits properties from the `projectile` archetype, but cannot home into enemies.**

Specific properties:

- `shotsPerLoop`: number, the amount of bullets fired per 'cycle'. Ex. if this is `4`, each bullet would be fired 90 degrees away from the last one.

### bulletDetonation
BulletDetonation-type abilities remove all of the ship's current bullets on the field, then cast an ability from their place. Used by the Porcupine ship for its shrapnel ability.

Specific properites:

- `boundAbility`: string, the ID of the ability to cast. *Does not need to be prefixed with your mod ID.*

### summonSuicide
Orders the user ship's summons to crash into enemy ships, destroying themselves in the process. Used by the Queen ship's active ability.

Specific properites:

- `summonSuicideAmount`: number, the maximum amount of summons to suicide at once.
- `damageMultiplier`: number, a multiplier to the damage dealt by the ships suiciding. The damage dealt by ships suiciding is equal to their maxmimum health.

### explosive
Causes an Area-of-Effect hit. **Inherits properties from the `projectile` archetype.**

Specific properites:

- `areaRadius`: number, the radius of the explosion. 100 by default.
- `explodeOnSelf`: boolean, if true, the explosion will be centered on the caster, and will not create a projectile (it will explode almost instantly).

### healing
Similar to `explosive`, but can deal percentage-based healing. Used by the Plover's active ability. **Inherits properties from the `explosive` archetype.**

Specific properites:

- `fractionHealing`: number, the fraction of the user ship's maximum HP that the ability will heal for.

### flurry
Flurry abilities cause the user ship to fire an additional ability while they're active (during their `duration`, which must be > 0 for this ability type to work). Used by the Gecko's active ability for its "manual firing mode".

Properties:

- `boundAbility`: string, the ID of the ability to use while the flurry is active. Must be a `projectile`-type ability, or one that inherits properties from it. This ability must have `ignoreShipBusyState` set to `true`, otherwise it will not fire. It must also have `canAutoFire` set to `false`.
- `clickingAbility`: string, the ID of the ability to use instead of `boundAbility` while the player is manually clicking on the battlefield. This requires the player to have the `flurryClicking` boost. While being used, the cooldown for `boundAbility` is repeatedly set to `0.25` so they cannot be used at the same time.
- `requiresClicking`: boolean, if true, the `boundAbility` will not be used, only the `clickingAbility` (which requires the player to click).
- `maxClicksPerSecond`: number, the maximum clicks per second that the `clickingAbility` admits. Set to negative to disable this limit.

**You do not need to prefix the ability IDs with your mod's ID.**

### sentry
Sentry abilities fire a projectile (the "sentry") that, until it expires, continuously casts another skill from its place, using the stats of the ship that started the ability. It is used by the Salamander's active ability and inherits properties from the `projectile` archetype. It is recommended to use these with `manuallyAimed`, `explodeAtCursor` set to `true` and `target` set to `-1`, so the sentry 'lands' where your cursor points.

Properties:

- `sentryAbility`: string, the ID of the ability to fire from the sentry's position. Should *not* be prefixed with your mod's ID.
- `onlyFireAfterArrival`: boolean, defaults to true; if false, the sentry will be able to use its ability before "settling in"