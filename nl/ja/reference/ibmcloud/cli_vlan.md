---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure cli, vlan cli, classic vlan cli, ibmcloud sl vlan, manage virtual network cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# クラシック・インフラストラクチャー VLAN の管理
{: #manage-classic-vlans}

{{site.data.keyword.cloud}} は、パブリック・ネットワークとプライベート・ネットワーク上のブロードキャスト・トラフィックを分離するために、仮想ローカル・エリア・ネットワーク (VLAN) を使用します。 VLAN は、他のオファリングを実現するために必要に応じて割り当てられます。

以下のコマンドを使用して、クラシック・インフラストラクチャーの VLAN を管理します。
{: shortdesc}

## ibmcloud sl vlan create
{: #sl_vlan_create}

新規 VLAN を作成します。
```
ibmcloud sl vlan create [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-t, --vlan-type</dt>
<dd>VLAN のタイプ。public または private のいずれか。</dd>
<dt>-r, --router</dt>
<dd>ルーターのホスト名。</dd>
<dt>-d, --datacenter</dt>
<dd>データ・センターの短縮名。</dd>
<dt>-n, --name</dt>
<dd>VLAN の名前。</dd>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

**例**:
```
ibmcloud sl vlan create -t public -d dal09 -s 16 -n myvlan
```
{: codeblock}

このコマンドは、データ・センター `dal09` に、16 個の IP アドレスを持ち、`myvlan` という名前のパブリック VLAN を作成します。

## ibmcloud sl vlan cancel
{: #sl_vlan_cancel}

VLAN を取り消します。
```
ibmcloud sl vlan cancel IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

**例**:
```
ibmcloud sl vlan cancel 12345678 -f
```
{: codeblock}

このコマンドは、ID `12345678` の VLAN を、確認を求めずに取り消します。

## ibmcloud sl vlan detail
{: #sl_vlan_detail}

VLAN についての詳細を取得します。
```
ibmcloud sl vlan detail IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>--no-vs</dt>
<dd>仮想サーバー・リストを非表示にします。</dd>
<dt>--no-hardware</dt>
<dd>ハードウェア・リストを非表示にします。</dd>
</dl>

**例**:
```
ibmcloud sl vlan detail 12345678  --no-vs --no-hardware
```
{: codeblock}

このコマンドは、ID `12345678` の VLAN の詳細を表示し、仮想サーバーおよびハードウェア・サーバーをリストしません。

## ibmcloud sl vlan edit
{: #sl_vlan_edit}

VLAN についての詳細を編集します。
```
ibmcloud sl vlan edit IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-n, --name</dt>
<dd>VLAN の名前。</dd>
</dl>

**例**:
```
ibmcloud sl vlan edit 12345678 -n myvlan-rename
```
{: codeblock}

このコマンドは、`ID 12345678` の VLAN を更新し、それに新しい名前 `myvlan-rename` を付けます。

## ibmcloud sl vlan list
{: #sl_vlan_list}

ご使用のアカウントのすべての VLAN をリストします。
```
ibmcloud sl vlan list [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>--sortby</dt>
<dd>ソートの基準にする列。オプション: id、number、name、firewall、datacenter、hardware、virtual_servers、public_ips。</dd>
<dt>-d, --datacenter</dt>
<dd>データ・センターの短縮名を基準にフィルター操作します。</dd>
<dt>-n, --number</dt>
<dd>VLAN 番号を基準にフィルター操作します。</dd>
<dt>--name</dt>
<dd>VLAN 名を基準にフィルター操作します。</dd>
<dt>--order</dt>
<dd>VLAN を購入した注文の ID を基準にフィルター操作します。</dd>
</dl>

**例**:
```
ibmcloud sl vlan list -d dal09 --sortby number
```
このコマンドは、現行アカウントのすべての VLAN をリストします。フィルター基準のデータ・センターは `dal09` で、VLAN 番号によってソートします。

## ibmcloud sl vlan options
{: #sl_vlan_options}

VLAN の作成に関するすべてのオプションをリストします。
```
ibmcloud sl vlan options
```
{: codeblock}

**例**:
```
ibmcloud sl vlan options
```
{: codeblock}

このコマンドは、VLAN を作成するためのすべてのオプション (例えば、VLAN タイプ、データ・センター、サブネット・サイズ、ルーターなど) をリストします。
