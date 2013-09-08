---
title: 'Accounts'
---

# Accounts

## Introduction 

A BigV account contains a set of groups, and each group contains a set of virtual machines. An account collects servers together for billing purposes, and BigV issues invoices a monthin advance.

## Fields

* id - Unique key (integer)

* name - Account name (string)

* suspended - Flag to indicate the account has been suspended (boolean - true/false)


## Parameters

There's also a view parameter, setting this to 'overview' which will
turn on nested information:

    GET /accounts?view=overview

This embeddeds other related information into the response to save making HTTP calls. Note though that not all fields are necessarily included in overview mode.


## Examples


#### All Accounts:

    GET /accounts

Response:

    [{"id":1,"name":"myaccountname","suspended":false}]

#### Single Account:

    GET /accounts/1

or

    GET /accounts/myaccount

Response:

    {"id":1,"name":"myaccountname","suspended":false}

#### Create New Account:

Request:

    POST /accounts

 Response:

    {"id":2,"name":"mynewaccountname","suspended":false}


## Curl Examples:

#### All Accounts:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/accounts

Response:

    {"id":1,"name":"accountname","suspended":false}

#### Create New Account:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         -X POST \
         -d '{"name":"mynewaccountname"}' \
         https://uk0.bigv.io/accounts

Response:

    {"id":2,"name":"mynewaccountname","suspended":false}

