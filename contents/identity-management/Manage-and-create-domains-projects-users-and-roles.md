## Manage and create domains, projects, users, and roles

### 1. Services

__NOTE__: this topic may be out of COA scope but it's included here for 
completeness.

  * __Available Methods__: CLI
  * __Method 1: CLI__
    * __Base command__: `openstack service [actions] [properties]`
    * __Actions__: `create, delete, list, set, show`
    * [Command Reference (API V3)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/service-v3.html) 
    * __Examples__:
      * Create service: 
          ```
          openstack service create
              [--name <name>]
              [--description <description>]
              [--enable | --disable]
              <type>
          
          # example:            
          openstack service create \
              --name glance \
              --description "OpenStack Image service" \
              image
          ```

### 2. Endpoints

__NOTE__: this topic may be out of COA scope but it's included here for 
completeness.

  * __Available Methods__: CLI
  * __Method 1: CLI__
    * __Base command__: `openstack endpoint [actions] [properties]`
    * __Actions__: `add project, create, delete, list, remove project, set, show`
    * [Command Reference (API V3)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/endpoint-v3.html) 
    * __Examples__:
      * Create endpoint: 
          ```
          openstack endpoint create
              [--region <region-id>]
              [--enable | --disable]
              <service>
              <interface>
              <url>
          
          # example:            
          openstack endpoint create \
              --region RegionOne \
              identity \
              public \
              http://controller:5000/v3
          ```

### 3. Domains

  * __Available Methods__: CLI
  * __Method 1: CLI__
    * __Base command__: `openstack domain [actions] [properties]`
    * __Actions__: `create, delete, list, set, show`
    * [Command Reference](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/domain.html) 
    * __Examples__:
      * Create domain: 
          ```
          openstack domain create
              [--description <description>]
              [--enable | --disable]
              [--or-show]
              [--immutable | --no-immutable]
              <domain-name>
          
          # example:
          openstack domain create \
              --description "An Example Domain" \
              --or-show \
              example
          ```
  
    __NOTE__: although `domains` cannot be managed using the GUI, you can still 
    list the existing domains. For that you can login to the GUI and clic on 
    __Identity->Domains__ on the left-hand menu. 

### 4. Projects

  * __Available Methods__: CLI, GUI
  * __Method 1: CLI__
    * __Base command__: `openstack project [actions] [properties]`
    * __Actions__: `create, delete, list, set, show`
    * [Command Reference (API V3)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/project-v3.html) 
    * __Examples__:
      * Create project: 
          ```
          openstack project create
              [--domain <domain>]
              [--parent <project>]
              [--description <description>]
              [--enable | --disable]
              [--property <key=value>]
              [--or-show]
              [--immutable | --no-immutable]
              [--tag <tag>]
              <project-name>
          
          # example:
          openstack  project create \
              --description "Development Project" \
              --or-show \
              dev
          ```
  * __Method 2: GUI__
    * __Actions__: `create, delete, update`
    * __GUI Section__: `Left-hand menu -> Identity -> Projects`
    * [GUI Reference](https://docs.openstack.org/horizon/latest/admin/manage-projects-and-users.html)

### 5. Users

  * __Available Methods__: CLI, GUI
  * __Method 1: CLI__
    * __Base command__: `openstack user [actions] [properties]`
    * __Actions__: `create, delete, list, password set, set, show`
    * [Command Reference (API V3)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/user-v3.html) 
    * __Examples__:
      * Create user: 
          ```
          openstack user create
            [--domain <domain>]
            [--project <project>]
            [--project-domain <project-domain>]
            [--password <password>]
            [--password-prompt]
            [--email <email-address>]
            [--description <description>]
            [--ignore-lockout-failure-attempts]
            [--no-ignore-lockout-failure-attempts]
            [--ignore-password-expiry]
            [--no-ignore-password-expiry]
            [--ignore-change-password-upon-first-use]
            [--no-ignore-change-password-upon-first-use]
            [--enable-lock-password]
            [--disable-lock-password]
            [--enable-multi-factor-auth]
            [--disable-multi-factor-auth]
            [--multi-factor-auth-rule <rule>]
            [--enable | --disable]
            [--or-show]
            <name>
          
          # example:
          openstack user create \
            --email "user1@example.com" \
            --description "Dev User1" \
            --project dev \
            --password-prompt \
            user1
          ```
  * __Method 2: GUI__
    * __Actions__: `create, delete, update`
    * __GUI Section__: `Left-hand menu -> Identity -> Users`
    * [GUI Reference](https://docs.openstack.org/horizon/latest/admin/manage-projects-and-users.html)

### 6. Roles

  * __Available Methods__: CLI, GUI
  * __Method 1: CLI__
    * __Base command__: `openstack role [actions] [properties]`
    * __Actions__: `add, assignment list, create, delete, list, remove, set, show`
    * [Command Reference (API V3)](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/role-v3.html) 
    * __Examples__:
      * Add role: 
          ```
          openstack role add
            [--system <system> | --domain <domain> | --project <project>]
            [--user <user> | --group <group>]
            [--group-domain <group-domain>]
            [--project-domain <project-domain>]
            [--user-domain <user-domain>]
            [--inherited]
            [--role-domain <role-domain>]
            <role>
          
          # example:
          openstack role add \
            --user user1 \
            --project dev \
            admin
          ```
  * __Method 2: GUI__
    * __Actions__: `create, edit, delete`
    * __GUI Section__: `Left-hand menu -> Identity -> Roles`
    * [GUI Reference](https://docs.openstack.org/horizon/latest/admin/admin-manage-roles.html)