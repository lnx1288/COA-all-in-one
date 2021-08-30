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

### Compute concepts

There are various important concepts to be familiar with related to the compute
service and instance management. The most important ones according to the 
[COA exam topics](https://www.openstack.org/coa/requirements) are briefly 
discussed below:

#### Flavors

In OpenStack, a flavor defines the compute, memory, and storage capacity of 
an instance. To put it simply, a flavor is an available hardware configuration 
for a VM and it defines the VM size that can be launched. As an administrative 
user, you can create, edit, and delete flavors. Immediately after installation 
of OpenStack, several predefined flavors are available to be used.

Flavors can also determine on which compute host a flavor can be used to launch 
an instance. 

#### Security groups

Security groups are sets of IP filter rules that are applied to all project 
instances, which define networking access to the instance. Group rules are 
project specific; project members can edit the default rules for their group 
and add new rule sets.

All projects have a `default` security group which is applied to any instance 
that has no other defined security group. Unless you change the default, this 
security group denies all incoming traffic and allows only outgoing traffic to 
the instance.

#### Snapshots

A `snapshot` is a mechanism that allows you to create a new image from a 
running instance. This mainly serves two purposes:

  * Backup: save the main disk of your instance to an image and later boot a 
new instance from this image with the saved data.
  * Templating: customise a base image and save it to use as a template for 
new instances.

It is important to know that a `snapshot` is not an instance recovery point,
it is the same as a regular Glance image. You can start a new virtual machine 
from a `snapshot` of another virtual machine.

#### Quotas

Nova uses a quota system for setting limits on resources such as number of 
instances or amount of CPU that a specific project or user can use. 


