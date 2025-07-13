---
description: Custom scripted weapon functionality
---

# Weapon Types

Weapons can have extra functionality added to them by setting the `ls_weapons_weaponType` property in the weapon's config.

## Akimbo
`ls_weapons_weaponType = 1`

When the weapon is fired, the weapon will alternate between the first two muzzles that are defined in the weapon's `muzzle` property. E.g. `muzzles[] = {"right", "left"};`. The muzzle will only be selected if it has ammo remaining.

Used by: Dual DC-17S Pistols
