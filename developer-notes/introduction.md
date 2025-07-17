# Introduction

This section covers how we do development at Legion Studios. Including things like macro usage, scripting practices, and how we organize our mods.

While this is primarily intended for our developers, we leave this public so that other modders can learn better practices and how large mods can be organized.

## Rundown
Our main rules can be summarized as:
1. All global variables, including variables saved to objects; namespaces; displays; etc *must* be prefixed with `ls_`.
2. All classes not defined in a custom class must be prefixed with `ls_`.
   - E.g. biology classes don't need an `ls_` prefix because define the `ls_biologies` class that they are all contained in.
3. Avoid the scheduler *whenever possible*. We can avoid scheduled code in 99% of cases. If you don't know that you need to run something scheduled, you probably don't have to.
4. Do not use `remoteExec(Call)`. We use CBA events for networking to avoid issues and encourage better code.
