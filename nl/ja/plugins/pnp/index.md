---

copyright:
  years: 2016, 2018
lastupdated: "2019-03-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# {{site.data.keyword.cloud_notm}} CLI 用のプライベート・ネットワーク・ピアリング・プラグイン
{: #private_network_cli}

プライベート・ネットワーク・ピアリング・コマンド・ライン・インターフェース (CLI) を使用して、2 つの {{site.data.keyword.cloud}} スペース間のプライベート・ネットワーク・ピアリングを構成および管理します。 プライベート・ネットワーク・ピアリングは、IBM Containers (Docker コンテナー) でサポートされます。 {{site.data.keyword.cloud_notm}} スペースは、同じ地域内の異なるアベイラビリティー・ゾーンに配置でき、また異なる地域に配置することもできます。 プライベート・ネットワーク・ピアリング CLI プラグインは、{{site.data.keyword.cloud_notm}} CLI プラグインで使用できます。

プライベート・ネットワーク・ピアリング CLI プラグインは、Windows、MAC、および Linux オペレーティング・システムで使用可能です。 環境に適したプラグインを使用してください。

開始する前に、{{site.data.keyword.cloud_notm}} スペースを作成します。 スペース内の各コンテナーに、異なるネットワークの IP アドレスを設定してください。

**注:** {{site.data.keyword.cloud_notm}} スペースでプライベート・ネットワーク・ピアリングを使用した後に、スペースを削除する必要が生じた場合、まず、当該スペースのプライベート・ネットワーク・ピアリング接続を削除してください。

まず、{{site.data.keyword.cloud_notm}} CLI をインストールします。 詳しくは、『[IBM Cloud CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli)』を参照してください。

## プライベート・ネットワーク・ピアリング CLI プラグインをインストールします。

**注**: 前のバージョンのプラグインがインストールされている場合、それをアンインストールする必要があります。 以下のコマンドを使用して、プラグインをアンインストールします。
```
ibmcloud plugin uninstall private-network-peering
```
{: codeblock}

### ローカル・インストール
ご使用のプラットフォーム用のプライベート・ネットワーク・ピアリング・プラグインを [{{site.data.keyword.cloud_notm}} CLI プラグイン・リポジトリー](https://plugins.cloud.ibm.com/ui/repository.html){: new_window} ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン") からダウンロードします。

以下のコマンドを使用して、プライベート・ネットワーク・ピアリング・プラグインをインストールします。

**注**: プラグインの場所に切り替えるか、プラグインの場所のパスを指定してください。

* Microsoft Windows OS の場合:
```
ibmcloud plugin install private-network-peering-windows-amd64.exe
```
{: codeblock}

* Apple MAC OS の場合:
```
ibmcloud plugin install private-network-peering-darwin-amd64
```
{: codeblock}

* Linux OS の場合:
```
ibmcloud plugin install private-network-peering-linux-amd64
```
{: codeblock}

**注**: Linux OS 用のプラグインをインストールしているときに、許可が拒否されたことを示すエラー・メッセージが表示された場合、以下のコマンドを実行し、許可を変更してください。
```
chmod a+x ./private-network-peering-linux-amd64
```
{: codeblock}

### {{site.data.keyword.cloud_notm}} リポジトリーからのインストール

以下のステップに従って、{{site.data.keyword.cloud_notm}} リポジトリーからプラグインをインストールします。

1. 以下のように、{{site.data.keyword.cloud_notm}} プラグイン・レジストリー・エンドポイントを追加します。
	```
	ibmcloud plugin repo-add IBMCloud http://plugins.cloud.ibm.com
	```
	{: codeblock}

2. 次のコマンドを実行します。
	```
	ibmcloud plugin install private-network-peering -r IBMCloud
	```
	{: codeblock}

## プライベート・ネットワーク・ピアリング・コマンドのリスト
以下のコマンドがサポートされます。 使用可能なコマンドのリストを表示するには、`ibmcloud network` コマンドを使用します。

| コマンド     | 説明                                    |
|-------------|------------------------------------------------|
| pnp-routers | ピアリングで使用可能なすべてのルーターをリストします        |
| pnp-create  | プライベート・ネットワーク・ピアリング接続を作成します   |
| pnp-delete  | プライベート・ネットワーク・ピアリング接続を削除します   |
| pnp-show    | すべてのプライベート・ネットワーク・ピアリング接続をリストします  |
{: caption="表 1. プライベート・ネットワーク・ピアリング・コマンド" caption-side="top"}


### コマンドの使用法
コマンドのヘルプ情報を表示するには、`ibmcloud network [command] -h` を実行します。

#### ピアリングで使用可能なすべてのルーターのリスト
```
ibmcloud network pnp-routers [--verbose (または -v)]
```

#####オプション・パラメーター
{: #op1}

* **--verbose (または -v)** (フラグ): 各ルーターに関する詳細ネットワーク情報を表示します。

######コマンドの例
{: #ex1}

すべてのルーターに関するネットワーク情報を表示するには、以下のようにします。

$ ibmcloud network pnp-routers
	Listing available routers ...
	OK

IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3

すべてのルーターに関する詳細ネットワーク情報を表示するには、以下のようにします。

$ ibmcloud network pnp-routers -v
	Listing available routers ...
	OK

Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
FIELD          VALUE
IP             129.41.234.246
Name           default-router
Compute        Container
Region         US-South
Organization   ywu@us.ibm.com
Space          demo1
Networks       172.31.0.0/16

Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
FIELD          VALUE
IP             129.41.237.172
Name           default-router
Compute        Container
Region         US-South
Organization   ywu@us.ibm.com
Space          demo2
Networks       172.25.0.0/16
...


#### IP アドレスを使用したプライベート・ネットワーク・ピアリング接続の作成
```
ibmcloud network pnp-create <router_ip> <router_ip> <name>
```

#####パラメーター
{: #p1}

* **router_ip**: 接続する 2 つのルーターの IP アドレス。 IP アドレスを確認するには、`ibmcloud network pnp-routers` コマンドを使用します。
* **name**: プライベート・ネットワーク・ピアリング接続の名前。

######コマンドの例
{: #ex2}

$ ibmcloud network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
OK

Private network peering connection 'demo' created.


####接続名を使用したプライベート・ネットワーク・ピアリング接続の作成

```
ibmcloud network pnp-create -i <name>
```

#####パラメーター
{: #p2}

* **--interactive (-i)** (フラグ): ルーターを選択する対話モード。
* **name**: プライベート・ネットワーク・ピアリング接続の名前。

######コマンドの例
{: #ex3}

$ ibmcloud network pnp-create -i demo
	Creating private network peering connection 'demo' ...
List of available routers (select TWO for peering):

#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

Select first router for peering> 1
	Select second router for peering> 2

Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
OK

Private network peering connection 'demo' created.


#### すべてのプライベート・ネットワーク・ピアリング接続のリスト
```
ibmcloud network pnp-show [--verbose (または -v)]
```

#####オプション・パラメーター
{: #op2}

* **--verbose (または -v)** (フラグ): 各ルーターに関する詳細ネットワーク情報を表示します。

######コマンドの例
{: #ex4}

基本情報を表示するには、以下のようにします。

$ ibmcloud network pnp-show
	Listing private network peering connections ...
	OK

ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

詳細情報を表示するには、以下のようにします。

$ ibmcloud network pnp-show -v
	Listing private network peering connections ...
	OK

Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
FIELD              VALUE
Name               demo
Status             Active
Router1 IP         129.41.234.246
Router1 Networks   172.31.0.0/16
Router2 Name       default-router
Router2 IP         129.41.237.172
Router2 Networks   172.25.0.0/16

#### プライベート・ネットワーク・ピアリング接続の削除
```
ibmcloud network pnp-delete [--force (または -f)] <connection_id>
```
#####パラメーター
{: #p3}
* **connection_id**: コンマで区切った、1 つ以上の接続 ID。

#####オプション・パラメーター
{: #op3}

* **--force (または -f)** (フラグ): 確認を求めるプロンプトを出さずに接続を削除します。

######コマンドの例:
{: #ex5}

接続を削除するには、以下のようにします。

$ ibmcloud network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
Are you sure you want to delete the connection? (yes/no)> yes

Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
OK

Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.

複数の接続を削除するには、以下のようにします。
```
ibmcloud network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
