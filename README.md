# grepip
[CLI] a simple bash script to filter in IPv4 addresses using GNU grep, one per line

## Examples

Let's have a random command showing up a few IPs to stdout:

`$ nslookup rackspace.com
Server:		10.0.1.1
Address:	10.0.1.1#53

Non-authoritative answer:
Name:	rackspace.com
Address: 173.203.44.122
`
We can use **grepip** to filter IPv4 so only them get displayed:

`$ nslookup rackspace.com | grepip
10.0.1.1
10.0.1.1
173.203.44.122
`

Let's also get rid of these local IPs:

`$ nslookup rackspace.com | grepip -x
173.203.44.122
`

There are a lot of way this could be improved, but for now I don't need more. 
