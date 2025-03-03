---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, bare metal, ibmcloud sl hardware, hardware, power-cycle, firmware

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# ベアメタル・サーバーの作成および操作
{: #sl-manage-bare-metal}

{{site.data.keyword.baremetal_long}} は、ハードウェア・リソースへの下位レベルのアクセス権限でパフォーマンスと制御の機能を提供する、シングル・テナントの物理サーバーです。 ベアメタル・サーバーは、プロセッサー集中型およびディスク入出力集中型のワークロードに必要とされる強力なパワーを提供します。 これらのサーバーには、標準の機能とサービスが含まれた、最も包括的なパッケージが付属しています。

以下のコマンドを使用して、{{site.data.keyword.cloud}} クラシック・インフラストラクチャーのベア・メタル・ハードウェア・サーバーを管理します。
{: shortdesc}

## ibmcloud sl hardware cancel
{: #sl_hardware_cancel}

ハードウェア・サーバーを取り消します。
```
ibmcloud sl hardware cancel IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-i, --immediate</dt>
<dd>請求応答日ではなく即時に、サーバーを取り消します。</dd>
<dt>-r, --reason</dt>
<dd>取り消しの理由 (オプション)。 使用可能なオプションのリストについては、「ibmcloud sl hardware cancel-reasons」を参照してください。</dd>
<dt>-c, --comment</dt>
<dd>取り消しチケットに付加するコメント (オプション)。</dd>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware cancel-reasons
{: #sl_hardware_cancel_reasons}

取り消しの理由のリストを表示します。
```
ibmcloud sl hardware cancel-reasons
```

## ibmcloud sl hardware create
{: #sl_hardware_create}

ハードウェア・サーバーを発注/作成します。
```
ibmcloud sl hardware create [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-H, --hostname</dt>
<dd>FQDN のホスト部分 (必須)。</dd>
<dt>-D, --domain</dt>
<dd>FQDN のドメイン部分 (必須)。</dd>
<dt>-s, --size</dt>
<dd>ハードウェア・サイズ (必須)。</dd>
<dt>-o, --os</dt>
<dd>OS インストール・コード (必須)。</dd>
<dt>-d, --datacenter</dt>
<dd>データ・センターの短縮名 (必須)。</dd>
<dt>-p, --port-speed</dt>
<dd>ポート速度 (必須)。</dd>
<dt>-b, --billing</dt>
<dd>請求レート。hourly または monthly のいずれかで、デフォルトは hourly です (指定されていない場合)。</dd>
<dt>-i, --post-install</dt>
<dd>ダウンロードするインストール後スクリプト。</dd>
<dt>-k, --key</dt>
<dd>root ユーザーに追加する SSH 鍵 (複数のオカレンスが許可されます)。</dd>
<dt>-n, --no-public</dt>
<dd>プライベート・ネットワークのみ。</dd>
<dt>-e, --extra</dt>
<dd>追加オプション (複数のオカレンスが許可されます)。</dd>
<dt>-t, --test</dt>
<dd>実際には仮想サーバーを作成しません。</dd>
<dt>-m, --template</dt>
<dd>コマンド・ライン・オプションをデフォルト設定するテンプレート・ファイル。</dd>
<dt>-x, --export</dt>
<dd>オプションをテンプレート・ファイルにエクスポートします。</dd>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware create-options
{: #sl_hardware_create_options}

特定のシャーシのサーバー・オーダー・オプション。
```
ibmcloud sl hardware create-options
```

## ibmcloud sl hardware credentials
{: #sl_hardware_credentials}

ハードウェア・サーバーの資格情報をリストします。
```
ibmcloud sl hardware credentials IDENTIFIER
```

## ibmcloud sl hardware detail
{: #sl_hardware_detail}

ハードウェア・サーバーの詳細を取得します。
```
ibmcloud sl hardware detail IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-p, --passwords</dt>
<dd>パスワードを表示します (背後に注意してください).</dd>
<dt>-c, --price</dt>
<dd>関連付けられた価格を表示します。</dd>
</dl>

## ibmcloud sl hardware edit
{: #sl_hardware_edit}

ハードウェア・サーバーの詳細を編集します。
```
ibmcloud sl hardware edit IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-H, --hostname</dt>
<dd>FQDN のホスト部分。</dd>
<dt>-D, --domain</dt>
<dd>FQDN のドメイン部分。</dd>
<dt>-g, --tag</dt>
<dd>設定するタグ、または、すべて削除する場合は空ストリング。</dd>
<dt>-F, --userfile</dt>
<dd>ユーザー・データをファイルから読み取ります。</dd>
<dt>-u, --userdata</dt>
<dd>ユーザー定義のメタデータ・ストリング。</dd>
<dt>-p, --public-speed</dt>
<dd>パブリック・ポート速度。オプション: 0、10、100、1000、10000。</dd>
<dt>-v, --private-speed</dt>
<dd>プライベート・ポート速度。オプション: 0、10、100、1000、10000。</dd>
</dl>

## ibmcloud sl hardware list
{: #sl_hardware_list}

ハードウェア・サーバーをリストします。
```
ibmcloud sl hardware list [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-c, --cpu</dt>
<dd>CPU コアの数を基準にフィルター操作します。</dd>
<dt>-D, --domain</dt>
<dd>ドメインを基準にフィルター操作します。</dd>
<dt>-H, --hostname</dt>
<dd>ホスト名を基準にしてフィルター操作します。</dd>
<dt>-d, --datacenter</dt>
<dd>データ・センターを基準にフィルター操作します。</dd>
<dt>-m, --memory</dt>
<dd>ギガバイト単位のメモリーを基準にフィルター操作します。</dd>
<dt>-n, --network</dt>
<dd>Mbps 単位のネットワーク・ポート速度を基準にフィルター操作します。</dd>
<dt>-g, --tag</dt>
<dd>タグを基準にフィルター操作します (複数のオカレンスが許可されます)。</dd>
<dt>-p, --public-ip</dt>
<dd>パブリック IP アドレスを基準にしてフィルター操作します。</dd>
<dt>-v, --private-ip</dt>
<dd>プライベート IP アドレスを基準にフィルター操作します。</dd>
<dt>-o, --order</dt>
<dd>ハードウェア・サーバーを購入した注文の ID を基準にフィルター操作します。</dd>
<dt>--owner</dt>
<dd>所有者の ID を基準にフィルター操作します。</dd>
<dt>--sortby</dt>
<dd>ソートの基準にする列。デフォルト: hostname、オプション: id、guid、hostname、domain、public_ip、private_ip、datacenter、status、ipmi_ip、created、created_by。</dd>
<dt>--column</dt>
<dd>表示する列。デフォルト: id、hostname、domain、public_ip、private_ip、datacenter、status、オプション: guid、cpu、memory、os、ipmi_ip、created、created_by、tags。</dd>
</dl>

## ibmcloud sl hardware power-cycle
{: #sl_hardware_power_cycle}

サーバーの電源サイクルを行います。
```
ibmcloud sl hardware power-cycle IDENTIFIER
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware power-off
{: #sl_hardware_power_off}

アクティブなサーバーを電源オフします。
```
ibmcloud sl hardware power-off IDENTIFIER
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware power-on
{: #sl_hardware_power_on}

サーバーを電源オンにします。
```
ibmcloud sl hardware power-on IDENTIFIER
```

## ibmcloud sl hardware reboot
{: #sl_hardware_reboot}

アクティブ・サーバーをリブートします。
```
ibmcloud sl hardware reboot IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>--hard</dt>
<dd>ハード・リブートを実行します。</dd>
<dt>--soft</dt>
<dd>ソフト・リブートを実行します。</dd>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware reload
{: #sl_hardware_reload}

サーバー上でオペレーティング・システムを再ロードします。
```
ibmcloud sl hardware reload IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-i, --postinstall</dt>
<dd>ダウンロードするインストール後スクリプト。HTTPS のみが実行し、HTTP はファイルを /root に残します。</dd>
<dt>-k, --key</dt>
<dd>root ユーザーに追加する SSH 鍵の ID (複数のオカレンスが許可されます)。</dd>
<dt>-b, --upgrade-bios</dt>
<dd>BIOS をアップグレードします。</dd>
<dt>-w, --upgrade-firmware</dt>
<dd>すべてのハード・ディスクのファームウェアをアップグレードします。</dd>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware rescue
{: #sl_hardware_rescue}

サーバーをレスキュー・イメージでリブートします。
```
ibmcloud sl hardware rescue IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>

## ibmcloud sl hardware update-firmware
{: #sl_hardware_update_firmware}

サーバー・ファームウェアを更新します。
```
ibmcloud sl hardware update-firmware IDENTIFIER [OPTIONS]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>-f, --force</dt>
<dd>確認なしで操作を強制します。</dd>
</dl>
