# Introduction #

Virttool was created to fill a niche on High avaliability solutions for virtualization. Other open-source virtualization management projects require a very specific setup for High Avaliability, requiring the user to change it's cluster architeture, or are hypervisor-bound.

Diferently, Virttool is designed around the [http://www.catb.org/esr/writings/taoup/html/ch01s07.html](KISS.md) concept, so that each of the interacting modules is created to be as simple as possible.

Virttool HA estrategy is more or less like [ganeti](http://code.google.com/p/ganeti/),as in we do note keep a machine memory state stored or replicated, so in case of hardware fault all the current conections are lost and the machine is restarted on another node.

Under the UNIX and KISS development philosophy, each module does only one thing. So we do not especify on architeture, leaving to the user the choice to make disk images/volumes avaliable on each of the nodes, like exporting images over [nfs](http://en.wikipedia.org/wiki/Network_File_System_(protocol)), replicating on [DRBD](http://www.linbit.com/en/products-services/drbd/), serving block devices over [NBD](http://nbd.sourceforge.net/) or using a [SAN](http://en.wikipedia.org/wiki/Storage_area_network).

## Daemon ##

The component to manage HA is simply called the daemon. It uses a simple database builds using the django framework to keep states of the cluster nodes and domains,  and in case of error takes the following actions:

  1. if one single domain on a node fails, try to restart it
  1. if restarting fails, load it on another node with enought resources or one node previously determined
  1. if loading on another node is not possible, send a message to the operator for intervention

In case of error on a whole node error, the following is tried:

  1. list each of the faulty node domains, and according to the domains priority.
  1. if there are note enough resources to run all the domains on the cluster, send a message to the operator for intervetion.