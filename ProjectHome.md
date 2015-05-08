# Virttool: Virtual Cluster management Tool #

Virttool is a tool for managing datacenters using virtualization technologies. It is comprised of two distinct but interacting modules, a lightweight high-avaliability monitoring daemon and a web interface for easy management.

It uses [libvirt](http://libvirt.org/) for node management and a database for configuration storage, and it is build using the [django framework](http://www.djangoproject.com/), giving the possibility of using many of the supported databases backends for nodes conviguration storage backend. As it inherits libvirt functionality, it is capable of managing whatever virtualization techonology libvirt supports, having been tested on production systems runing [xen](http://www.xen.org) and on a test cluster running [qemu](http://wiki.qemu.org/).

When requiring high-avaliability or live migration functionality, it is necessary to also run the virttool daemon, at it is the daemon that coordinates virtual machine placement and resource management.

