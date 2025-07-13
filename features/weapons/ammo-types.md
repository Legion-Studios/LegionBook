---
description: Custom scripted ammo functionality
---

# Ammo Types

Ammo can have extra functionality added to them by setting the `ls_weapons_ammoType` property in the ammo's (`CfgAmmo`) config.

## Stun
```cpp
ls_weapons_ammoType = 1;
ls_weapons_stunDuration = 10; // Time in seconds
```

Stun rounds stun organic units (humans, aliens, etc.) for a configurable amount of time. Stun rounds have no affect on holograms.

Used by: Stun Round Magazine

## Ion
```cpp
ls_weapons_ammoType = 2;
ls_weapons_stunDuration = 10; // Time in seconds
ls_weapons_ionEngineDamage = 0.05; // % of engine damage
ls_weapons_ionFuelBurn = 0.05; // % of fuel to drain
```

Ion rounds act similarly to stun rounds but for inorganic units (droids, etc.). If an ion round hits a vehicle, the round will damage the engine and burn a percentage of the vehicle's fuel.

Used by: Ion Round Magazine

## Ragdoll
`ls_weapons_ammoType = 3`

Ragdoll rounds will ragdoll an enemy when they are hit.

Used by: Caltrops, Caltrops Dispenser
