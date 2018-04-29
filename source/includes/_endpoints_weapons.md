# Weapons
## Get All Weapons
```shell
curl "https://mhw-db.com/weapons"
```

```javascript
fetch('https://mhw-db.com/weapons')
    .then(response => response.json())
    .then(weapons => {
        // your code here
    });
```

> The above command returns an array of [`Weapon`](#weapon-fields) objects. Some fields have been truncated for brevity.

```json
[
  {
    "id": 1,
    "slug": "buster-sword-1",
    "name": "Buster Sword 1",
    "type": "great-sword",
    "rarity": 1,
    "slots": [...],
    "elements": [...],
    "attributes": {
      "attack": 384,
      "sharpnessRed": 25,
      "sharpnessOrange": 12,
      "sharpnessYellow": 13
    },
    "crafting": {
      "craftable": true,
      "previous": null,
      "branches": [...],
      "craftingMaterials": [...],
      "upgradeMaterials": [...]
    },
    "sharpness": {
      "red": 25,
      "orange": 12,
      "yellow": 13,
      "green": 0,
      "blue": 0
    }
  }
]
```

This endpoint retrieves a list of all weapons.

### HTTP Request
`GET https://mhw-db.com/weapons`

### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
q | No | See the [Searching the API](#searching-the-api) section

### Response
This endpoint returns an array of weapons. For field information, see the [Weapon Fields](#weapon-fields) section.

## Get a Specific Weapon
```shell
curl "https://mhw-db.com/weapons/1"
```

```javascript
fetch('https://mhw-db.com/weapons/1')
    .then(response => response.json())
    .then(weapon => {
        // your code here
    });
```

> The above command returns a single [`Weapon`](#weapon-fields) object. Some fields have been truncated for brevity.

```json
{
  "id": 1,
  "slug": "buster-sword-1",
  "name": "Buster Sword 1",
  "type": "great-sword",
  "rarity": 1,
  "slots": [...],
  "elements": [...],
  "attributes": {
    "attack": 384,
    "sharpnessRed": 25,
    "sharpnessOrange": 12,
    "sharpnessYellow": 13
  },
  "crafting": {
    "craftable": true,
    "previous": null,
    "branches": [...],
    "craftingMaterials": [...],
    "upgradeMaterials": [...]
  },
  "sharpness": {
    "red": 25,
    "orange": 12,
    "yellow": 13,
    "green": 0,
    "blue": 0
  }
}
```

This endpoint retrieves a weapon by it's ID or slug.

### HTTP Request
`GET https://mhw-db.com/weapons/<idOrSlug>`

### Path Parameters
Parameter | Type | Description
--------- | ---- | -----------
idOrSlug | Integer &#124; String | The ID or slug of the weapon to retrieve

### Response
This endpoint returns a single weapon. For field information, see the [Weapon Fields](#weapon-fields) section.

## Weapon Fields
```json
{
  "id": 94,
  "slug": "iron-grace-3",
  "name": "Iron Grace 3",
  "type": "long-sword",
  "rarity": 5,
  "slots": [
    {
      "rank": 1
    }
  ],
  "elements": [
    {
      "type": "water",
      "damage": 120,
      "hidden": true
    }
  ],
  "attributes": {
    "attack": 462,
    "slotsRank1": 1,
    "elementHidden": true,
    "elementDamage": 120,
    "elementType": "Water",
    "sharpnessRed": 22,
    "sharpnessOrange": 13,
    "sharpnessYellow": 12,
    "sharpnessGreen": 20,
    "sharpnessBlue": 8
  },
  "crafting": {
    "craftable": false,
    "previous": 93,
    "branches": [
      95
    ],
    "craftingMaterials": [],
    "upgradeMaterials": [
      {
        "quantity": 8,
        "item": {
          "id": 119,
          "name": "Carbalite Ore",
          "description": "Ore obtained from mining outcrops. Still ...",
          "rarity": 0,
          "carryLimit": 0,
          "sellPrice": 0,
          "buyPrice": 0
        }
      }
    ]
  },
  "sharpness": {
    "red": 22,
    "orange": 13,
    "yellow": 12,
    "green": 20,
    "blue": 8
  }
}
```

> A sample `Weapon` object. Some fields have been truncated for brevity.

Field | Type | Description
----- | ---- | -----------
id | Integer | The ID of the weapon
slug | String | A human readable unique identifier
name | String | The name of the weapon
type | [WeaponType](#weapon-types) | The weapon's type
rarity | Integer | The rarity of the weapon
slots | Array&lt;[Slot](#slot-objects)&gt; | An array containing slot information for the weapon
elements | Array&lt;[WeaponElement](#weapon-elements)&gt; | An array containing element damage info for the weapon
crafting | [WeaponCraftingInfo](#weapon-crafting-info) | Contains crafting information for the weapon
sharpness | [WeaponSharpness](#weapon-sharpness) | Contains sharpness information
attributes | [WeaponAttributes](#weapon-attributes) | See [WeaponAttributes](#weapon-attributes) for more information

### Weapon Types
A weapon's type can be one of the following values:

| | | |
|-|-|-|
great-sword | long-sword | sword-and-shield
dual-blades | hammer | hunting-horn
lance | gunlance | switch-axe
charge-blade | insect-glaive | light-bowgun
heavy-bowgun | bow

### Weapon Crafting Info
Field | Type | Description
----- | ---- | -----------
craftable | Boolean | Indicates whether or not the weapon may be directly crafted
previous | Integer &#124; Null | The ID of the weapon that this weapon is upgraded from, or `null` if nothing upgrades into this weapon
branches | Array&lt;Integer&gt; | An array of IDs that the weapon may be upgraded into
craftingMaterials | Array&lt;[CraftingCost](#craftingcost-objects)&gt; | An array containing the material cost to create the weapon; will always be empty if `craftable` is false
upgradeMaterials | Array&lt;[CraftingCost](#craftingcost-objects)&gt; | An array containing the material cost to upgrade the weapon identified by `previous` into this weapon; will always be empty if `previous` is null

### Weapon Elements
Field | Type | Description
----- | ---- | -----------
type | [ElementType](#element-types) | The element's damage type
damage | Integer | The power of the element
hidden | Boolean | Indicates whether or not the element is a hidden element

### Weapon Sharpness
Since MHW does not disclose actual sharpness values, sharpness is represented as a whole number out of 100, with 100 being the maximum possible sharpness a weapon can have. The total sharpness value is split across several different colors, indicating what percentage of the weapon's max sharpness belongs to each color.

It's easiest to visualize sharpness as a single bar, 100 pixels wide. For example, the great sword "<a href="https://mhw-db.com/weapons/6" target="_blank">Buster Sword 3</a>" has 25 red, 12 orange, 13 yellow, 20 green, and 5 blue. A bar representing that might look like the bar below.

<div class="sharpness-bar">
  <div class="red" style="width: 25px"></div>
  <div class="orange" style="width: 12px;"></div>
  <div class="yellow" style="width: 13px;"></div>
  <div class="green" style="width: 20px;"></div>
  <div class="blue" style="width: 5px;"></div>

  <div class="clearfix"></div>
</div>

All fields in the sharpness can be found in table below.

Field | Type | Description
----- | ---- | -----------
red | Integer | The red sharpness value
orange | Integer | The orange sharpness value
yellow | Integer | The yellow sharpness value
green | Integer | The green sharpness value
blue | Integer | The blue sharpness value

### Weapon Attributes
The weapon attributes object is a dictionary of attribute modifiers attached to a weapon. These fields are planned to be slowly phased out over several releases, and instead provided by specialized fields (such as `sharpness`).

Possible attribute keys are listed below.

Name | Type | Description
---- | ---- | -----------
ammoCapacities | [AmmoCapacities](#ammo-capacities) | For "light-bowgun" and "heavy-bowgun" weapons only
attack | Integer | The attack power of the weapon
affinity | Integer | The affinity of the weapon
boostType | [BoostType](#boost-types) | For "insect-glaive" weapons only
coatings | Array&lt;[Coating](#bow-coatings)&gt; | For "bow" weapons only
damageType | [DamageType](#damage-types) | The type of damage the weapon deals
deviation | [Deviation](#bowgun-deviation) | For "light-bowgun" and "heavy-bowgun" weapons only
elderseal | [Elderseal](#elderseal-types) | The elderseal type attributed to the weapon
phialType | [PhialType](#phial-types) | For "switch-axe" and "charge-blade" weapons only
shellingType | [ShellingType](#shelling-types) | For "gunlance" weapons only
specialAmmo | [SpecialAmmoType](#special-ammo-types) | For "light-bowgun" and "heavy-bowgun" weapons only
elementType | [ElementType](#element-types) | ([_deprecated_](#deprecation-schedule)) The primary element type of the weapon
elementDamage | Integer | ([_deprecated_](#deprecation-schedule)) The power of the weapon's primary element
elementHidden | Boolean | ([_deprecated_](#deprecation-schedule)) If true, indicates that the primary element is a hidden element
elementType2 | [ElementType](#element-types)) | ([_deprecated_](#deprecation-schedule)) The secondary element type of the weapon
elementDamage2 | Integer | ([_deprecated_](#deprecation-schedule)) The power of the weapon's secondary element
elementHidden2 | Boolean | ([_deprecated_](#deprecation-schedule)) If true, indicates that the secondary element is a hidden element
sharpnessRed | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's red sharpness bar
sharpnessOrange | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's orange sharpness bar
sharpnessYellow | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's yellow sharpness bar
sharpnessGreen | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's green sharpness bar
sharpnessBlue | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's blue sharpness bar
sharpnessWhite | Integer | ([_deprecated_](#deprecation-schedule)) The size of the weapon's white sharpness bar
slotsRank1 | Integer | ([_deprecated_](#deprecation-schedule)) The number of rank 1 slots available on the weapon
slotsRank2 | Integer | ([_deprecated_](#deprecation-schedule)) The number of rank 2 slots available on the weapon
slotsRank3 | Integer | ([_deprecated_](#deprecation-schedule)) The number of rank 3 slots available on the weapon

### Ammo Capacities
Light and heavy bowguns use the `attributes.ammoCapacities` field to specify ammo capacities for their various ammo types. In the `ammoCapacities` object, the key is the name of the ammo type, and the value is an array of capacities for each level of the ammo type.

Ammo Name | Levels |   | Ammo Name | Levels
--------- | :----: | - | --------- | :----:
normal | 3 | | flaming | 1
piercing | 3 | | water | 1
spread | 3 | | freeze | 1
sticky | 3 | | thunder | 1
cluster | 3 | | dragon | 1
recover | 2 | | slicing | 1
poison | 2 | | wyvern | 1
paralysis | 2 | | demon | 1
sleep | 2 | | armor | 1
exhaust | 2 | | tranq | 1

### Boost Types
An insect glaive's boost type may be one of the following values.

- Sever Boost
- Speed Bost
- Element Boost
- Health Boost
- Stamina Boost
- Blunt Boost

### Bow Coatings
A bow's coating may be one of the following values.

- Close Range
- Paralysis
- Poison
- Sleep
- Blast
- Power

### Bowgun Deviation
A bowgun's deviation may be one of the following values.

- None
- Low
- Average
- High

### Damage Types
A weapon's damage type will be one of the following values:

- blunt
- piercing
- slashing

### Elderseal Types
A weapon's elderseal type may be one of the following values:

- low
- average
- high

### Phial Types
A phial type is represented in one of two forms. The first of which is a simple form, which may be one of the following values.

- Impact Phial
- Element Phial
- Power Phial

The second is a dynamic form, for phial types that also include a strength. Such phial types may be one of the following values, followed by a number that indicates their strength (e.g. "Dragon Phial 300").

- Dragon Phial
- Exhaust Phial
- Para Phial
- Poison Phial

### Shelling Types
A gunlance's shelling type may be one of the following values, followed by a level indicator in the form "Lv#" (e.g. "Normal Lv2").

- Normal
- Long
- Wide

### Special Ammo Types
A light or heavy bowgun's special ammo type may be one of the following values.

- Wyvernblast
- Wyvernheart
- Wyvernsnipe