NITB VM Setup Instructions
==========================

Need to setup virtualbox

Need to install host extensions to the virtualbox host environment to
allow high speed USB control.

Need to add user to vboxusers

`sudo usermod -a -G vboxusers <username>`

Import and Provision the VM with vagrant/ansible

Download the UHD images sudo uhd_images_downloader
*Is there a way to make USB accessible to the vagrant user?

Need to log into guest machine and test usb interface (sudo uhd_find_devices)

Install osmocom packages
------------------------

osmo-hlr

osmo-msc

osmo-mgw debian 9 latest build from 17-12-9 depends on libosmo-mgcp0
but it is not available. libosmo-mgcp1 is available though, maybe a
dependency specification issue? Might not be apparent when testing
packages not on a fresh system. Will try nightly. Nightly works!

osmo-stp

osmo-bsc

osmo-bts

osmo-trx

