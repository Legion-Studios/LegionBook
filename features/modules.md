---
description: >-
  Legion Studios' modules for Eden and Zeus.
---

# Modules
Descriptions and instructions for how to use the various models added by Legion Studios.

Some more complicated modules are detailed separately

## Add Reinsert Action
Available in: Eden ✅ | Zeus ✅

### Description
Adds the "Notify Pilots" scroll wheel action to the specified object(s). Using the scroll wheel option will display a message to all players with the "Pilot" skill, see [skills](skills.md) for more information.

### How to use
#### Eden
1. Select the module
2. Place the module anywhere
3. Synchronize any object(s) you'd like to the module
#### Zeus
1. Select the module
2. Place the module on an object

## Aircraft Spawner
Available in: Eden ✅ | Zeus ❌

### Description
Continiously spawns selected aircraft at the module's position, with options for when to spawn waves, the size of the waves, and vehicle types to spawn..

### How to use
1. Select the module
2. Place the module at the position aircraft should spawn near
   - Aircraft will spawn with a horizontal and vertical offset from the module to prevent crashing into each other
3. Place a trigger with an area
   - This is what activate the module and begin spawning aircraft
4. Set the trigger's activation conditions
   - E.g. "Any Player Present"
5. Sync the trigger to the module
6. Sync the module to any object(s) you want to deactivate the module
   - Once activated, the spawner will keep spawning vehicles until all the synced objects are destroyed
   - Any object can be synced, e.g. units, vehicles, props, etc.
   - At least one object **must** be synced, the module will never activate if no objects beside the trigger are synced.

![Aircraft spawner eden module](../features/assets/modules/aircraftSpawner_eden.gif)

## Area Heal
Available in: Eden ✅ | Zeus ❌

### Description
Creates a healing area that will heal players when they enter it.

### How to use
1. Select the module
2. Place the module anywhere
3. Adjust the module's size and position to change the healing area

## Breach Door
Available in: Eden ❌ | Zeus ✅

### Description
Orders an AI unit to breach a nearby closed door. The selected AI will walk up to the closest door (based on the options selected), place a breaching charge on the door, and return to their original group / position. The charge will then explode, breaching the door.

### How to use
1. Select the module
2. Place the module on a unit
3. Select OK

## Delete Groups
Available in: Eden ❌ | Zeus ✅

### Description
Deletes empty groups that are marked as "deleteable" by the engine. The module runs on all machines and will delete groups on all machines, and then give the user a count of how many groups were deleted on *their* machine.

### How to use
1. Select the module
2. Place the module anywhere

## Droid Dispenser
Available in: Eden ✅ | Zeus ✅

See [Droid Dispensers](dispensers.md#zeus)

## Mount AT-RT
Available in: Eden ❌ | Zeus ✅

### Description
Orders an AI to mount an AT-RT. If no available AT-RT is nearby, then a message will be displayed.

### How to use
1. Select the module
2. Place the module on a unit
3. Select OK
4. If [ACE](https://steamcommunity.com/workshop/filedetails/?id=463939057) is loaded, select a position near an AT-RT and the unit will mount that AT-RT.
5. If ACE is not loaded, the AI will mount a nearby AT-RT.

## Dismount AT-RT
Available in: Eden ❌ | Zeus ✅

### Description
Orders an AI to dismount their AT-RT.

### How to use
1. Select the module
2. Place the module on a unit riding an AT-RT **or** an AT-RT with a rider
3. Select OK

## Set Skills
Available in: Eden ❌ | Zeus ✅

See [Skills](skills.md#id-1.2-zeus-module)

## Toggle Camo
Available in: Eden ❌ | Zeus ✅

### Description
Toggles a unit's active camoflauge.

### How to use
1. Select the module
2. Place the module on a unit
   - If the unit has an active camo-compatible uniform, they will activate it.
   - If not, a message will display and nothing will happen.
