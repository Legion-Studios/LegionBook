---
description: >-
  Legion Studios' "lighting" framework, allowing modders to add built in lights
  to different pieces of equipment.
---

# Lighting (Headlamps)

This system has gone through a complete rewrite, and has not been kept backwards compatible for the sake of new functionality and better code overall. If you've made changes in your own mods, you will need to update them for their effects to take place.

### 1. Configuration

### 1.1 Adding a flashlight to equipment

The lighting framework currently supports helmets, goggles (facewear), uniforms, and vests. Configuration is consistent between all types of gear.

Example One:

```cpp
class CfgWeapons {
    class TAG_myHelmet {
        class ls_lighting {
            enabled = 1; // 0-Disabled, 1-Enabled
            // Array of CfgVehicles classes, explained further below
            lightModes[] = {
                "ls_lighting_whiteHigh", "ls_lighting_whiteLow",
                "ls_lighting_redHigh", "ls_lighting_redLow",
                "ls_lighting_blueHigh", "ls_lighting_blueLow"
            };
            // CfgSounds class to play when turning on the light
            soundOn = "ls_lighting_activationRepublic";
            // CfgSounds class to play when turning off the light
            soundOff = "ls_lighting_deactivationRepublic";
            // CfgSounds class to play when changing the light mode
            soundToggle = "ls_lighting_toggle";

            sources[] = {"center"}; // Array of class names for where to spawn lights
            class center {
                attachBone = "head"; // Bone to attach the light to
                attachBoneFollow = 1; // 0-Don't rotate with bone, 1-Rotate with bone
                attachOffset[] = {0, 0, 0}; // Offset to spawn light at (OPTIONAL)
                attachVectorDir[] = {0, 0, 0}; // Direction vector (OPTIONAL)
                attachVectorUp[] = {0, 0, 0}; // Up vector (OPTIONAL)
            };
        };
    };
};
```

Example Two:&#x20;

Here's a second example showing how to set up multiple lights. All lights will always be in the same light mode.

```cpp
sources[] = {"left", "right"};
class left {
    attachBone = "head";
    attachBoneFollow = 1;
    attachOffset[] = {-1, 0, 0};
    attachVectorDir[] = {0, 0, 0};
    attachVectorUp[] = {0, 0, 0};
};
class right: left {
    attachOffset[] = {1, 0, 0};
};
```

### 1.2 Adding a custom light mode

Light modes for gear are handled via `CfgVehicles` classes with `Reflectors` defined. This approach requires less caching on our end to keep scripts performant as well as allowing more functionality to be added since they behave like any other object. This also keeps our system up to date with any possible additions to the Reflectors class, since the engine would automatically apply any effects.

Here's a quick example of how to create your own custom light mode, this one being purple.

```cpp
class CfgVehicles {
    class Lamps_base_f;
    class ls_lighting_default: Lamps_base_f {
        class Reflectors {
            class Light_1;
        };
    };
    class TAG_myLightMode: ls_lighting_default {
        displayName = "My Cool Light Mode"; // Used in the ACE Arsenal stat
        class Reflectors {
            class Light_1: Light_1 {
                color[] = {255, 0, 255}; // R, G, B - This makes a purple light
            };
        };
    };
};
```
