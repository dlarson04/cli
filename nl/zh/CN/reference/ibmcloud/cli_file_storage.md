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

# 使用 File Storage 服务
{: #sl-file-storage-service}

{{site.data.keyword.filestorage_full}} 是一种网络连接的基于 NFS 的 {{site.data.keyword.filestorage_short}}，具有持久、快速、灵活的特点。在此网络连接存储器 (NAS) 环境中，您对文件共享功能和性能具有完全控制权。

使用以下命令可管理 {{site.data.keyword.cloud_notm}} 经典基础架构 File Storage 服务中的给定卷。
{: shortdesc}
 
## ibmcloud sl file access-authorize
{: #sl_file_access_authorize}

授权主机访问给定卷。
```
ibmcloud sl file access-authorize VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-d, --hardware-id</dt>
<dd>要授权的一个硬件服务器的标识。</dd>
<dt>-v, --virtual-id</dt>
<dd>要授权的一个虚拟服务器的标识。</dd>
<dt>-i, --ip-address-id</dt>
<dd>要授权的一个 IP 地址的标识。</dd>
<dt>-p, --ip-address</dt>
<dd>要授权的 IP 地址。</dd>
<dt>-s, --subnet-id</dt>
<dd>要授权的一个子网的标识。</dd>
</dl>

**示例**：
```
ibmcloud sl file access-authorize 12345678 --virtual-id 87654321
```

此命令授权标识为 `87654321` 的虚拟服务器访问标识为 `12345678` 的卷。

## ibmcloud sl file access-list
{: #sl_file_access_list}

列出 ACL。
```
ibmcloud sl file access-list VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>--sortby</dt>
<dd>要作为排序依据的列，选项为：id、name、type、private_ip_address、host_iqn、username 或 password。</dd>
<dt>--column</dt>
<dd>要显示的列，选项为：id、name、type、private_ip_address、host_iqn、username 或 password。</dd>
</dl>

**示例**：
```
ibmcloud sl file access-list 12345678 --sortby id
```

此命令列出有权访问标识为 `12345678` 的卷的所有主机，并按标识对其排序。

## ibmcloud sl file access-revoke
{: #sl_file_access_revoke}

撤销主机访问给定卷的授权。
```
ibmcloud sl file access-revoke VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-d, --hardware-id</dt>
<dd>要撤销的一个硬件服务器的标识。</dd>
<dt>-v, --virtual-id</dt>
<dd>要撤销的一个虚拟服务器的标识。</dd>
<dt>-i, --ip-address-id</dt>
<dd>要撤销的一个 IP 地址的标识。</dd>
<dt>-p, --ip-address</dt>
<dd>要撤销的 IP 地址。</dd>
<dt>-s, --subnet-id</dt>
<dd>要撤销的一个子网的标识。</dd>
</dl>

**示例**：
```
ibmcloud sl file access-revoke 12345678 --virtual-id 87654321
```

此命令撤销标识为 `87654321` 的虚拟服务器对标识为 `12345678` 的卷的访问权。

## ibmcloud sl file replica-failback
{: #sl_file_replica_failback}

从副本对文件卷执行故障恢复操作。
```
ibmcloud sl file replica-failback VOLUME_ID
```

**示例**：
```
ibmcloud sl file replica-failback 12345678
```
此命令对标识为 `12345678` 的卷执行故障恢复操作。

## ibmcloud sl file replica-failover
{: #sl_file_replica_failover}

从文件卷故障转移到给定的副本卷。
```
ibmcloud sl file replica-failover VOLUME_ID REPLICA_ID
```


**示例**：
```
ibmcloud sl file replica-failover 12345678 87654321
```
此命令对标识为 `12345678` 的卷执行到标识为 `87654321` 的副本卷的故障转移操作。

## ibmcloud sl file replica-locations
{: #sl_file_replica_locations}

列出给定卷的适用复制数据中心。
```
ibmcloud sl file replica-locations VOLUME_ID
```


**示例**：
```
ibmcloud sl file replica-locations 12345678
```
此命令列出标识为 `12345678` 的文件卷的适用复制数据中心。

## ibmcloud sl file replica-order
{: #sl_file_replica_order}

订购文件存储器副本卷。
```
ibmcloud sl file replica-order VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-s, --snapshot-schedule</dt>
<dd>必需。用于复制的快照安排，选项为：HOURLY、DAILY 或 WEEKLY。</dd>
<dt>-d, --datacenter</dt>
<dd>必需。副本的数据中心的短名称，例如 dal09。</dd>
<dt>-t, --tier</dt>
<dd>可选。为其订购副本的主卷的耐久性存储器层 (IOPS/GB)，选项为：0.25、2、4 或 10；如果未指定任何层，那么将使用原始卷的层。</dd>
<dt>-i, --iops</dt>
<dd>性能存储器 IOPS，介于 100 到 6000 之间，是 100 的倍数；如果未指定 IOPS，那么将使用原始卷的 IOPS。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file replica-order 12345678 -s DAILY -d dal09 --tier 4
```

此命令为标识为 `12345678` 的卷订购副本，此副本执行 DAILY 复制，位于 `dal09`，层级为 4。

## ibmcloud sl file replica-partners
{: #sl_file_replica_partners}

列出文件卷的现有副本卷。
```
ibmcloud sl file replica-partners VOLUME_ID [OPTIONS]
```


**示例**：
```
ibmcloud sl file replica-partners 12345678
```

此命令列出标识为 `12345678` 的文件卷的现有副本卷。

## ibmcloud sl file snapshot-cancel
{: #sl_file_snapshot_cancel}

取消给定卷的现有快照空间。
```
ibmcloud sl file snapshot-cancel SNAPSHOT_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>--reason</dt>
<dd>可选的取消原因。</dd>
<dt>--immediate</dt>
<dd>立即取消快照空间，而不是在计费周年取消。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-cancel 12345678 --immediate -f
```

此命令立即取消标识为 `12345678` 的快照，而不要求确认。

## ibmcloud sl file snapshot-create
{: #sl_file_snapshot_create}

创建给定卷的快照。
```
ibmcloud sl file snapshot-create VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-n, --note</dt>
<dd>要对新快照设置的注释。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-create 12345678 --note snapshotforibmcloud
```
此命令创建标识为 `12345678` 的卷的快照，并添加注释 `snapshotforibmcloud`。

## ibmcloud sl file snapshot-disable
{: #sl_file_snapshot_disable}

禁止按指定安排生成给定卷的快照。
```
ibmcloud sl file snapshot-disable VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-s, --schedule-type</dt>
<dd>必需。快照安排，选项为：HOURLY、DAILY 或 WEEKLY。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-disable 12345678 -s DAILY
```

此命令禁止为标识为 `12345678` 的卷生成每日快照。

## ibmcloud sl file snapshot-enable
{: #sl_file_snapshot_enable}

允许按指定安排生成给定卷的快照。
```
ibmcloud sl file snapshot-enable VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-s, --schedule-type</dt>
<dd>必需。快照安排，选项为：HOURLY、DAILY 或 WEEKLY。</dd>
<dt>-c, --retention-count</dt>
<dd>必需。要保留的快照数。</dd>
<dt>-m, --minute</dt>
<dd>应生成快照的时刻（分钟，0 到 59 之间的整数）。</dd>
<dt>-r, --hour</dt>
<dd>应生成快照的时刻（小时，0 到 23 之间的整数）。</dd>
<dt>-d, --day-of-week</dt>
<dd>应生成快照的日期（星期，0 到 6 之间的整数）。0 表示周日，1 表示周一，2 表示周二，3 表示周三，4 表示周四，5 表示周五，6 表示周六。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-enable 12345678 -s WEEKLY -c 5 -m 0 --hour 2 -d 0
```

此命令允许为标识为 `12345678` 的卷生成快照。快照将在每周日 2:00 生成，最多保留 5 个快照。

## ibmcloud sl file snapshot-delete
{: #sl_file_snapshot_delete}

删除给定卷的快照。
```
ibmcloud sl file snapshot-delete SNAPSHOT_ID
```

**示例**：
```
ibmcloud sl file snapshot-delete 12345678
```

此命令删除标识为 `12345678` 的快照。

## ibmcloud sl file snapshot-list
{: #sl_file_snapshot_list}

列出文件存储器快照。
```
ibmcloud sl file snapshot-list VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>--sortby</dt>
<dd>要作为排序依据的列，选项为：id、name、created 或 size_bytes。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-list 12345678 --sortby id
```

此命令列出标识为 `12345678` 的卷的所有快照，并按标识对它们排序。

## ibmcloud sl file snapshot-order
{: #sl_file_snapshot_order}

为文件存储卷订购快照空间。
```
ibmcloud sl file snapshot-order VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-s, --size</dt>
<dd>必需。要创建的快照空间的大小（以 GB 为单位）。</dd>
<dt>-t, --tier</dt>
<dd>可选。为其订购空间的文件卷的耐久性存储器层 (IOPS/GB)，选项为：0.25、2、4 或 10。</dd>
<dt>-i, --iops</dt>
<dd>性能存储器 IOPS，介于 100 到 6000 之间，是 100 的倍数。</dd>
<dt>-u, --upgrade</dt>
<dd>指示订单是升级的标志。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file snapshot-order 12345678 -s 1000 -t 4
```
此命令为标识为 `12345678` 的卷订购快照空间，大小为 1000 GB，层级为 4 IOPS/GB。

## ibmcloud sl file snapshot-restore
{: #sl_file_snapshot_restore}

使用给定快照复原文件卷。
```
ibmcloud sl file snapshot-restore VOLUME_ID SNAPSHOT_ID
```

**示例**：
```
ibmcloud sl file snapshot-restore 12345678 87654321
```

此命令通过标识为 `87654321` 的快照复原标识为 `12345678` 的卷。

## ibmcloud sl snapshot-schedule-list
{: #sl_snapshot_schedule_list}

列出给定卷的快照安排
```
ibmcloud sl snapshot-schedule-list VOLUME_ID
```

**示例**：
```
ibmcloud sl file snapshot-schedule-list 12345678
```

此命令列出标识为 `12345678` 的卷的快照安排。

## ibmcloud sl file volume-cancel
{: #sl_file_volume_cancel}

取消现有文件存储卷。
```
ibmcloud sl file volume-cancel VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>--reason</dt>
<dd>可选的取消原因。</dd>
<dt>--immediate</dt>
<dd>立即取消文件存储卷，而不是在计费周年取消。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file volume-cancel 12345678 --immediate -f
```

此命令立即取消标识为 `12345678` 的卷，而不要求确认。

## ibmcloud sl file volume-count
{: #sl_file_volume_count}

列出每个数据中心的文件存储卷数。
```
ibmcloud sl file volume-count [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-d, --datacenter</dt>
<dd>按数据中心短名称过滤。</dd>
</dl>

## ibmcloud sl file volume-list
{: #sl_file_volume_list}

列出文件存储器。
```
ibmcloud sl file volume-list [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-u, --username</dt>
<dd>按卷用户名过滤。</dd>
<dt>-d, --datacenter</dt>
<dd>按数据中心短名称过滤。</dd>
<dt>-t, --storage-type</dt>
<dd>按存储卷类型过滤，选项为：performance 或 endurance。</dd>
<dt>-o, --order</dt>
<dd>按购买了文件存储器的订单的标识过滤。</dd>
<dt>--sortby</dt>
<dd>要作为排序依据的列，选项为：id、username、datacenter、storage_type、capacity_gb、bytes_used、ip_addr、active_transactions 或 mount_addr。</dd>
<dt>--column</dt>
<dd>要显示的列，选项为：id、username、datacenter、storage_type、capacity_gb、bytes_used、ip_addr、mount_addr 或 notes。</dd>
</dl>

**示例**：
```
ibmcloud sl file volume-list -d dal09 -t endurance --sortby capacity_gb
```

此命令列出当前帐户中位于 `dal09` 的所有耐久性卷，并按容量对它们排序。

## ibmcloud sl file volume-detail
{: #sl_file_volume_detail}

显示指定卷的详细信息。
```
ibmcloud sl file volume-detail VOLUME_ID
```


**示例**：
```
ibmcloud sl file volume-detail 12345678
```

此命令显示标识为 `12345678` 的卷的详细信息。

## ibmcloud sl file volume-duplicate
{: #sl_file_volume_duplicate}

通过复制现有卷来订购文件卷。
```
ibmcloud sl file volume-duplicate VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-o, --origin-snapshot-id</dt>
<dd>用于复制的原始卷快照的标识。</dd>
<dt>-s, --duplicate-size</dt>
<dd>复制文件卷的大小（以 GB 为单位），如果未指定大小，那么将使用原始卷的大小。</dd>
<dt>-i, --duplicate-iops</dt>
<dd>性能存储器 IOPS，介于 100 到 6000 之间，是 100 的倍数；如果未指定 IOPS，那么将使用原始卷的 IOPS。</dd>
<dt>-t, --duplicate-tier</dt>
<dd>耐久性存储器层，如果未指定层，那么将使用原始卷的层。</dd>
<dt>-n, --duplicate-snapshot-size</dt>
<dd>订购用于复制的快照空间的大小，如果未指定快照空间大小，那么将使用原始卷的快照空间大小。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file volume-duplicate 12345678
```

此命令显示通过复制标识为 `12345678` 的卷来订购新卷。

## ibmcloud sl file volume-order
{: #sl_file_volume_order}

订购文件存储卷。
```
ibmcloud sl file volume-order [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-t, --storage-type</dt>
<dd>必需。存储卷的类型，选项为：performance 或 endurance。</dd>
<dt>-s, --size</dt>
<dd>必需。存储卷大小 (GB)</dd>
<dt>-i, --iops</dt>
<dd>性能存储器 IOPS，介于 100 到 6000 之间，是 100 的倍数 [storage-type 为 performance 时是必需的]。</dd>
<dt>-e, --tier</dt>
<dd>耐久性存储器层 (IOP/GB) [storage-type 为 endurance 时是必需的]，选项为：0.25、2、4 或 10。</dd>
<dt>-d, --datacenter</dt>
<dd>必需。数据中心短名称。</dd>
<dt>-n, --snapshot-size</dt>
<dd>用于订购快照空间和卷的可选参数。</dd>
<dt>-b, --billing</dt>
<dd>计费费率的可选参数（缺省值为 monthly），选项为：hourly 或 monthly。</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：
```
ibmcloud sl file volume-order --storage-type performance --size 1000 --iops 4000  -d dal09
```

此命令订购性能卷，大小为 1000 GB，IOPS 为 4000，位于 `dal09`。

## ibmcloud sl file volume-modify
{: #sl_file_volume_modify}

修改现有文件存储卷
```
ibmcloud sl file volume-modify VOLUME_ID [OPTIONS]
```

<strong>命令选项</strong>：
<dl>
<dt>-c, --new-size</dt>
<dd>文件卷的新大小，以 GB 为单位。***如果未给定大小，那么将使用卷的原始大小。***可能的大小为：[20, 40, 80, 100, 250, 500, 1000, 2000, 4000, 8000, 12000] 最小值为：[卷的原始大小]</dd>
<dt>-i, --new-iops</dt>
<dd>性能存储器 IOPS，介于 100 到 6000 之间，是 100 的倍数 [仅限性能卷] ***如果未指定 IOPS 值，那么将使用卷的原始 IOPS 值。*** 要求：[如果卷的原始 IOPS/GB 小于 0.3，那么新 IOPS/GB 必须也小于 0.3。如果卷的原始 IOPS/GB 大于或等于 0.3，那么卷的新 IOPS/GB 必须也大于或等于 0.3。]</dd>
<dt>-t, --new-tier</dt>
<dd>耐久性存储层 (IOPS/GB) [仅限耐久性卷] ***如果未指定任何层，那么将使用卷的原始层。***
要求：[如果卷的原始 IOPS/GB 为 0.25，那么卷的新 IOPS/GB 必须也是 0.25。如果卷的原始 IOPS/GB 大于 0.25，那么卷的新 IOPS/GB 必须也大于 0.25。]</dd>
<dt>-f, --force</dt>
<dd>强制操作而不确认。</dd>
</dl>

**示例**：

```
ibmcloud sl file volume-modify 12345678 --new-size 1000 --new-iops 4000
```

此命令将卷 `12345678` 的大小修改为 1000 GB，将 IOPS 修改为 4000。

```
ibmcloud sl file volume-modify 12345678 --new-size 500 --new-tier 4
```

此命令将卷 `12345678` 的大小修改为 500 GB，将层级修改为 4 IOPS/GB。


## ibmcloud sl file volume-options
{: #sl_file_volume_options}

列出用于订购文件存储器的所有选项。
```
ibmcloud sl file volume-options
```

**示例**：
```
ibmcloud sl file volume-options
```
此命令列出用于创建文件存储卷的所有选项，包括存储器类型、卷大小、IOPS、层级、数据中心和快照大小。
