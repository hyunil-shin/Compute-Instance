<a id="compute-image-console-guide"></a>
## Compute > Image > Console Guide

<a id="create-image"></a>
## Create Image

Images can be created from the root block storage of an instance. For t2, m2, c2, r2, and x1 type instances (excluding u2 type), images can be created while the instance is running, but data consistency is not guaranteed. For u2 type instances, images can only be created when the instance is in a stopped state.

Before creating an image of a Linux instance, it is recommended to initialize the machine-id to prevent duplication. For detailed instructions on initializing the machine-id, see [Guide for Initialization of Linux machine-id](#guide-for-initialization-of-linux-machine-id).

To create an image of a Windows instance, it is recommended to prepare for image creation using Sysprep and then stop the instance. For detailed instructions on using Sysprep, see [Windows Sysprep Guide](#windows-sysprep).

When creating an image from a running Windows instance, if the Windows instance was created from an image distributed before May 28, 2019, preliminary steps are required for proper operation. The Windows version of the image used to create the instance can be found under **Image Name** in the **Instance Details**. For more details, see [Guide to Creating Images from Running Windows Instances](#guide-to-creating-images-from-running-windows-instances).

> [Caution]
> The size of the created image may be larger than the actual usage of the root block storage.