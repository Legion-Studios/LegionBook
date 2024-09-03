---
description: >-
  Legion Studios' biology framework, including how to use it and how to add your
  own biologies.
---

# Biology

The biology framework won't do much on its own, and is primarily intended for third party modders to use in their own mods.

## 1. Getting a unit's biology

To check the biology of a unit, use the `ls_common_fnc_getBiology` function.

Here we get the biology of the current unit that the player is controlling (`ls_player`) and display a groan sound if the player is a zombie.

```sqf
private _biology = ls_player call ls_common_fnc_getBiology;
_biology params ["_type", "_isOrganic", "_bloodModels"];

if (_type == "zombie") then {
    systemChat "rurrgghhh";
};
```

## 2. Configuration

### 2.1 Creating a custom biology

You can easily create your own custom biology via config. Here is a biology already included in Legion Studios: Core as an example.

```cpp
class ls_biologies {
    class biology_base; // default biology class, contains default values
    class hologram: biology_base {
        scope = 2; // Only biologies with scope > 0 are used
        type = "hologram"; // The type, such as human, an alien species, droid, etc.
        isOrganic = 0; // 0-Non-organic being, 1-Organic being
        // Condition for a unit to be this biology.
        // Passed params: [_unit]
        condition = "call ls_common_fnc_biologyCondition_isHologram";
        // Array of models to use when this unit bleeds.
        // A hologram doesn't bleed, so this stays empty.
        bloodModels[] = {};
    };
};
```

## 3. Examples of using biologies

Biologies can be used for lots of different systems, such as "ion" or "emp" ammunition not doing anything, or having a lesser effect on organic beings.

Legion Studios: Core also uses the blood models when ACE Medical is loaded. Normal blood drops will be replaced with custom ones defined in the unit's biology.
