---
title: Snaps and Snapd
---

# Introduction

*Snap* is the latest packaging format and the go-to format for distributing software in Ubuntu and many other Linux distributions. This includes Ubuntu Core (IoT) and classic Ubuntu (Desktop, Server, cloud, IoT).

*Snapd* is the daemon that controls snaps, avialable on all Ubuntu and on most Linux distributions. 

Snaps and snapd are documented, designed, and discussed extensively on [snapcraft.io](https://snapcraft.io).

Let's do a quick overview of some basics.

# Snaps

Snap is the native Ubuntu Core packaging system. There is no Debian package support in the runtime of Ubuntu Core. And, Snaps are increasingly used in classic Ubuntu flavours and other Linux distributions. 

Snaps solve multiple problems at the same time:

 - It’s easy to package applications pulled from multiple upstream sources using diverse build systems.
Each snap includes its own dependencies, freeing publishers from problems when  implicit dependencies change without their knowledge.
 - Developers publish snaps in a snap store (the global snap store or a private Brand store) and take responsibility for their quality, making software distribution fast and free of procedural obstacles.
 - Snaps are sandboxed from each other and from the OS, providing system stability and overall security. Powerful slot-and-plug (“interface”) capabilities enable content sharing of all kinds, including data, sockets, D-Bus and much more. 
 - Snaps use simple declarations for system access (for example network or GPIO), and IoT product developers control whether and how this access is granted. 
 - Automatic roll-backs to a previous installed revision occur if a snap upgrade issue arises, with manual reversion as needed.

All you need to do is write a snapcraft.yaml file and you can build a snap from diverse upstream repositositories with a wide range of build plugins (autotools, go, ROS, and many moreO. 

## Snap types

| Snap Type | UC16       | UC18 | Classic | Comment |
| ----------|------------|--------------|------------|--|
| Kernel    | ✔                 | ✔                     | Debian | |
| Gadget    | ✔                 | ✔                     | optional | |
| Core      | ✔ ("core") | ✔ ("core18") | | The rootfs |
| Snapd     |            | ✔                     | Debian | |
| App       | ✔                 | ✔                     | ✔ | |

## Confinement

Snaps are confined by snapd on both Ubuntu Core and classic Ubuntu. This means that snaps run in a limited environment created separately for each snap. The snap's view of the rootfs is restricted, and their ability to modify any files is restricted. Access to system calls, hardware, and various parts of the file system is severly restricted by default. 

### Interfaces allow access

*Interfaces* allow snaps to escape confinement in specific ways to access the system, hardware, files, etc. 

Interfaces are defined in snapd and consiste of a plug and a slot. Many slots are defined in the Core/Core18 snaps so they are always available. Applications can also declare some plug types. Application snaps can declare plugs. When the interface plug is connected to the interfcace slot, the snap gains access to what is defined for the interface. 

Many interfaces automatically connect (for example the *network* interface.) On boot up, snaps with auto connecting interfaces *just work,* and have access through the internface. 

Many interfaces do not auto connect (they grant too much power). These can be connected in varoius ways. 

 - They can be connected from terminal
 - Brand Store owners can configure autoconnection
 - They can be connected from Gadget snaps


## Base snaps

Ubuntu Core 18 introduces *bases*. A base provides a rootfs snap (either "core" or "core18). An Ubuntu Core 18 image includes the "core18" snap, and an Ubuntu Core 16 image contains the "core" snap.

An application snap can specify its base. If the base is not present, it is installed as needed. For example, if you installed an app snap that specifies a core18 base on a core16 system, or an a classic system, the core18 snap is automatically installed, and that application snap uses the core18 snap's rootfs as it's runtime root file system.






