
### What are kernel modules?

Kernel modules are pieces of code that can be loaded into the Linux kernel at runtime to extend its functionality—like drivers for hardware devices (e.g., USB, audio, network cards).



The `lsmod` command displays the status of **loaded kernel modules**.

When you run `lsmod`, you get a list with columns like this:
```
Module                  Size  Used by
i915                   252800  2
drm_kms_helper         180224  1 i915
```
- **Module**: Name of the kernel module.
- **Size**: Size of the module in bytes.
- **Used by**: Number of times the module is being used, and (sometimes) which other modules depend on it.

**Related commands:**
- `modinfo <module>` — Get detailed info about a specific module.
- `modprobe <module>` — Load a module into the kernel.
- `rmmod <module>` — Remove a module from the kernel.