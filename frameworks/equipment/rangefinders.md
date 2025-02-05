---
description: Adds extra information to Night Vision Goggles.
---

# Rangefinders

Legion's "rangefinder framework" allows you to specify a custom display to be created when a player enables NVG or thermals.

## 1. Configuration

Here's an example of adding the rangefinder HUD from Legion to an NVG.

### 1.1  NVG Config

```cpp
class CfgWeapons {
    class TAG_yourNVG {
        // Class name in RscTitles to create
        ls_equipment_rangefinderDisplay = "ls_RscCloneRangefinder";
    };
};
```

### 1.2 Creating your own HUD

To create your own HUD element, simply create a new display in `configFile >> "RscTitles`". If you'd like to use the functionality of the LS rangefinder in your custom one, you can simply inherit from the `ls_RscCloneRangefinder` class.

```cpp
class RscTitles {
    class ls_RscCloneRangefinder {
        class controls {
            class Distance;
            class Time;
            class Bearing;
            class BearingArrow;
        };
    };

    class TAG_yourCustomHUD: ls_RscCloneRangefinder {
        idd = ...; // Your unique numerical ID for this display
        class controls: controls {
            class Distance: Distance {
                // Your changes here
            };
            class Time: Time {};
            class Bearing: Bearing {};
            class BearingArrow: BearingArrow {};
        };
    };
};
```

If you want to add further functionality, you can modify the `onLoad` and `onUnload` properties for the display itself. For example:

```cpp
class TAG_yourCustomHUD: ls_RscCloneRangefinder {
    onLoad = "call ls_equipment_fnc_rangefinderOnLoad; call TAG_fnc_myOnLoad";
    onUnload = "call ls_equipment_fnc_rangefinderOnUnload; call TAG_fnc_myOnUnload";
};
```
