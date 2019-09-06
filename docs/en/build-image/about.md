---
title: "Getting started"
table_of_contents: true
---

# Getting started

The `ubuntu-image snap` command builds an Ubuntu Core image in minutes. 

Install this with:

```bash
snap install ubuntu-image --beta --classic
```

You can also build classic images with `ubuntu-image classic ...`, although this is experimental. 

## Model

Every image is built as a certian model as defined by its Model assertion. See [The Model](./model.md).

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




