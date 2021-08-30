## Create and manage flavors

In OpenStack, flavors define the compute, memory, and storage capacity of nova 
computing instances. To put it simply, a flavor is an available hardware 
configuration for a server. It defines the size of a virtual server that can be 
launched.

A flavor consists of a list of parameters including Name, vCPUs, RAM, etc. Check
[here](https://docs.openstack.org/nova/latest/user/flavors.html) for a full 
list of the available specs.

* __Available Methods__: CLI, GUI
  * __Method 1: CLI__
    * __Base command__: `openstack flavor [actions] [properties]`
    * __Actions__: `create, delete, list, set, show`
    * [Command Reference (API V2)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/flavor.html)
    * [__Examples__](https://docs.openstack.org/nova/latest/admin/flavors.html):
      * Create flavor: 
          ```
          openstack flavor create
            [--id <id>]
            [--ram <size-mb>]
            [--disk <size-gb>]
            [--ephemeral <size-gb>]
            [--swap <size-mb>]
            [--vcpus <vcpus>]
            [--rxtx-factor <factor>]
            [--public | --private]
            [--property <key=value>]
            [--project <project>]
            [--description <description>]
            [--project-domain <project-domain>]
            <flavor-name>
          
          # example:            
          openstack flavor create \
            --public m1.extra_tiny \
            --id auto \
            --ram 256 \
            --disk 5 \
            --vcpus 1
          ```

  * __Method 2: GUI__
      * __Actions__: `create, delete, update`
      * __GUI Section__: `Left-hand menu -> Compute -> Flavors`
      * [GUI Reference](https://docs.openstack.org/horizon/latest/admin/manage-flavors.html)