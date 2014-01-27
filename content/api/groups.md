---
title: 'Groups'
---

# Groups


## Introduction

Groups are quite simply a collection of virtual machines. By default, each account contains a single group called 'default' and new virtual machines will be added to that group. You can however create more groups of your choosing to group collections of virtual machines. You can then give other users control of those groups, intead of the whole account where you might not want them to have access to everything, or individual virtual machines which would be tedious if you had a lot and multiple users.

Another use of groups, apart from just grouping collections of virtual machines is for VLAN's. With assistance from Bytemark Support, each group of virtual machines can have their own private network. This will be reflected in the vlan_id field of the nic assigned to the virtual machines.

To understand how this fits with accounts, users and privileges, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV Groups can be found here: [http://www.bigv.io/support/howto/group/](http://www.bigv.io/support/howto/group/)


## Endpoints

    GET    /accounts/ACC_ID/groups     # all groups
    GET    /accounts/ACC_ID/groups/ID  # single group
    POST   /accounts/ACC_ID/groups     # create
    PUT    /accounts/ACC_ID/groups/ID  # update
    DELETE /accounts/ACC_ID/groups/ID  # delete

Replace ACC_ID with the account id or name and ID with the group id or name.

Deletes will fail if the group is not empty (i.e has virtual machines in it).


## Attributes

* **id** - unique key (integer).
* **account_id** - id of the account this group belongs to.
* **name** - group name.


## Examples

#### All Groups

##### Request:

    GET /accounts/myaccountname/groups/

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups

##### Response:

    [{"account_id":1,"id":1,"name":"default"}]


#### Single Group

##### Request:

    GET /accounts/myaccountname/groups/1

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts/myaccountname/groups/1

##### Response:

    {"account_id":1,"id":1,"name":"default"}

