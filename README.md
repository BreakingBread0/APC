APC Network Power Management Controller
=======================================

Payton Quackenbush

[![Build Status](https://travis-ci.org/quackenbush/APC.svg?branch=master)](https://travis-ci.org/quackenbush/APC)

Controls rebooting of APC network PDU switches with 'telnet' network interface.
Tested with the AP7900, but likely works with other models.

This handles locking of the device so that parallel calls will block, since
APC has a single telnet session.

Requirements
------------

- Python 2.x or Python 3.x
- Python Expect (pexpect) library.  To install: 'pip install pexpect'
- APC with telnet network interface (tested on AP7900)

Installation
------------

```bash
$ pip install git+https://github.com/quackenbush/APC
```

or

Download source and run

```bash
$ python setup.py install
```

The APC needs to be set up with telnet enabled, and using a fixed IP address.
If a DHCP address is used, it may change, and you will have trouble connecting.

Usage
-----

### Power cycle (reboot) a single port
```$ apc --reboot PORT```

### Example: reboot power port 1
```$ apc --reboot 1```

### Display help
```
$ apc --help

usage: apc [-h] [--host HOST] [-v] [--quiet] [--user USER]
              [--password PASSWORD] [--debug] [--reboot REBOOT] [--off OFF]
              [--on ON]

APC Python CLI

optional arguments:
  -h, --help           show this help message and exit
  --host HOST          Override the host
  --user USER          Override the username
  --password PASSWORD  Override the password
  -v, --verbose        Verbose messages
  --quiet              Quiet
  --debug              Debug mode
  --reboot REBOOT      Reboot an outlet
  --off OFF            Turn off an outlet
  --on ON              Turn on an outlet
```

Environment Variables
---------------------

The following environment variables will override the APC connection:
- $APC_HOST
- $APC_USER
- $APC_PASSWORD

Example session
---------------

```
$ apc --reboot 8
Acquiring lock /tmp/apc.lock
Connecting to APC @ 10.8.0.142
Logged in as user apc, version 3.7.3
APC 10.8.0.142: Outlet #8 Rebooted
DISCONNECTED from 10.8.0.142
```
