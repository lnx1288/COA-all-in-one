## Manage image metadata/properties

  * [Manage image metadata/properties](https://docs.openstack.org/image-guide/introduction.html#image-metadata)
  * [List of image properties](https://docs.openstack.org/glance/latest/admin/useful-image-properties.html)

Image metadata (also known as “image properties”) provide information about 
the virtual disk stored by the Image service. The metadata is stored as part 
of the image record associated with the image data by the Image service. Image 
metadata can help end users determine the nature of an image, and is used by 
associated OpenStack components and drivers which interface with the Image 
service.

You can add metadata to Image service images by using the `--property key=value` 
parameter with the `openstack image create` or `openstack image set` command. 
All associated properties for an image can be displayed using the 
`openstack image show <image-name>` command. 

  * __Examples__:
    * Using `openstack image set`:
        ``` 
        openstack image set --property architecture=arm \
                --property hypervisor_type=qemu image_name_or_id
        ```

