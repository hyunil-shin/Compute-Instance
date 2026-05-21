<a id="third-party-user-guide-terraform-user-guide"></a>
## Third Party User Guide > Terraform User Guide
This document describes how to use NHN Cloud with Terraform.

<a id="terraform"></a>
## Terraform
Terraform is an open-source tool that lets you easily build and safely change infrastructure, and also efficiently manage configuration of infrastructure. The main features of Terraform are as follows:

* **Infrastructure as Code**
    * You can increase the productivity and transparency by defining infrastructure as code.
    * You can easily share the defined code for efficient collaboration.
* **Execution Plan**
    * By separating change planning and change execution, you can reduce the potential for mistakes when making changes.
* **Resource Graph**
    * You can see in advance how minor changes will affect the entire infrastructure.
    * By creating a dependency graph, you can make a plan based on the graph and see how your infrastructure changes when you apply the plan.
* **Change Automation**
    * You can automate the process so that infrastructure with the same configuration can be built and changed in multiple locations.
    * You can save time to build infrastructure and reduce mistakes.

<a id="supported-resources"></a>
#### Supported Resources

* Compute
    * nhncloud_compute_instance_v2
    * nhncloud_compute_volume_attach_v2
    * nhncloud_compute_keypair_v2
* Network
    * nhncloud_lb_loadbalancer_v2
    * nhncloud_lb_listener_v2
    * nhncloud_lb_pool_v2
    * nhncloud_lb_member_v2
    * nhncloud_lb_monitor_v2
    * nhncloud_networking_floatingip_v2
    * nhncloud_networking_floatingip_associate_v2
    * nhncloud_networking_port_v2
    * nhncloud_networking_vpc_v2
    * nhncloud_networking_vpcsubnet_v2
    * nhncloud_networking_routingtable_v2
    * nhncloud_networking_routingtable_attach_gateway_v2
    * nhncloud_networking_secgroup_v2
    * nhncloud_networking_secgroup_rule_v2
    * nhncloud_keymanager_secret_v1
    * nhncloud_keymanager_container_v1
* Block Storage
    * nhncloud_blockstorage_volume_v2
* Object Storage
    * nhncloud_objectstorage_container_v1
    * nhncloud_objectstorage_object_v1
* Container
    * nhncloud_kubernetes_cluster_v1
    * nhncloud_kubernetes_nodegroup_v1
    * nhncloud_kubernetes_cluster_resize_v1
    * nhncloud_kubernetes_nodegroup_upgrade_v1

<a id="supported-data-sources"></a>
#### Supported Data Sources

* nhncloud_images_image_v2
* nhncloud_blockstorage_volume_v2
* nhncloud_compute_flavor_v2
* nhncloud_compute_keypair_v2
* nhncloud_blockstorage_snapshot_v2
* nhncloud_networking_vpc_v2
* nhncloud_networking_vpcsubnet_v2
* nhncloud_networking_routingtable_v2
* nhncloud_networking_secgroup_v2
* nhncloud_keymanager_secret_v1
* nhncloud_keymanager_container_v1
* nhncloud_kubernetes_cluster_v1
* nhncloud_kubernetes_nodegroup_v1

<a id="note"></a>
### Note

* **The version of the Terraform used in the examples below is 1.0.0.**
* **The name and number of the components including the version can be changed, so make sure you check the information before use.**

<a id="terraform-installation"></a>
## Terraform Installation
Go to [Download Terraform](https://www.terraform.io/downloads.html) and download the file suitable for the operating system of your local PC. Decompress the file to an appropriate path and add the path to your environment setting, and the installation is complete.

See the following example for Linux(Ubuntu/Debian) installation.

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-initialization"></a>
## Terraform Initialization
Before using Terraform, create a provider configuration file as follows.

The name of the provider file can be set randomly. This example uses `provider.tf` as the filename.

For provider version, please write it based on the [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)'s `VERSION` information.

```
# Define required providers
terraform {
  required_providers {
    nhncloud = {
      source = "nhn-cloud/nhncloud"
      version = "{VERSION}"
    }
  }
}

# Configure the nhncloud Provider
provider "nhncloud" {
  user_name   = "terraform-guide@nhncloud.com"
  tenant_id   = "aaa4c0a12fd84edeb68965d320d17129"
  password    = "difficultpassword"
  auth_url    = "https://api-identity-infrastructure.nhncloudservice.com/v2.0"
  region      = "KR1"
}
```

* **user_name**
    * Use the NHN Cloud ID.
* **tenant_id**
    * From **Compute > Instance > Management** on NHN Cloud console, click **Set API Endpoint** to check the Tenant ID.
* **password**
    * Use **API Password** that you saved in **Set API Endpoint**.
    * Regarding how to set API passwords, see **User Guide > Compute > Instance > API Preparations**.
* **auth_url**
    * Specify the address of the NHN Cloud identification service.
    * From **Compute > Instance > Management** on NHN Cloud console, click **Set API Endpoint** to check Identity URL.
* **region**
    * Enter the region to manage NHN Cloud resources.
    * **KR1**: Korea (Pangyo) Region
    * **KR2**: Korea (Pyeongchon) Region
    * **JP1**: Japan (Tokyo) Region

On the path where the provider configuration file is located, use the `init` command to initialize Terraform.

```
$ ls
provider.tf
$ terraform init
```



<!-- viewer demo: tiny en-only edit -->
