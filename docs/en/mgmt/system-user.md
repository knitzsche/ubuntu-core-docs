---
title: System user
table_of_contents: true 
---

# System user

As noted, Ubuntu Core runs and updates without any added users. Applications run as root, confined by Apparmor and Secconp.

However, you can create a System User. The system user allows you to ssh to device and execute commands, including with sudo.

By default, a System-User is created on first boot after Ubuntu SSO account data is entered in terminal. (You must have placed the user's public SSH key on login.ubuntu.com)

**Note**: This terminal application is called console-conf. Console-conf can be suppressed: Contact Canonical for information. 

When console-conf is completed, a system-user is created, and `snap managed` command returns true:

```bash
$ snap managed
true
```

If console-conf is never completed, no System User is created and the `snap managed` command returns `false`.

**Note**: Only one system user is possible, although extra users are. 

On with no System User, you can create one by inserting a USB drive that contains a signed system-user assertion. 

Depending on the model assertion, the key that signs the system-user assertion may need to be registered by the Brand Account. 

The model can contain an optional "system-user-authority" field to delegate system-user signing to another Ubuntu account, or by using an asterisk, to any account, although this is no recommended for security reasons. 

ETC.

TODO
