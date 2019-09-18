---
title: "Build customized Ubuntu Core"
table_of_contents: true
---

# Build customized Ubuntu Core

## Introduction
This section covers how to build an Ubuntu Core image using a customized Model Assertion.

Custom Model Assertions allow:

* Modifying the snaps that are built into image, including the kernel, the gadget and "required" snaps.
* Modifying the Model name.
* Modifying the Brand authority.
* Pointing the Model (and therefore the device) at a Brand Store (See [Building Ubuntu Core for Brand Store](./brand-store-core.md]
* Setting the Model's CPU architecture

And more!

To get started, you may want to review [The Model](./model.md).

## Goals

As noted, Model Assertions can be customized many ways. Our goals are to modify a stock Ubuntu Core 18 Raspberry Pi3 Model as follows: 

* Change the Brand-ID in to your Ubuntu SSO Account ID, listed here as [Snap Account-Id](https://dashboard.snapcraft.io/dev/account/).
* Change the Model Name
* Add a new required snap: hello-world.

### Brand Accounts

Brand Accounts ensure Brand control of images, Brand Stores and the snaps they curate and provide to devices and systems.

A Brand Account is an normal Ubuntu SSO Account. However, such Brand Accounts should be limited to Brand purposes. For example, Brand Accounts accounts have keys that sign Model Assertions, and they are used to root Brand Stores. There are other important aspects of Brand Accounts covered elsewhere. 

Here, you can use your Ubuntu SSO Account as a Brand Account by entering is Account ID into the `brand-id` and the `autority-id` fields in the Model Assertion, as explained below. 

## Requirements

 - Work on a classic Ubuntu system.
 - The ubuntu-image snap must be installed See [Getting Started](./about.md)


## Customizing the Pi3 UC18 Model

Follow the [Custom Models](./model.md) process, but change following fields in the Model JSON:

* `brand-id` Set this to your Ubuntu SSO Account ID.
* `authority-id` Set this to your Ubuntu SSO Account ID.
* `model` Set this to model name.
* `required-snaps` Add snaps in a JSON array, in the example below we add only `hello-world` snap. Every snap listed must be published in the global Brand Store.
* `timestamp` Generate and add a timestamp with `date -Iseconds --utc`


```json
{
  "type": "model",
  "authority-id": "YOUR_UBUNTU_SSO_ACCOUNT_ID",
  "brand-id": "YOUR_UBUNTU_SSO_ACCOUNT_ID",
  "series": "16",
  "model": "YOUR_MODEL_NAME",
  "architecture": "armhf",
  "base": "core18",
  "gadget": "pi=18-pi3",
  "kernel": "pi-kernel=18-pi3",
   "required-snaps": ["hello-world"],
  "timestamp": "<timestamp>"
}
```

Complete the procedure to create the signed Model Assertion. This involves:

* Generating a Snapcraft key when logged into snapcraft as the Brand Account
* Registering the key
* Actually signing the Model JSON using a command like this: `cat model.json | snap sign -k KEYNAME > my-pi3.model`.

The end result is a signed Model Assertion that can be used with `ubuntu-image` to build the image directly. 

## Building an Ubuntu Core image

Here we build an image that uses the global Snap Store using the signed, custom Model Assertion created previously.

The following command builds the image from the specified my-pi3.mkodel file. Snaps are pulled from the `candidate` channel. The build results are put into `img-pi3` directory (the `-O DIRECTORY` argument):

```bash
ubuntu-image snap --channel=candidate -O img-docs-pi3 my-pi3.model
Fetching snapd
Fetching core18
Fetching pi-kernel
Fetching pi
Fetching hello-world
[sudo] password for USER:
$
``` 

On success, the `img-pi3` directory contains the image and a few supporting files. 
```bash
$ ls img-docs-pi3/
pi.img  seed.manifest  snaps.manifest
```

You may now flash the `pi3.img` file to an SD card for booting. But before getting to that part, let's add a snap to the image as an argument to the `ubuntu-image` command. 

## Including snaps on the command line

We saw above that you can include snaps through the Model Asssertion (kernel, gadget, and required).  

You can also include additional snaps not referenced in the Model Assertions with the `--snaps SNAP` argument. (This can be used multiple times to add multiple snaps.)

For example:

```bash
ubuntu-image -snap --snap rocketchat-server --snap nextcloud -O img-2 my-pi3.model
```

The `--snap` argument takes either a snap name or path to a local snap file. 

**Note** Snap files added in this way are only for testing purposes. Such snaps cannot be updated in the live image later (unless the snap is also referenced in the Model Assertion, and this is not an appropriate approach outside of development).


# Installing the image

Installation procedures differ by plaftform. In this case, we have build a pi3 image which can simply be flashed to an SD card, from which the pi3 can be booted.

So in this case, use a tool like `dd` to write the image to an SD card and boot your device

**Warning**; Replace *sdXX* with the node for your storage device. This command overrites the entire device so be very sure you have named it correctly.

```bash
sudo dd if=pi3-test/pi3.img of=/dev/sdXX bs=32M
sync
```

## First boot

For the pi3:

 - Power it off
 - Insert the SD card
 - Connect Ethernet to a LAN that has internet connectivity
 - Connect an HDMI monitor (or connect a UART for serial and use minicom or similar)
 - Power on

**Note**: It is often useful to connect a serial cable so that you can watch and engage with the boot process in a terminal.

## Console-conf

As noted in, a first boot experience allows you to set up a custom network configuration and add a system user. See  [Building a stock Ubuntu Core image](./stock-core.md#first-boot-configuration-experience)

By default, Ubuntu Core systems run a program that allows you to configure the network and to provide an Ubuntu SSO account email address that allows you to log in as the System User. You must have uploaded an SSH key to the [account](https://login.ubuntu.com/ssh-keys).

It is not always necessary to complete this program. If you want to use a WiFi AP, you should compelte the program. The default network configuration probably just works for Ethernt with DHCP.

Ubuntu Core is designed to be able to run without a user. Many production system operate without a user. However, it is often convenient to add yourself as a System User, which means you can log into the device over SSH. 

After completing console-conf, the device IP address is displayed and you can log into it over SSH.

**Note**: There is no default `ubuntu` user on these images, but you can run `sudo passwd <account name>` to set a password in case you need a local console login.


