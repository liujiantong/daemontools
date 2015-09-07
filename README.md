Copyright 2001
D. J. Bernstein
http://cr.yp.to/daemontools.html

**Fixed compile error in src/conf-cc**

# Launch daemontools:

http://www.tuxad.de/blog/archives/2011/12/31/djb_daemontools_with_upstart_or_systemd/index.html

## Using the traditional SysV-init

it is most easy to launch the daemontools processes:

1. Put the line (completed by package/install already) at the end of /etc/inittab.
```
SV:12345:respawn:/command/svscanboot
```

2. $ initctl reload-configuration
3. $ initctl start svscan

## Upstart offers event-based booting. 

A time ago it was dealed as a successor to SysV-init. To start daemontools as a upstart-service you must create a config file:

$ cat /etc/init/daemontools.conf
```
description     "DJB daemontools"
start on filesystem
stop on runlevel [06]
respawn
exec /command/svscanboot3
```

## Linux distros switch to systemd

Launch daemontools as following:

1. $ cat /usr/lib/systemd/system/daemontools.service
```
[Unit]
Description=DJB daemontools
After=sysinit.target

[Service]
ExecStart=/command/svscanboot
Restart=always

[Install]
WantedBy=multi-user.target
```

2. $ systemctl enable daemontools.service
3. $ systemctl start daemontools.service
