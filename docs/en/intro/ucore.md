---
title: About Ubuntu Core
table_of_contents: true 
---

# About Ubuntu Core

Let's provide a nice explanation of Ubuntu core here, more specific than the getting started page.

- All-snaps system
    - [Kernel snap](https://docs.snapcraft.io/the-kernel-snap/697)
    - [Gadget snap](https://docs.snapcraft.io/the-gadget-snap/696)
    - Base snap (Documentation pending)
    - Snapd snap
    - [Application snaps](https://docs.snapcraft.io/getting-started/3876)
- Confinement through Apparmor and Seccomp
- Interfaces to grant snaps modular access 
- ubuntu-image command to build image
- Auto rollback to previous installed revision
    - kernel rolled back if boot fails
    - core (base) rolled back if can't boot the OS
    - snapd rllback? TODO 

## No user needed

Ubuntu Core is designed to operate and without an additional user. Applications run as root user (confined by Apparmor and Seccomp). 

You can create a system-user by completing the console-conf wizard that displays on terminal on first boot (and on subsequent boots until it is completed).

**Note**: console-conf can be suppressed. Contact Canonical.

See System User content for more informoation.

## Ubuntu Core 18

Ubuntu Core 18 uses a different set of snaps than Ubuntu 16.

In Ubuntu Core 18, snapd itself is a snap, and it is required. (In ubuntu Core 16, snapd was provided in the rootfs provided by the Core snap.

Also, Ubuntu Core 18 introced the concept of a Base snap, and the base snap an image uses must be named in the image's model assertion.

Learn more about the Ubuntu Core 18 model assertion [here](https://forum.snapcraft.io/t/model-assertions-for-core18/6870). 

An Ubunt Core 18 system consists of the follow snap types:

- kernel
- gadget
- base (provides the rootfs)
- snapd
- application snaps

## Ubuntu Core 16

Ubuntu Core 16 is the first widely used version of Ubuntu Core. 

An Ubunt Core 16 system consists of the follow snap types:

- kernel
- gadget
- core (provides the rootfs and snapd)
- application snaps




