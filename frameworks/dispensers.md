---
description: >-
  Legion Studios' droid dispensers, allowing Zeuses to have AI engage players quickly and take some of the load off of the Zeuses.
---

# Droid Dispensers

## 1. Group Configuration
Droid Dispensers use CfgGroups classes for their spawning logic. Groups can be enabled/disabled at the faction, category, and group levels. The `ls_dispenser_available` variable controls whether something should be shown and has three states:
- `-1` - Hidden
- `0` - Use value of the higher class (default)
- `1` - Shown

### 1.1 Examples
`Group1` is available, but not `Group2`.
```cpp
class CfgGroups {
    class East {
        class MyFaction {
            class Infantry {
                class Group1 {
                    ls_dispenser_available = 1;
                };
                class Group2 {
                    // ...
                };
            };
        };
    };
};
```

All groups in `Infantry` are available by default, but `Group1` is disabled.
```cpp
class CfgGroups {
    class East {
        class MyFaction {
            class Infantry {
                ls_dispener_available = 1;
                class Group1 {
                    ls_dispener_available = -1;
                };
                class Group2 {
                    // ...
                };
                class Group3 {
                    // ...
                };
            };
        };
    };
};
```

### 1.2 Misc
The group UI will show the `icon` of the faction as defined in `CfgFactionClasses`. In the examples above, it would look at `"CfgFactionClasses" >> "MyFaction" >> "icon"` for the icon.

If no icon is found, it will use a blank square texture that is the side of the faction instead.

For groups, the group's icon (set in the group class itself) will be used and be colored to the faction's side.

## 2. Module Configuration
You can configure your own Zeus modules to make it easy for Zeuses to spawn your own Droids without making them select them via the module GUI.

```cpp
class CfgFactionClasses {
    class NO_CATEGORY;
    class MyPrefix_modules: NO_CATEGORY {
        displayName = "[Unit Name] Modules";
    };
};

// Make sure ls_loadorder is present in your requiredAddons
// Make sure to add the module class name to your `CfgPatches >> yourAddon >> units` list to it appears in Zeus
class CfgVehicles {
    class ls_moduleDroidDispenser_zeus;
    class MyPrefix_moduleDroidDispenser_B1_zeus: ls_moduleDroidDispenser_zeus {
        author = "Me";
        displayName = "Droid Dispenser (B1)";
        category = "MyPrefix_modules";

        ammo = "ls_dispenser_ordnance"; // Optional, ammo class name that is dropped

        // ls_dispenser_group can either be an string which points to a class in CfgGroups, using `>>` as a separator between class names
        // Or it can be an array of unit class names directly
        ls_dispenser_group = "MyFaction>>Infantry>>Group1"; // Valid
        ls_dispenser_group[] = {"MyPrefix_B1", "MyPrefix_B1_Heavy"}; // Also valid

        ls_dispenser_vehicle = "ls_droidDispenser"; // Optional, you can use your own droid dispenser class if you'd like to change the textures, armor, etc.

        ls_dispenser_limit = 50; // Optional, maximum number of units to spawn before the dispenser is deactivated
    };
};
```

## 3. Dispenser Configuration
You can configure your own Zeus modules to make it easy for Zeuses to spawn your own Droids without making them select them via the module GUI.

```cpp
class CfgVehicles {
    // Not needed, but does set some basic variables
    class ls_droidDispenser_base;
    class YourPrefix_dispenser: ls_droidDispenser_base {
        author = "Me";
        displayName = "My Custom Dispenser";

        ls_dispenser_hatchCount = 3; // Total number of hatches
        ls_dispenser_hatchHitpoint = "HitHatch%1"; // Optional: Name format for hitpoints, used to disable hatches if a given hitpoint is destroyed. %1 is placeholder for hatch number (1 - hatchCount)
        ls_dispenser_hatchAnimation = "Hatch%1_move"; // Name format for AnimationSources names. %1 is placeholder for hatch number (1 - hatchCount)
        ls_dispenser_hatchDirections[] = {90, 330, 210}; // Directions that units will face while on each hatch, must be in order
        ls_dispenser_activationSelection[] = {"hiddenSelectionName", "#(rgb,8,8,3)color(0.9,0,0.2,0.7)"}; // Name in hiddenSelections and the texture to use while the dispenser is active. Selection is also used for when a dispenser fails to spawn a unit because the hitpoint is destroyed
        ls_dispenser_unitAnimation = "ls_droid_folded"; // Animation to use for while a unit is on the rack

        // Additionally, created units will be spawned at and attached to the `Spawn%1` memory point. %1 is placeholder for hatch number (1 - hatchCount)

        class HitPoints {
            class HitBody { ... };
            class HitHatch1 { ... };
            class HitHatch2: HitHatch1 { ... };
            class HitHatch3: HitHatch1 { ... };
        };

        animationList[] = {
            "Hatch1_move", 0,
            "Hatch2_move", 0,
            "Hatch3_move", 0
        };
        class AnimationSources {
            class Hatch1_move { ... };
            class Hatch2_move: Hatch1_move { ... };
            class Hatch3_move: Hatch1_move { ... };
        };
    };
};
```

## 4. Functions
### 4.1 `ls_dispenser_fnc_activate`
#### Description
Activates a droid dispenser and starts the loop for droid dispensers to spawn units if needed. Spawn group must either be an array of units or a string pointing to a group (same as `ls_dispenser_group` in module config).

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |
| 1     | Spawn group | String, Array |               |

#### Return Value
None

### 4.2 `ls_dispenser_fnc_deactivate`
#### Description
Deactivates a droid dispenser.

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |

#### Return Value
None

### 4.3 `ls_dispenser_fnc_setSpawnGroup`
#### Description
Sets the spawn group of a given droid dispenser. Handles changing the side of the droid dispenser's UAV crew if the new group is of a different side.

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |
| 1     | Spawn group | String, Array |               |

#### Return Value
None

### 4.4 `ls_dispenser_fnc_dropDispenser`
#### Description
Spawns a falling dispenser at the given position, *note that the altitude is used directly, so spawning at [x, y, 0] will cause it to immediately land on the ground*. We reccomend a minimum height of 1000m. See [Module Configuration](frameworks/dispensers#id-2.-module-configuration) for more information on the dispenser parameters.

#### Parameters
| Index | Description      | Datatype(s) | Default Value |
| ----- | ---------------- | ----------- | ------------- |
| 0     | Dispenser params | Hashmap     |               |
| 1     | PositionATL      | Array       |               |
| 2     | Velocity         | Array       | [0, 0, -100]  |

#### Return Value
The created projectile

#### Examples
```sqf
[createHashMapFromArray [
    ["spawnGroup", "ls_cis>>cis_baseInfantry>>base_b1_fireteam"],
], [0, 0, 1000]] call ls_dispenser_fnc_dropDispenser;

[createHashMapFromArray [
    ["spawnGroup", ["ls_droid_b1", "ls_droid_b2"]],
    ["spawnLimit", 3], // Optional
    ["dispenserClass", "ls_droidDispenser"], // Optional
    ["ammoClass", "ls_dispenser_ordnance"] // Optional
], [0, 0, 1000]] call ls_dispenser_fnc_dropDispenser;
```
