---
title: Ubuntu Classic for IoT
---

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


## Core and classic compared

|                      | Core                                                                                                     | classic                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Minimum requirements | 500 MHz single core processor256 MB RAM512 MB storage                                                    | 1 GHz dual core processor512 MB RAM1.5 GB storage                                                                                                              |
| Graphical UI         | None by default (can utilize Wayland or Mir)                                                             | Xorg and GNOME Shell or Wayland and GNOME Shell                                                                                                                |
| Package system       | snaps                                                                                                    | Debs & snaps                                                                                                                                                   |
| Application security | Isolation via AppArmor and Seccomp                                                                       | Traditional user and group permissions (for Debs);Strict isolation via AppArmor and Seccomp for snaps;Transitional security with classic confinement for snaps |
| Updates              | Pushed from the Global (public) store & optionally a Brand (private) store;All updates are transactional | Traditional apt repository updates;Also from public store & optionally Brand store for snaps;Updates for snaps are transactional                               |


