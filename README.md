# cosmosforge

Fully-remote version of Forge using iPXE and S3

# EXPERIMENTAL

This is a stripped-down version of the code for managing Brian's Forge system for network booting/configuring Linux systems,
aimed primarily at use via the Internet, using AWS S3 for storage/HTTP access to files and configs, and expecting an iPXE boot
system to retrieve information.

Set AWS_PROFILE to the profile that has access to the S3 bucket.

playbook_bootinfo.yml only needs to be run to update the boot images for the relevant distros and versions. Unless adding a distro or version, or if you know a distro has had a point release update, it doesn't need to be run every time as it needs to download the images locally and then upload them to S3 which may just waste time. If it downloads it, it will upload it as it cannot detect if it has changed.

## True RHEL

Note that while we can easily grab boot files for non-RHEL RHEL-ish distros, we can't do that for RHEL itself as the repos are not public/obfuscated. Instead, manually get the vmlinuz and initrd.img files from the ISO installer and place them similarly. The smaller "boot" ISO is fine for getting the files.
