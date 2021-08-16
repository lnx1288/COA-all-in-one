## Create and manage policy files and user access rules

### Policy files

Each OpenStack service defines the access policies for its resources in an 
associated policy file. A resource, for example, could be API access, the 
ability to attach to a volume, or to fire up instances. The policy rules are 
specified in JSON format and the file is called 
[`policy.json`](https://docs.openstack.org/ocata/config-reference/policy-json-file.html). 
Policy files for services are usually located in the `/etc/SERVICE` directory. 
For example, the full path of the `policy.json` file for Compute (nova) would 
be `/etc/nova/policy.json`.

These policies can be modified or updated by the cloud administrator to control 
the access to the various resources. Changes to the 
[`policy.json`](https://docs.openstack.org/ocata/config-reference/policy-json-file.html) file become 
effective immediately and do not require the service to be restarted.

A good reference on policies can be found [here](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.1/html/security_and_hardening_guide/policies).

### User access rules

Access rules are fine-grained permissions for application credentials. An 
access rule comprises of a service type, a request path, and a request method. 
Access rules may only be created as attributes of application credentials, 
but they may be viewed and deleted independently.