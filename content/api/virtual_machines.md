---
title: 'Virtual Machines'
---

# Virtual Machines (Work In Progress)


## Introduction

Todo


## Endpoints

* POST   /accounts/:id/groups/:id/virtual_machines     - create a new VM
* GET    /accounts/:id/groups/:id/virtual_machines     - list of VMs
* GET    /accounts/:id/groups/:id/virtual_machines/:id - details of existing VM
* PUT    /accounts/:id/groups/:id/virtual_machines/:id - update existing VM
* DELETE /accounts/:id/groups/:id/virtual_machines/:id - delete VM

* POST   /accounts/:id/groups/:id/virtual_machines/:id/reimage - reimage a VM
* POST   /accounts/:id/groups/:id/virtual_machines/:id/signal  - signal a VM


## Attributes

Todo


## Examples

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines
