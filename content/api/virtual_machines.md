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

The rules for what can be changed on a running vm are currently complex - the simple advice is to power down a machine before making changes to an existing vm.


## Attributes

* **id** - unique key (integer).
* **autoreboot_on** - boolean specifying whether the machine will automatically turn back on on shutdown/reboot.
* **cdrom_url** - url of an iso to expose to the vm as a cd drive.
* **cores** - number of cpu cores available.
* **group_id** - id of the group this vm belongs to.
* **management_address** - ssh'ing to this ip will allow (out-of-band) access to the virtual machine using it's console. If the vm is not responding or you are locked out for some reason, this is very useful!
* **memory** - amount of memory, in megabytes.
* **name** - name of the virtual machine.
* **power_on** - boolean specifying whether the machine is turned on.
* **keymap**
* **deleted** - boolean specifying whether the machine has been deleted.
* **hostname** - bigv hostname for the machine.
* **head** - location of the vm on bytemark's host machines (heads).
* **hardware_profile** - which hardware profile is being used (see the [definitions page](/api/definitions))
* **hardware_profile_locked** - whether the hardware profile is locked and thefore will not be auto upgraded.


## Parameters

If you would like to see deleted VM's (i.e VM's where the deleted field is set to true), you need to pass: the include_deleted=true paramter through in the query string, eg:

    GET /accounts/myaccountname/groups/default/virtual_machines?include_deleted=true

or if you are using the overview parameter in accounts:

    GET /accounts?view=overview&include_deleted=true


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


