---
title: Introdcution to image building
table_of_contents: true
---

# Introduction

# Model assertion

Every image requires a signed model assertion. yada yada

Its fields are critically important, setting for example the Brand, the model name, the store-ID, required-snapsi, kernel snap, gadget snap, base (for UCore 18) and more. 

for details, See (link to model assertion reference doc). 

The Brand can create and sign a model, or you can use a Canonical signed model.

## Brand signed model assertion

Can point at brand store.

brand registered key must sign. 

key must be local. 

If you have no key, you need to create and register one. 

### Creating and registering a key

yada

### Completinge the model json

yada

### Signing the json model

yada

## Using a Canonical model assertion

you can build an image with a Canonical-signed model assertion you download.

download here: yada yada 

# Ubuntu-image command

Used to build images. 

Can build Ubuntu Core or Ubuntu Classic images. 

Takes signed model as final arg 

Sets image channel.

Other flags

# Snaps included

You can include snaps in your image in various ways.

## From model

required-snaps field.

cannot be removed at run time without manual override.

## From ubuntu-core buld argument: --extra snaps

# Gadget snap

signed by brand or by canonical.

prepare-device hook to authorize device with Brand Store.

# Kernel snap

signed by brand or by canonical.

reference kernels

enablement option from Canonical

your own enablement

