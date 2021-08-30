## Compute

__References__:
  * [OpenStack Compute (nova)](https://docs.openstack.org/nova/latest/)
  * [Nova System Architecture](https://docs.openstack.org/nova/latest/user/architecture.html)
  * [Compute service overview](https://docs.openstack.org/nova/latest/install/get-started-compute.html)

Nova is the OpenStack project that provides a way to provision compute 
instances (aka virtual servers). Nova supports creating virtual machines, 
baremetal servers (through the use of ironic), and has limited support for 
system containers. Nova runs as a set of daemons on top of existing Linux 
servers to provide that service.

It requires the following additional OpenStack services for basic function:

  * Keystone
  * Glance
  * Neutron
  * Placement (responsible for tracking inventory of resources available in a 
cloud and assisting in choosing which provider of those resources will be used 
when creating a virtual machine)

Nova can also integrate with other services to include: persistent block 
storage, encrypted disks, and baremetal compute instances.

### Nova Architecture

Nova comprises multiple server processes, each performing different functions. 
The user-facing interface is a REST API, while internally Nova components 
communicate via an RPC message passing mechanism. 

![alt text](https://docs.openstack.org/nova/latest/_images/architecture.svg)

  * `nova-api` service: Accepts and responds to end user compute API calls. 
  * `nova-api-metadata` service: Accepts metadata requests from instances. 
  * `nova-compute` service: A worker daemon that creates and terminates VM 
instances through hypervisor APIs. For example, `libvirt` for KVM or QEMU and
VMwareAPI for VMware. Processing is fairly complex. Basically, the daemon 
accepts actions from the queue and performs a series of system commands such 
as launching a KVM instance and updating its state in the database.
  * `nova-scheduler` service: Takes a virtual machine instance request from 
the queue and determines on which compute server host it runs.
  * `nova-conductor` module: Mediates interactions between the `nova-compute` 
service and the database. It eliminates direct accesses to the cloud database 
made by the `nova-compute` service. The `nova-conductor` module scales 
horizontally. However, do not deploy it on nodes where the `nova-compute` 
service runs. 
  * `nova-novncproxy` daemon: Provides a proxy for accessing running instances 
through a VNC connection. Supports browser-based `novnc` clients.
  * `nova-spicehtml5proxy` daemon: Provides a proxy for accessing running 
instances through a SPICE connection. Supports browser-based HTML5 client.
  * `queue`: A central hub for passing messages between daemons. Usually 
implemented with RabbitMQ but other options are available.
  * SQL `database`: Stores most build-time and run-time states for a cloud 
infrastructure, including: available instance types, instances in use, 
available networks, projects. Theoretically, OpenStack Compute can support any 
database that SQLAlchemy supports. Common databases are SQLite3 for test and 
development work, MySQL, MariaDB, and PostgreSQL.

RPC messaging is done via the `oslo.messaging` library, an abstraction on top 
of message queues. Most of the major nova components can be run on multiple 
servers, and have a manager that is listening for RPC messages. The one major 
exception is `nova-compute`, where a single process runs on the hypervisor it 
is managing (except when using the VMware or Ironic drivers). The manager also, 
optionally, has periodic tasks.