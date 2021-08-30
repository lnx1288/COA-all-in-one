# How to pass the Certified Openstack Administrator (COA) exam

The [Certified Openstack Administrator (COA)](https://www.openstack.org/coa) 
exam is hands-on, meaning that you will get access to a live Openstack 
environment and you will be asked to solve a number of questions either via 
the console or the Openstack GUI (Horizon).

The skills/contents you need to master to pass the exam are listed 
[here](https://www.openstack.org/coa/requirements). This repo intends to 
define a learning path for COA takers. In addition, a summary and/or cheatsheet 
for each examp topic is included.

## Certified Openstack Administrator: learning Path

1. __Get familiar with the exam__ structure, number of questions, duration, 
contents, etc. For this step I'd suggest the below resources:
    * [Short video introducing the exam](https://www.openstack.org/videos/summits/virtual/OpenStack-COA-Info-Session)
    * [COA exam topics](https://www.openstack.org/coa/requirements)
    * [COA handbook](https://www.openstack.org/coa/)

2. __Get a solid theoretical background__ about the Openstack architecture, core
services and projects, etc. For this step I'd suggest the below resources:
    * Udemy course "[Preparing to Certified OpenStack Administrator Exam Course](https://www.udemy.com/course/preparing-to-certified-openstack-administrator-coa-exam/)"

      At the time of this writing (Aug 2021) the course is a bit outdated. 
      Nonetheless, I believe it offers an excellent theoretical background 
      that should be more than enough to pass the exam. In addition, it gives 
      you a useful set of exercises to practice for the exam.

    * Complement the above course with any of the following books (I'd suggest 
reading the most recent one):
      * "Certified Openstack Administrator Study Guide" - Andrei Markelov
      * "Preparing for the Certified OpenStack Administrator Exam" - Matt Dorn
    
      If you're already familiar with Openstack, any of the above books plus
      hands-on practice on test labs (to work on task exeution speed) may be 
      even enough to tackle the exam (without going through the Udemy course).

    * Review [Openstack docs](https://docs.openstack.org/) if you feel that 
some topics need further explanation.

    * You may consider using the content section in this repo as a cheatsheet 
to consolidate your knowledge prior to the exam. 

3. __Practice...Practice...Practice!__

    Being performance-based, the COA exam will test your ability to perform 
    day-to-day operations on an Openstack cloud. There are two key limitations 
    on the exam: time and knowledge-base. In previous exam you were allowed to 
    use the Openstack docs as a reference but that's no longer the case.
    As a consequence you need to master both the CLI and GUI-based methods to 
    perform all the tasks listed in 
    [COA exam topics](https://www.openstack.org/coa/requirements). 

    Luckily, you can still use the embedded help on both the CLI and the GUI
    tools. I'd recommend to be quite familiar in the use of the CLI help 
    (`--help` option for the `openstack` CLI) to avoid memorizing all the 
    available options. Being proficient in using the CLI tool help will save 
    you quite a lot of time.

    To gain hands-on knowledge of Openstack I'd suggest leveraging DevStack 
    which can be used to deploy a fully-functional
    [Openstack cloud in a single host](https://docs.openstack.org/devstack/latest/guides/single-machine.html). 

    Other useful resources to practice are the 
    * [OpenStack Training Labs](https://docs.openstack.org/training_labs/).
    * [COA practice questions](https://github.com/AJNOURI/COA)

4. __Exam readiness check__

    Overall, you can consider yourself ready for the exam if:

    * You have thoroughly reviewed and practiced the 
[COA exam topics](https://www.openstack.org/coa/requirements)
    * You are able to perform these COA exam tasks:
      * without referring to the online doc for every task
      * without referring to personal notes or cheat sheets
      * without referring to content from a class
      * without relying on the online help or man pages
        
        If you use help (`--help`), do you understand the output?

## Exam tips

  * Immediately report issues to the proctor, e.g., if you notice the CLI is 
slow and affecting your speed to type and modify commands.
  * __Read each question carefully__ and answer the questions you're familiar 
with first. 
  * Copy/paste data from the question (e.g., instance/project names, flavour 
specs) to avoid wasting time typing and prevent typos.
  * Use the embedded notebook to track skipped/non-completed/flagged questions 
so that you can get back to them later.
  * Ensure that you're fully aware of any question requirements (e.g., avoid 
using a specific IP range, compulsory use of either the CLI or the GUI).
  * __Don't overthink the questions__, e.g., flavours are accessible across all 
projects unless access is specified.
  * __Consider using the CLI for the entire exam but only if you're proficient 
with it__. Fewer context switches might make things easier and less error-prone. 
However, __if for some reason you're more confortable with a GUI, then stick to 
Horizon__, most of the tasks can be done there.
  * For every topic, make sure you know which client method (CLI or GUI) is 
the best (i.e., the quickest) for you.
  * __Some tasks can only be executed via CLI__, make sure you know which ones.
Here is a non-exhaustive list of "CLI-only" tasks:
    * Managing `domains`
    * Managing `endpoints`
    * Downloading Glance images
    * Managing `swift` ACL rules and expiration dates 
  * __Check, check and check again__ to ensure your work has met the criteria, 
even if you know for a fact that your command/steps were correct. 
  * Based on my experience, the exam can be completed rather easily in half the 
time you're allowed to use. In any case, I'd suggest you save at least 30min to 
double check your work. 
  * For any tasks where you need to use floating IPs from within a project, 
create the floating IPs before any other internal network-related tasks.

## Exam contents

See below the list of contents you need to master for the COA exam. Most of the
sections have a __Reference__ included so that you can expand the summarized
content on this repo with official sources. 

#### 1. [Identity management](../main/contents/identity-management/Identity-management.md)
 * [Manage and create domains, projects, users, and roles](../main/contents/identity-management/Manage-and-create-domains-projects-users-and-roles.md)
 * [Understand the differences between the member and admin roles](../main/contents/identity-management/Understand-the-differences-between-the-member-and-admin-roles.md)
 * [Create roles for the environment](../main/contents/identity-management/Manage-and-create-domains-projects-users-and-roles.md)
 * [Create and manage policy files and user access rules](../main/contents/identity-management/Create-and-manage-policy-files-and-user-access-rules.md)
 * [Create and manage RC files to authenticate with Keystone for command line use](../main/contents/identity-management/Create-and-manage-RC-files-to-authenticate-with-Keystone-for-command-line-use.md)
#### 2. [Compute](../main/contents/compute/Compute.md)
 * [Create and manage flavors](../main/contents/compute/Create-and-manage-flavors.md)
 * Create and manage compute instances (for example, launch, shutdown, terminate)
 * Generate and manage SSH keys for use when connecting to instances
 * Access an instance using an SSH key
 * Configure an instance with a floating IP address;use it to connect to the instance
 * Create instances with security groups
 * Manage Nova host consoles (VNC, NOVNC, spice)
 * Manage instance snapshots
 * Manage instance quotas
#### 3. Object Storage
 * Use the command line client to upload and manage files to Swift containers
 * Manage permissions on a container in object storage
#### 4. Block Storage
 * Create and manage volumes
 * Attach volumes to instances
 * Create a new Block Storage volume and mount it to a Nova instance
 * Manage volume quotas
 * Backup and restore volumes
 * Manage volume snapshots (for example, create, list, recover)
#### 5. Networking
 * Manage network resources (routers, networks, subnets)
 * Create external/public networks
 * Create project networks
 * Create project routers
 * Attach routers to public and project networks
 * Manage network services for a virtual environment
 * Manage network quotas
 * Manage network interfaces on compute instances
 * Create and manage project security groups and rules
 * Assign security group to instance
 * Create and manage floating IP addresses
 * Assign floating IP address to instance
 * Detach floating IP address from instance
#### 6. [Image management](../main/contents/image-management/Image-management.md)
 * [Upload a new image to an OpenStack image repository](../main/contents/image-management/Upload-a-new-image-to-an-OpenStack-image-repository.md)
 * [Manage images (for example, add, update, remove)](../main/contents/image-management/Manage-images.md)
 * [Understand the difference between public versus private images](../main/contents/image-management/Understand-the-difference-between-public-versus-private-images.md)
 * [Manage image metadata/properties](../main/contents/image-management/Manage-image-metadata-properties.md)
 * [Manage image types and backends](../main/contents/image-management/Manage-image-types-and-backends.md)