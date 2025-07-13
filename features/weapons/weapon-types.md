---
description: Custom scripted weapon functionality
---

# Weapon Types

Weapons can have extra functionality added to them by setting the `ls_weapons_weaponType` property in the weapon's config.

## Akimbo
When the weapon is fired, the weapon will alternate between the first two muzzles that are defined in the weapon's `muzzle` property. E.g. `muzzles[] = {"right", "left"};`. The muzzle will only be selected if it has ammo remaining.

Used by: Dual DC-17S Pistols

Weapon config:
```cpp
ls_weapons_weaponType = 1;
ls_weapons_akimboDummy = "ls_weapon_dc17s_dual_dummyWeapon"; // NVG class, see below
ls_weapons_akimboReloadTime = 2.49; // How long to keep the dummy NVG equipped

// Need to add a call to ls_weapons_fnc_animateAkimbo in the muzzle's reload event.
// This triggers at the *start* of the reload, which is why it must be added here.
modes[] = {};
muzzles[] = {"Right", "Left"};
class Right {
    displayName = "Right Hand";
    class EventHandlers {
        reload = "call ls_weapons_fnc_animateAkimbo";
    };
};
class Left: Right {
    displayName = "Left Hand";
    showToPlayer = 0;
};
```

NVG config:
```cpp
// To animate the second pistol, we use a dummy NVG class that is temporarily added.
class Binocular;
class NVGoggles: Binocular {
    class ItemInfo;
};
class ls_weapon_dc17s_dual_dummyWeapon: NVGoggles {
    scope = 1;
    author = "You";
    displayName = "";
    descriptionShort = "";

    model = "\path\to\dummy\model.p3d";;
    hiddenSelections[] = {...};
    hiddenSelectionsTextures[] = {...};

    visionMode[] = {"Normal"};
    thermalMode[] = {};

    class ItemInfo: ItemInfo {
        uniformModel = "\path\to\dummy\model.p3d";
        modelOff = "\path\to\dummy\model.p3d";
        hiddenSelections[] = {...};
        mass = 0;
    };
};
```

The NVG dummy model will need to be rotated similarly to the attached image. The left shows the model for the dual DC-17S weapon, and the right shows the model used for the dummy NVG item used for the reload.
![Normal and dummy Dual DC-17S models](assets\akimbo_models.png)
