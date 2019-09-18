---
title: "Building a stock Ubuntu Core image"
table_of_contents: true
---

# Build a stock Ubuntu Core image

Here we explain how to build an stock Ubuntu Core 18 image. A "stock" image is based on an unmodified Model Assertion that is signed be Canonical. 

Let's get started with an amd64 image that can be launched in a KVM virtual machine on a classic Ubuntu system. 


## Requirements

 - You should be working on an Ubuntu system.
 - You need an Ubuntu SSO Account to which you have [uploaded](https://login.ubuntu.com/ssh-keys) an SSH key.
 - For KVM, `sudo apt install qemu-kvm`, then run `kvm-ok` and ensure the output indicates KVM exists and KVM acceleration can be used.
 - Install the ubuntu-image snap: `snap install ubuntu-image --beta --classic`.

## Get the stock amd64 Model

Download the stock Ubuntu Core 18 amd64 Model assertion:

```bash
snap known --remote model series=16 model="ubuntu-core-18-amd64" brand-id=canonical > ubuntu-core-18-amd64 > ubuntu-core-18-amd64.model
```

The ubuntu-core-18-amd64.model file should be like this:

```bash
type: model
authority-id: canonical
series: 16
brand-id: canonical
model: ubuntu-core-18-amd64
architecture: amd64
base: core18
display-name: Ubuntu Core 18 (amd64)
gadget: pc=18
kernel: pc-kernel=18
timestamp: 2018-08-13T09:00:00+00:00
sign-key-sha3-384: 9tydnLa6MTJ-jaQTFUXEwHl1yRx7ZS4K5cyFDhYDcPzhS7uyEkDxdUjg9g08BtNn

AcLBXAQAAQoABgUCW37NBwAKCRDgT5vottzAEut9D/4u9lD3lFWXoHx1VQT+mUCROcFHdXQBY/PJ
... [OMITTED] ...
NG54bznx12KgOT3+YiHtfE95WiXUcJUrEXAgfVBVoA==
```

## Building the Ubuntu Core image

The following builds the image from the `stable` channel. The build results and placed into the `img-amd64` directory:

```bash
$ ubuntu-image snap --channel=stable -O img-ubuntu-core-18-amd64 ubuntu-core-18-amd64.model 
Fetching snapd
Fetching core18
Fetching pc-kernel
Fetching pc: 
$
```

On success, here are the contents of the created build output directory:

```bash
$ ls img-ubuntu-core-18-amd64/
pc.img  seed.manifest  snaps.manifest
```

`pc.img` is the Ubuntu Core image and can be launched in KVM, as described next.

## Launching in KVM

Launch this Ubuntu Core 18 amd64 image in a KVM virtual machine as follows:

**Note** The following command includes the path to the Ubuntu Core image file (`pc.img`) previously created.

```bash
kvm -smp 2 -m 1500 -netdev user,id=mynet0,hostfwd=tcp::8022-:22,hostfwd=tcp::8090-:80 -device virtio-net-pci,netdev=mynet0 -vga qxl -drive \
file=img-ubuntu-core-18-amd64/pc.img,format=raw
```

On success, the image boots in a new window. Next, you need to complete the first boot configuration experience.

## First boot configuration experience

When you launch a stock Ubuntu Core image, there is a first boot experience through the terminal. 

By default, Ubuntu Core systems run a program (console-conf) that allows you to configure the network and to provide an Ubuntu SSO account email address that allows you to log in as the System User. You must have uploaded an SSH key to the [account](https://login.ubuntu.com/ssh-keys).

It is not always necessary to complete this program. There are two reasons you may want to complete it: configuration the network and adding yourself as a user.

### Configuring the network

You may need to complete the first boot configration wizard (on terminal) if you want to use a custom network configuration such as connecting to a WiFi access point or using a static IP address. The default network configuration just works for Ethernt with DHCP.

### Adding yourself as user

Ubuntu Core is designed to be able to run without a user. Many production system operate without a user. 

However, it is often convenient to add yourself as a System User, which means you can log into the device over SSH, and then have root access. 

As prompted, provide your email address for which you previously made an Ubuntu SSO account and for which you uploaded an SSH key.

**Note** Because Ubuntu Core mounts much of the file system as read-only, even root cannot modify most of it. 

After completing console-conf, the device IP address is displayed and you can log into it over SSH.

## SSH to Ubuntu Core in KVM

On a device, you can typically log in with `ssh USER@IP`, where the USER is the username associated Ubuntu SSO account with the SSH key. 

But, logging into the Ubuntu Core system on KVM requires stating the port number used in the KVM launch command (8022 in this case, see above) and `localhost` instead of the IP address, as follows:

```bash
$ ssh -p 8022 knitzsche@localhost
```

If prompted with the following, you may need to delete the public key of the host:

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
[. . . ]
Offending ECDSA key in /home/USER/.ssh/known_hosts:23
  remove with:
  ssh-keygen -f "/home/USER/.ssh/known_hosts" -R [localhost]:8022
```

Simply execute the complete `ssh-keygen` command shown in the output, then run the complete `ssh` command again to login. 

On success, you are logged in. Let's try a few things.

## Try a few things

### snap list

 Try running `snap list`:

```bash
USER@localhost:~$ snap list
Name       Version       Rev   Tracking  Publisher   Notes
core18     20190904      1144  stable    canonical✓  base
pc         18-2          36    18        canonical✓  gadget
pc-kernel  4.15.0-64.73  298   18        canonical✓  kernel
snapd      2.41          4605  stable    canonical✓  snapd
```

### Show the Model

As noted, the Model Assertion is built into the image (and it cannot be modified). Display it as follows:

```bash
USER@localhost:~$ snap known model
type: model
authority-id: canonical
series: 16
brand-id: canonical
model: ubuntu-core-18-amd64
architecture: amd64
base: core18
display-name: Ubuntu Core 18 (amd64)
gadget: pc=18
kernel: pc-kernel=18
timestamp: 2018-08-13T09:00:00+00:00
sign-key-sha3-384: 9tydnLa6MTJ-jaQTFUXEwHl1yRx7ZS4K5cyFDhYDcPzhS7uyEkDxdUjg9g08BtNn

AcLBXAQAAQoABgUCW37NBwAKCRDgT5vottzAEut9D/4u9lD3lFWXoHx1VQT+mUCROcFHdXQBY/PJ
NriRiDwBaOjEo5mvHMRJ2UulWvHnwqyMJctJKBP+RCKlrJEPX8eaLP/lmihwIiFfmzm49BLaNwli
si0entond1sVWfiNr7azXoEuAIgYvxmJIvE+GZADDT0/OTFQRcLU69bhNEAQKBnkT0y/HTpuXwlJ
TuwwJtDR0vZuFtwzj6Bdx7W42+vGmuXE7M4Ni6HUySNKYByB5BsrDf3/79p8huXyBtnWp+HBsHtb
fgjzQoBcspj65Gi+crBrJ4jS+nfowRRVXLL1clXJOJLz12za+kN0/FC0PhussiQb5UI7USXJ+RvA
Y8U1vrqG7bG5GYGqe1KB9GbLEm+GBPQZcZI3jRmm9V7tm9OWQzK98/uPwTD73IW7LrDT35WQrIYM
fBfThJcRqpgzwZD/CBx82maLB9tmsRF5Mhcj2H1v7cn8nSkbv7+cCzh25lKv48Vqz1WTgO3HMPWW
0kb6BSoC+YGpstSUslqtpLdY/MfFI0DhshH2Y+h0c9/g4mux/Zb8Gs9V55HGn9mr2KKDmHsU2k+C
maZWcXOxRpverZ2Pi9L4fZxhZ9H+FDcMGiHn2vJFQhI3u+LiK3aUUAov4k3vNRPGSvi1AGhuEtUa
NG54bznx12KgOT3+YiHtfE95WiXUcJUrEXAgfVBVoA==
```

### Show snap changes

Snapd state events are viewable as snap changes:

```bash
knitzsche@localhost:~$ snap changes
ID   Status  Spawn               Ready               Summary
1    Done    today at 17:31 UTC  today at 17:31 UTC  Initialize system state
2    Done    today at 17:31 UTC  today at 17:31 UTC  Initialize device
```

