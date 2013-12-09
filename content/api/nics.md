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
    POST /accounts/1/groups/1/virtual_machines/1/nics/1/ip_create  # add an ip address

Replace ACC_ID with the account id or name, GROUP_ID with the group id (or default), VM_ID with the id of the virtual machine and ID with the nic id.

The rules for what can be changed on a running vm are currently complex - the simple advice is to power down a machine before making changes to nics.

Note that NICs can not be changed while the VM they're assigned to is deleted.


## Attributes

* **id** - unique key (integer).
* **label** - unique device name.
* **ips** - list of ip's assigned to the interface (ipv4 and ipv6).
* **vlan_num** - maps to a bytemark vlan (contact support for vlan setup)
* **mac - mac** address for the interface.
* **extra_ips** - additional ip's (aliases).
* **virtual_machine_id** - id of the virtual machine the nic is linked to.


## Examples

#### All NICs on a VM

##### Request:

    GET /accounts/myaccountname/groups/default/virtual_machines/1234/nics

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/default/virtual_machines/1234/nics

##### Response:

    [{"id":1,"label":null,"ips":["213.123.123.123","2001:1234:1:1:ffff:ff:ff:f12f"],"vlan_num":1,"mac":"fe:ff:00:ff:ff:ff","extra_ips":{},"virtual_machine_id":1234}]
