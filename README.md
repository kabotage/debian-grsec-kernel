About
==============
 
This script will:
 
 - Check the build environment.
	- will exit+warn if it can't find build packages.
	- will exit if run as root.
 - Check the grsecuity website (over HTTPS) for the most recent testing version of the patch. 
 - Download grsec patch and the Linux Kernel sources (over HTTPS) that the patch uses, if we don't have them locally. 
 - Verify downloads with pgp keys.
	- will download keys from keyservers if missing.
 - Untar Linux source (will keep compressed source).
 - Patch the kernel with the most recent grsec patch.
	- if there is a new grsec patch then rm the old linux dir and untar.
 - Build the .deb packages, if we have a .config file.
 - Copy .deb files and .config from build into a folder

Use
---
 
Link to this script from where you want to build/store the kernels, eg:

    ln -sf <path_to_repo>/kernel-builder.sh ~/src/kernel/

For usage information run with no options, such as:

    ./kernel-builder.sh

Grsec notes
-----------
It has been found that PAX was killing update-grub programs, which are run after a kernel 
install by /etc/kernel/postinst.d/zz-update-grub and on removing a kernel by 
/etc/kernel/postrm.d/zz-update-grub

To stop this use the paxctl command to disable protections on /usr/sbin/grub-probe and 
/usr/bin/grub-script-check

Backup the binaries first before converting them. (paxctl -cC /bin/program) 

Credit
---------
This script was initially based on [get-and-build.sh by StalkR](https://github.com/StalkR/misc/blob/master/kernel/get-and-build.sh)

It was radically altered by [redrs](https://github.com/redrs/debian-grsec-kernel)

[auraltension](https://github.com/auraltension/debian-grsec-kernel) then picked up the project,
and as pull requests upstream have not been responded to, nor has the code been touched in
over a year, I consider this repo to be the up-to-date project.
