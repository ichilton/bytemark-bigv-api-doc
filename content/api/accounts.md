---
title: 'Accounts'
---

# Accounts

## Introduction 

Accounts are a billable entity. Accounts would generally relate to a company, organisation, or maybe a persion. An account can be accessed by multiple users (eg: employees) and a user can access multiple accounts (so the same user could for example, access the accounts of multiple companies and/or have a personal account). Accounts contain groups and virtual machines.

To understand how this fits with groups, users and privileges, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV Accounts can be found here: [http://www.bigv.io/support/howto/account/](http://www.bigv.io/support/howto/account/)


## Endpoints

* POST   /accounts     - create a new account
* GET    /accounts     - list of accounts
* GET    /accounts/:id - details of existing account
* PUT    /accounts/:id - update existing account
* DELETE /accounts/:id - delete account (fails if account not empty)


## Attributes

* id - Unique key (integer)

* name - Account name (string)

* suspended - Flag to indicate the account has been suspended (boolean - true/false)


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


