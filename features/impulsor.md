---
description: >-
  Legion Studios' impulsor framework, allowing vehicles to move much faster at
  the cost of fuel.
---

# Impulsor

## 1. Usage

Legion Studios' impulsor system is added to the LAAT/i, HMP, and LAAT/le and any vehicle that inherits from them. To activate a vehicle's impulse, you can either use the keybinds or scroll wheel actions added to Legion Studios vehicles.

The keybinds will always work for compatible vehicles, however some mods may remove the scroll wheel actions for their own vehicles.

### 1.1 Impulse Requirements

In order for a vehicle's pilot to activate impulse, the vehicle must:

* Have its engine on, and in good condition (yellow or better)
* Have fuel
* Be airborne

## 2. Overcharge

"Overcharge" can be activated by using increasing the impulse level (i.e. using the keybind or scroll wheel action). Overcharge pushes the vehicle's engine to the limit and grants more speed, but is only intended for short periods of time to escape danger. Using overcharge has a (configurable) chance to damage the engine while it is being used and uses more fuel compared to normal impulse.

When disabling overcharge, a cooldown, 60 seconds by default, will start and prevent overcharge from being used until the timer ends.

## 3. Keybinds

| Name                     | Description                                                                         | Default Key             |
| ------------------------ | ----------------------------------------------------------------------------------- | ----------------------- |
| Activate Impulsor        | Increases the ship's impulsor level.                                                | Ctrl + Mouse Wheel Up   |
| Overcharge Damage Chance | Decreases the ship's impulsor level, or activates repulsor if impulsor is disabled. | Ctrl + Mouse Wheel Down |

### 3.1 Alternate Keybinds

For those who use an input device other than mouse and keyboard, you can assign inputs from your controller to the vanilla "Custom Controls" keybinds. Then in CBA's keybind menu, you can assign one of the custom control keys to a CBA keybind.

This allows you to use flight sticks, console controllers, etc. for CBA keybinds.

## 4. Settings

| Name                     | Description                                                                                 | Default Value |
| ------------------------ | ------------------------------------------------------------------------------------------- | ------------- |
| Hint Display             | Changes the type of the impulse display.                                                    | "Hint"        |
| Overcharge Damage Chance | When using overcharge, this is the chance that the engine will be damaged every 10 seconds. | 50%           |
