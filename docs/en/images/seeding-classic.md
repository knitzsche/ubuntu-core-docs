---
title: Seeding Ubuntu Classic
table_of_contents: true
---

# Introduction

What is seeding.

# Image to start with

Your own classic image. 

A released Ubuntu cloud image such as: http://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img 

This document uses a cloud image and then launches it in a KVM virtual machine.

# What to seed

- model assertion

- account assertion

- account-key assertion

- snaps

- for each snap, the snap's assertions 

One usually seeds a gadget snap that is set up to point the system at the 

# Obtain the assertions and snaps

lots of detail here.

# Download the Ubuntu cloud image

## Create the cloud-init seed file

Note: this is another use of the term "seed."

# mount the image

# seed the image

use the snap-prepare 
 


sudo \
  UBUNTU_STORE_ID=Cl02oo6Dea1fievulein \
  UBUNTU_STORE_AUTH_DATA_FILENAME=./cyberdyne.auth
  snap prepare-image --classic \
  --extra-snaps hello \
  cl02-classic_model.assert \
  /tmp/img/

# unmount the image

# launch the image in KVM



