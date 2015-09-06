Copyright 2001
D. J. Bernstein
http://cr.yp.to/daemontools.html

# Launch daemontools:

## Using the traditional SysV-init it is most easy to launch the daemontools processes:

1. Put the line (completed by package/install already) at the end of /etc/inittab.

    SV:12345:respawn:/command/svscanboot


2. $ initctl reload-configuration
3. $ initctl start svscan

## Some latest Linux (actual "linux-only") distros switch to systemd. Launch daemontools as following:

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
