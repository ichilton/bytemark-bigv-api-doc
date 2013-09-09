---
title: 'Virtual Machines'
---

# Virtual Machines (Work In Progress)


## Introduction

Todo


## Endpoints

    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines     - create a new VM
    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines     - list of VMs
    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  - details of existing VM
    PUT    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  - update existing VM
    DELETE /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  - delete VM

    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/reimage  - reimage a VM
    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/signal   - signal a VM

Replace ACC_ID with the account id or name, GROUP_ID with the group id (or default) and ID with the id of the virtual machine.


## Attributes

Todo


## Examples

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines
