---
description: Legion Studios' viv "framework" to make loading vehicles easier for pilots.
---

# Vehicle-In-Vehicle Loading

For easier reading, "**carrier**" will refer to the vehicle trying to load a vehicle(s) using the vehicle-in-vehicle (ViV) system.

The actions, ACE Actions, etc. described here apply to the Legion Studios LAAT/i and LAAT/c and any vehicle that inherits from them. Other mods may remove these actions in their own vehicles.

## 1. Usage

If a nearby object can be loaded, the pilot or co-pilot is able to us the "Load vehicle" scrollwheel action. This will load the closest vehicle to the carrier's loading point (typically near the rear of the vehicle). The distance to load objects is customizable via a setting. To unload a vehicle, use the "Unload all vehicles" action from vanilla, which will slowly unload all loaded vehicles.

### 1.1 ACE Compatibility

If ACE is loaded, there will be ACE Actions for (un)loading vehicles, similar to the vanilla ones, as well as child actions to (un)load specific vehicles. This makes it easier to act on specific vehicles if there are multiple vehicles nearby. For loading vehicles, the distance (in meters) will also be displayed to make it easier to identify specific vehicles.

This functionality is simply not possible in vanilla.



## 2. Keybinds

| Name                | Description                            | Default Key |
| ------------------- | -------------------------------------- | ----------- |
| Load Vehicle        | Loads the closest compatible vehicle.  | None        |
| Unload All Vehicles | Unloads all currently loaded vehicles. | None        |

## 3. Settings

| Name                  | Description                                                   | Default Value |
| --------------------- | ------------------------------------------------------------- | ------------- |
| Default Loading Range | The default range (in meters) for loading a vehicle with ViV. | 5             |
