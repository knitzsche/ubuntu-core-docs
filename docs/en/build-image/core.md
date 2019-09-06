---
title: "Build Ubuntu Core"
table_of_contents: true
---

# Build Ubuntu Core

Here we explain actually building an Ubuntu Core image.

## Requirements

 - Work on an Ubuntu system
 - A signed Model Assertion
 - All snaps in the Model Assertion must be available from the global Snap Store, or, if the Model ASsertion specifies a Brand Store, then all snaps must be available through it.
 - The ubuntu-image snap must be installed


```bash
snap install --classic ubuntu-image
```

# Building the Ubuntu Core image

Here we build an image that uses the global Snap Store.

Build the image from the `beta` channel and put build results into `img-pi3` directory:

```bash
ubuntu-image -channel=candidate -O pi3-test pi3.model
```

# Building from a Brand Store

## Get credentials

If the Model Assertion specifies a Brand Store, you must first generate a credentials file that authorizes downloading snaps from the specific Brand Store. 

The Ubuntu SSO account used to generate the credentials must have Viewer role in the Brand Store (or it must be the Brand Account, although use of the Brand Account is not recommended for security reasons). An Administrator of the Brand Store can add the Ubuntu SSO Account as a Viewer. 

As Viewer, export the credentials file ("creds"), as follows:

```bash
snapcraft export-login --acls package_access creds
```
As prompted, enter the email address and the password for the Viewer Ubuntu SSO Account.

On success, you should have a file named "creds" in the current working directory. 

## Build the image

Now, you can build the Ubuntu Core image by declaring an environment variable that specifies the credentials file:

```bash
UBUNTU_STORE_AUTH_DATA_FILENAME=/home/auser/build_images/creds ubuntu-image -channel=candidate -O pi3-test pi3.model
```

# Including snaps

You can include additional snaps not referenced in the Model Assertions with one ore more of the `--snaps SNAP` arguments. 

For example:

```bash
sudo ubuntu-image -c beta --snap rocketchat-server --snap nextcloud -o img-pi3-snaps.img pi3.model
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

# First boot

For the pi3:

 - Power it off
 - Insert the SD card
 - Connect Ethernet to a LAN that has internet connectivity
 - Connect an HDMI monitor
 - Power on

**Note**: It is often useful to connect a serial cable so that you can watch and engage with the boot process in a terminal.

## Console-conf

By default, Ubuntu Core systems run a program that allows you to configure the network and to provide an Ubuntu SSO account email address that allows you to log in as the System User. You must have uploaded an SSH key to the [account](https://login.ubuntu.com/ssh-keys).

It is not always necessary to complete this program. If you want to use a WiFi AP, you should compelte the program. The default network configuration probably just works for Ethernt with DHCP.

Ubuntu Core is designed to be able to run without a user. Many production system operate without a user. However, it is often convenient to add yourself as a System User, which means you can log into the device over SSH. 

After completing console-conf, the device IP address is displayed and you can log into it over SSH.

**Note**: There is no default `ubuntu` user on these images, but you can run `sudo passwd <account name>` to set a password in case you need a local console login.


