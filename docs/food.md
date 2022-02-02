# Food
Food items are created in the `Food` folder.

## Example
A food item with a ridiculously high probability of appearing in lunchboxes.
```json
{
	"stringId": "test_food",
	"boostId": "test_upgrade_boost",
	"localizationString": "test_food",
	"lunchboxWeight": 10000
}
```

## Properties
Like with all other content, food items must have, at the very least, a `stringId` property with a unique internal name for the food.

The `boostId` field should be the ID of the [boost](boosts.md) the food will grant. For foods, the boost is awarded as many times as the amount of the food that the player owns, meaning they are stackable.

Other properties:

- `sprite`: string, filename (without extension) of the icon to use for the food, pulled from the `Sprites` folder.
- `localizationString`: string, the [text key](custom-text.md) for the item's name, pulled from the `Language` folder. The description and flavour text will use this key as well, but suffixed with `.desc` and `.flavour` respectively.
- `lunchboxWeight`: number, the weighted chance of this food appearing in lunchboxes. Use `0` to prevent it from ever appearing. For vanilla foods, this value is on average `20`.
- `isBasicIngredient`: boolean, used for the achievement that requires you to obtain all basic ingredients.
- `isLunchbox`: boolean, if true, the food will have the following properties:
    - Owning any amount of it will show a <!> sticker on the cooking menu button
    - The item will not be usable in cooking
    - When clicked, the item will be consumed and the lunchbox interface will appear
    - The item will be awarded from conquests that reward lunchboxes (the game picks one lunchbox-type food at random to give out each conquest)