---
description: >-
  Legion Studios' active camo feature, allowing players to camoflauge themselves.
---

# Active Camoflauge

## 1. Usage

Legion Studios' active camo system is added to the Katarn series armor sets, DC-17M, its magagazines and attachments, and the DC-15SA. To activate active camo, you can use the keybind (unbound by default). If ACE is loaded, there is also a self interaction under Equipment.

For mission makers, there is a "Toggle Active Camo" Zeus module to (de)activate active camo for units.

In order to activate active camo, your uniform must be configured to use system. All other items will be replaced with their active camo versions, or left the same if no camo version is found.

## 2. Keybinds

| Name               | Description                | Default Key  |
| ------------------ | -------------------------- | ------------ |
| Toggle Active Camo | Toggle active camo on/off. | Unbound      |

## 3. Settings

| Name                        | Description                                                                          | Default Value |
| --------------------------- | ------------------------------------------------------------------------------------ | ------------- |
| Enabled                     | If enabled, players will be able to activate active camo on configured armor sets.   | True          |
| Camo Coefficient            | Coefficient for a unit's camo skill when using active camo. Lower = more hidden.     | 0             |
| Cooldown After Deactivating | Time in seconds after deactivating before active camo can be re-activated.           | 5             |
| Allow Firing                | If enabled, players will be able to activate active camo on configured armor sets.   | True          |
| Maximum Allowed Hits        | Allowed number of hits a player can take when in active camo. -1 = Don't deactivate. | 5             |