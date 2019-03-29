---
title: NetworkManager
---

# NetworkManager

NetworkManager is a system network service that manages your network devices and connections, attempts to keep network connectivity active when available. It manages Ethernet, WiFi, mobile broadband (WWAN) and PPPoE devices while also providing VPN integration with a variety of different VPN serivces.

By default network management on Ubuntu Core is handled by systemd's networkd and netplan. While NetworkManager has some support to handle netplan configuration files, Ethernet support is disabled by default and has to be turned on explicitly to avoid conflicts with existing network configuration.

What NetworkManager Offers
The upstream NetworkManager project offers a wide range of features which are partially available in the snap version. However, as the snap should be always delivered in high quality we don't have yet all upstream features enabled.

Currently we provide support for the following high level features:

- WiFi connectivity
- WWAN connectivity (together with ModemManager)
- Ethernet connectivity

Currently the following features are not supported:

- VPN

## Upstream documentation

Existing documentation from the upstream project can be found [network-manager](network-manager/docs/index.md).

