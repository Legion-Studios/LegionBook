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
// Make sure ls_loadorder is present in your requiredAddons
// Make sure to add the module class name to your units list to it appears in Zeus
class CfgVehicles {
    class ls_moduleDroidDispenser_zeus;
    class MyPrefix_moduleDroidDispenser_B1_zeus: ls_moduleDroidDispenser_zeus {
        author = "Me";
        displayName = "Droid Dispenser (B1)";

        faction = "MyPrefix_modules";

        // ls_dispenser_group can either be an string which points to a class in CfgGroups, using `>>` as a separator between class names
        // Or it can be an array of unit class names directly
        ls_dispenser_group = "MyFaction>>Infantry>>Group1"; // Valid
        ls_dispenser_group[] = {"MyPrefix_B1", "MyPrefix_B1_Heavy"}; // Also valid

        ls_dispenser_vehicle = "ls_droidDispenser"; // Optional, you can use your own droid dispenser class if you'd like to change the textures, armor, etc.
    };
};
```

## 3. Functions
### 3.1 `ls_dispenser_fnc_activate`
#### Description
Activates a droid dispenser and starts the loop for droid dispensers to spawn units if needed. Spawn group must either be an array of units or a string pointing to a group (same as `ls_dispenser_group` in module config).

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |
| 1     | Spawn group | String, Array |               |

#### Return Value
None

### 3.2 `ls_dispenser_fnc_deactivate`
#### Description
Deactivates a droid dispenser.

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |

#### Return Value
None

### 3.3 `ls_dispenser_fnc_setSpawnGroup`
#### Description
Sets the spawn group of a given droid dispenser. Handles changing the side of the droid dispenser's UAV crew if the new group is of a different side.

#### Parameters
| Index | Description | Datatype(s)   | Default Value |
| ----- | ------------| ------------- | ------------- |
| 0     | Dispenser   | Object        |               |
| 1     | Spawn group | String, Array |               |

#### Return Value
None
