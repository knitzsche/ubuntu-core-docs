---
title: Connecting Interfaces
table_of_contents: true 
---

# Introduction

As explained on [snapcraft.io](https://snapcraft.io/docs/interface-management), snapd provides a set of [interfaces](https://snapcraft.io/docs/supported-interfaces) through which confined snaps can obtain access to otherwise blocked parts of the system. 

Many interfaces auto connect simply through a snap declaring the plug in its snapcraft.yaml. (Check the docs linked above to determine which interfaces auto connect.). For example, a snap that simply declares the `network` plug in its snapcraft.yaml auto connects to the `network` interface on install, thus allowing the snap access to everything provided by this interface. 

Other interfaces do not auto connect. This projects systems by requiring the user to take an action to connect the interface.  

However, there are additional methods to auto connect such interfaces reserved for Brand customers.

## Auto connecting from the Brand Store

Brand Stores provide a user interface through which users with the proper permissions can configure many such interfaces to auto connect. See [Auto conneting from a Brand Store](../store/connecting_interfaces.md). 

## Auto connecting through the Support portal

Brand customers can request auto connecting through their Support portal. 

Indeed, this is the only method for auto connecting hardware related interfaces.

## Autoconnecting through the gadget snap

The gadget.yaml file in a gadget snap enbables auto connecting specified interfaces. 

**Note** Gadget snaps can only be published in Brand Stores. 

TBD: explain how.
