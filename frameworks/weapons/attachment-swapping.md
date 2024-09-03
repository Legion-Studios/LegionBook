---
description: Automatically swap attachments after loading a magazine.
---

# Attachment Swapping

This function is triggered upon reloading a magazine, and can be used to add any "weapon item", which includes weapon attachments and magazines. For specifics on what can be used, check out the [addWeaponItem](https://community.bistudio.com/wiki/addWeaponItem) script command.

## 1. Configuration

Here's an example of adding the attachment swap functionality to a DC-17M, although it can be applied to any weapon.

### 1.1 Weapon Config

```cpp
class CfgWeapons {
    class TAG_yourDC17M {
        ls_weapons_attachmentSwapEnabled = 1; // (0-Disabled, 1-Enabled)
        ls_weapons_attachments[] = {
            // Array of config property in magazine, weapon item to add
            // If the newly loaded magazine has <property> = 1 in config,
            // the given weapon item will be added
            {"TAG_weapons_isBlasterMag", "ls_muzzle_dc17m_blaster"},
            {"TAG_weapons_isATMag", "ls_muzzle_dc17m_antiArmor"},
            {"TAG_weapons_isSniperMag", "ls_muzzle_dc17m_sniper"}
        };
    };
};
```

### 1.2 Magazine Config

```cpp
class CfgMagazines {
    class TAG_yourDC17M_mag {
        // If TAG_yourDC17M_mag is loaded, ls_muzzle_dc17m_blaster
        // will be added to the weapon
        TAG_weapons_isBlasterMag = 1;
    };
};
```
