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
class CfgVehicles {
    class ls_laati;
    class TAG_myLAATi: ls_laati {
        ls_impulsor_enabled = 1; // 0-Disabled, 1-Enabled
        ls_impulsor_boostSpeed_1 = 400; // Impulse speed in km/h
        ls_impulsor_boostSpeed_2 = 600; // Overcharge speed in km/h
        // Percentage of fuel used per 1/2 second when using impulse
        ls_impulsor_fuelDrain_1 = 0.0001;
        // Same for but overcharge
        ls_impulsor_fuelDrain_2 = 0.0003;
        // CfgSounds class to play when impulse is activated
        ls_impulsor_impulseSoundOn = "ls_impulseOn_laat";
        // CfgSounds class to play when impulse is de-activated
        ls_impulsor_impulseSoundOff = "ls_impulseOff_laat";
        // CfgSounds class to play when repulse is activated
        ls_impulsor_repulseSoundOn = "";
        // CfgSounds class to play when repulse is de-activated
        ls_impulsor_repulseSoundOff = "";
        // Time in seconds before overcharge can be used after turning it off
        ls_impulsor_overchargeCooldown = 60;
    }; 
};
```

**NOTE**: The config setup may receive an overhaul for better naming conventions and better organization.

## 2. Events

### 2.1 Listenable

| Name                       | Description                          | Arguments                                                       | Global / Local |
| -------------------------- | ------------------------------------ | --------------------------------------------------------------- | -------------- |
| `ls_impulsor_activated`    | Vehicle's impulsor is activated.     | `[_vehicle, _impulseSettings]`                                  | Global         |
| `ls_impulsor_deactivated`  | Vehicle's impulsor is deactivated.   | `[_vehicle, _impulseSettings]`                                  | Global         |
| `ls_impulsor_levelChanged` | Vehicle's impulsor level is changed. | `[_vehicle, _impulseSettings, _impulseLevel, _oldImpulseLevel]` | Local          |
