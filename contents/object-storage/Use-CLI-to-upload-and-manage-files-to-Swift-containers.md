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
  * [Command Reference](https://docs.openstack.org/python-swiftclient/latest/cli/index.html)
  * [GUI Reference](https://docs.openstack.org/horizon/latest/user/manage-containers.html)
### Object expiration (optional)

__NOTE__: this section is out of the COA exam requirements scope at the time of
this writing, but it is included here for completeness. 

  * Any object can be set to expire at a defined moment in time.
  * An expired object is no longer accessible and eventually deleted (it can 
still be listed for some time)
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
      * Remove expiration date: 
          ```
          swift post container1 obj1 -H "X-Remove-Delete-At:"
        ```