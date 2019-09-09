---
title: Ubuntu for IoT
---

# Ubuntu Core for IoT

Ubuntu Core is the newest Ubuntu operating system (OS). It primarily targets
the requirements of headless IoT devices and their distributors. It is a
minimalist rendition of Ubuntu that is lightweight, highly secure, and
transactionally updated. Every application and data are isolated from every
other application and data.

An Ubuntu Core system is built using snaps: a core snap, a kernel snap, a gadget
snap, and one or more application snaps. Canonical provides
reference snaps and OS images for some current best-of-breed IoT platforms. 
You can also roll your own image. 

Ubuntu Core uses a rolling release model that
aligns with Ubuntu LTS releases. The latest Ubuntu Core is currently UC16 and is
based on the 16.04 long-term support (LTS) release of classic Ubuntu, and UC18, aligned with 18.04 LTS. 

## Ubuntu Core features

 - Faster, more reliable, with stronger security guarantees for applications and
   users compared to a traditional Linux distribution.
 - Atomic transactional upgrades for applications and the OS itself, all of which
   can be rolled back if needed automating most maintenance and upgrades.
 - Separation of OS and application files into sets of distinct read-only images,
   to easily and securely add multiple applications and additional functionality onto a device.
 - Applications are distributed via snaps, a simple application packaging system
   that makes it easy for developers to build and distribute applications across
   many Linux distributions from a public or private app store.
 - Public/private key-based validation and authentication is built-in at every
   stage, proving that what runs is exactly what OS and app developers intend.

# Ubuntu Classic for IoT

Classic Ubuntu includes the traditional Ubuntu Desktop, Ubuntu Server and 
Ubuntu Cloud distributions. These well-known Ubuntu versions have broad
support for various device configurations including user-interactive desktop
systems, enterprise server systems and Internet of Things (IoT) devices.

Ubuntu Desktop, Server and Cloud are widely deployed across diverse public and
private sectors by millions of people and thousands of organizations. Built
from the common Ubuntu Debian package archives, they are well-known, time-tested
and proven in the field.

While one can use classic Ubuntu on IoT devices, Ubuntu Core provides many features that make it a better fit. 


# Core and classic compared

|                      | Core                                                                                                     | classic                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Minimum requirements | 500 MHz single core processor256 MB RAM512 MB storage                                                    | 1 GHz dual core processor512 MB RAM1.5 GB storage                                                                                                              |
| Graphical UI         | None by default (can utilize Wayland or Mir)                                                             | Xorg and GNOME Shell or Wayland and GNOME Shell                                                                                                                |
| Package system       | snaps                                                                                                    | Debs & snaps                                                                                                                                                   |
| Application security | Isolation via AppArmor and Seccomp                                                                       | Traditional user and group permissions (for Debs);Strict isolation via AppArmor and Seccomp for snaps;Transitional security with classic confinement for snaps |
| Updates              | Pushed from the Global (public) store & optionally a Brand (private) store;All updates are transactional | Traditional apt repository updates;Also from public store & optionally Brand store for snaps;Updates for snaps are transactional                               |



