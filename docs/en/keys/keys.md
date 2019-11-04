---
title: "Getting Started"
table_of_contents: true
---

# Getting Started

Not everyone needs to generate and use Snapcraft keys. For example, you can build stock Canonical Ubuntu Core images without them. And you can publish snaps without them.

But, if you want to build a custom Ubuntu Core image, set up a commercial Brand store, and more, you need to understand the simple steps to generate and register Snapcraft keys.

Fortunately, the ```snapcraft``` tool creates and registers keys for you. 

## About Snapcraft keys

Snapcraft keys are, behind the scenes, actually GPG keys. As such they have a public and a private part. They are generated on an Ubuntu classic system with snapcraft installed..  

Registering the key uploads the public part of the key to Canonical servers. Key registration is specific to the user currently logged in through ```snapcraft login```. Regsitering key associates it with this particular Ubuntu SSO Account. 

This process enables Canonical authentication and verification of items signed by the key, such as rAassertions. It also restricts certain actions as appropriate for the Ubuntu account. For example, only Brand Account registered keys can sign Model Assertions that allow devices to connect to a Brand Store. And only authorized accounts can use registered keys to sign System User assertions. 

# Security warning

Snapcraft keys are used for critical purposes. Access to the keys and should be strictly limited. And the keys should be securely backed up. 

Snapcraft keys are written into the current user's home directory:

```bash
~/.snap/gnupg/
```
