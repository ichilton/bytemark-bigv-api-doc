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

    POST   /accounts/ACC_ID/groups/GROUP_ID/vm_create

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


## Account Overview

The account overview endpoint includes all virtual machines under the account, and includes their discs and nics. See the [accounts page](/api/accounts) for more information and an example.


## Reimage

The reimage endpoint allows a virtual machine to be re-installed from a clean operating system image and returned to the same state as a new machine.

Re-image requests can only be made against a powered off machine.

It is initiated by using:

    POST /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/reimage

..and accepts the following parameters:

* **distribution** - the name of a distribution - valid options can be found by using the GET /definitions call ([see the definitions page]](/api/definitions))

* **root_password** - the root password the machine should have after re-imageing.

An example is shown below.


## Signal

The signal endpoint can be used to send signals to the machine (eg: shutdown or key presses).

Signal requests can only be made against a powered-on virtual machine.

The endpoint is:

    POST /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/ID/signal 

The following parameters are accepted:

* **signal** - this can either be:
   - powerdown
   - reset
   - sendkey

* **data** - only valid if the signal is 'sendkey'. A dash-separated list of keys to press, eg: 'a-b-c-ctrl-alt-del'

The valid sendkeys can be found using the GET /definitions call (See the [definitions page](/api/definitions)).

reset and powerdown are the ACPI signals of the same name.


## VM Creation

A virtual machine can be created by using POST /accounts/ACC_ID/groups/GROUP_ID/virtual_machines, but it will only be a machine, it will not have a disc or be installed with anything.

To reduce calls, a transactional version of POST virtual_machines, POST discs and POST reimage are provided in a single call.

It takes a hash like:

    {
      "virtual_machine" => { ... },
      "discs"   => [ { ... }, { ... } ],
      "reimage" => { ... }
    }

The permitted attributes for each element are identical to the permitted attributes for creating a new VM or disc, or doing a reimage.

I've included a full example below.


## Power

The signal endpoint can be used to send ACPI signals to the machine, but there is also the more brute force approach - like the mains plug on a physical machine.

The power_on attribute specifies that the machine should be turned on (or that it is turned on when queried).

The autoreboot_on attribute specifies that the machine should be restarted upon power off.

Therefore the following can be achieved:

### Start:

    autoreboot_on = true
    power_on = true

### Stop:

    autoreboot_on = false
    power_on = false

### Reboot:

    autoreboot_on = true
    power_on = false


## Deleting and Purging

When a virtual machine is deleted using the DELETE endpoint, it still exists, but has it's deleted attribute set to true. This means it will be taken down and will only show 
whent he include_deleted=true query string is used.

However, it can be undeleted by setting deleted back to false for a certain amount of time after deletion (Bytemark haven't made public how long that will be).

If you wish to purge a virtual machine - either a previously deleted one, or delete a live one and ensure it can't be undeleted, you can use the purge=true query string with the 
DELETE endpoint. This will competely remove the server, put the IP address back into the
pool and allow the name to be re-used.


## Return codes

Most endpoints will block until complete and return.

The virtual machine creation calls (POST into virtual_machines and vm_create) will return 202 on success and will process the creation in the background so you need to poll and check the power_on attribute for when the machine has been powered on (if power_on was set to true when created.


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


#### Create:

Coming Soon


#### vm_create:

Coming Soon


#### Reimage:

Coming Soon


#### Signal:

Coming Soon
