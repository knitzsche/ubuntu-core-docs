---
title: Serial console
table_of_contents: true 
---

# Serial console

Most IoT devices have built-in support for a serial-console. You can use this to observe messages output during boot, including those by U-Boot, for example. 

**Note**: console-conf displays on the serial console. 

Using the serial console typically involves:

- Physically connecting an Ubuntu lapop to the device. Many devices have dedicated physical pins. You can use a USB adapater that provides electrical leads to connect to the appropriate pins and plug the USB to your Ubuntu system.
- Using Minicom (or similar) application on Ubuntu to interact with the console.

**Note** Minicom may need link layer configuration to operate with the particular device. You may also need to configure Minicom to use Serial port named `/dev/ttyUSB0`.



