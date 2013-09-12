---
title: 'IPs'
---

# IPs

## Introduction

Each virtual machine can have multiple ip addresses. The ips endpoint allows management of the Reverse DNS for these ip addresses.


## Endpoints

    GET /ips/<ipaddress>  # show details of ip
    PUT /ips/<ipaddress>  # update rdns

    POST /accounts/1/groups/1/virtual_machines/1/nics/1/ip_create # add ip to vm


## Attributes

These are the attributes for /ips:

* **address** - The ip address.
* **rdns** - The hostname for reverse dns.

These are the attribute for /accounts/1/groups/1/virtual_machines/1/nics/1/ip_create:

* **addresses** - how many addresses are being requested (integer)
* **contiguous** - Does the user want a block, or are they happy with a non-contiguous allocation? (currently not implemented)
* **family** - "ipv4" or "ipv6"
* **reason** - A description of why the user requires this allocation (string)


## Examples

#### IP Information:

##### Request:

    GET /ips/213.123.123.123

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/ips/213.123.123.123

##### Response:

    {"address":"213.123.123.123","rdns":"myhost.mydomain.com"}


#### Update Reverse DNS:

##### Request:

    PUT /ips/213.123.123.123

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         -X PUT -d '{"rdns":"mynewhost.mydomain.com"}' \
         https://uk0.bigv.io/ips/213.123.123.123

##### Response:

    {"address":"213.123.123.123","rdns":"mynewhost.mydomain.com"}
