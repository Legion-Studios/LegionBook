---
description: Legion Studios' viv "framework" to make loading vehicles easier for pilots.
---

# Vehicle-In-Vehicle Loading

This "framework" consists of only a couple of functions that you could add to your vehicles. If your vehicle already inherits from the Legion Studios LAAT/i or LAAT/c and does not overwrite the `UserActions` and/or `ACE_SelfActions` classes, you do not need to add these actions.

## 1. Configuration

### 1.1 Vanilla

Here is an example of adding the "load vehicle" user action to a vehicle.

```cpp
class CfgVehicles {
    class Helicopter_Base_F;
    class Helicopter_Base_H: Helicopter_Base_F {
        class UserActions;
    };
    class TAG_myCarrier: Helicopter_Base_H {
        class UserActions: UserActions {
            class TAG_loadVehicle {
                displayName = "Load vehicle";
                position = "pilotcontrol";
                radius = 5;
                onlyForPlayer = 0;
                // "ViV_exit" is a memory point on the LAAT/c that is used as the
                // center for the vehicle "scan". You can leave this as-is, and it
                // will use the vehicle's center if undefined.
                condition = "[this, ls_player] call ls_common_fnc_isPilot and {[this, 'ViV_exit'] call ls_vehicles_fnc_vivCanLoad}";
            };
        };
    };
};
```

### 1.2 ACE

Here is an example on adding the "load vehicle" and "unload vehicle" actions to a vehicle.&#x20;

```cpp
class CfgVehicles {
    class Helicopter_Base_F;
    class Helicopter_Base_H: Helicopter_Base_F {
        class ACE_SelfActions;
    };
    class TAG_myCarrier: Helicopter_Base_H {
        class ACE_SelfActions: ACE_SelfActions {
            class TAG_loadVehicle {
                displayName = "Load vehicle";
                exceptions[] = {"isNotInside"};
                icon = "\A3\3DEN\data\cfgwaypoints\load_ca.paa";
                condition = "[_target_, _player] call ls_common_fnc_isPilot and {[_target] call ls_vehicles_fnc_vivCanLoad}";
                statement = "";
                insertChildren = "call ls_vehicles_fnc_vivLoad_insertChildren";
            };
            class TAG_unloadVehicle: TAG_loadVehicle {
                displayName = "Unload all vehicles";
                icon = "\A3\3DEN\data\cfgwaypoints\unload_ca.paa";
                condition = "getVehicleCargo _target isNotEqualTo [] and {[_target, _player] call ls_common_fnc_isPilot}";
                statement = "_target call ls_vehicles_fnc_vivUnload";
                insertChildren = "call ls_vehicles_fnc_vivUnload_insertChildren";
            };
        };
    };
};
```
