# grepip
[CLI] a simple bash script to filter in IPv4 addresses using GNU grep, one per line

Examples
----------

Let's suppose we have a random command showing along a few IPs to stdout:

  $ nslookup rackspace.com
  Server:		10.0.1.1
  Address:	10.0.1.1#53
  
  Non-authoritative answer:
  Name:	rackspace.com
  Address: 173.203.44.122

We can use **grepip** so that only IPv4 get displayed:

  $ nslookup rackspace.com | grepip
  10.0.1.1
  10.0.1.1
  173.203.44.122

The --no-local option, aka -x, will exclude local IPv4 addresses.
In short, it will not show IPs like 192.168.x.x, 10.x.x.x and (some of) the 172.x.x.x (RFC 1918 for details).

  $ nslookup rackspace.com | grepip -x
  173.203.44.122

