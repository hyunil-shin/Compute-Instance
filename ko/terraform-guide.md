<a id="third-party-user-guide-terraform-user-guide"></a>
## 서드파티 사용 가이드 > Terraform 사용 가이드
이 문서는 Terraform으로 NHN Cloud를 사용하는 방법을 설명합니다.

<a id="terraform"></a>
## Terraform
Terraform은 인프라를 손쉽게 구축하고 안전하게 변경하고, 효율적으로 인프라의 형상을 관리할 수 있는 오픈 소스 도구입니다. Terraform의 주요 특징은 다음과 같습니다.

* **Infrastructure as Code**
    * 인프라를 코드로 정의하여 생산성과 투명성을 높일 수 있습니다.
    * 정의한 코드를 쉽게 공유할 수 있어 효율적으로 협업할 수 있습니다.
* **Execution Plan**
    * 변경 계획과 변경 적용을 분리하여 변경 내용을 적용할 때 발생할 수 있는 실수를 줄일 수 있습니다.
* **Resource Graph**
    * 사소한 변경이 인프라 전체에 어떤 영향을 미칠지 미리 확인할 수 있습니다.
    * 종속성 그래프를 작성하여 이 그래프를 바탕으로 계획을 세우고, 이 계획을 적용했을 때 변경되는 인프라 상태를 확인할 수 있습니다.
* **Change Automation**
    * 여러 장소에 같은 구성의 인프라를 구축하고 변경할 수 있도록 자동화할 수 있습니다.
    * 인프라를 구축하는 데 드는 시간을 절약할 수 있고, 실수도 줄일 수 있습니다.


#### Resources 지원

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

#### Data sources 지원

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
### 알아두기

* **아래 예시에 사용된 Terraform 버전은 1.0.0입니다.**
* **버전을 포함한 구성요소의 이름과 숫자는 변경될 수 있으니, 확인 후 사용하시기 바랍니다.**


<a id="terraform-installation"></a>
## Terraform 설치
[Terraform 다운로드 페이지](https://www.terraform.io/downloads.html)에서 로컬 PC의 운영체제에 맞는 파일을 다운로드합니다. 파일의 압축을 해제하고 원하는 경로에 넣은 다음 환경 설정에 해당 경로를 추가하면 설치가 완료됩니다.

다음은 Linux(Ubuntu/Debian) 설치 예시입니다.

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```


<a id="terraform-initialization"></a>
## Terraform 초기화
Terraform을 사용하기 전에 다음과 같이 공급자 설정 파일을 생성합니다.

공급자 파일 이름은 임의로 설정 가능하며, 이 예제에서는 `provider.tf`를 사용합니다.

provider 버전은 [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)의 `VERSION` 정보를 참고하여 작성합니다.

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
    * NHN Cloud ID를 사용합니다.
* **tenant_id**
    * NHN Cloud 콘솔의 **Compute > Instance > 관리** 메뉴에서 **API 엔드포인트 설정** 버튼을 클릭해 테넌트 ID를 확인합니다.
* **password**
    * **API Endpoint 설정** 대화 상자에서 저장한 **API 비밀번호**를 사용합니다.
    * API 비밀번호 설정 방법은 **사용자 가이드 > Compute > Instance > API 사용 준비**를 참고합니다.
* **auth_url**
    * NHN Cloud 신원 서비스 주소를 명시합니다.
    * NHN Cloud 콘솔의 **Compute > Instance > 관리** 메뉴에서 **API 엔드포인트 설정** 버튼을 클릭해 신원 서비스(identity) URL을 확인합니다.
* **region**
    * NHN Cloud 리소스를 관리할 리전 정보를 입력합니다.
    * **KR1**: 한국(판교) 리전
    * **KR2**: 한국(평촌) 리전
    * **JP1**: 일본(도쿄) 리전

공급자 설정 파일이 있는 경로에서 `init` 명령을 이용해 Terraform을 초기화합니다.

```
$ ls
provider.tf
$ terraform init
```


