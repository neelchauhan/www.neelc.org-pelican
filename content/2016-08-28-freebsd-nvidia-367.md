Title: FreeBSD, NVIDIA Driver 367.35 (or later), and dealing with the change of kernel module name to nvidia-modeset
Date: 2016-08-28 17:00
Category: FreeBSD
Tags: freebsd, nvidia, graphics

**UPDATE:** A cleaner solution to this can be found at the end of this article,
as suggested by people on Reddit. I recommend you use the cleaner version
rather than the `cron` based solution.

After upgrading the software on my desktop computer from
[FreeBSD Ports](https://www.freebsd.org/ports/), I noticed that a new version
of the [NVIDIA](http://www.nvidia.com/) driver landed.

But this isn't just a seamless upgrade. And I'm not talking about
[(Wine](https://www.winehq.org/), but about the fact that the name of the
kernel module for the NVIDIA driver has changed from `nvidia` to
`nvidia-modeset`.

The change of the module name may not seem like a big deal, but the parser in
the FreeBSD bootloader (or at least the UEFI one) doesn't recognize dashes for
module names in `/boot/loader.conf`, and this is an issue for `nvidia-modeset`,
but the good news: you can use `cron` as a workaround.

How? You need to put this in `/etc/crontab` (assuming that you don't use a login manager):

	@reboot root /sbin/kldload nvidia-modeset

While the module won't load at boot time, it will load around the time you get
to the login prompt. To make the changes active, just reboot. If you do not use
a login manager, you can stop here.

On the other hand, if you do use a login manager, then a shell script can load
both the NVIDIA driver and the login manager. If you do this, first, remove
the line for your login manager in `/etc/rc.conf`, and then create a shell
script containing these contents:

	#!/bin/sh
	PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin:~/bin
	export PATH
	kldload nvidia-modeset
	sleep 2
	gdm

Replace `gdm` with the name of your login manager of choice. Here, I use `gdm`
because I use GNOME (at the time of writing), but you can make it something
else like `xdm` or `lightdm`. Keep in mind that you need to have the `PATH`
lines I shown otherwise your login manager might crash on startup (this has
been confirmed by me with `gdm`). If you were wondering, the `PATH` variable is
derived from FreeBSD's `.profile`.

After you made the shell script, you should make the shell script executable.
In case you forgot how to do this, run this:

	# chmod a+x PATH_OF_YOUR_NEWLY_CREATED_SCRIPT

And if you took the script approach, put this in your `/etc/crontab`:

	@reboot root PATH_OF_YOUR_NEWLY_CREATED_SCRIPT

And reboot your system to take advantages of the changes.

And that's it. I hope you enjoy what I done.

**Cleaner Solution:** Looking at the comments on
[FreeBSD's subreddit](https://www.reddit.com/r/freebsd/comments/501g7e/freebsd_nvidia_driver_36735_or_later_and_dealing/),
user *rhavenn* has come up with a cleaner solution. It doesn't require cron,
but instead uses `kld_list` in `/etc/rc.conf`. What you need to put in
`rc.conf` is:

	kld_list="nvidia nvidia-modeset"

This solution is cleaner, and has the benifit of loading the driver before
services are loaded, rather than after.
