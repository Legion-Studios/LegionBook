---
description: Playing sounds when aiming down the sight of a weapon.
---

# Aim Down Sight Sounds

Weapons can be configured to play sounds when aiming down the sight. These sounds can be set per-weapon as well as per-optic, meaning you can have separate "iron sight" sounds as well as sounds for looking down a scope.

If an optic is equipped, its sounds will always overwrite the weapon's; even if the optic as no sounds.

**Note:** This system is not perfect, there is no specific method of detecting when a player actually aims down the sight of their weapon. Instead, we simply check a number of specific conditions whenever the player presses their right mouse button.

## 1. Configuration

For sounds, you can either provide an array of sounds, or for multiple sounds, you can use an array.

```cpp
class CfgWeapons {
    class TAG_yourRifle {
        // Fine
        ls_weapons_adsSounds[] = {
            "TAG_ironSightDownSound",
            "TAG_ironSightReleaseSound"
        };
        // Also fine
        ls_weapons_adsSounds[] = {
            {"TAG_ironSightDownSound1", "TAG_ironSightDownSound2"},
            "TAG_ironSightReleaseSound"
        };
    };

    class TAG_yourSniperScope {
        ls_weapons_adsSounds[] = {
            "TAG_sniperScopeDownSound", 
            "TAG_sniperScopeReleaseSound"
        };
    };
};
```
