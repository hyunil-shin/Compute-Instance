```markdown
<a id="third-party-user-guide-terraform-user-guide"></a>
## サードパーティー使用ガイド > Terraform使用ガイド
この文書はTerraformでNHN Cloudを使用する方法を説明します。

<a id="terraform"></a>
## Terraform
Terraformはインフラを簡単に構築し、安全に変更し、効率的にインフラの形状を管理できるオープンソースのツールです。Terraformの主な特徴は次のとおりです。

* **Infrastructure as Code**
    * インフラをコードで定義して生産性と透明性を高めることができます。
    * 定義したコードを簡単に共有でき、効率的に協業できます。
* **Execution Plan**
    * 変更計画と変更適用を分離して変更内容を適用する時に発生しうる失敗をへらすことができます。
* **Resource Graph**
    * 些細な変更がインフラ全体にどんな影響を与えるかを事前に確認できます。
    *従属性グラフを作成し、このグラフを元に計画を立て、この計画を適用した時に変更されるインフラの状態を確認できます。
* **Change Automation**
    * 複数の場所に同じ構成のインフラを構築し、変更できるように自動化できます。
    * インフラを構築するのにかかる時間を節約することができ、失敗も減らすことができます。


<a id="note"></a>
### 注意

* **下記例のすべてのデータは実際の情報ではありません。必ず正確な情報に修正して使用します。**
* **下記の例はすべてTerraform 0.12.24を利用しました。**


<a id="terraform-installation"></a>
## Terraformインストール
[Terraformダウンロードページ](https://www.terraform.io/downloads.html)でローカルPCのOSに合ったファイルをダウンロードします。ファイルの圧縮を解凍し、任意の場所に入れた後、次の環境設定に該当パスを追加するとインストールが完了します。

次はLinux(Ubuntu/Debian)のインストール例です。

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-provider-provided"></a>
## Terraform NHN Cloud provider提供

Terraform NHN Cloud providerは次のような**OS/アーキテクチャ**の互換性を提供し、リンクからバイナリファイルをダウンロードできます。
現在提供するTerraform NHN Cloud providerのバージョンは**1.0.2**です。

* macOS / AMD64
  * [1.0.0](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_amd64/terraform-provider-nhncloud_v1.0.0)
  * [1.0.1](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_amd64/terraform-provider-nhncloud_v1.0.1)
  * [1.0.2](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_amd64/terraform-provider-nhncloud_v1.0.2)
* macOS / Apple silicon
  * [1.0.0](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_arm64/terraform-provider-nhncloud_v1.0.0)
  * [1.0.1](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_arm64/terraform-provider-nhncloud_v1.0.1)
  * [1.0.2](https://static.toastoven.net/prod_cloud_terraform_provider/darwin_arm64/terraform-provider-nhncloud_v1.0.2)
* Linux / AMD64
  * [1.0.0](https://static.toastoven.net/prod_cloud_terraform_provider/linux_amd64/terraform-provider-nhncloud_v1.0.0)
  * [1.0.1](https://static.toastoven.net/prod_cloud_terraform_provider/linux_amd64/terraform-provider-nhncloud_v1.0.1)
  * [1.0.2](https://static.toastoven.net/prod_cloud_terraform_provider/linux_amd64/terraform-provider-nhncloud_v1.0.2)
* Windows / AMD64
  * [1.0.0](https://static.toastoven.net/prod_cloud_terraform_provider/windows_amd64/terraform-provider-nhncloud_v1.0.0)
  * [1.0.1](https://static.toastoven.net/prod_cloud_terraform_provider/windows_amd64/terraform-provider-nhncloud_v1.0.1)
  * [1.0.2](https://static.toastoven.net/prod_cloud_terraform_provider/windows_amd64/terraform-provider-nhncloud_v1.0.2)


<a id="local-provider"></a>
### Local provider設定

Local provider設定を通じてTerraform NHN Cloud providerを使用できます。

Local providerを探すためのディレクトリ構造を作成した後、ダウンロードしたバイナリファイルをプラグインのパスに追加します。バイナリファイルには実行権限が必要です。

以下はOSごとのプラグイン基本パスです。より詳しい基本パスの説明は[Terraformサイト](https://developer.hashicorp.com/terraform/cli/config/config-file#provider-installation)の`Implied Local Mirror Directories
`項目を参照してください。

* **Linux / macOS** : `${HOME}/.terraform.d/plugins/terraform.local/local/nhncloud/${version}/${platforms}`
* **Windows** : `%APPDATA%/terraform.d/plugins/terraform.local/local/nhncloud/${version}/${platforms}`

プラグイン基本パス構成ルールについての説明です。

* **version**
    * providerのバージョンです。
* **platforms**
    * パッケージがあるプラットフォームを説明するオブジェクトの配列で、OS識別キーワードとCPUアーキテクチャ識別キーワードで構成されています。
    * **darwin_adm64** : macOS / AMD64
    * **darwin_arm64** : macOS / Apple silicon
    * **linux_amd64** : Linux / AMD64
    * **windows_amd64** : Windows / AMD64

以下は、バイナリダウンロード後、**OS/アーキテクチャ**ごとのプラグイン設定例です。 

**プラグインを設定する際は1.0.2バージョンを使用することを推奨します。**

`macOS / AMD64`プラグインの設定例です。

```
$ mkdir -p $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_amd64
$ cp terraform-provider-nhncloud_v1.0.2 $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_amd64
$ chmod +x $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_amd64/terraform-provider-nhncloud_v1.0.2
```

`macOS / Apple silicon`プラグインの設定例です。

```
$ mkdir -p $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_arm64
$ cp terraform-provider-nhncloud_v1.0.2 $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_arm64
$ chmod +x $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/darwin_arm64/terraform-provider-nhncloud_v1.0.2
```

`Linux / AMD64`プラグインの設定例です。

```
$ mkdir -p $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/linux_amd64
$ cp terraform-provider-nhncloud_v1.0.2 $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/linux_amd64
$ chmod +x $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/linux_amd64/terraform-provider-nhncloud_v1.0.2
```

`Windows / AMD64`プラグインの設定例です。

```
$ mkdir -p %APPDATA%/terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/windows_amd64
$ cp terraform-provider-nhncloud_v1.0.2 $HOME/.terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/windows_amd64
$ copy terraform-provider-nhncloud_v1.0.2 %APPDATA%/terraform.d/plugins/terraform.local/local/nhncloud/1.0.2/windows_amd64
```


<a id="terraform-initialization"></a>
## Terraformの初期化
Terraformを使用する前に、次のようにプロバイダー設定ファイルを作成します。

プロバイダーファイルの名前は任意で設定可能で、この例では`provider.tf`を使用します。

providerバージョンは[NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)の `VERSION` 情報を参考にして作成します。

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
    * NHN Cloud IDを使用します。
* **tenant_id**
    * NHN Cloudコンソールの**Compute > Instance > 管理**メニューで**APIエンドポイント設定**ボタンを押してテナントIDを確認します。
* **password**
    * **API Endpoint設定**ウィンドウで保存した**APIパスワード**を使用します。
    * APIパスワードの設定方法は**ユーザーガイド > Compute > Instance > API使用準備**を参照します。
* **auth_url**
    * NHN Cloud身元サービスアドレスを明示します。
    * NHN Cloudコンソールの**Compute > Instance > 管理**メニューで**APIエンドポイント設定**ボタンをクリックして身元サービス(identity) URLを確認します。
* **region**
    * NHN Cloudリソースを管理するリージョン情報を入力します。
    * **KR1**：韓国(パンギョ)リージョン
    * **KR2**：韓国(ピョンチョン)リージョン
    * **JP1**：日本(東京)リージョン

プロバイダー設定ファイルがあるパスで`init`コマンドを利用してTerraformを初期化します。

```
$ ls
provider.tf
$ terraform init
```

### Local providerの交換

新しいバージョンのlocal providerがリリースされた場合、変更するバージョンに[local provider設定](#local-provider)を行った後、`init`コマンドの`--upgrade`オプションでプラグインをアップグレードできます。

```
$ terraform init --upgrade
Initializing the backend...
Initializing provider plugins...
- Finding terraform.local/local/nhncloud versions matching "1.0.2"...
- Installing terraform.local/local/nhncloud v1.0.2...
- Installed terraform.local/local/nhncloud v1.0.2 (unauthenticated)
Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.
```


<a id="terraform-usage"></a>
## Terraform基本使用方法

Terraformを利用したインフラ構築は、通常下記のようなライフサイクルになります。

1. tfファイル作成
2. 構築計画を確認
3. リソース作成
4. リソース修正
5. リソース削除

まず構築したいインフラの形状をtfファイルに作成します。作成されたtfファイルによる構築計画は、下記のように`plan`コマンドで確認します。

```
$ terraform plan
```

構築計画が問題なければ`apply`コマンドを利用してリソースを作成、修正、削除します。

```
$ terraform apply
```

次のセッションでは、この段階を例を用いて詳しく説明します。

<a id="create-tf-files"></a>
### tfファイル作成

プロバイダー設定ファイルがあるパスにtfファイルを作成します。複数のリソース設定を1つのtfファイルに集めるか、リソースごとに別々のtfファイルでも作成可能です。Terraformは作成された全体tfファイルを一度に読み込んで構築計画を立てます。

下記は`instance.tf`ファイルにインスタンスを作成するリソースを定義したtfファイルの例です。

```
$ ls
instance.tf provider.tf
$ cat instance.tf
resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
  name      = "terraform-instance-01"
  region    = "KR1"
  flavor_id = "da74152c-0167-4ce9-b391-8a88a8ff2754"
  key_pair  = "terraform-keypair"
  network {
    uuid = "00d5b852-cb77-4307-b6be-d81dad24eec1"
  }
  security_groups = ["default"]
  block_device {
    uuid = "6d0993b4-cd6d-4242-b59b-94258f265331"
    source_type = "image"
    destination_type = "volume"
    boot_index = 0
    volume_size = 20
    delete_on_termination = true
  }
}
```


<a id="check-the-execution-plan"></a>
### 構築計画の確認

tfファイルを通して変更されるリソースを`plan`コマンドで確認できます。`plan`コマンドを実行すると、Terraformが.tfファイルをロードして設定が正しいかを確認し、DBと比較してプランを作成します。プラン作成が完了すると、プランをタイプごとに集計して出力します。

```
$ terraform plan
```

作成されたプランが無効な場合、tfファイルを修正し、再度反復して`plan`コマンドを実行します。`plan`コマンドは実際のNHN Cloudリソースを変更しないため、インフラ変更事項を負担なく確認できます。


<a id="create-resources"></a>
### リソースを作成する

任意のプランでtfファイルを作成した後、`apply`コマンドでリソースを作成します。

下記は、上で作成した`instance.tf`ファイルを利用して`apply`コマンドを実行した結果の例です。

```
$ terraform apply
...
nhncloud_compute_instance_v2.terraform-instance-01: Creating...
nhncloud_compute_instance_v2.terraform-instance-01: Still creating... [10s elapsed]
nhncloud_compute_instance_v2.terraform-instance-01: Still creating... [20s elapsed]
nhncloud_compute_instance_v2.terraform-instance-01: Still creating... [30s elapsed]
nhncloud_compute_instance_v2.terraform-instance-01: Creation complete after 39s [id=1e846787-04e9-4701-957c-78001b4b7257]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
...
```

`apply`コマンドを実行すると、プラン変更履歴を記録するDBファイル(terraform.tfstate)が現在のディレクトリに作成されます。このファイルを削除しないように注意してください。


<a id="modify-resources"></a>
### リソースを修正する

変更するリソースが定義された`.tf`ファイルを開き、任意の情報を修正し、プランを適用します。変更できる仕様は一部プロパティに制限されます。もし変更できないプロパティを修正した場合、該当リソースは削除後に新たに再び作成されます。

次はインスタンスに`terraform-sg`セキュリティグループをもう1つ追加する例です。上で作成した`instance.tf`ファイルを下記のように修正します。

```
resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
  ...
  security_groups = ["default", "terraform-sg"]
  ...
}
```

構築計画を確認したら、変更されたセキュリティグループ情報を整理して出力します。

```
$ terraform plan
...
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  # nhncloud_compute_instance_v2.terraform-instance-01 will be updated in-place
  ~ resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
        id                  = "1e846787-04e9-4701-957c-78001b4b7257"
        name                = "terraform-instance-01"
      ~ security_groups     = [
          + "terraform-sg",
            # (1 unchanged element hidden)
        ]
        # (13 unchanged attributes hidden)


        # (2 unchanged blocks hidden)
    }

Plan: 0 to add, 1 to change, 0 to destroy.
```

プランを適用すると、インスタンスに新しいセキュリティグループが追加されます。
```
$ terraform apply
...
nhncloud_compute_instance_v2.terraform-instance-01: Modifying... [id=1e846787-04e9-4701-957c-78001b4b7257]
nhncloud_compute_instance_v2.terraform-instance-01: Modifications complete after 5s [id=1e846787-04e9-4701-957c-78001b4b7257]

Apply complete! Resources: 0 added, 1 changed, 0 destroyed.
```


<a id="delete-resources"></a>
### リソースを削除する

Terraformで作成したリソースを削除するには、該当の`.tf`ファイルを削除します。

```
$ rm instance.tf
```

構築計画を通して、該当リソースが削除されることを確認できます。

```
$ terraform plan
...
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # nhncloud_compute_instance_v2.terraform-instance-01 will be destroyed
  - resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
...

Plan: 0 to add, 0 to change, 1 to destroy.
...
```

`apply`コマンドを実行すると、作成されたinstanceが削除されます。

```
$ terraform apply
...
nhncloud_compute_instance_v2.terraform-instance-01: Destroying... [id=1e846787-04e9-4701-957c-78001b4b7257]
nhncloud_compute_instance_v2.terraform-instance-01: Still destroying... [id=1e846787-04e9-4701-957c-78001b4b7257, 10s elapsed]
nhncloud_compute_instance_v2.terraform-instance-01: Destruction complete after 11s

Apply complete! Resources: 0 added, 0 changed, 1 destroyed.
...
```


<a id="data-sources"></a>
## Data sources

tfファイルの作成に必要なインスタンスタイプID、イメージIDなどは、コンソールを通して確認するか、Terraformが提供するdata sourcesを利用して取得できます。Data sourcesはtfファイル内に作成し、取得した情報は修正できません。参照のみ可能です。

Data sourcesは、`{data sourcesリソースタイプ}.{data source名前}`で参照します。下記の例では`nhncloud_images_image_v2.ubuntu_1804_20200218`で取得したイメージ情報を参照します。

```
data "nhncloud_images_image_v2" "ubuntu_2004_20201222" {
  name = "Ubuntu Server 18.04.3 LTS (2020.02.18)"
  most_recent = true
}
```

Data sources内で別のdata sourceを参照できます。

```
data "nhncloud_blockstorage_volume_v2" "volume_00"{
  name = "ssd_volume1"
  status = "available"
}

data "nhncloud_blockstorage_snapshot_v2" "my_snapshot" {
  name = "my-snapshot"
  volume_id = data.nhncloud_blockstorage_volume_v2.volume_00.id
  status = "available"
  most_recent = true
}
```

次のセッションでは、NHN Cloudが提供する各種リソースをdata sources機能で取得する方法を説明します。


<a id="image"></a>
### イメージ

イメージ情報を取得します。NHN Cloudが提供するパブリックイメージまたは個人イメージをサポートします。

```
data "nhncloud_images_image_v2" "ubuntu_1804_20200218" {
  name = "Ubuntu Server 18.04.3 LTS (2020.02.18)"
  most_recent = true
}

# 同じ名前のイメージの中から、最も古いイメージを照会
data "nhncloud_images_image_v2" "windows2016_20200218" {
  name = "Windows 2016 STD with MS-SQL 2016 Standard (2020.02.18) KO"
  sort_key = "created_at"
  sort_direction = "asc"
  owner = "c289b99209ca4e189095cdecebbd092d"
  tag = "_AVAILABLE_"
}
```
| 名前 | 形式 | 必須 | 説明 |
| ------ | ---- | ---- | --------- |
| name | String | - | 照会するイメージ名<br>イメージ名は、**NHN CloudコンソールCompute > Instanceでインスタンス作成ボタン**を押すとNHN Cloudが提供するイメージリストで確認します。<br>イメージ名はNHN Cloudコンソールに表示された**<イメージ説明>**で作成する必要があります。<br>もし言語項目が存在する場合、上の例のように**「<イメージ説明> <言語>」**形式で入力する必要があります。 |
| size_min | Integer | - | 照会するイメージの最小サイズ(byte) |
| size_max | Integer | - | 照会するイメージの最大サイズ(byte) |
| properties | Object | - | 照会するイメージのプロパティ<br>すべてのプロパティ値が一致するイメージを照会 |
| sort_key | String | - | 特定プロパティを基準に照会したイメージリストをソート<br>デフォルト値は`name` |
| sort_direction | String | - | 照会したイメージリストのソート方向 <br>`asc`：昇順(デフォルト値) <br>`desc`：降順 |
| owner | String | - | 照会するイメージが属しているテナントID |
| tag | String | - | 特定タグが存在するイメージを検索 |
| visibility | String | - | 照会するイメージの表示プロパティ<br>public、private、sharedのうち、いずれか1つの値のみ選択可能<br>省略するとすべての種類のイメージリストを返す |
| most_recent | Boolean | - | `true`：照会したイメージリストのうち、最近作られたイメージ選択<br>`false`：照会された順序でイメージ選択 |
| member_status | String | - | 照会するイメージメンバーの状態 <br>`accepted`、`pending`、`rejected`、`all`のうちいずれか1つ。|


<a id="block-storage"></a>
### ブロックストレージ

```
data "nhncloud_blockstorage_volume_v2" "volume_00" {
  name = "ssd_volume1"
  status = "available"
}
```

| 名前 | 形式 | 必須 | 説明 |
| ------ | ---- | ---- | --------- |
| name | String | - | 照会するブロックストレージ名 |
| status | String | - | 照会するブロックストレージの状態 |
| metadata | Object | - | 照会するブロックストレージと関連するメタデータ |


<a id="instance-flavor"></a>
### インスタンスタイプ

インスタンスタイプ名は**NHN CloudコンソールCompute > Instanceでインスタンス作成 > インスタンスタイプ選択ボタン**を押すと確認できます。

```
data "nhncloud_compute_flavor_v2" "m2c2m4"{
  name = "m2.c2m4"
}
```

| 名前 | 形式 | 必須 | 説明 |
| ------ | ---- | ---- | --------- |
| name | String | - | 照会するインスタンスタイプ名 |


<a id="key-pair"></a>
### キーペア

```
data "nhncloud_compute_keypair_v2" "my_keypair"{
  name = "my_keypair"
}
```

| 名前  | 形式 | 必須 | 説明       |
| ------ | ---- |----|------------|
| name | String | O  | 照会するキーペア名 |

<a id="snapshot"></a>
### スナップショット

```
data "nhncloud_blockstorage_snapshot_v2" "my_snapshot" {
  name = "my-snapshot"
  volume_id = data.nhncloud_blockstorage_volume_v2.volume_00.id
  status = "available"
  most_recent = true
}
```

| 名前 | 形式 | 必須 | 説明 |
| ------ | ---- | ---- | --------- |
| name | String | - | 照会するスナップショットの名前 |
| volume_id | String | - | 照会するスナップショットの原本ブロックストレージID |
| status | String | - | 照会するスナップショットの状態 |
| most_recent | Boolean | - | `true`：照会したスナップショットリストのうち、最近作られたスナップショットを選択<br>`false`：照会された順序でスナップショットを選択 |


<a id="vpc"></a>
### VPC

VPCネットワークのUUIDは、**NHN CloudコンソールNetwork > VPC**でVPCを選択して確認可能です。

```
data "nhncloud_networking_vpc_v2" "default_network" {
  region = "KR1"
  tenant_id = "ba3be1254ab141bcaef674e74630a31f"
  id = "e34fc878-89f6-4d17-a039-3830a0b78346"
  name = "Default Network"
}
```

| 名前 | タイプ | 必須 | 説明       |
| --- | --- |---|------------|
| region | String | - | 照会するVPCが属するリージョン名 |
| tenant\_id | String | - | 照会するVPCが属するテナントID |
| id | String | - | 照会するVPCのID |
| name | String | - | 照会するVPCの名前 |


<a id="vpc-subnet"></a>
### VPCサブネット

サブネットIDはNHN Cloudコンソール **Network > サブネット**で