## Manage permissions on a container in object storage

  * [Manage access](https://docs.openstack.org/newton/user-guide/cli-swift-manage-access-swift.html)
  * [Access Control Lists (ACLs)](https://docs.openstack.org/swift/latest/overview_acl.html)

Permissions in Swift can be configured through Access Control Lists (ACLs). 
Users can set up access control lists (ACLs) at the container level and define 
the read and write access. To successfully write to a container, in addition to 
write access, a user must also have read access on the container. 

When defining an ACL, one can replace the project/user name with project/user 
UUID, i.e., `<project_uuid>:<user_uuid>`. If using multiple keystone domains, 
UUID format is required.

There are two types of ACLs:

  * __Container ACLs__:. These are specified on a container and apply to that 
container only and the objects in the container.
  * __Account ACLs__: These are specified at the account level and apply to all 
containers and objects in the account.

Each ACL is a comma-delimited list of ACL elements. These elements can be built 
in two ways:

  1. Based on URL

       *  `.r:*`: every user has access, no Auth Token required
       *  `.r:test.com`: access is granted if ULRL referrer is from `test.com`
       *  `.rlistings`: user can list content on container if read access is 
granted

        Example: `.r:*,.rlistings` --> everyone can list container, read and
download objects 
  
  2. Based on Keystone object (auth token needed)

       * `<project-id>:<user-id>`: specific user scoped to specific project 
       * `<project-id>:*`: all users in specific project
       * `*:<user-id>`: specific user scoped to any project
       * `*:*`: all users in all projects
       * if a single word is passed Swift assumes its a role meaning that it 
targets any user granted that role in the project owning the container.

__IMPORTANT__: if a user is granted access to a container but scoped to a 
project different than the container owner, the `--os-storage-url` must be used.
Example: `swift download container1 object1 --os-storage-url http://controller:8080/v1/AUTH_b123bdb345b345bb6345b345` 