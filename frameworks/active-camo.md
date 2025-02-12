---
description: >-
  Legion Studios' active camo framework, and how to add your
  own active camo items.
---

# Active Camoflauge

Legion Studios' active camo system works by iterating through a unit's loadout, and replacing any item that has an active camo version. If no camo version is found, then the item is left as-is.

This allows you to create camo versions of anything in a unit's inventory, such as weapons; attachments; magazines; helmets; etc. etc.

## 1. Configuration

The configuration will be the same for any class, but we'll use a helmet as an example. The item replacement will look for a class with the same name with `_activeCamo` added to the end. You can overwrite this by defining `ls_activeCamo_camoItem = "TAG_camoClassName"` in the class.

This saves time adding the property to each class, but also prevents issues with child classes being changed to the wrong item. Legion does not define the `camoItem` property on any of its "base" classes. E.g. the standard plain white Katarn I helmet does not define it, but the specific squad member helmets will have it defined to save us having to make the "same" helmets for each variant.

```cpp
class CfgWeapons {
    class ls_cloneHelmet_commando;
    class TAG_cloneHelmet_commando: ls_cloneHelmet_commando {
        author = "You";
        // Your normal changes
    };
    class TAG_cloneHelmet_commando_activeCamo: TAG_cloneHelmet_commando {
        scope = 1;
        author = "You";

        // These should be applied to every selection
        hiddenSelectionsTextures[] = {
            "\ls\core\addons\data\textures\blank_ca.paa",
            "\ls\core\addons\data\textures\blank_ca.paa"
        };
        hiddenSelectionsMaterials[] = {
            "\ls\core\addons\data\materials\activeCamo.rvmat",
            "\ls\core\addons\data\materials\activeCamo.rvmat"
        };
    };
};
```

For uniforms, you can also define the `ls_activeCamo_camouflageCoefficient` property (in the CfgWeapons class), which will be used instead of the setting if defined. For example, if the camouflage setting is set to `0.5`, but the uniform defines `ls_activeCamo_camouflageCoefficient = 0`, the `0` will be used for the camouflage skill.

## 2. Events

### 2.1 Listenable

| Name                        | Description                          | Arguments | Global / Local |
| --------------------------- | ------------------------------------ | --------- | -------------- |
| `ls_activeCamo_activated`   | Unit's active camo is activated.     | `[_unit]` | Local          |
| `ls_activeCamo_deactivated` | Unit's active camo is deactivated.   | `[_unit]` | Local          |

## 3. Functions
### 3.1 `ls_activeCamo_fnc_activate`
| Index | Description                                | Datatype(s) | Default Value |
| ----- | ------------------------------------------ | ----------- | ------------- |
| 0     | Unit                                       | Object      |               |
| 1     | Is curator, skips some conditions if true. | Bool        | False         |

**Return Value**

None

### 3.2 `ls_activeCamo_fnc_canActivate`
| Index | Description                                | Datatype(s) | Default Value |
| ----- | ------------------------------------------ | ----------- | ------------- |
| 0     | Unit                                       | Object      |               |
| 1     | Is curator, skips some conditions if true. | Bool        | False         |

**Return Value**

| Description  | Datatype(s) |
| ------------ | ----------- |
| Can activate | Bool        |

### 3.3 `ls_activeCamo_fnc_deactivate`
| Index | Description                                | Datatype(s) | Default Value |
| ----- | ------------------------------------------ | ----------- | ------------- |
| 0     | Unit                                       | Object      |               |

**Return Value**

None

### 3.4 `ls_activeCamo_fnc_canDeactivate`
| Index | Description                                | Datatype(s) | Default Value |
| ----- | ------------------------------------------ | ----------- | ------------- |
| 0     | Unit                                       | Object      |               |

**Return Value**
| Description    | Datatype(s) |
| -------------- | ----------- |
| Can deactivate | Bool        |
