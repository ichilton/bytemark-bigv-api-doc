---
title: 'Virtual Machines'
---

# Virtual Machines (Work In Progress)


## Introduction

Todo


## Endpoints

    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines     # all vm's
    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  # single vm
    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines     # create
    PUT    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  # update
    DELETE /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID  # delete

    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/reimage  # re-image
    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/signal   # signal

Replace ACC_ID with the account id or name, GROUP_ID with the group id (or default) and ID with the id of the virtual machine.


## Attributes

Todo


## Examples

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines
