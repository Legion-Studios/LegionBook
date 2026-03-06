---
description: >-
  Legion Studios' impulsor framework, allowing vehicles to move much faster at
  the cost of fuel.
---

# Impulsor

## 1. Configuration

Making a vehicle use the impulsor framework is very straightforward. Previous iterations required calling the `ls_vehicle_fnc_impulsorMonitor` function, this is no longer the case. This function is no longer used, but kept for backwards compatibility.

Here is an example setup for the impulsor framework using default values:

```cpp
// This class contains default values for impulse settings
// It is strongly encouraged to use this class or inherit
// from the ls_impulsor class of a vehicle itself.
class ls_impulsor_base {
    enabled = 1; // 0-Disabled, 1-Enabled

    // CfgSounds class to play when impulse is activated
    impulseSoundOn = "ls_impulseOn_laat";
    // CfgSounds class to play when impulse is de-activated
    impulseSoundOff = "ls_impulseOff_laat";
    repulseSoundOn = ""; // Same but for repulse
    repulseSoundOff = ""; // Same but for repulse

    // List of class names for impulsor modes
    // These names are arbitrary, and the current mode is stored as a number which is the index in this array.
    // E.g. -2 is repulse, -1 is disabled, 0 is "impulsor", and 2 is "overcharge"
    levels[] = {"impulsor", "overcharge"};
    class impulsor {
        speed = 400; // Speed in km/h
        fuelDrain = 0.0001; // Percent of fuel used every 1/2 seconds
    };
    class overcharge {
        speed = 600;
        fuelDrain = 0.0003;
        cooldown = 60; // Time in seconds before this mode (or any higher mode) can be used after turning it off
        isOvercharge = 1; // Enables engine damage chance and mode cooldown: 0-false, 1-true
    };
};

class CfgVehicles {
    class ls_laati;
    class TAG_myLAATi: ls_laati {
        class ls_impulsor: ls_impulsor_base {
            // Whatever changes you'd like here
        };
    };
};
```

## 2. Events

### 2.1 Listenable

| Name                       | Description                          | Arguments                                                       | Global / Local |
| -------------------------- | ------------------------------------ | --------------------------------------------------------------- | -------------- |
| `ls_impulsor_activated`    | Vehicle's impulsor is activated.     | `[_vehicle, _impulseSettings]`                                  | Global         |
| `ls_impulsor_deactivated`  | Vehicle's impulsor is deactivated.   | `[_vehicle, _impulseSettings]`                                  | Global         |
| `ls_impulsor_levelChanged` | Vehicle's impulsor level is changed. | `[_vehicle, _impulseSettings, _impulseLevel, _oldImpulseLevel]` | Local          |

## 3. Variables

| Name                           | Description                            | Type    |
| ------------------------------ | -------------------------------------- | ------- |
| `ls_impulsor_active`           | Whether the impulsor is active or not. | Boolean |
| `ls_impulsor_level`            | The current impulsor mode.             | Number  |
| `ls_impulsor_overchargeActive` | Whether overcharge is active or not.   | Boolean |