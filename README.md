# microforge

Fully-remote version of Forge using iPXE and S3, with the miminal amout of files.

# EXPERIMENTAL

This is a stripped-down version of the code for managing Brian's Forge system for network booting/configuring Linux systems,
aimed primarily at use via the Internet, using AWS S3 for storage/HTTP access to files and configs, and expecting an iPXE boot
system to retrieve information.

Set AWS_PROFILE to the profile that has access to the S3 bucket.

playbook_bootinfo.yml only needs to be run to update the boot images for the relevant distros and versions. Unless adding a distro or version, or if you know a distro has had a point release update, it doesn't need to be run every time as it needs to download the images locally and then upload them to S3 which may just waste time. If it downloads it, it will upload it as it cannot detect if it has changed.

## True RHEL

Note that while we can easily grab boot files for non-RHEL RHEL-ish distros, we can't do that for RHEL itself as the repos are not public/obfuscated, unless we embed RHEL account credentials in the kickstart file which isn't very secure. Instead, manually get the vmlinuz and initrd.img files from the ISO installer and place them similarly, along with the BaseOS and AppStream repos (typically around 8-15GB) from the ISO. We can then install the OS without registration, which can be done after the fact (with ansible, etc.)

You also need to create an "images/" directory under BaseOS, and copy the "efiboot.img" and "install.img" files (i.e. the "stage2" installers) from the "images/" directory on the ISO. (TODO: See if this can be located in a better place)

## AWS

We CAN iPXE in AWS (see https://ipxe.org/howto/ec2 for AMIs by region), but the menu is a pain (can use the serial console, but that only works partially), so you may want to have specific ipxe profiles. 
