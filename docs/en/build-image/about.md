---
title: "Getting started"
table_of_contents: true
---

# Getting started

Anyone can build an Ubuntu Core image in just a couple minutes from an Ubuntu classic system.

All you really need in the `ubuntu-image` tool, easily installable as a snap, and a signed Model Assertion. 


## Ubuntu-image tool 

Install `ubuntu-image` with:

```bash
snap install ubuntu-image --beta --classic
```

**Note** When building an Ubuntu Core image, use `ubuntu-image snap ARGS`. You can also build classic images with `ubuntu-image classic ARGS`, although this is experimental. 

## Model

To build an Ubuntu Core image, you need a signed Model Assertion. This defines the image in every respect, including its architecture, what Snap Store it points at, what snaps are included in the image and so on. You can use a stock Canonical Model Assertion, or create and sign your own. For more information, see [The Model](./model.md).


## Reference platforms 

You can build an image for a [reference platform](https://ubuntu.com/download/iot). Or you can build an image for your own platform. Building for a non reference platform may require enablement work.

**Note**: to get started, if you lack an IoT device, you can always build an image for use in a KVM virtual machine and run it on classic Ubuntu.

## Channel

When you build the image, snaps are downloaded from the *channel* you specify as a flag on the `ubuntu-image` command line (for example, `--channel=stable`, or `--channel=beta`). 

The default channel is stable.

## Snaps

By default, the snaps listed in the Model Assertion are installed. (See the Model Assertion section below). 

You can also add snaps to the image at build time by listing them as arguments on the `ubuntu-image` command line. (For example. `--snap network-manager`.) You can also specify the channel and the track to pull the snap from. For example, `--snap network-manager=1.10` installs from the 1.10 track, and `--snap network-manager=1.10/beta` installs from the 1.10 track's beta channel. 

## The generated image

**Note**: It is recommended to use the `-O DIRECTORY` option to place all build artifacts into the specified directory.

The output is a *img file that can be written to the device and a device-specific manner. 

There are also  seed.manifest and snap.manifest files that provide key information about the snaps installed in the image. 


