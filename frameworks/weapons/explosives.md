---
description: Custom explosive properties
---

# Breaching Charge

Handles the scripted logic for the breaching charge.

## 1. Configuration

### 1.1 Ammo Config

Here shows the values set in `ls_explosive_breachCharge_ammo`, with comments explaining what they do.

```cpp
class CfgAmmo {
    class TAG_yourExplosive_ammo {
        ls_explosives_isBreachCharge = 1; // 0=disabled, 1=enabled

        // Any submunitions created by an explosive marked as a breaching charge will have its submunitions rotated to face into the surface
        submunitionAmmo = "ls_explosive_breachCharge_submunition_ammo";
        submunitionConeType[] = {"custom", {{0, 0}}}; // Spawn submunition exactly below main charge
        submunitionInitialOffset[] = {0, -0.6, 0}; // Reccomended minimum of 0.6m below the charge, to not be caught in the raycast from the explosive itself
    };
};
```

### 1.2 Object Config

Any object that inherits from `Wall` or `Fence`, or has `ls_explosives_destroyWhenBreached = 1;` in config will be destroyed when a breaching charge directly hits them (i.e. placed on the object).

For terrain objects specifically, those with `"wall"` or `"fence"` in the model name will also be destroyed. This is because simple terrain objects don't have classes, as opposed to a terrain placed house which does have a class.

# Caltrops
See [features/weapons/ammo-types](https://legion-studios.gitbook.io/legion-studios/features/weapons/ammo-types#ragdoll).
