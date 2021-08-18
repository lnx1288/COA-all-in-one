## Architecture and Main Components of Keystone

The Keystone or OpenStack Identity service acts as a catalog of all OpenStack 
services and provides the ability for authenticating and managing user accounts 
and role information for the cloud environment. 

Keystone supports multiple forms of authentication, including login name and
password, token-based credentials, and REST API logins. 

__IMPORTANT NOTE__: The Keystone operational scope is limited to the Openstack services, users, 
projects, etc. This means that, for example, if you create a new user that 
needs permissions to launch VMs in a given Openstack project, Keystone will 
be in charge of the authentication steps for this user. However, if you deploy 
a certain application within Openstack, let's say, a VM with an email server 
running on it, Keystone __won't have anything to do__ with the 
authentication of the users using the email server itself. 
### Key Keystone concepts

__Reference__: [Keystone Concepts](https://docs.openstack.org/keystone/latest/getting-started/architecture.html)

* __Service__: OpenStack cloud component listed in Keystone catalog. 
Examples of the services are Nova, Neutron, Glance, Keystone itself, etc. 
Service provides one or more endpoints through which users can access 
service’s API.
* __Endpoint__: URL from which the service is available. Service can have 
three endpoints: internal, public, and administration. They can have different 
subsets of API calls. 
* __Project__: Represents the base unit of ownership in OpenStack. Networks,
VMs, users, roles, and so on belong to a particular project. 
* __Domain__: Represents a collection of projects, groups, and users that 
defines administrative boundaries for managing OpenStack Identity entities.
* __Region__: Separates the OpenStack environment with dedicated API 
endpoints but with common Keystone service.
* __Token__: Issued by Keystone service then passed to API requests and used
by OpenStack to verify that the client is authorized to run the requested
operation. The token is issued for a limited time and, if necessary, may be
withdrawn prior to the expiration. In order to get the user token, the user must
either provide a name and password, or the name and the key to access the
API (API key). The token also contains a list of roles that defines the roles
available to the user.
* __User__: Individual API consumer. User can be associated with roles, 
projects, or both.
* __Role__: Specific set of operations associated with a user. A role 
includes a set of rights and privileges.  

### Keystone architecture

  * API endpoints typically listen on ports `5000` (for privileged calls) and 
`35357` for regular user API calls.
  * Resources throughout an Openstack cloud are identified using human-readable 
and UUIDs. Since names can be ambiguous or even not unique, UUIDs are the main
way used by Keystone to identify Openstack resources.


### Keystone services

Keystone is organized as a group of internal services exposed on one or more 
endpoints. Many of these services are used in a combined fashion by the 
frontend. For example, an authenticate call will validate user/project 
credentials with the Identity service and, upon success, create and return a 
token with the Token service. The services provided by Keystone are listed 
below:

  1. Identity: provides auth credential validation and data about users and 
groups. Both users and groups must be owned by a specific domain (not globally 
unique).
  2. Resource: provides data about projects and domains.
    * Projects: represent the base unit of ownership in OpenStack. A project 
      may contain VMS, networks, etc.
    * Domains: high-level containers for projects, users and groups.
  3. Assignment: provides data about roles and role assignments.
    * Roles: dictate the level of authorization the end user can obtain. Roles 
can be granted at either the domain or project level. A role can be assigned at 
the individual user or group level. 
    * Role Assignments: 3-tuple that has a Role, a Resource and an Identity.
  4. Token: validates and manages tokens used for authenticating requests
  5. Catalog and endpoints: provides an endpoint registry used for endpoint 
discovery.