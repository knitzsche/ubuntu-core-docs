---
title: "Creating and registering"
table_of_contents: true
---

# Requirements

hese procedures assume you are working on an Ubuntu classic system.

You must also have an Ubuntu SSO account. See the "Getting Started" section.

# Creating a key

To generate a key that can then be linked to your Ubuntu Store account, run the following:

```bash
$ snapcraft create-key KEY_NAME
```

Provide a strong password as prompted to protect the key.

Generating the key takes some time: the key is 4096 bits long, and the system needs entropy to complete the process. Moving the mouse or typing can help to speed up the process, as will installing the `rng-tools` package beforehand.

After the key is created, list your keys with:

```bash
snapcraft list-keys
```

The output shows all keys and shows whether each key is registered (by the current snapcraft user).

# Registering a key

During this step, you are asked to select an existing key (if you have more than one) and to log in with your account credentials:

```bash
snapcraft register-key
```

On success, the key is registered and can be used for various purposes.

If you run ```snapcraft list-keys``` this new key is now shown to be registered. 
