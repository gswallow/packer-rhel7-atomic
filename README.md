## Project status
I have no idea what I'm doing.  Clone / use this repo at your own risk. :)

I'm following [Red Hat's guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/single/installation_and_configuration_guide).

## Building from ISO
Download the Red Hat Atomic Host [Installer](https://access.redhat.com/downloads/content/271)
The ISO_URL environment variable must be set to the ISO location:

    ISO_URL=iso/rhel-atomic-installer-7.4.2-1.x86_64.iso packer build rhel-atomic-7.4-vbox.json

## Registering with RedHat
Run `sudo subscription-manager register --username XXXX --auto-attach` once logged in.

## Issues
Vagrant is going to try to mount shares and install VirtualBox guest additions, and it will fail.

## Why?
[Because.](http://rhelblog.redhat.com/2017/03/13/introducing-the-red-hat-enterprise-linux-atomic-base-image/)

I couldn't get the atomic Docker image to install any packages on regular RHEL 7.

    docker pull registry.access.redhat.com/rhel7-atomic
    docker run -t -i -- registry.access.redhat.com/rhel7-atomic /bin/bash
    microdnf --enablerepo=rhel-7-server-rpms install java-1.8.0-openjdk-headless --nodocs
