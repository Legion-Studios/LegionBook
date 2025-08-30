---
description: >-
  Legion Studios' skills framework, including how to use it and adding restrictions.
---

# Skills

The skills framework aims to make mission and mod makers able to easily check if a unit has the skills in a certain field, like piloting, driving, or slicing / hacking.

Skills like medic, engineer, and EOD are compatible with vanilla and ACE.

## 1. Getting / setting a skill
### 1.1 Config
Skills like tech specialist, pilot, and crewman can be set via config.
```cpp
class YourPrefix_allTheSkills_unit {
    ls_common_pilot = 1;
    ls_common_crewman = 2;
    ls_common_tech = 0;
};
```

### 1.2 Script
You can check if a unit has a certain level of skill by using `ls_common_fnc_getSkill`. You can also supply a certain level, though some skills only have untrained / trained states (e.g. EOD).

This is also open ended, meaning you can easily add your own new skills if you'd like.

```sqf
// "medic" is the skill being checked, 2 is the minimum level needed
private _isDoctor = [player, "medic", 2] call ls_common_fnc_getSkill;
```

```sqf
// Sets engineer level to 1
[player, "engineer"] call ls_common_fnc_setSkill;
// Sets engineer level to 2
[player, "engineer", 2] call ls_common_fnc_setSkill;
```

For skills that don't have special handling (i.e. like setting ACE variables), a variable is just set on the unit named `"ls_skill_<name>"` with the given level that was passed.

If you need to do your own special handling, see the events section below.

## 2. Events

There are the `ls_common_skillSet` and `ls_common_skillGet` CBA events that allow modders to do additional handling if needed.

### 2.1 Additional handling for skills

If something needs additional handling, the `ls_common_skillGet` event runs each time that `ls_common_fnc_getSkill` is ran, so you can check additional conditions if the single variable isn't enough.

Here's an example of the medic skill being checked as an event handler. Medic is already handled by Legion so this is just an example.

```sqf
// This would be added in something like an initPlayerLocal.sqf
["ls_common_skillGet", {
    params ["_unit", "_skill", "_level", "_return"];

    // If the unit has the vanilla medic trait, also set the
    if (_skill == "medic" && _unit getUnitTrait "medic") then {
        _this set [3, true]; // modify the return value of the getSkill function
    };
}] call CBA_fnc_addEventHandler;
```

### 2.2 Restricting skills

You can use these events to restrict certain skills from being used together. Here's an example that would remove a player's engineer permissions if they're getting medic perms.

```sqf
// This would be added in something like an initPlayerLocal.sqf
["ls_common_skillSet", {
    params ["_unit", "_skill", "_level"];

    // Removes a player's engineer permissions if they would get medic permissions
    if (isPlayer _unit && _skill == "medic" && { [_unit, "engineer"] call ls_common_fnc_getSkill }) then {
        [_unit, "engineer", 0] call ls_common_fnc_setSkill;
    };
}] call CBA_fnc_addEventHandler;
```
