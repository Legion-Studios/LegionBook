---
description: >-
  Legion Studios' "map" framework, making changes / additions to the map display.
---

# Map

Adds custom map icons for configured objects, mostly for large capital ships to make their presence felt more.

## 1. Configuration

```cpp
class CfgVehicles {
    class myShip {
        ls_map_icon = "\path\to\icon_ca.paa"; // Icon to display on the map

        /*
        Optional, uses displayName if not set.
        Can be used to remove the name from the map at all, or to use a different name.
        E.g. "Acclamator (Landed)" vs "Landed Acclamator"
        */
        ls_map_name = "My Ship";

        /*
        Optional, size in meters of the object.
        Uses first visual lod bounding box size if not defined or set to -1.
        Mutli-part structures require setting this explicitly since they either don't have a visual lod or its empty.
        As a fallback, you can use the memory lod as a semi-accurate measure:

        (boundingBoxReal [_yourObject, "MEMORY"]) select 2
        */
        ls_map_size = 100;
    };
};
```
