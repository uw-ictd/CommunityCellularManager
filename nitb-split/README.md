NITB VM Setup Instructions
==========================

Need to setup virtualbox

Need to install host extensions to the virtualbox host environment to
allow high speed USB control.

Need to add user to vboxusers

`sudo usermod -a -G vboxusers <username>`

Import and Provision the VM with vagrant/ansible

Download the UHD images sudo uhd_images_downloader
* Is there a way to make USB accessible to the vagrant user?

Need to log into guest machine and test usb interface (sudo uhd_find_devices)
* On my system the radio performed best when connected directly to a
  superspeed usb port on my computer, bypassing any external hubs.

Install osmocom packages
------------------------

These packages should be installed by ansible via vagrant as a part of machine provisioning:
 * osmo-hlr
 * osmo-msc
 * osmo-mgw
 * osmo-stp
 * osmo-bsc
 * osmo-bts-trx
 * osmo-trx

 Installed manually for now:
 * osmo-ggsn
 * osmo-sgsn

Do Osmocom Config
-----------------

Ansible via vagrant will copy the osmocom configuration files in
version control here into the guest VM. If they are modified they will
need to be recopied to /etc/osmocom/*

Ansible will make an osmocom directory at `/var/lib/osmocom` for the
hlr database.

`sudo mkdir -p /var/lib/osmocom`


Scratch for packet data bringup
-------------------------------

Need to setup the box ip address to match the vagrant assigned ip address

Log colorization is nice: `sudo tail -F /var/log/syslog | ccze -A`

Need to manually enable ip forwarding and ip masquerade

To enable ip forwarding with echo you need to do so from a root shell,
`sudo su ; echo 1 > /proc/sys/net/ipv4/ip_forward ; exit`

Need to automate disabling the default osmo services and installing the nitb service files.

Enable IP masquerade on the eth0 output interface

`iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE`

Need to set an APN in the phone, but it doesn't matter what is set, as
long as it's *not* the apn set in the osmocom config for some reason.
