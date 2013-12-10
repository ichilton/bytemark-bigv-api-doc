---
title: 'Accounts'
---

# Accounts

## Introduction 

Accounts are a billable entity. Accounts would generally relate to a company, organisation, or maybe a persion. An account can be accessed by multiple users (eg: employees) and a user can access multiple accounts (so the same user could for example, access the accounts of multiple companies and/or have a personal account). Accounts contain groups and virtual machines.

To understand how this fits with groups, users and privileges, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV Accounts can be found here: [http://www.bigv.io/support/howto/account/](http://www.bigv.io/support/howto/account/)


## Endpoints

    GET    /accounts      # all accounts
    GET    /accounts/ID   # single account
    POST   /accounts      # create
    PUT    /accounts/ID   # update
    DELETE /accounts/ID   # delete

Replace ID with the account id or name.

Account names can not be updated once created. Accounts can only be deleted by a user with higher permissions than the user it was created with (which may mean that currently you can't delete accounts you have created).


## Attributes

* **id** - Unique key (integer).

* **name** - Account name (string).

* **suspended** - Flag to indicate the account has been suspended (boolean - true/false).


## Parameters

There is a view parameter - setting this to 'overview' which will turn on nested information:

    GET /accounts?view=overview

This embeds other related information into the response to save making HTTP calls. Note though that not all fields are necessarily included in overview mode.


## Examples


#### All Accounts:

##### Request:

    GET /accounts

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts

##### Response:

    {"id":1,"name":"accountname","suspended":false}


#### Single Account:

##### Request:

    GET /accounts/1

or

    GET /accounts/myaccount

##### Response:

    {"id":1,"name":"myaccountname","suspended":false}

#### Create New Account:

##### Request:

    POST /accounts

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         -X POST \
         -d '{"name":"mynewaccountname"}' \
         https://uk0.bigv.io/accounts

##### Response:

    {"id":2,"name":"mynewaccountname","suspended":false}


#### Account Overview:

##### Request:

    GET /accounts?view=overview

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname?view=overview


##### Response:

    {"id"=>123, "name"=>"myaccountname", "suspended"=>false, "groups"=>[{"type"=>"application/vnd.bigv.group", "account_id"=>123, "id"=>123, "name"=>"default", "virtual_machines"=>[{"type"=>"application/vnd.bigv.virtual-machine", "autoreboot_on"=>false, "cdrom_url"=>nil, "cores"=>1, "group_id"=>123, "id"=>1234, "management_address"=>"213.123.123.123", "memory"=>1024, "name"=>"my_vm", "power_on"=>false, "keymap"=>nil, "deleted"=>false, "hostname"=>"myvm.default.myaccountname.uk0.bigv.io", "head"=>nil, "hardware_profile"=>"virtio2013", "hardware_profile_locked"=>false, "discs"=>[{"type"=>"application/vnd.bigv.disc", "id"=>1234, "label"=>"vda", "size"=>25600, "virtual_machine_id"=>1234, "storage_pool"=>"tail1-sata1", "storage_grade"=>"sata"}], "network_interfaces"=>[{"type"=>"application/vnd.bigv.network-interface", "id"=>1234, "label"=>nil, "ips"=>["213.123.123.12", "2001:1abc:12:123:ffff:ff:ffff:ff00"], "vlan_num"=>1, "mac"=>"ff:ff:00:00:00:00", "extra_ips"=>{}, "virtual_machine_id"=>1234}]}}
