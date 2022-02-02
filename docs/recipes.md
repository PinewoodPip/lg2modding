# Recipes
Custom cooking recipes go in the `Recipes` folder.

## Example
This advanced-tier recipe creates the vanilla meat item, with 2 meats and 1 egg, defying the laws of conservation of energy.

```json
{
	"stringId": "test_food",
	"resultId": "meat",
	"ingredients": ["meat", "egg", "meat"],
	"tier": 1
}
```

## Properties
As with all modded content, the `stringId` field is essential.

Additionally, your recipe must have a `resultId`, the string ID of the food item it creates. You may use IDs for food items from the base game; see the [vanilla IDs](#vanilla-ids) section for them.

You must also provide a list of the string IDs of the 3 `ingredients` that the recipe will use. You cannot make recipes that use fewer or more ingredients.

Other properties:

- `cookingTime`: number, the seconds it takes to cook the recipe.
- `tier`: number, the tier of the recipe. Recipes can only be cooked if the player owns a [boost](boosts.md) that unlocks the respective tier.
    - `0`: basic
    - `1`: advanced
    - `2`: gourmet
    - `3`: hidden; always cookable, but does not appear in the cooking book

## Vanilla IDs
Basic: `milk, fruit, butter, egg, flour, meat, sugar, water`

From basic recipes: `pasta, dough, lemonade, ice_cream, cheese, omelette, soup, chocolate, marshmallows, crepes`

From advanced recipes: `bread, milkshake, cake, cookies, cheese_soup, ramen, ice_crepes, pizza, brownies, casserole`

From gourmet recipes: `ice_cream_sandvich, dessert, burger`

Others: `lunchbox, smores, fruit_pizza`