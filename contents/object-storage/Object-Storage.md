## Object Storage

  * [Swift Architectural Overview](https://docs.openstack.org/swift/latest/overview_architecture.html)

In contrast to file storage, object storage works with an object that contains 
data and metadata itself. Generally, object storage provides access through an 
API. Objects are available via URLs and HTTP/HTTPS protocols. Object storage 
can distribute requests across a number of storage hosts. All objects are 
accessible in one single namespace, and object storage systems are usually 
highly scalable.

OpenStack Object Storage (swift) is used for redundant, scalable data storage 
using clusters of standardized servers to store petabytes of accessible data. 
Object Storage uses a distributed architecture with no central point of control, 
providing greater scalability, redundancy, and permanence. Objects are written 
to multiple hardware devices, with the OpenStack software responsible for 
ensuring data replication and integrity across the cluster. Storage clusters 
scale horizontally by adding new nodes. Should a node fail, OpenStack works to 
replicate its content from other active nodes. Because OpenStack uses software 
logic to ensure data replication and distribution across different devices, 
inexpensive commodity hard drives and servers can be used in lieu of more 
expensive equipment.

__IMPORTANT__: only some Swift-related operations are available using the 
`openstack` CLI client and even less are available through the Horizon 
dashboard. Therefore, the use of the `swift` client is recommended for the exam.    

### Swift Architecture

Logically, Swift consists of three levels: accounts, containers, and objects.
Each account can own many containers and one container can contain many objects.
One object can only be contained in one container. However, while the container 
can only be owned by one account, other accounts can be granted read/write 
access.

On the other hand, containers are flat namespaces, meaning that there is no 
such thing as subcontainers, folders, directories, etc. Therefore, each object 
name in a container must be unique.    

OpenStack Object Storage (swift) service provides software that stores and 
retrieves data over HTTP (all objects stored have a URL). Objects (blobs of 
data) are stored in an organizational hierarchy that offers anonymous read-only 
access, ACL defined access, or even temporary access. Object Storage supports 
multiple token-based authentication mechanisms implemented via middleware.

All objects in Swift are stored with multiple copies and are replicated in 
_as-unique-as-possible_ availability zones and/or regions.

You can identify each object by its path: 
`/account_name/container_name/object_name`

By default, the data stored in Swift will be replicated 3 times. The main 
services of Swift are object, account, and container services.

The Swift architecture is made of the following components:

  * __Proxy Server__: responsible for tying together the rest of the Swift 
architecture. For each request, it will look up the location of the account, 
container, or object in the ring (see below) and route the request accordingly.
  * [__The Ring__](https://docs.openstack.org/swift/latest/overview_ring.html): 
represents a mapping between the names of entities stored on disk and their 
physical location. The rings determine where data should reside in the cluster. 
When other components need to perform any operation on an object, container, 
or account, they need to interact with the appropriate ring to determine its 
location in the cluster. The Ring maintains this mapping using
zones, devices, partitions, and replicas. Each partition in the ring is 
replicated, by default, 3 times across the cluster, and the locations for a 
partition are stored in the mapping maintained by the ring. The ring is also 
responsible for determining which devices are used for handoff in failure 
scenarios.
  * [__Storage Policies__](https://docs.openstack.org/swift/latest/overview_policies.html): 
provide a way for object storage providers to differentiate service levels, 
features and behaviors of a Swift deployment. Each device in the system is 
assigned to one or more Storage Policies.
  * __Object Server__: simple blob storage server that can store, retrieve and 
delete objects stored on local devices.
  * __Container Server__: handle listings of objects. It doesn’t know where 
those object’s are, just what objects are in a specific container. The listings 
are stored as sqlite database files, and replicated across the cluster similar 
to how objects are.
  * __Account Server__: similar to the Container Server, excepting that it is 
responsible for listings of containers rather than objects.
  * [__Replication__](https://docs.openstack.org/swift/latest/overview_replication.html): 
designed to keep the system in a consistent state in the face of temporary 
error conditions like network outages or drive failures. The replication 
processes compare local data with each remote copy to ensure they all contain 
the latest version. Object replication uses a hash list to quickly compare 
subsections of each partition, and container and account replication use a 
combination of hashes and shared high water marks.
  * __Reconstruction__: used by Erasure Code policies and is analogous to the 
replicator for Replication type policies.
  * __Updaters__: There are times when container or account data can not be 
immediately updated. This usually occurs during failure scenarios or periods of 
high load. If an update fails, the update is queued locally on the filesystem, 
and the updater will process the failed updates.
  * __Auditors__: crawl the local server checking the integrity of the objects, 
containers, and accounts. If corruption is found (in the case of bit rot, for 
example), the file is quarantined, and replication will replace the bad file 
from another replica. If other errors are found they are logged (for example, 
an object’s listing can’t be found on any container server it should be).

### Swift implementation details

Unlike other Openstack projects, Swift can be deployed standalone (not 
integrated to an Openstack cloud) and therefore it keeps its own accounts 
database. If Swift is integrated into Openstack then Swift account auto-creation 
based on Keystone data.