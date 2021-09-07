## Use the CLI to upload and manage files to Swift containers

### Upload objects

  * To upload an object to a container, your current working directory 
must be where the file is located or you must provide the complete path to the 
file. In other words, the `–object-name <object-name>` is an option that will 
upload file and name object to `<object-name>` or upload directory and use 
`<object-name>` as object prefix. In the case that you provide the complete path 
of the file, that complete path will be the name of the uploaded object.
  * Swift has a single object size limit of 5GiB. In order to upload files 
larger than this, we must create a large object that consists of smaller 
segments.

  * __Available methods__: CLI, GUI 
  * __Method: CLI__
    * __Base command__: `swift [properties] upload [<subcommand options>]`
    * [Command Reference](https://docs.openstack.org/python-swiftclient/latest/cli/index.html)
    * [__Examples__](https://docs.openstack.org/python-swiftclient/latest/cli/index.html#examples):
      * Upload object: 
          ```
          swift upload [--changed] [--skip-identical] [--segment-size <size>]
                    [--segment-container <container>] [--leave-segments]
                    [--object-threads <thread>] [--segment-threads <threads>]
                    [--header <header>] [--use-slo] [--ignore-checksum]
                    [--object-name <object-name>]
                    <container> <file_or_directory> [<file_or_directory>] [...]  

          # example:            
          swift upload TestContainer testSwift.txt

          # example: upload large file as static large object in 1GiB segments
          swift upload videos --use-slo --segment-size 1G myvideo.mp4
          ```

  * __Method 2: GUI__
    * __GUI Section__: `Left-hand menu -> Object Store`
    * [GUI Reference](https://docs.openstack.org/horizon/latest/user/manage-containers.html#upload-an-object)

### Manage files to Swift containers

  * __Reference__:
    * [Swift CLI tool](https://docs.openstack.org/python-swiftclient/latest/cli/index.html)
    * [GUI Reference](https://docs.openstack.org/horizon/latest/user/manage-containers.html)

### Manage containers

  * __Reference__:
    * [Openstack CLI tool](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/container.html)
    * [GUI Reference](https://docs.openstack.org/horizon/latest/user/manage-containers.html#create-a-container)

### Manage objects

  * __Reference__:
    * [Openstack CLI tool](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/object.html)
    * [GUI Reference](https://docs.openstack.org/horizon/latest/user/manage-containers.html#manage-an-object)

### Object expiration (optional)

__NOTE__: this section is out of the COA exam requirements scope at the time of
this writing, but it is included here for completeness. 

  * Any object can be set to expire at a defined moment in time.
  * An expired object is no longer accessible and eventually deleted (it can 
still be listed for some time)

  * __Available methods__: CLI
  *  __Method: CLI__
    * __Base command__: `swift post <container-name> <obj-name> -H <header>`
    * [Command Reference](https://docs.openstack.org/python-swiftclient/latest/cli/index.html)
    * [__Examples__](https://docs.openstack.org/python-swiftclient/latest/cli/index.html#examples):
      * Set object to expire after amount of seconds: 
          ```
          # 60-second expiration example
          swift post container1 obj1 -H "X-Delete-After:60"
          ```
      * Set object to expire at specific time in epoch: 
          ```
          # date --date "Dec 1 2021 CEST 00:00:00" +%s -> 1638309600
          swift post container1 obj1 -H "X-Delete-At:1638309600"
          ```
      * Remove expiration dateh: 
          ```
          swift post container1 obj1 -H "X-Remove-Delete-At:"
          ```