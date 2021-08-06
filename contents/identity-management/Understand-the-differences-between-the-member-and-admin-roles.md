## Understand the differences between the member and admin roles

A role is a personality that a user assumes to perform a specific set of 
operations. A role includes a set of rights and privileges. A user assumes 
that role inherits those rights and privileges. Finally, roles are assigned 
to user-project pairs.

OpenStack Identity service defines a user’s role on a project, but it is 
completely up to the individual service to define what that role means. 
This is referred to as the service’s policy. To get details about what the 
privileges for each role are, refer to the `policy.json` file available for 
each service in the `/etc/SERVICE/policy.json` file. 

Keystone provides three main roles called __admin__, __member__, and 
__reader__ by default. Operators can grant these roles to any actor 
(e.g., group or user) on any scope (e.g., system, domain, or project).

### [Roles Definitions](https://docs.openstack.org/keystone/latest/admin/service-api-protection.html#roles-definitions)

  * The `admin` role implies the `member` role, and the `member` role implies 
the `reader` role. These implications mean users with the `admin` role 
automatically have the `member` and `reader` roles, and users with the `member` 
role automatically have the `reader` role.
  * __Admin role__:
    * The most privileged operations within a given scope.
    * Having admin on a project, domain, or the system carries separate 
authorization and are not transitive. For example, users with admin on the 
system should be able to manage every aspect of the deployment because they’re 
operators. Users with admin on a project shouldn’t be able to manage things 
outside the project because it would violate the tenancy of their role 
assignment
  * __Member role__: 
    * No distinct advantage to having the `member` role instead of the `reader` 
role. 
    * More applicable to other services.
    * Provides granularity between `admin` and `reader` roles.
  * __Reader role__: 
    * provides read-only access to resources within the system, 
a domain, or a project. Depending on the assignment scope, two users with the 
`reader` role can expect different API behaviors. For example, a user with the 
`reader` role on the system can list all projects within the deployment. A user 
with the `reader` role on a domain can only list projects within their domain.
    * `reader` is the least authoritative role in the hierarchy

  __IMPORTANT__: The `admin` role is global, not per project, so granting a 
  user the `admin` role in any project gives the user administrative rights 
  across the whole environment.



