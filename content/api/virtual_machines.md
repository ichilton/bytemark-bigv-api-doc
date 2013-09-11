---
title: 'Virtual Machines'
---

# Virtual Machines


## Introduction

I don't think virtual machines require any explaination, as that's why you are using BigV! :)


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

* autoreboot_on
* cdrom_url
* cores
* group_id
* id
* management_address
* memory
* name
* power_on
* keymap
* deleted
* hostname
* head
* hardware_profile
* hardware_profile_locked


## Examples

#### All VM's in Group

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines

##### Response:

    [{"autoreboot_on":true,"cdrom_url":null,"cores":1,"group_id":1,"id":1234,"management_address":"213.123.123.123","memory":1024,"name":"www1","power_on":true,"keymap":null,"deleted":false,"hostname":"www1.default.myaccount.uk0.bigv.io","head":"head212","hardware_profile":"virtio2013","hardware_profile_locked":false}]


#### Single VM:

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines/1234

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines/1234

##### Response:

    [{"autoreboot_on":true,"cdrom_url":null,"cores":1,"group_id":1,"id":1234,"management_address":"213.123.123.123","memory":1024,"name":"www1","power_on":true,"keymap":null,"deleted":false,"hostname":"www1.default.myaccount.uk0.bigv.io","head":"head212","hardware_profile":"virtio2013","hardware_profile_locked":false}]


