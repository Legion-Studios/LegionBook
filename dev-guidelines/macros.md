# Macro Usage

Legion Studios uses the CBA macro library, things like `QPATHTOF` for file paths, `GVAR` for (most) global variables, and `FUNC` for functions. These macros make development easier by reducing the amount that developers need to write. They also force things to be named consistently.

This section won't cover *all* of the macros we use, but will cover the most common ones that we use.

## Common
Common macros that are often used in other macros.

1. `QUOTE` - Takes a single parameter and puts double quotes (`"`) around it.
    - `QUOTE(a)` -> `"a"`
    - Macros that begin with `Q` almost always have their output wrapped in quotes. E.g. `QGVAR(a)` = `QUOTE(GVAR(a))`
2. `DOUBLES` - Takes two parameters and combines them using an underscore.
    - `DOUBLES(a,b)` -> `"a_b"`
3. `TRIPLES` - Same as `DOUBLES`, but takes three parameters.
    - `TRIPLES(a,b,c)` -> `"a_b_c"`

## File Paths
The `PATHTOF`, "path to file", series of macros shorten file paths; it helps prevent typos since there is less to write and the beginning of the file path is always consistent.

These macros will path to the current addon, but there are also `PATHTOEF` versions of these macros which path to an *external* file (i.e. another addon). These macros will also point to the *current subaddon* instead of the parent addon if working in a subaddon.

E.g. using `QPATHTOF` in the characters addon will result in `"\ls\core\addons\characters\..."`, but using it any of the `characters_X` subaddons will instead result in `"\ls\core\addons\characters_X\..."`. In cases where a leading slash should not be used, use the `PATHTOF2` version of the given macro instead.

Examples:

PATHTOF
1. `PATHTOF(data\camo1_co.paa)` -> `\ls\core\addons\<addon>\data\camo1_co.paa`
2. `PATHTOF2(data\camo1_co.paa)` -> `ls\core\addons\<addon>\data\camo1_co.paa`
3. `QPATHTOF(data\camo1_co.paa)` -> `"\ls\core\addons\<addon>\data\camo1_co.paa"`
4. `QPATHTOF2(data\camo1_co.paa)` -> `"ls\core\addons\<addon>\data\camo1_co.paa"`

PATHTOEF
1. `PATHTOEF(common,data\camo1_co.paa)` -> `\ls\core\addons\common\data\camo1_co.paa`
2. `PATHTOEF2(common,data\camo1_co.paa)` -> `ls\core\addons\common\data\camo1_co.paa`
3. `QPATHTOEF(common,data\camo1_co.paa)` -> `"\ls\core\addons\common\data\camo1_co.paa"`
4. `QPATHTOEF2(common,data\camo1_co.paa)` -> `"ls\core\addons\common\data\camo1_co.paa"`

## Global Variables
For global variables, we use the `GVAR` series of macros. Which adds the current addon's name to the beginning of the variable. E.g. `GVAR(enabled)` -> `ls_common_enabled`. Similar to `PATHTOF`, there are also quoted and external versions of these macros as well (`QGVAR` and `EGVAR` respectively).

## Function Names
Functions will use the `FUNC` series of macros, which function similarly to `GVAR` but add a `fnc_` in the name to denote that it is a function. E.g. `FUNC(dummy)` -> `ls_common_fnc_dummy`. Similarly to `PATHTOF`, there are quoted and external versions of these macros as well (`QFUNC` and `EFUNC` respectively).
