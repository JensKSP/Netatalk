# Netatalk 2.x
A fork of the Netatalk 2 codebase which takes in post-2.2.6 downstream patches from various sources, while adding some modern conveniences such as [systemd unit configurations for all daemons](https://github.com/rdmark/Netatalk/tree/branch-netatalk-2-2-x/distrib/initscripts).

The primary focus of this fork is to have a version of Netatalk 2 that runs well on modern OSes, in particular Linux and NetBSD.

As of Netatalk 3.0, support for Apple's legacy AppleTalk (DDP) protocol was dropped. AppleTalk is required for Macs running System 6.0 through Mac OS 7.6, as well as supported Apple II systems, to be able to connect to an AppleShare server out of the box. Additionally, AppleTalk support brings the convenience of a printer server (papd) which can act as a two-way bridge for using modern printers on old Macs, and vice versa, as well as a time server (timelord,) plus an Apple II netboot server (a2boot.)

At the same time, the ability of Netatalk 2.2 to understand both AppleTalk (DDP) and TCP/IP (DSI) allows it to serve as a bridge between very old Apple II and Mac systems, and modern macOS and other systems that understand AFP.

Hence, the need among the vintage Apple community to keep maintaining the Netatalk 2.2 codebase.

# Installation
Follow the installation steps in the [official Netatalk 2.2 documentation](http://netatalk.sourceforge.net/2.2/htmldocs/installation.html) to configure and install Netatalk.

As supplementary information when installing on Debian derivate Linux distros, you need at least these apt packages:
```
$ apt install libssl-dev libdb-dev autotools-dev automake libtool
```

## Configuration Examples
Classic Mac OS AppleTalk service discovery support only, with CUPS to enable printer sharing, running as systemd services that are enabled and started during installation.
```
$ apt install libcups2-dev cups
$ ./configure --enable-systemd --enable-systemd-start
```

Supporting Mac OS X 10.2 through macOS Mavericks: libgrypt to build the DHX2 UAM, as well as libavahi for Zeroconf (Bonjour) service discovery.
```
$ apt install libgcrypt20-dev libavahi-client-dev
$ ./configure --enable-systemd --enable-systemd-start --enable-zeroconf
```

Same as the above, but with SLP support instead of Zeroconf, for Mac OS X 10.0 and 10.1 service discovery.
```
$ apt install libslp-dev
$ ./configure --enable-systemd --enable-systemd-start --enable-srvloc --disable-zeroconf
```

# Documentation
Comprehensive [documentation for Netatalk 2.2](http://netatalk.sourceforge.net/2.2/htmldocs/) can be found on SourceForge.net