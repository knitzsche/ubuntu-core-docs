---
title: "Buildin for a Brand Store"
table_of_contents: true
---

# Building Ubuntu Core for a Brand Store

Ubuntu Core (and classic Ubuntu) images can be built to point at a Brand Store (instead of pointing at the global Snap Store, which is the default). 

This is done by adding the Brand Store ID to the Model Assertion. So a custom model assertion is required. For background, see [The Model](./model/md) and [Building custom Ubuntu Core](./custom-core.md).

Brand Stores are protected and don't allow snaps to be downloaded without authentication. Here we cover how to build an Ubuntu Core image where the Model assertion points at a Brand Store, thus the snaps are downloaded through the Brand Store, and authentication is required. 

Here we explain how to build an Ubuntu Core image using a customized Model Assertion.

## Requirements

 - You should be working on an Ubuntu system.
 - You need an Ubuntu SSO Account to which you have [uploaded](https://login.ubuntu.com/ssh-keys) an SSH key.
 - For KVM, `sudo apt install qemu-kvm`, then run `kvm-ok` and ensure the output indicates KVM exists and KVM acceleration can be used.
 - Install the ubuntu-image snap: `snap install ubuntu-image --beta --classic`.
 - You must have a Brand Store, and you must know the STORE_ID (provided to you with the Brand Store).
 - You must have access the Brand Ubuntu SSO Account credentials because you need to sign a custom Model Assertion
 - All snaps referenced in the Model or as `--snap SNAPNAME` arguments must be available through the Brand Store. (The core* snaps are always available in every Snap Store.
 - Every Brand Store requires a properly configured Serial Vault for device authentication, and the gadget snap must be configured to use it. See [Snap Stores](../store/intro.md)

## Creating your custom Model

Systems point at a Brand Store through their Model Assertion. 

Let's take a look at several important points about Model Assertions in the context of Brand Stores:

* The Model Assertion requires the `"store:" "STORE_ID"` filed to point the system at the Brand Store. The Brand Store store ID is provided to you on purchase.
* When a Model Assertion points at a Brand Store, two fields in the Model must be set to the [Brand SSO Snap Account ID](https://dashboard.snapcraft.io/dev/account/): `brand-id` and `authority-id`. If these are not the Brand Account ID, the system cannot authenticate with the Brand Store, which means it cannot install or refresh snaps.
* The Model assertion must be signed by a key registered under the Brand Account. This prevents unauthorized systems from accessing snaps curated in the Brand Store.

Instructions for creating and signing a custom model are [here](./model.md#custom-models). Follow those instructions while making the changes noted above. Be sure to sign the Model with a Snapcraft Key registered by the Brand Account. 

After signing a Brand Store custom model assertion, it looks something like this:

```bash
type: model
authority-id: BRAND_SNAP_ACCOUNT_ID
series: 16
brand-id: BRAND_SNAP_ACCOUNT_ID
model: my-brand-model
architecture: armhf
base: core18
gadget: GADGET_THAT_WORKS_WITH_SERIAL_VAULT
kernel: pi-kernel=18-pi3
store: BRAND_STORE_ID
timestamp: 2019-06-06T15:27:51Z
sign-key-sha3-384: UqUliKa38ifdIAcbJiG4qDNfreV847i8-1yzCXXcgNtDBrwNbjRLQu32y0ZcsdJm

AcLBUgQAAQoABgUCXPkw9wAAMnkQAJYtmUVfSDHgPU9noxis78hpu+IZct6hWn7g4TjNhqZht8eQ
[ . . . ] OMITTED . . . }
eFVFg++mt1ckV8oau8nJZANKcLef
```

Take note of the values that are all capital letters in the above. These need special attention as explained previously.

## Getting credentials

Building an Ubuntu Core image requires downloading snaps from the Snap Store at which the Model Assertion points. When the Model Assertion points at a Brand Store, downloading is protecteed. So, you must first generate a credentials file that authorizes downloading snaps from the specific Brand Store. 

The Ubuntu SSO account used to generate the credentials must have Viewer role in the Brand Store (or it must be the Brand Account, although use of the Brand Account is not recommended for security reasons). An Administrator of the Brand Store can add the Ubuntu SSO Account as a Viewer. 

As Viewer, export the credentials file ("creds"), as follows:

```bash
snapcraft export-login --acls package_access creds
```
As prompted, enter the email address and the password for the Viewer Ubuntu SSO Account.

On success, you should have a file named "creds" in the current working directory. 


## Building the image

Now, you can build the Ubuntu Core image by declaring an environment variable that specifies the credentials file:

```bash
UBUNTU_STORE_AUTH_DATA_FILENAME=/home/auser/build_images/creds ubuntu-image --channel=candidate -O img-brand-store SIGNED_MODEL_ASSERTION
```

## Next steps

Your image can be installed on a device using an appropriate approach for the hardware. 

After booting it and logging in you can check whether the system is authenticated with the Brand Store by displaying the Serial Assertion with `snap known serial` and verifying the `brand-id` is the Brand Account ID. If no serial assertion is returned, there's an error to fix. If the `brand-id` is Canonical, it is a stock image that points at the global Snap Store, not at your Brand Store, and something needs to be fixed. 
