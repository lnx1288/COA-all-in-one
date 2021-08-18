## Manage image types and backends

### Image types

__Reference__: [Disk and Container Formats](https://docs.openstack.org/glance/latest/user/formats.html)

The disk format of a virtual machine image is the format of the underlying disk 
image. Virtual appliance vendors have different formats for laying out the 
information contained in a virtual machine disk image. On the other hand, the 
container format refers to whether the virtual machine image is in a file 
format that also contains metadata about the actual virtual machine.

### Glance storage backends

__Reference__: [Configure Glance storage backends](https://docs.openstack.org/glance/latest/configuration/configuring.html#configuring-glance-storage-backends)

Glance can support various data store backends, such as Swift, Ceph, NFS, local 
file system, and others. Storage vendors like EMC or NetApp produce plug-ins 
for their own hardware. You can define each particular back end in the 
`[glance_store]` section of the configuration file 
`/etc/glance/glance-api.conf`. Here is the simplest example of the local file 
system:

```
[glance_store]
...
default_store = file
filesystem_store_datadir = /var/lib/glance/images/
```

If you look at this directory, you can find files with the names that are equal 
to the image’s ID:

```
# ls -l /var/lib/glance/images/
total 329080
-rw-r----- 1 glance glance 13287936 Mar 12 21:25 e5791edb-30dd-475a-9bc4-5938341db655
-rw-r----- 1 glance glance 323682816 Mar 12 21:41 f42295b8-d600-4a67-86b7-dcda07652db4
ls -l /var/lib/glance/images/
```

```
$ openstack image list
+--------------------------------------+---------------------+
| ID                                   | Name                |
+--------------------------------------+---------------------+
| f42295b8-d600-4a67-86b7-dcda07652db4 | ubuntu-amd64        |
| e5791edb-30dd-475a-9bc4-5938341db655 | cirros-0.3.4-x86_64 |
+--------------------------------------+---------------------+
```

Glance can serve multiple backends at the same time. In this case Glance will 
choose a particular backend depending on the free space and priority.