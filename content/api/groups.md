---
title: 'Groups'
---

# Groups (Work In Progress)


## Introduction

Groups are quite simply a collection of virtual machines. By default, each account contains a single group called 'default' and new virtual machines will be added to that group. You can however create more groups of your choosing to group collections of virtual machines. You can then give other users control of those groups, intead of the whole account where you might not want them to have access to everything, or individual virtual machines which would be tedious if you had a lot and multiple users.

To understand how this fits with accounts, users and privileges, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV Groups can be found here: [http://www.bigv.io/support/howto/group/](http://www.bigv.io/support/howto/group/)


## Endpoints

    GET    /accounts/ACC_ID/groups     # all groups
    GET    /accounts/ACC_ID/groups/ID  # single group
    POST   /accounts/ACC_ID/groups     # create
    PUT    /accounts/ACC_ID/groups/ID  # update
    DELETE /accounts/ACC_ID/groups/ID  # delete

Replace ACC_ID with the account id or name and ID with the group id.

Deletes will fail if the group is not empty (i.e has virtual machines in it).


## Attributes

Todo


## Examples

Todo
