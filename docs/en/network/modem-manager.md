---
title: ModemManager
---
# ModemManager

ModemManager is a DBus-activated daemon which controls mobile broadband (2G/3G/4G) devices and connections. ModemManager is able to prepare and configure a wide variety of modems and setup connections with them.

ModemManager should be used in most cases jointly with the network-manager snap. NetworkManager can be used to set cellular connection settings and to start and stop the connection. The recommended way of using a modem in Ubuntu Core is described in NetworkManager documentation. This documentation serves as further reference in case more control on the cellular modem is needed. It is important to note that many of the things explained are automatically performed when using NetworkManager.

## What ModemManager Offers

ModemManager offers a wide range of features, with the vast majority of them available in the snap version.

The main features provided by the ModemManager snap are:

- Cellular connectivity for a wide variety of modems
- SMS messages Support for USB modems Support for AT commands, QMI, and MBIM
- interfaces

What is not yet supported:

- RS232 devices
- Bluetooth-paired phones

## Upstream documentation

Existing documentation from the upstream project is [here](https://www.freedesktop.org/wiki/Software/ModemManager/).
