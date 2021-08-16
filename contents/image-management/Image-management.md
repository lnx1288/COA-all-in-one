## Architecture and Main Components of Glance

### What is an image?

A virtual machine image, usually referred to simply as image, is a single file 
that contains a virtual disk that has a bootable operating system installed on 
it. Images are used to create virtual machine instances within the cloud. Other
than an operating system, images may contain middleware or application software
such as Apache, MySQL, etc., in order to make deployments more agile.

### Glance Architecture

  __Reference__: [Glance Architecture](https://docs.openstack.org/glance/latest/contributor/architecture.html) 

  The following components are present in the Glance architecture:

  * A client - any application that makes use of a Glance server.
  * REST API - Glance functionalities are exposed via REST.
  * Database Abstraction Layer (DAL) - an application programming interface
(API) that unifies the communication between Glance and databases.
  * Glance Domain Controller - middleware that implements the main
Glance functionalities such as authorization, notifications, policies, 
database connections.
  * Glance Store - used to organize interactions between Glance and various
data stores.
  * Registry Layer - optional layer that is used to organise secure
communication between the domain and the DAL by using a separate service.

Glance uses plugins for particular storage, which can be your local file system, 
Swift object storage, Ceph storage, NFS, or other back ends. Metadata of images 
are stored in the Glance database. By default, `glance-api` listens on port 
`9292`. 

To validate requests made to the Glance API, you must configure the 
authentication parameters for Keystone on the Glance configuration files, i.e.,
`/etc/glance/glance-api.conf` and `/etc/glance/glance-registry.conf`:

  ```
  [keystone_authtoken]
  auth_uri=http://10.0.2.15:5000/v2.0
  identity_uri=http://10.0.2.15:35357
  admin_user=glance
  admin_password=password
  admin_tenant_name=services
  
  [paste_deploy]
  flavor=keystone
```

Depending on the OpenStack version you will need to put RabbitMQ settings 
either in the `[oslo_messaging_rabbit]` or in `[DEFAULT]` section of 
`/etc/glance/glance-api.conf` file .