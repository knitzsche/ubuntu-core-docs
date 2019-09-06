---
title: Snap Stores
---

# Snap Stores

Snap Stores are a key part of Ubuntu IoT development as they provide a mechanism to store and deliver versions of applications packaged as snaps to devices, to classic Ubuntu, indeed to most Linux system. 

Without a store, a vendor has to manually distribute their snaps to their users having a difficult time keeping track of who’s received the latest version of their application.

The most general type of store is the global snap store. It is the default store that every modern Linux distribution with snapd installed points to and from which to retrieve snaps. It is public and it is global so that a common repository of software is available and searchable to as wide an audience as possible. Anyone with a valid Ubuntu SSO account may publish and distribute their snapped application via the global snap store.

The global snap store has a concept of paid apps which places some restrictions on who can download an application. All paid applications are searchable in the store just like non-paid apps. However, paid applications can only be installed after a user has paid for gaining access to this application.

You may follow this [step-by-step guide][step-by-step-guide] that will show you how to distribute snaps to your devices through the snap store.

Another type of store that can be used for distributing snaps to devices is one called a Brand store. A Brand store provides you with the ability to restrict the scope with which your snaps are visible, which gives you complete control over what devices may search and install your applications.

A Brand store can be configured such that it can inherit all snaps from the global snap store and/or inherit snaps from another Brand store. It is possible to inherit snaps from as many other stores as desired creating as flexible of a hierarchy as needed to deliver your snaps and control the deployment to the right set of devices.

The following table covers some scenarios when you’d want to use the global snap store versus a private Brand store.

| Scenario                                                      | Global Snap Store | Private Brand Store |
|---------------------------------------------------------------|-------------------|---------------------|
| Distribute an application to anyone                           |        ✓          |                     |
| Distribute an application to certain clients via a paywall    |        ✓          |                     |
| Distribute an application to a specific set of client devices |                   |          ✓          |
| Canonical-hosted store solution                               |        ✓          |          ✓          |
| Can be proxied and cached on local premises                   |        ✓          |          ✓          |
| *Self-hosted store solution                                   |                   |          ✓          |

(* A self-hosted store solution is an upcoming feature).

There are many other important things to know about the global snap store
and Brand stores. These are covered in greater detail in later sections of
this documentation.

Follow this [guide][guide] to request a Brand store or
[get in contact][get-in-contact] with someone from Canonical to learn more
about getting your own Brand store.
