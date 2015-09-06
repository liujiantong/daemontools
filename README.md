Copyright 2001
D. J. Bernstein
http://cr.yp.to/daemontools.html

# Installation:

## Using the traditional SysV-init it is most easy to launch the daemontools processes:
* Put the line (completed by package/install already) at the end of /etc/inittab.
SV:12345:respawn:/command/svscanboot


* $ initctl reload-configuration
* $ initctl start svscan

## Some latest Linux (actual "linux-only") distros switch to systemd. Install daemontools as following:

$ cat /usr/lib/systemd/system/daemontools.service
[Unit]
Description=DJB daemontools
After=sysinit.target

[Service]
ExecStart=/command/svscanboot
Restart=always

[Install]
WantedBy=multi-user.target

$ systemctl enable daemontools.service
$ systemctl start daemontools.service
