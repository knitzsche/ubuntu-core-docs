---
title: "About"
table_of_contents: true
---

# About

Before you can build a custom image or take other fun steps, you need to generate and register a *snapcraft key*.

The ```snapcraft``` tool creates and registers keys for you. 

The keys are technically GPG keys, with a public and a private part. 

Registering the key uploads the public part of the key to Canonical servers. Key registration is specific to the user currently logged in through ```snapcraft login```. The regsitered key is associated with this particular Ubuntu SSO Account. 

This process enables Canonical authentication and verification of items signed by the key, such as assertions. It also restricts certain actions as appropriate for the Ubuntu account. For example, only Brand Account registered keys can sign Model Sssertions that allow devices to connect to a Brand Store. And only authorized accounts can use registered keys to sign System User assertions. 


# Security warning

Snapcraft keys are used for critical purposes. Access to the keys and should be strictly limited. And the keys should be securely backed up. 

Snapcraft keys are written into the current user's home directory:

```bash
~/.snap/gnupg/
```
