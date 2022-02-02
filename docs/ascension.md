# Ascension
The Ascension tree can be modified for each campaign by creating a file in the campaign folder named the same way as the campaign file, with the `.ascensiontree` extension.

The file is in the `json` format, with the following structure, with 2 top-level properties: `nodes` and `offset`.

`nodes` is dictionary containing the upgrades in the tree, with the following format:

```json
"ascension_discounts_guilds": {
    "coords": [-357, 93],
    "parents": ["ascension_discounts_upgrades"]
},
```

The key is the upgrade ID. Must be prefixed with your mod's ID and an underscore if using your own upgrades.

`coords` are the coordinates of the upgrade in the menu.

`parents` is a list of upgrades that must be bought before this one can be bought. It defines the connections in the tree, and can be empty.

------

`offset` is a dictionary with the following format. The coordinates here are used to offset the whole tree. It's optional, but useful for centering the tree onto the screen.

```json
"offset": {
    "x": -70,
    "y": 0
}
```

## Example
The following example is the Ascension tree of the vanilla campaign; useful as a starting point, or to reference coordinate positions.

```json
{
    "nodes": {
        "ascension_core": {
            "coords": [57, -401],
            "parents": []
        },

        "overtime": {
            "coords": [-143, -284],
            "parents": ["ascension_core"]
        },
        "ascension_discounts_upgrades": {
            "coords": [-240, -78],
            "parents": ["overtime"]
        },
        "ascension_discounts_guilds": {
            "coords": [-357, 93],
            "parents": ["ascension_discounts_upgrades"]
        },
        "ascension_offline_2": {
            "coords": [-387, -240],
            "parents": ["overtime"]
        },
        "ascension_offline_3": {
            "coords": [-493, -55],
            "parents": ["ascension_offline_2"]
        },
        "ascension_offline_4": {
            "coords": [-508, 133],
            "parents": ["ascension_offline_3"]
        },
        "ascension_offline_5": {
            "coords": [-511, 346],
            "parents": ["ascension_offline_4"]
        },
        "ascension_bulk_research": {
            "coords": [-178, 128],
            "parents": ["ascension_discounts_upgrades"]
        },
        "ascension_bulk_select": {
            "coords": [-325, 283],
            "parents": ["ascension_bulk_research"]
        },

        "ascension_basebuilding_replicators": {
            "coords": [8, -151],
            "parents": ["ascension_core"]
        },
        "ascension_basebuilding_synergies_tier2": {
            "coords": [-10, 67.00005],
            "parents": ["ascension_basebuilding_replicators"]
        },
        "ascension_basebuilding_synergies_tier3": {
            "coords": [-46, 246],
            "parents": ["ascension_basebuilding_synergies_tier2"]
        },

        "ascension_clicking_base_asteroid_value": {
            "coords": [191, -184],
            "parents": ["ascension_core"]
        },
        "ascension_candy_effect": {
            "coords": [236, -21],
            "parents": ["ascension_clicking_base_asteroid_value"]
        },
        "ascension_clicking_keyboard": {
            "coords": [252, 149],
            "parents": ["ascension_candy_effect"]
        },
        "ascension_clicking_keyboard_strast": {
            "coords": [312, 303],
            "parents": ["ascension_clicking_keyboard"]
        },

        "ascension_lunchboxes": {
            "coords": [300, -341.6],
            "parents": ["ascension_core"]
        },
        "ascension_combat_cooking_t1": {
            "coords": [400, -170.6],
            "parents": ["ascension_lunchboxes"]
        },
        "ascension_headstart": {
            "coords": [637, -140],
            "parents": ["ascension_combat_cooking_t1"]
        },
        "ascension_combat_cooking_t2": {
            "coords": [482.7, -15.6],
            "parents": ["ascension_combat_cooking_t1"]
        },
        "ascension_fleet_cooldown": {
            "coords": [375, 100],
            "parents": ["ascension_combat_cooking_t2"]
        },
        "ascension_combat_cooking_t3": {
            "coords": [511.6999, 157],
            "parents": ["ascension_combat_cooking_t2"]
        },
        "ascension_multicast": {
            "coords": [533, -319],
            "parents": ["ascension_lunchboxes"]
        },
        "ascension_map_queue": {
            "coords": [675, -280],
            "parents": ["ascension_multicast"]
        },
        "ascension_autohealthpacks": {
            "coords": [810, -210],
            "parents": ["ascension_map_queue"]
        },
        "ascension_academy_unlock": {
            "coords": [700, 47],
            "parents": ["ascension_headstart"]
        },
        "ascension_pumpjack_unlock": {
            "coords": [697, 219],
            "parents": ["ascension_academy_unlock"]
        }
    },
    "offset": {
        "x": -70,
        "y": 0
    }
}
```