<a id="compute-image-console-guide"></a>
## Compute > Image > Console Guide

<a id="create-image"></a>
## Create Image

Images can be created from the root block storage of an instance. For t2, m2, c2, r2, and x1 type instances (excluding u2 type), images can be created while the instance is running, but data consistency is not guaranteed. For u2 type instances, images can only be created when the instance is in a stopped state.

Before creating an image of a Linux instance, it is recommended to initialize the machine-id to prevent duplication. For detailed instructions on initializing the machine-id, see [Guide for Initialization of Linux machine-id](#guide-for-initialization-of-linux-machine-id).

To create an image of a Windows instance, it is recommended to prepare for image creation using Sysprep and then stop the instance. For detailed instructions on using Sysprep, see [Windows Sysprep Guide](#windows-sysprep).

When creating an image from a running Windows instance, if the Windows instance was created from an image distributed before May 28, 2019, preliminary steps are required for accurate operation. The Windows version of the image used to create the instance can be found under **Image Name** in **Instance Details**. For more details, see [Guide to Creating Images from Running Windows Instances](#guide-to-creating-images-from-running-windows-instances).

> [Caution]
> The size of the created image may be larger than the actual usage of the root block storage.

<a id="modify-image"></a>
## Modify Image

On the **Compute > Image** service page, select the desired image and click **Modify Image** to modify the image. The image modification items are as follows.

* **Image Name**: The name of the image.
* **Description**: The description of the image.
* **OS Type**: The OS type of the image. The OS type cannot be changed.
* **OS Version**: The OS version of the image.
* **Maximum CPU**: The maximum number of CPU cores when creating an instance with this image. If not specified, no maximum CPU core limit is applied.
* **Minimum CPU**: The minimum number of CPU cores when creating an instance with this image. If not specified, no minimum CPU core limit is applied.
* **Minimum Memory**: The minimum RAM size when creating an instance with this image. The default unit is **MB**. The minimum memory value is required.
* **Minimum Block Storage**: The minimum disk size when creating an instance with this image. The default unit is **GB**. The minimum block storage value is required.
* **Image Creation Feature**: Whether to allow creating other images from this image.
* **Image Download Feature**: Whether to allow users to directly download the image file.
* **User Script Feature**: Whether to enable the user script feature when creating an instance with this image.
* **Target Services**: The services where this image will be exposed. This setting only determines image visibility in the respective service and does not guarantee normal operation.