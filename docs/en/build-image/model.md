---
title: "The Model"
table_of_contents: true
---


# The Model

Ubuntu has the core concept of a *Model*. The Model defines all required parts of an Ubuntu-Core image. Models can also be used in custom Ubuntu classic images. 

The Model is defined in a Model Assertion. Model assertions are signed, thus they can be authenticated and verified as unchanged. 

The `ubuntu-image` command requires a signed model assertion filename as the final argument. 

Let's take a closer look.

## Model Assertion

### Fields

|Description|Sample|Comment|
|--|--|--|
| Type| `type: model`| required|
| Model name |`model: NAME`|lower-case|
| Series|`series: 16`|must be '16'|
| Brand Account ID|`brand-id: BRAND-ACCOUNT-ID`| See [Account ID](https://dashboard.snapcraft.io/dev/account/)|
| Authority ID | `authority-id: BRAND-ACCOUNT-ID`|Currently the same as the Brand ID|
| Architecture| `architecture: armhf | arm64 | amd64 | i386 | etc `|
| Brand Store ID | `store: STORE-ID` | global Snap Store when absent |
| UC16 or a UC18 image | `base: core` or `base: core18`| UC16 when absent |
| Kernel and gadget snap names| `kernel: KERNELSNAP` and `gadget: GADGETSNAP`| Can specify track/channel. `kernel: pc-kernel=18` means track `18`.|
| Additional snaps | `required-snaps: LIST OF SNAP NAMES` | Can't be removed from image |
| Timestamp| `timestamp: TIMESTAMP`| Generate with `date -Iseconds --utc`| 
| Classic| `classic: true`| Absent means Ubuntu Core| 


## Stock models

You can use a Canonical signed stock model assertion ot build and Ubuntu Core image for an official platform.

Such stock images point at the global Snap Store. They incldue the stock set of snaps.

You can download a few stock model assertions.

### UC16/Pi3

```bash
curl -H "Accept: application/x.ubuntu.assertion" "https://assertions.ubuntu.com/v1/assertions/model/16/canonical/pi3"
```

### UC16/Pi2

```bash
curl -H "Accept: application/x.ubuntu.assertion" "https://assertions.ubuntu.com/v1/assertions/model/16/canonical/pi2"
```

### UC16/Dragonboard

```bash
curl -H "Accept: application/x.ubuntu.assertion" "https://assertions.ubuntu.com/v1/assertions/model/16/canonical/dragonboard"
```

### UC18

You can also find Canonical UC18 Model Assertions [here](http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/).

## Custom models

You can create and use your own signed Model Assertion to build a custom image. Such custom images may point at your Brand Store and include snaps puboished in your Brand store. They can also include snaps from the global Snap Store if your Brand Store Administrator has included them into the Brand Store. (Core, Core18, and Snapd snaps are always included in every Brand Store.)

You point an image at a snap store with the `store: STORE-ID` key in the Model assertion. See below.

### Signing a custom Model Assertion

To create an image with a custom Model, you need to sign a Model Assertion. 

#### Requirements

 - The snapcraft key used to sign must be registered. See [Snapcraft keys](../keys/keys.md)
 - The snapcraft key must be available on the Ubuntu system for the current Ubuntu user
 - For Models that point at a Brand Store, the key must be Registered under the Brand Account
 - `snapcraft login` as the Ubuntu SSO Account to which the key is registered

#### Creating a JSON Model

To sign, you need your Model Assertion in JSON format.

Here is a sample that builds an Ubuntu Core 18 image for a Raspberry Pi 3. The JSON file is named `pi3-model.json`:

```json
{
  "type": "model",
  "authority-id": "<your account id>",
  "brand-id": "<your account id>",
  "series": "16",
  "model": "my-pi3",
  "architecture": "armhf",
  "base": "core18",
  "gadget": "pi=18-pi3",
  "kernel": "pi-kernel=18-pi3",
  "timestamp": "<timestamp>"
}
```

You can generate a current timestamp in the correct format with: `date -Iseconds --utc`.

You may also add `required-snaps` as a JSON array: `required-snaps: [ foo-snap, bar-snap]`

**Note**: To target a Brand Store, use your Brand SSO Account's account-id in the `authority-id` and `brand-id` fields. Also add a `store` key whose value is your Brand `store-id`. 

#### Signing

Signing is done by piping the JSON model file into the `snap sign -k <key name>` command. 


```bash
cat pi3-model.json | snap sign -k KEY_NAME &> pi3.model
```

Enter the key's password as prompted.

Check the created `pi3.model` file to ensure success. 

