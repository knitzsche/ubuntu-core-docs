---
title: System user
table_of_contents: true 
---

# System user

The special system user allows you to ssh to device and execute commands as root. 

By default is created on first boot on user entered ubuntu account creds. (Must have placed you publish ssh key on login.ubuntu.com)

Can suppress that, or simply never complete it, if so device is "unmanaged". 

only one system user is possible, although extra users are. 

Note: in most cases, IoT devices do not require a user. 

On unmanaged devices, you can create the system-user by inserting a USB drive that contains a signed system-user assertion. 

Depending on the model assertion, the key that signs the system-user assertion may need to be registered by the Brand Account. 

The model can contain an optional "system-user-authority" field to delegate system-user signing to another Ubuntu account, or by using an asterisk, to any account, although this is no recommended for security reasons. 

ETC.

