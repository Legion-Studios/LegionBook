---
description: >-
  Legion Studios' skills framework, showing how to use / add your own skills.
---

# Skills

The skills framework aims to make it easier on mission / mod makers to check for things like if a unit is a medic, pilot, tank driver, etc.

Legion's skill framework will handle setting vanilla / ACE skills when used, e.g. using ACE's `ace_medical_medicClass` variable when using the `"medic"` skill.

## 1. Unit skill levels

To get the skill level of a unit, use the `ls_common_fnc_getSkill` function.

```sqf
private _medicLevel = [player, "medic"] call ls_common_fnc_getSkill;

private _message = [
    "Player is untrained in medical",
    "Player is a medic",
    "Player is a doctor"
] select _medicLevel;
systemChat _message;
```

To set a level in a certain skill, use `ls_common_fnc_setSkill`. This sets the player as an advanced engineer in vanilla / ACE.
```sqf
[player, "engineer", 2] call ls_common_fnc_setSkill;
```

To check if a unit possesses a certain skill level, you can use `ls_common_fnc_checkSkill`, which returns true if the unit has a greater than or equal skill level to the one given. This is just a shorthand for: `([player, "skillName"] call ls_common_fnc_getSkill) >= _requiredLevel`.

Checks if the player has at least a level 1 tech skill.
```sqf
[player, "tech", 1] call ls_common_fnc_checkSkill;
```

## 2. Configuration

### 2.1 Adding a custom skill

Adding a skill on its own is very easy and nothing is explicitly needed, you can just use `[_unit, "yourSkillName"] call ls_common_fnc_setSkill` and it will set the necessary variable that you can use with `ls_common_fnc_getSkill` and `ls_common_fnc_checkSkill`.

To have your skill appear in the Zeus module, you can add some data to the `ls_skills` config class. For example you could make a "leadership" skill to denote if a unit is an NCO / command member.
```cpp
class ls_skills {
    class default;
    class leader: default {
        scope = 2;
        name = "Leadership";
        tooltip = "Unit's skill in leading and commanding others.";
    };
};
```

## 3. Functions

### 3.1 `ls_common_fnc_setSkill`
#### Description
Sets a certain skill level for a unit.

#### Parameters
| Index | Description | Datatype(s) | Default Value |
| ----- | ------------| ----------- | ------------- |
| 0     | Unit        | Object      |               |
| 1     | Skill name  | String      |               |
| 2     | Skill level | Number      | 1             |

#### Return Value
None

### 3.1 `ls_common_fnc_getSkill`
#### Description
Returns a unit's skill level.

#### Parameters
| Index | Description | Datatype(s) | Default Value |
| ----- | ------------| ----------- | ------------- |
| 0     | Unit        | Object      |               |
| 1     | Skill name  | String      |               |

#### Return Value
Unit's skill level

### 3.2 `ls_common_fnc_checkSkill`
#### Description
Checks if a unit has a certain skill.

#### Parameters
| Index | Description | Datatype(s) | Default Value |
| ----- | ------------| ----------- | ------------- |
| 0     | Unit        | Object      |               |
| 1     | Skill name  | String      |               |
| 2     | Skill level | Number      | 1             |

#### Return Value
True if unit's skill level is greater than or equal to given skill level, otherwise false.

## 4. Examples

Get a list of all advanced BLUFOR pilots
```sqf
private _bluforPilots = ([] call CBA_fnc_players) select {
    side group _x == west && {
        // 0 = untrained, 1 = trained, 2 = advanced
        [_x, "pilot", 2] call ls_common_fnc_checkSkill;
    };
};
```
