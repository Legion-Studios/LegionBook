---
description: >-
  Legion Studios' impulsor framework, allowing vehicles to move much faster at
  the cost of fuel.
---

# Impulsor

## 1. Configuration

Making a vehicle use the impulsor framework is very straightforward. Previous iterations required executing the `ls_vehicle_fnc_impulsorMonitor`, this is no longer the case and this function is no longer used, but kept for backwards compatibility.

Here is an example setup for the impulsor framework using default values:

```cpp
// This class contains default values for impulse settings
// It is strongly encouraged to use this class or inherit
// from the ls_impulsor class of a vehicle itself.
class ls_impulsor_base {
    enabled = 1; // 0-Disabled, 1-Enabled
    speed = 400; // Speed in km/h
    fuelDrain = 0.0001; // Percent of fuel used every 1/2 seconds
    overchargeSpeed = 600; // Same but for overcharge
    overchargeFuelDrain = 0.0003; // Same but for overcharge
    // Time in seconds before overcharge can be used after turning it off
    overchargeCooldown = 60;

    // CfgSounds class to play when impulse is activated
    impulseSoundOn = "ls_impulseOn_laat";
    // CfgSounds class to play when impulse is de-activated
    impulseSoundOff = "ls_impulseOff_laat";
    repulseSoundOn = ""; // Same but for repulse
    repulseSoundOff = ""; // Same but for repulse
}

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
