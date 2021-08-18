## Understand the difference between public versus private images

__References__: 
  * [Image visibility](https://docs.openstack.org/api-ref/image/v2/index.html#general-information)
  * [Image Sharing](https://docs.openstack.org/image-guide/share-images.html)
  * [Glance visibility wiki](https://wiki.openstack.org/wiki/Glance-v2-community-image-visibility-design)

The `visibility` property of an image determines who has access to the image. 
The possible values for image `visibility` are presented in the below table
(the default value is `private`):

__IMPORTANT__: The descriptions above discuss read access to images. Only the 
image owner (or an administrator) has write access to image properties and the 
image data payload. Further, in order to promise image immutability, the Image 
service will allow even the owner (or an administrator) only write-once 
permissions to specific image properties and the image data payload.

| Visibility                | Description                                     |
| ------------------------- | :-----------------------------------------------| 
| `public`                  | Any user may read the image and its data payload. Additionally, the image appears in the default image list of all users.|
| `community`               | Any user may read the image and its data payload, but the image does not appear in the default image list of any user other than the owner. (This visibility value was added in the Image API v2.5)|
| `shared`                  | An image must have this visibility in order for image members to be added to it. Only the owner and the specific image members who have been added to the image may read the image or its data payload. The image appears in the default image list of the owner. It also appears in the default image list of members who have accepted the image. See the Image Sharing section of this document for more information. If you do not specify a visibility value when you create an image, it is assigned this visibility by default. Non-owners, however, will not have access to the image until they are added as image members. (This visibility value was added in the Image API v2.5). |
| `private`                 | Only the owner image may read the image or its data payload. Additionally, the image appears in the owner’s default image list. Since Image API v2.5, an image with private visibility cannot have members added to it. |

Images may be shared among projects by creating members on the image. Image 
members have read-only privileges on the image. An image member is an identifier 
for a consumer with whom the image is shared. In OpenStack clouds, where the 
value of the owner property of an image is a project ID, the appropriate 
identifier to use for the member_id is the consumer’s project ID (which used to 
be called the “tenant ID”).

Image sharing is project-to-project. Thus all the individual users in the 
consuming project have access to the image. You cannot share an image with 
only one specific user in the target project. When an image is shared, the 
member is given immediate access to the image. In order to prevent spamming 
other users’ image lists, a shared image does not appear in a member’s image 
list until the member “accepts” the image.

Only the image owner may create members. Only an image member may modify his 
or her member status.

## Summary: Private vs. Public images

| Property           | Public Image               | Private Image             | 
| ------------------ | :--------------------------| :-------------------------| 
| Image creation     | Created by cloud admin     | Created by project admin  |
| Visibility         | Every user and project     | Project users only        |
