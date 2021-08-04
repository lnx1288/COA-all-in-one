## Architecture and Main Components of Keystone

The Keystone or OpenStack Identity service acts as a catalog of all OpenStack 
services and provides the ability for authenticating and managing user accounts 
and role information for the cloud environment. 

Keystone supports multiple forms of authentication, including login name and
password, token-based credentials, and REST API logins. 

Let’s define some terms which Keystone operates with:

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