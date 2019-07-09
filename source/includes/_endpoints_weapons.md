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
    "attack": {
      "display": 384,
      "raw": 80
    },
    "slots": [...],
    "elements": [...],
    "attributes": {},
    "crafting": {
      "craftable": true,
      "previous": null,
      "branches": [...],
      "craftingMaterials": [...],
      "upgradeMaterials": [...]
    },
    "assets": {
      "icon": "https://assets.mhw-db.com/weapons/great-sword/icons/...",
      "image": "https://assets.mhw-db.com/weapons/great-sword/..."
    },
    "sharpness": {
      "red": 25,
      "orange": 12,
      "yellow": 13,
      "green": 0,
      "blue": 0,
      "white": 0
    },
	  "durability": [...]
  }
]
```

This endpoint retrieves a list of all weapons.

### HTTP Request
`GET https://mhw-db.com/weapons`

### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
p | No | See the [Projecting Results](#projecting-results) section
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
  "attack": {
    "display": 384,
    "raw": 80
  },
  "slots": [...],
  "elements": [...],
  "attributes": {},
  "crafting": {
    "craftable": true,
    "previous": null,
    "branches": [...],
    "craftingMaterials": [...],
    "upgradeMaterials": [...]
  },
  "assets": {
    "icon": "https://assets.mhw-db.com/weapons/great-sword/icons/...",
    "image": "https://assets.mhw-db.com/weapons/great-sword/..."
  },
  "sharpness": {
    "red": 25,
    "orange": 12,
    "yellow": 13,
    "green": 0,
    "blue": 0,
    "white": 0
  },
  "durability": [...]
}
```

This endpoint retrieves a weapon by it's ID or slug.

### HTTP Request
`GET https://mhw-db.com/weapons/<idOrSlug>`

### Path Parameters
Parameter | Type | Description
--------- | ---- | -----------
idOrSlug | Integer &#124; String | The ID or slug of the weapon to retrieve

### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
p | No | See the [Projecting Results](#projecting-results) section

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
  "attack": {
    "display": 462,
    "raw": 140
  },
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
  "attributes": {},
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
  "assets": {
    "icon": "https://assets.mhw-db.com/weapons/long-sword/icons/...",
    "image": "https://assets.mhw-db.com/weapons/long-sword/..."
  },
  "sharpness": {
    "red": 22,
    "orange": 13,
    "yellow": 12,
    "green": 20,
    "blue": 8,
    "white": 0
  },
  "durability": [
    {
      "red": 90,
      "orange": 50,
      "yellow": 50,
      "green": 80,
      "blue": 30,
      "white": 0
    }
  ]
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
attack | [Attack](#weapon-attack) | Contains information about the attack values of the weapon
slots | Array&lt;[Slot](#slot-objects)&gt; | An array containing slot information for the weapon
elements | Array&lt;[WeaponElement](#weapon-elements)&gt; | An array containing element damage info for the weapon
crafting | [WeaponCraftingInfo](#weapon-crafting-info) | Contains crafting information for the weapon
assets | [WeaponAssets](#weapon-assets) | Contains information about weapon UI assets (such as preview images)
sharpness | [WeaponSharpness (d)](#weapon-sharpness-deprecated) | ([_deprecated_](#deprecation-schedule)) Contains sharpness information
durability | Array&lt;[WeaponSharpness](#weapon-sharpness)&gt; | An array of sharpness information, ordered by handicraft level; base sharpness can always be found at index 0
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

### Weapon Attack
Field | Type | Description
----- | ---- | -----------
display | Integer | The attack value of the weapon that's displayed in game
raw | Integer | The true raw attack value of the weapon

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

Please note that the `type` field can be any [`ElementType`](#element-types) value **except for** `stun`.

### Weapon Assets
Field | Type | Description
----- | ---- | -----------
icon | String | The weapon's icon
image | String | An image showing the weapon's in game model

### Weapon Sharpness
Since [v1.13.0](https://github.com/LartTyler/MHWDB-API/releases/tag/1.13.0), the API provides true sharpness values for
weapons. For each color, sharpness is represented as an integer indicating the number of normal hits the weapon can
make before sharpness degrades (that is to say, the number of hits that did not bounce off of a monster due to the
body part being too hard for the weapon or sharpness level).

All fields in a sharpness object can be found in the table below.

Field | Type | Description
----- | ---- | -----------
red | Integer | The number of normal hits the weapon can make at red sharpness
orange | Integer | The number of normal hits the weapon can make at orange sharpness
yellow | Integer | The number of normal hits the weapon can make at yellow sharpness
green | Integer | The number of normal hits the weapon can make at green sharpness
blue | Integer | The number of normal hits the weapon can make at blue sharpness
white | Integer | The number of normal hits the weapon can make at white sharpness

In previous versions, these docs provided a simple method for visually representing sharpness values, since they were
represented as percetages (which could be mapped 1:1 to pixels for a 100px wide sharpness bar). You can achieve the
same result by taking the new sharpness values and using the following formula to convert them into their old percetage
value, then flooring the result: <code>&lfloor;sharpness / 400 * 100&rfloor;</code>.

So, for example, the long sword "<a href="https://mhw-db.com/weapons/156" target="_blank">Dark Scimitar 3</a>" has a
base durability of 110 red, 30 orange, 60 yellow, 80 green, 40 blue, and 30 white. This converts to the old system as
follows.

<code>
Red: &lfloor;110 / 400 * 100&rfloor; = 27<br>
Orange: &lfloor;30 / 400 * 100&rfloor; = 7<br>
Yellow: &lfloor;60 / 400 * 100&rfloor; = 15<br>
Green: &lfloor;80 / 400 * 100&rfloor; = 20<br>
Blue: &lfloor;40 / 400 * 100&rfloor; = 10<br>
Red: &lfloor;30 / 400 * 100&rfloor; = 7
</code>

Since, for a 100px wide bar, those percentages map 1:1, the resulting bar would look something like the bar below.

<div class="sharpness-bar">
  <div class="red" style="width: 27px"></div>
  <div class="orange" style="width: 7px;"></div>
  <div class="yellow" style="width: 15px;"></div>
  <div class="green" style="width: 20px;"></div>
  <div class="blue" style="width: 10px;"></div>
  <div class="white" style="width: 7px;"></div>

  <div class="clearfix"></div>
</div>

### Weapon Sharpness (_deprecated_)
Since MHW does not disclose actual sharpness values, sharpness is represented as a whole number out of 100, with 100 being the maximum possible sharpness a weapon can have. The total sharpness value is split across several different colors, indicating what percentage of the weapon's max sharpness belongs to each color.

It's easiest to visualize sharpness as a single bar, 100 pixels wide. For example, the long sword "<a href="https://mhw-db.com/weapons/156" target="_blank">Dark Scimitar 3</a>" has 27 red, 8 orange, 15 yellow, 20 green, 10 blue, and 7 white. A bar representing that might look like the bar below.

<div class="sharpness-bar">
  <div class="red" style="width: 27px"></div>
  <div class="orange" style="width: 8px;"></div>
  <div class="yellow" style="width: 15px;"></div>
  <div class="green" style="width: 20px;"></div>
  <div class="blue" style="width: 10px;"></div>
  <div class="white" style="width: 7px;"></div>

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
white | Integer | The white sharpness value

### Weapon Attributes
The weapon attributes object is a dictionary of attribute modifiers attached to a weapon. Most of these fields are planned to be slowly phased out over several releases, and instead provided by specialized fields (such as `sharpness`).

Possible attribute keys are listed below.

Name | Type | Description
---- | ---- | -----------
ammoCapacities | [AmmoCapacities](#ammo-capacities) | For "light-bowgun" and "heavy-bowgun" weapons only
affinity | Integer | The affinity of the weapon
boostType | [BoostType](#boost-types) | For "insect-glaive" weapons only
coatings | Array&lt;[Coating](#bow-coatings)&gt; | For "bow" weapons only
damageType | [DamageType](#damage-types) | The type of damage the weapon deals
defense | Integer | Some weapons (namely "gunlance" types) augment player defense; such weapons indicate that with this field
deviation | [Deviation](#bowgun-deviation) | For "light-bowgun" and "heavy-bowgun" weapons only
elderseal | [Elderseal](#elderseal-types) | The elderseal type attributed to the weapon
phialType | [PhialType](#phial-types) | For "switch-axe" and "charge-blade" weapons only
shellingType | [ShellingType](#shelling-types) | For "gunlance" weapons only
specialAmmo | [SpecialAmmoType](#special-ammo-types) | For "light-bowgun" and "heavy-bowgun" weapons only

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

- sever
- speed
- element
- health
- stamina
- blunt

### Bow Coatings
A bow's coating may be one of the following values.

- close range
- paralysis
- poison
- sleep
- blast
- power

### Bowgun Deviation
A bowgun's deviation may be one of the following values.

- none
- low
- average
- high

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

- impact
- element
- power
- power element

The second is a dynamic form, for phial types that also include a strength. Such phial types may be one of the following values, followed by a number that indicates their strength (e.g. "dragon 300").

- dragon
- exhaust
- para
- poison

### Shelling Types
A gunlance's shelling type may be one of the following values, followed by a level indicator in the form "Lv#" (e.g. "Normal Lv2").

- Normal
- Long
- Wide

### Special Ammo Types
A light or heavy bowgun's special ammo type may be one of the following values.

- wyvernblast
- wyvernheart
- wyvernsnipe