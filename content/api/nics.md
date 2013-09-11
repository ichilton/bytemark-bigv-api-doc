---
title: 'NICs'
---

# NICs


## Introduction

The nics interface allows you to configure the network interfaces on a virtual machine.


## Endpoints

    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/nics    # all
    GET    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/nics/ID # nic
    POST   /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/nics    # create
    PUT    /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/nics/ID # update
    DELETE /accounts/ACC_ID/groups/GROUP_ID/virtual_machines/VM_ID/nics/ID # delete

Replace ACC_ID with the account id or name, GROUP_ID with the group id (or default), VM_ID with the id of the virtual machine and ID with the nic id.


## Attributes

* id
* label
* ips
* vlan_num
* mac
* extra_ips
* virtual_machine_id


## Examples

#### All NICs on a VM

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines/1234/discs

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines/1234/nics

##### Response:

    [{"id":1,"label":null,"ips":["213.123.123.123","2001:1234:1:1:ffff:ff:ff:f12f"],"vlan_num":1,"mac":"fe:ff:00:ff:ff:ff","extra_ips":{},"virtual_machine_id":1234}]
