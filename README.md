# grepip
A simple bash filter for IPv4 and IPv6 addresses. This takes anything on stdin, and will only print the addresses to the output.

*Disclaimer: this script is intended for console work only. For integration inside languages use the tools provided by your language (e.g.: in Java see InetAddress, in .NET see IPAddress etc). The reasons for this is 1) any implementation using regular expressions may have bugs and 2) this depends on GNU grep, therefore it depends on the environment and may not be conveniently deployed).*

IPv4 examples
----------

Say we have this:

```bash
$ nslookup rackspace.com
Server:		10.0.1.1
Address:	10.0.1.1#53

Non-authoritative answer:
Name:	rackspace.com
Address: 173.203.44.122
```

Let's filter in IP addresses (IPv4 only for the time being):

```bash
$ nslookup rackspace.com | grepip
10.0.1.1
10.0.1.1
173.203.44.122
```

Let's exclude local IPs (see RFC1918):

```bash
$ nslookup rackspace.com | grepip -x
173.203.44.122
```

IPv6 examples
-------------

Note we don't yet make a distinction between IPv6 addresses (e.g.: ::1) and masks (e.g.: ::1/128). That distinction may be introduced in a future version.

Say we have this command:

```bash
$ /sbin/route -A inet6               
Kernel IPv6 routing table
Destination                    Next Hop                   Flag Met Ref Use If
::1/128                        ::                         Un   0   1476629 lo
fe80::223:32ff:fe93:1cf0/128   ::                         Un   0   1     0 lo
fe80::/64                      ::                         U    256 0     0 eth0
ff00::/8                       ::                         U    256 0     0 eth0
::/0                           ::                         !n   -1  1 68283 lo
```

As before we can filter IPv6 addresses/masks:

```bash
$ /sbin/route -A inet6 | grepip -6
::1/128
fe80::223:32ff:fe93:1cf0/128
fe80::/64
ff00::/8
::/0
```

Finally, we can filter non-locale addresses with -x:

```bash
$ /sbin/route -A inet6 | grepip -6 -x
ff00::/8
```

Usage
-------
```bash
$ grepip -h
grepip v0.2 - extract and show IP addresses (IPv4 or IPv6), one per line
Syntax: somecommand | grepip [OPTIONS]

OPTIONS:
 -x --no-local      Exclude local IPs
 -4                 Enable IPv4 mode (the default)
 -6                 Enable IPv6 mode
 --help -h          Show help and exit
 --version -v       Show version and exit
```
