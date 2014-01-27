---
title: 'Discs'
---

# Discs

## Introduction

As described by the [discs page](http://www.bigv.io/support/howto/disc/){:target="_blank"}:

A BigV virtual machine can have up to eight discs attached to it. Each disc device can provide up to 2TiB of storage, and is permanent. Each device can be one of four grades:

* sata: Ordinary storage (based on SATA discs in 6-8 drive RAID10)
* sas: Faster storage (based on 15,000 RPM discs)
* ssd: Lightning-fast storage (based on Intel SSD devices)
* archive: Cheap, voluminous storage (based on SATA discs in 6-8 drive RAID6)

Each storage grade is priced differently.

The currently available storage grades are defined in the [definitions call](/api/definitions).

The rules for what can be changed on a running vm are currently complex - the simple advice is to power down a machine before making changes to discs.

Note that discs can not be changed while the VM they're assigned to is deleted.

## Endpoints

    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/discs    # all
    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/discs/ID # single
    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/discs    # create
    PUT    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/discs/ID # update
    DELETE /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/discs/ID # delete

Replace ACC_ID with the account id or name, GROUP_ID with the group id or name (or "default" if you don't use groups!), VM_ID with the id of the virtual machine and ID with the disc id.


## Attributes

* **id** - unique key (integer).
* **label** - unix device label.
* **size** - size in bytes.
* **virtual_machine_id** - id of the vm it's attached to.
* **storage_pool** - location of the drive on BigV's storage servers (tails).
* **storage_grade** - device type, eg: sata, sas, ssd or archive.


## Examples

#### All Discs on a VM

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines/1234/discs

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines/1234/discs

##### Response:

    [{"id":1111,"label":"vda","size":25600,"virtual_machine_id":1234,"storage_pool":"tail1-sata1","storage_grade":"sata"}]


#### Single Disc on a VM

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines/1234/discs/1111

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines/1234/discs

##### Response:

    {"id":1111,"label":"vda","size":25600,"virtual_machine_id":1234,"storage_pool":"tail1-sata1","storage_grade":"sata"}

