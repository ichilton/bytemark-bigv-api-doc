---
title: 'Introduction'
---

# Introduction

The API is a RESTful and therefore the type of HTTP request determines the action:

 - GET - Read Data
 - POST - Create a new entry
 - PUT - Update an existing entry
 - DELETE - Delete an entry

If you are using curl, you can specify the method with the -X parameter, eg: -X POST, -X PUT and -X DELETE.

See the examples in each section for more information about this.

It's also worth noting that PUT effectively works like PATCH - it will only update the fields supplied instead of the whole record.


## Data Format

The API uses the JSON data format.


## URL

The endpoint (url) for the API is: https://uk0.bigv.io


## Accounts, Users, Privileges and Groups

Use of all of these terms can seem a little confusing at first, but it's actually quite simple once you get your head around how things are structured and what each one is for.

Users generally relate to physical people. Each person who needs to access BigV will generally have a single user. Users can be granted access to multiple accounts.

Accounts are a billable entity. Accounts would generally relate to a company, organisation, or maybe a persion. An account can be accessed by multiple users (eg: employees) and a user can access multiple accounts (so the same user could for example, access the accounts of multiple companies and/or have a personal account). Accounts contain groups and virtual machines.

Groups are quite simply a collection of virtual machines. By default, each account contains a single group called 'default' and new virtual machines will be added to that group. You can however create more groups of your choosing to group collections of virtual machines. You can then give other users control of those groups, intead of the whole account where you might not want them to have access to everything, or individual virtual machines which would be tedious if you had a lot and multiple users. Another use of groups, apart from just grouping collections of virtual machines is for VLAN's. With assistance from Bytemark Support, each group of virtual machines can have their own private network. This will be reflected in the vlan_id field of the virtual machines.

Privileges define if (and under what conditions) a user can access either an account, a group or a virtual machine. For example, a user could be an account admin for an account under the same name, if they know their password and have a yubikey - or know their password and are coming from a certain ip address. The same user could also be the account admin for a different account if they know their password and have a yubikey. They could then be allowed to access a certain group of machines from another account just by providing their password.
