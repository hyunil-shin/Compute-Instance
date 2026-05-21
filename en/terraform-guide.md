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

<a id="terraform-provider-provided"></a>
## Terraform provider provided

NHN Cloud is an official partner of HashiCorp and offers Terraform provider through [Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest).