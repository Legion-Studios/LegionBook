---
description: Custom scripted magazine functionality
---

# Magazine Properties

## Recharging
Magazines can be configured to recharge ammo to the magazine every X seconds. The recharging begins after firing, only one magazine will be recharged at a time. The magazine will continue to recharge if swapping to another weapon.

The recharge will stop if the magazine is unloaded (to free other weapons), and will not continue if a new magazine is loaded. It will only start again when a bullet it fired.

```cpp
class YourPrefix_myMagazine {
    ls_weapons_rechargeRate = 1; // Return an ammo every 1 second, 2 = 2 seconds, etc.
                                 // 0 = disabled.
};
