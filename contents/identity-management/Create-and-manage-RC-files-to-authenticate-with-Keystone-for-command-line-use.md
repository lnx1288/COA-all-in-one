## Create and manage RC files to authenticate with Keystone for command line use

In order to use the OpenStack CLI, you must authenticate to Keystone so that you 
can be authorized to perform an action. You can submit the required credentials 
using the command-line arguments for the OpenStack CLI client, or you can store 
the credentials as environment variables which can then be used by the 
OpenStack clients. Using environment variables is often easier.

Here is a table with the core environment variables you will have to set up:

| Environment Variable      | Purpose                                         | 
| ------------------------- | :-----------------------------------------------| 
| OS_USERNAME               | Name of your user                               |
| OS_USER_DOMAIN_NAME       | Name of the user’s domain                       |
| OS_PASSWORD               | Password for your user                          | 
| OS_PROJECT_NAME           | Name of your project                            |
| OS_PROJECT_DOMAIN_NAME    | Name of the project’s domain                    |
| OS_AUTH_URL               | URL of the keystone authentication server       |
| OS_IDENTITY_API_VERSION   | This should always be set to 3                  |

### Create and source the OpenStack RC file

1. Create a file named `openrc` (this is a convention, the name maybe 
arbitrary) and add the variable export commands:

    ```
    export OS_USERNAME=my_username
    export OS_USER_DOMAIN_NAME=my_user_domain
    export OS_PASSWORD=my_password
    export OS_PROJECT_NAME=my_project
    export OS_PROJECT_DOMAIN_NAME=my_project_domain
    export OS_AUTH_URL=http://localhost:5000/v3
    export OS_IDENTITY_API_VERSION=3
    ```
2. Source the file by executing:
   
   `source openrc`

   or

   `. openrc`

   This will ensure the variables are set up.

__NOTE__: you can pass the above variables to each `openstack` command using flags
instead of using environment variables, although the file-based method saves 
time if multiple commands are to be run. Example of flag usage:

```
openstack --os-username=admin --os-user-domain-name=Default \
            --os-password=secret \
            --os-project-name=admin --os-project-domain-name=Default \
            --os-auth-url=http://localhost:5000/v3 --os-identity-api-version=3 \
            user list
```

### Download the OpenStack RC file from the Horizon dashboard

The RC file can also be obtained from the Horizon dashboard. To download it 
just: 
    1. Clic on the top-right menu
    2. Clic on OpenStack RC file 

By doing this you will get the RC file for the user and project you were using.
If you change projects and download a new RC file, it will be set to the new 
project you changed into.  

