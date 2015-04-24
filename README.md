# ansible-jails

Roles to manage jails on a FreeBSD host.

Right now it only setup the host and a few test jails.

There's a few caveats, you _have_ to specify one IPv4 and one IPv6 per jail
but there is no configuration of the IPv6's on the host.

Also it's kind of too static in the creation on the IPv4 configuration and
it assumes you'll be nat'ing them on a clone interface.

It uses's PF as the firewall which prevents the use of VIAMGE and virtual
network stacks in the jails.

# TODO:

* optional v4 / v6 config per jail
* creation of IP addresses at the jail creation, not a pool before
* dynamic firewall configuration at jail creation time
* mounted filesystems for the jails data (like volumes in docker)
* versionning of the master template / redeploy of jails
* linux jails
* VIMAGE support
* more modularity in what we configure (ansible tags, ability to not deal with network / firewall config)
* flexible install of the base template (fetch from remote url / build / install from sources)

