---
title: 'Definitions'
---

# Definitions

## Introduction 

This call gives general information about the platform, like available distributions, hardware profiles and storage grades.

This call does not require authentication and is read only.


## Endpoints

    GET /definitions


## Attributes

Each set of information contains a text id field and a data field containing an array.

The id's are as follows:

* distributions
* storage_grades
* hardware_profiles
* keymaps
* sendkeys


## Sections


### Distributions

The operating systems / distributions available to install on new VM's

* centos-5.8 - Centos 5.8
* centos-6.3 - Centos 6.3
* oneiric - Ubuntu 12.04 (precise)
* precise - Ubuntu 12.04 (precise)
* squeeze - Debian 6.0 (squeeze)
* symbiosis - Bytemark Symbiosis (based on Debian/squeeze - see [http://symbiosis.bytemark.co.uk](http://symbiosis.bytemark.co.uk])
* wheezy - Debian 7.0 (wheezy)
* winweb2k8r2 - Windows Server 2008r2
* winstd2012 - Windows Server 2012


### Storage Grades

Several different storage grades are provided to cater for different price vs performance requirements.

* archive - Cheapest storage - great for low performance requirements.
* sata - Medium grade discs - default for new vm's
* sas - Higher grade storage - ideal for more demanding tasks such as database access
* ssd - Fastest, solid state storage, SSD-backed

Note VM's with the the older compatibility2011 hardware profile (see below) might not see much benefit when using SSD's, over SAS due to the comparatively inefficient storage driver.


### Hardware Profiles

Several different hardware profiles are provided for different different performance vs backwards compatibility requirements.

* compatibility2011 - Older QEmu version
* compatibility2013 - Newer QEmu version - will not (currently) be auto upgraded
* virtio2011 - Will be upgraded to virtio2013 on restart
* virtio2013 - Faster, newer version of QEmu - may be auto-upgraded in future

For consistent behaviour between reboots, choose one of the compatibility options. The virtio profiles
(virtio2013 for example) can be used if you'd prefer to be upgraded automatically on shutdown/restart
when a new profile is available. Some operating systems without the appropriate drivers may need the
compatibility2011 option.

More information here: [http://www.bigv.io/support/howto/vm/hwprofile](http://www.bigv.io/support/howto/vm/hwprofile) and here: [http://blog.bytemark.co.uk/2013/05/09/hardware-profiles-upgrades](http://blog.bytemark.co.uk/2013/05/09/hardware-profiles-upgrades)


### Keymaps

Keyboard mappings for VNC/SSH.


### Sendkeys

Used for defining how to send special keys for VNC/SSH.


## Examples

##### Request:

    GET /definitions

##### Curl:

    curl -H "Content-type: application/json" \
         -sslv3 \
         -X GET \
         https://uk0.bigv.io/definitions

##### Response:

    [{"id":"distributions","data":["centos-5.8","centos-6.3","oneiric","precise","squeeze","symbiosis","wheezy","winweb2k8r2","winstd2012"]}
    {"id":"storage_grades","data":["archive","sata","ssd","sas"]},
    {"id":"hardware_profiles","data":["virtio2011","compatibility2011","virtio2013","compatibility2013"]},
    {"id":"keymaps","data":["ar","de-ch","es","fo","fr-ca","hu","ja","mk","no","pt-br","sv","da","en-gb","et","fr","fr-ch","is","lt","nl","pl","ru","th","de","en-us","fi","fr-be","hr","it","lv","nl-be","pt","sl","tr"]},{"id":"sendkeys","data":["shift","shift_r","alt","alt_r","altgr","altgr_r","ctrl","ctrl_r","menu","esc","1","2","3","4","5","6","7","8","9","0","minus","equal","backspace","tab","q","w","e","r","t","y","u","i","o","p","ret","a","s","d","f","g","h","j","k","l","z","x","c","v","b","n","m","comma","dot","slash","asterisk","spc","caps_lock","f1","f2","f3","f4","f5","f6","f7","f8","f9","f10","num_lock","scroll_lock","kp_divide","kp_multiply","kp_subtract","kp_add","kp_enter","kp_decimal","sysrq","kp_0","kp_1","kp_2","kp_3","kp_4","kp_5","kp_6","kp_7","kp_8","kp_9","<","f11","f12","print","home","pgup","pgdn","end","left","up","down","right","insert","delete"]}]
