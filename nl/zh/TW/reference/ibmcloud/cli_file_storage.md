---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, file storage service, ibmcloud sl file, snapshot, file storage, storage, nfs, nas, iops, volume, datacenter, file storage cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:codeblock: .codeblock}

# 使用 File Storage 服務
{: #sl-file-storage-service}

{{site.data.keyword.filestorage_full}} 是持續性、快遞、連接彈性網路並以 NFS 為基礎的 {{site.data.keyword.filestorage_short}}。在這個網路連接儲存空間 (NAS) 環境中，您可以完全控制檔案共用功能及效能。

請使用下列指令在 {{site.data.keyword.cloud_notm}} 標準基礎架構的 File Storage 服務中管理給定磁區。
{: shortdesc}
 
## ibmcloud sl file access-authorize
{: #sl_file_access_authorize}

授權主機存取給定的磁區。
```
ibmcloud sl file access-authorize VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-d, --hardware-id</dt>
<dd>要授權的某部硬體伺服器的 ID。</dd>
<dt>-v, --virtual-id</dt>
<dd>要授權的某部虛擬伺服器的 ID。</dd>
<dt>-i, --ip-address-id</dt>
<dd>要授權的某個 IP 位址的 ID。</dd>
<dt>-p, --ip-address</dt>
<dd>要授權的 IP 位址。</dd>
<dt>-s, --subnet-id</dt>
<dd>要授權的某個子網路的 ID。</dd>
</dl>

**範例**：
```
ibmcloud sl file access-authorize 12345678 --virtual-id 87654321
```

這個指令會授權 ID 為 `87654321` 的虛擬伺服器存取 ID 為 `12345678` 的磁區。

## ibmcloud sl file access-list
{: #sl_file_access_list}

列出 ACL。
```
ibmcloud sl file access-list VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--sortby</dt>
<dd>直欄排序方式，選項包含：id、name、type、private_ip_address、host_iqn、username、password。</dd>
<dt>--column</dt>
<dd>要顯示的直欄，選項包含：id、name、type、private_ip_address、host_iqn、username、password。</dd>
</dl>

**範例**：
```
ibmcloud sl file access-list 12345678 --sortby id
```

這個指令會列出獲授權存取 ID 為 `12345678` 的磁區的所有主機，並依 ID 排序。

## ibmcloud sl file access-revoke
{: #sl_file_access_revoke}

撤銷主機存取給定磁區的授權。
```
ibmcloud sl file access-revoke VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-d, --hardware-id</dt>
<dd>要撤銷的某部硬體伺服器的 ID。</dd>
<dt>-v, --virtual-id</dt>
<dd>要撤銷的某部虛擬伺服器的 ID。</dd>
<dt>-i, --ip-address-id</dt>
<dd>要撤銷的某個 IP 位址的 ID。</dd>
<dt>-p, --ip-address</dt>
<dd>要撤銷的 IP 位址。</dd>
<dt>-s, --subnet-id</dt>
<dd>要撤銷的某個子網路的 ID。</dd>
</dl>

**範例**：
```
ibmcloud sl file access-revoke 12345678 --virtual-id 87654321
```

這個指令會撤銷 ID 為 `87654321` 的虛擬伺服器對 ID 為 `12345678` 的磁區的存取權。

## ibmcloud sl file replica-failback
{: #sl_file_replica_failback}

從抄本進行檔案磁區失效回復。
```
ibmcloud sl file replica-failback VOLUME_ID
```

**範例**：
```
ibmcloud sl file replica-failback 12345678
```
這個指令會針對 ID 為 `12345678` 的磁區執行失效回復作業。

## ibmcloud sl file replica-failover
{: #sl_file_replica_failover}

將檔案磁區失效接手至給定的抄本磁區。
```
ibmcloud sl file replica-failover VOLUME_ID REPLICA_ID
```


**範例**：
```
ibmcloud sl file replica-failover 12345678 87654321
```
這個指令會執行將 ID 為 `12345678` 的磁區失效接手至 ID 為 `87654321` 的抄本磁區的作業。

## ibmcloud sl file replica-locations
{: #sl_file_replica_locations}

列出給定磁區的適當抄寫資料中心。
```
ibmcloud sl file replica-locations VOLUME_ID
```


**範例**：
```
ibmcloud sl file replica-locations 12345678
```
這個指令會列出 ID 為 `12345678` 的檔案磁區的適當抄寫資料中心。

## ibmcloud sl file replica-order
{: #sl_file_replica_order}

訂購檔案儲存空間抄本磁區。
```
ibmcloud sl file replica-order VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-s, --snapshot-schedule</dt>
<dd>必要。要用於抄寫的 Snapshot 排程，選項包含：HOURLY、DAILY、WEEKLY。</dd>
<dt>-d, --datacenter</dt>
<dd>必要。抄本資料中心的簡稱，例如：dal09。</dd>
<dt>-t, --tier</dt>
<dd>選用。已訂購抄本之主要磁區的耐久性儲存空間層級（每 GB 的 IOPS），選項包含：0.25、2、4、10，如果未指定層級，將會使用原始磁區的層級。</dd>
<dt>-i, --iops</dt>
<dd>效能儲存空間 IOPS，此值為 100 的倍數，介於 100 與 6000 之間，如果未指定 IOPS，將會使用原始磁區的 IOPS。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file replica-order 12345678 -s DAILY -d dal09 --tier 4
```

這個指令會訂購 ID 為 `12345678` 的磁區的抄本，此抄本會執行 DAILY 抄寫、位於 `dal09`、層級層次為 4。

## ibmcloud sl file replica-partners
{: #sl_file_replica_partners}

列出檔案磁區的現有抄本磁區。
```
ibmcloud sl file replica-partners VOLUME_ID [OPTIONS]
```


**範例**：
```
ibmcloud sl file replica-partners 12345678
```

這個指令會列出 ID 為 `12345678` 的檔案磁區的現有抄本磁區。

## ibmcloud sl file snapshot-cancel
{: #sl_file_snapshot_cancel}

取消給定磁區的現有 Snapshot 空間。
```
ibmcloud sl file snapshot-cancel SNAPSHOT_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--reason</dt>
<dd>選用性的取消原因。</dd>
<dt>--immediate</dt>
<dd>立即取消 Snapshot 空間，而不是在計費週年日取消。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-cancel 12345678 --immediate -f
```

這個指令會立即取消 ID 為 `12345678` 的 Snapshot，而不要求確認。

## ibmcloud sl file snapshot-create
{: #sl_file_snapshot_create}

在給定的磁區上建立 Snapshot。
```
ibmcloud sl file snapshot-create VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-n, --note</dt>
<dd>要設定於新 Snapshot 的附註。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-create 12345678 --note snapshotforibmcloud
```
這個指令會針對 ID 為 `12345678` 的磁區建立 Snapshot，並新增附註 `snapshotforibmcloud`。

## ibmcloud sl file snapshot-disable
{: #sl_file_snapshot_disable}

依給定磁區的指定排程停用 Snapshot。
```
ibmcloud sl file snapshot-disable VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-s, --schedule-type</dt>
<dd>必要。Snapshot 排程，選項包含：HOURLY、DAILY、WEEKLY。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-disable 12345678 -s DAILY
```

這個指令會針對 ID 為 `12345678` 的磁區停用每日 Snapshot。

## ibmcloud sl file snapshot-enable
{: #sl_file_snapshot_enable}

依指定的排程為給定磁區啟用 Snapshot。
```
ibmcloud sl file snapshot-enable VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-s, --schedule-type</dt>
<dd>必要。Snapshot 排程，選項包含：HOURLY、DAILY、WEEKLY。</dd>
<dt>-c, --retention-count</dt>
<dd>必要。要保留的 Snapshot 數目。</dd>
<dt>-m, --minute</dt>
<dd>應該在幾分擷取 Snapshot，選項為 0 到 59 之間的整數。</dd>
<dt>-r, --hour</dt>
<dd>應該在幾點擷取 Snapshot，選項為 0 到 23 之間的整數。</dd>
<dt>-d, --day-of-week</dt>
<dd>應該在星期幾擷取 Snapshot，選項為 0 到 6 之間的整數。0 表示星期日、1 表示星期一、2 表示星期二、3 表示星期三、4 表示星期四、5 表示星期五、6 表示星期六。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-enable 12345678 -s WEEKLY -c 5 -m 0 --hour 2 -d 0
```

這個指令會針對 ID 為 `12345678` 的磁區啟用 Snapshot、在每週的星期日 2:00 擷取 Snapshot，且最多保留 5 個 Snapshot。

## ibmcloud sl file snapshot-delete
{: #sl_file_snapshot_delete}

在給定的磁區上刪除 Snapshot。
```
ibmcloud sl file snapshot-delete SNAPSHOT_ID
```

**範例**：
```
ibmcloud sl file snapshot-delete 12345678
```

這個指令會刪除 ID 為 `12345678` 的 Snapshot。

## ibmcloud sl file snapshot-list
{: #sl_file_snapshot_list}

列出檔案儲存空間 Snapshot。
```
ibmcloud sl file snapshot-list VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--sortby</dt>
<dd>直欄排序方式，選項包含：id、name、created、size_bytes。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-list 12345678 --sortby id
```

這個指令會列出 ID 為 `12345678` 的磁區的所有 Snapshot，並依 ID 排序。

## ibmcloud sl file snapshot-order
{: #sl_file_snapshot_order}

訂購檔案儲存空間磁區的 Snapshot 空間。
```
ibmcloud sl file snapshot-order VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-s, --size</dt>
<dd>必要。要建立的 Snapshot 空間大小（以 GB 為單位）。</dd>
<dt>-t, --tier</dt>
<dd>選用。已訂購空間之檔案磁區的耐久性儲存空間層級（每 GB 的 IOPS），選項包含：0.25、2、4、10。</dd>
<dt>-i, --iops</dt>
<dd>效能儲存空間 IOPS，此值為 100 的倍數，介於 100 與 6000 之間。</dd>
<dt>-u, --upgrade</dt>
<dd>該旗標指出訂單為升級。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file snapshot-order 12345678 -s 1000 -t 4
```
這個指令會針對 ID 為 `12345678` 的磁區訂購 Snapshot 空間、大小為 1000GB、層級層次為每 GB 4 個 IOPS。

## ibmcloud sl file snapshot-restore
{: #sl_file_snapshot_restore}

使用給定的 Snapshot 還原檔案磁區。
```
ibmcloud sl file snapshot-restore VOLUME_ID SNAPSHOT_ID
```

**範例**：
```
ibmcloud sl file snapshot-restore 12345678 87654321
```

這個指令會從 ID 為 `87654321` 的 Snapshot 還原 ID 為 `12345678` 的磁區。

## ibmcloud sl snapshot-schedule-list
{: #sl_snapshot_schedule_list}

列出給定磁區的 Snapshot 排程。
```
ibmcloud sl snapshot-schedule-list VOLUME_ID
```

**範例**：
```
ibmcloud sl file snapshot-schedule-list 12345678
```

這個指令會針對 ID 為 `12345678` 的磁區列出 Snapshot 排程。

## ibmcloud sl file volume-cancel
{: #sl_file_volume_cancel}

取消現有的檔案儲存空間磁區。
```
ibmcloud sl file volume-cancel VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--reason</dt>
<dd>選用性的取消原因。</dd>
<dt>--immediate</dt>
<dd>立即取消檔案儲存空間磁區，而不是在計費週年日取消。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file volume-cancel 12345678 --immediate -f
```

這個指令會立即取消 ID 為 `12345678` 的磁區，而不要求確認。

## ibmcloud sl file volume-count
{: #sl_file_volume_count}

列出每個資料中心的檔案儲存空間磁區數目。
```
ibmcloud sl file volume-count [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-d, --datacenter</dt>
<dd>依資料中心簡稱進行過濾。</dd>
</dl>

## ibmcloud sl file volume-list
{: #sl_file_volume_list}

列出檔案儲存空間。
```
ibmcloud sl file volume-list [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-u, --username</dt>
<dd>依磁區使用者名稱進行過濾。</dd>
<dt>-d, --datacenter</dt>
<dd>依資料中心簡稱進行過濾。</dd>
<dt>-t, --storage-type</dt>
<dd>依儲存空間磁區的類型進行過濾，選項包含：performance、endurance。</dd>
<dt>-o, --order</dt>
<dd>依購買檔案儲存空間的訂單 ID 進行過濾。</dd>
<dt>--sortby</dt>
<dd>直欄排序方式，選項包含：id、username、datacenter、storage_type、capacity_gb、bytes_used、ip_addr、active_transactions、mount_addr。</dd>
<dt>--column</dt>
<dd>要顯示的直欄，選項包含：id、username、datacenter、storage_type、capacity_gb、bytes_used、ip_addr、mount_addr、notes。</dd>
</dl>

**範例**：
```
ibmcloud sl file volume-list -d dal09 -t endurance --sortby capacity_gb
```

這個指令會列出現行帳戶上位於 `dal09` 的所有耐久性磁區，並依容量排序。

## ibmcloud sl file volume-detail
{: #sl_file_volume_detail}

顯示指定磁區的詳細資料。
```
ibmcloud sl file volume-detail VOLUME_ID
```


**範例**：
```
ibmcloud sl file volume-detail 12345678
```

這個指令會顯示 ID 為 `12345678` 的磁區的詳細資料。

## ibmcloud sl file volume-duplicate
{: #sl_file_volume_duplicate}

複製現有磁區，以訂購檔案磁區。
```
ibmcloud sl file volume-duplicate VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-o, --origin-snapshot-id</dt>
<dd>要用於複製的原始磁區 Snapshot 的 ID。</dd>
<dt>-s, --duplicate-size</dt>
<dd>複製檔案磁區的大小（以 GB 為單位），如果未指定大小，將會使用原始磁區的大小。</dd>
<dt>-i, --duplicate-iops</dt>
<dd>效能儲存空間 IOPS，此值為 100 的倍數，介於 100 與 6000 之間，如果未指定 IOPS，將會使用原始磁區的 IOPS。</dd>
<dt>-t, --duplicate-tier</dt>
<dd>耐久性儲存空間層級，如果未指定層級，將會使用原始磁區的層級。</dd>
<dt>-n, --duplicate-snapshot-size</dt>
<dd>要針對複製項目訂購的 Snapshot 空間大小，如果未指定 Snapshot 空間大小，將會使用原始磁區的 Snapshot 空間大小。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file volume-duplicate 12345678
```

這個指令會顯示如何複製 ID 為 `12345678` 的磁區來訂購新磁區。

## ibmcloud sl file volume-order
{: #sl_file_volume_order}

訂購檔案儲存空間磁區。
```
ibmcloud sl file volume-order [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-t, --storage-type</dt>
<dd>必要。儲存空間磁區的類型，選項包含：performance、endurance。</dd>
<dt>-s, --size</dt>
<dd>必要。儲存空間磁區的大小（以 GB 為單位）。</dd>
<dt>-i, --iops</dt>
<dd>效能儲存空間 IOPS，此值為 100 的倍數，介於 100 與 6000 之間 [storage-type performance 的必要項目]。</dd>
<dt>-e, --tier</dt>
<dd>耐久性儲存空間層級（每 GB 的 IOP）[storage-type endurance 的必要項目]，選項包含：0.25、2、4、10。</dd>
<dt>-d, --datacenter</dt>
<dd>必要。資料中心簡稱。</dd>
<dt>-n, --snapshot-size</dt>
<dd>隨磁區訂購 Snapshot 空間的選用參數。</dd>
<dt>-b, --billing</dt>
<dd>計費頻率的選用參數（預設為 monthly），選項包含：hourly、monthly。</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl file volume-order --storage-type performance --size 1000 --iops 4000  -d dal09
```

這個指令會訂購效能磁區：大小為 1000GB、IOPS 為 4000、位於 `dal09`。

## ibmcloud sl file volume-modify
{: #sl_file_volume_modify}

修改現有的檔案儲存空間磁區
```
ibmcloud sl file volume-modify VOLUME_ID [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-c, --new-size</dt>
<dd>檔案磁區的新大小（以 GB 為單位）。***如果未給定大小，則會使用磁區的原始大小。***可能大小：[20、40、80、100、250、500、1000、2000、4000、8000、12000] 最小：[磁區的原始大小]</dd>
<dt>-i, --new-iops</dt>
<dd>效能儲存空間 IOPS，此值為 100 的倍數，介於 100 與 6000 之間 [僅適用於效能磁區] ***如果未指定 IOPS 值，將會使用磁區的原始 IOPS 值。***需求：[如果磁區的原始 IOPS/GB 小於 0.3，新的 IOPS/GB 也必須小於 0.3。如果磁區的原始 IOPS/GB 大於或等於 0.3，磁區的新 IOPS/GB 也必須大於或等於 0.3。]</dd>
<dt>-t, --new-tier</dt>
<dd>耐久性儲存空間層級（每 GB 的 IOPS）[僅適用於耐久性磁區] ***如果未指定層級，將會使用磁區的原始層級。***
需求：[如果磁區的原始 IOPS/GB 為 0.25，磁區的新 IOPS/GB 也必須是 0.25。如果磁區的原始 IOPS/GB 大於 0.25，磁區的新 IOPS/GB 也必須大於 0.25。]</dd>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：

```
ibmcloud sl file volume-modify 12345678 --new-size 1000 --new-iops 4000
```

這個指令會修改磁區 `12345678`：大小為 1000GB、IOPS 為 4000。

```
ibmcloud sl file volume-modify 12345678 --new-size 500 --new-tier 4
```

這個指令會修改磁區 `12345678`：大小為 500GB、層級層次為每 GB 4 個 IOPS。


## ibmcloud sl file volume-options
{: #sl_file_volume_options}

列出用來訂購檔案儲存空間的所有選項。
```
ibmcloud sl file volume-options
```

**範例**：
```
ibmcloud sl file volume-options
```
這個指令會列出用來建立檔案儲存空間磁區的所有選項，包括儲存空間類型、磁區大小、IOPS、層級層次、資料中心及 Snapshot 大小。
