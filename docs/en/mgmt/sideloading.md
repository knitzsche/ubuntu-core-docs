---
title: Intalling snaps offline
table_of_contents: true 
---

# Installing snaps offline

You can download a snap and then manually install it. This is often called "sidloading". 

**Note**: You can also do this programmatically from a snap that uses the [snapd-control interface](https://docs.snapcraft.io/the-snapd-control-interface/7915) and the {snapd REST API](https://github.com/snapcore/snapd/wiki/REST-API). 

## Downloading the snap and the snap assertion

how to download right rev for cpu arch and from secure store

## Installing

snap ack the assertion

snap install the snap file

## Installing in dangerous mode

dangerous mode explained:

- unasserted, so snap may not be what you think it is: security warning. 
- can't be updated later from store

how to so it:
snap install SNAP_FILE --dangerous


