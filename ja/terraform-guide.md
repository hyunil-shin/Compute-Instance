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
* **Change Automation**
    * 複数の場所に同じ構成のインフラを構築し、変更できるように自動化できます。
    * インフラを構築するのにかかる時間を節約することができ、失敗も減らすことができます。


<a id="supported-resources"></a>
#### Resourcesサポート

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
#### Data sourcesサポート

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

<a id="terraform-provider-provided"></a>
## Terraformプロバイダー提供

NHN CloudはHashiCorp社の公式パートナーとして[Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest)を通じてTerraformプロバイダーを提供しています。

Terraformはterraformバイナリファイルを起点として、ローカル環境やデプロイサーバーなどのリモート環境で目的のターゲットを呼び出す方式で実行されます。この際、「目的のターゲット」は呼び出し方式が異なる場合がありますが、ターゲットのプロバイダー、つまりプロバイダーが提供するAPIを呼び出して相互作用します。ここでTerraformがターゲットとの相互作用を可能にするのが「プロバイダー」です。



<a id="terraform-usage"></a>
## Terraform基本使用法

Terraformを使用したインフラ構築は、通常以下のようなライフサイクルを持ちます。

1. tfファイルを作成
2. 構築計画を確認
3. リソースを作成
4. リソースを修正
5. リソースを削除

まず、構築するインフラ形状をtfファイルに記述します。記述されたtfファイルに基づく構築計画は、以下のように`plan`コマンドで確認します。

```
$ terraform plan
```

構築計画に問題がなければ、`apply`コマンドを使用してリソースを作成、修正、削除します。

```
$ terraform apply
```

次のセクションでは、これらのステップを例とともにより詳しく説明します。


<a id="create-tf-files"></a>
### tfファイルを作成

プロバイダー設定ファイルがあるパスにtfファイルを作成します。複数のリソース設定を1つのtfファイルにまとめるか、リソース別に別々のtfファイルとして作成することもできます。Terraformは記述されたすべてのtfファイルを一度に読み込んで構築計画を立てます。

以下は、`instance.tf`ファイルにインスタンスを作成するリソースを定義したtfファイルの例です。

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