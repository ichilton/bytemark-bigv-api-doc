---
title: 'Privileges'
---

# Privileges (Work In Progress)

## Introduction

Todo

## Fields

* id
* username
* level
* creating_username
* yubikey_required
* yubikey_otp_max_age
* ip_restrictions
* virtual_machine_id
* group_id
* account_id

## Examples

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/users/myusername/privileges


    [{"id":1,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/25"},"user":{"href":"/users/25"},"account":{"href":"/accounts/24","title":"Account myaccountname"}},"account_id":1},{"id":5273,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/5273"},"user":{"href":"/users/25"},"account":{"href":"/accounts/5114","title":"Account myotheraccount"}},"account_id":2}]
