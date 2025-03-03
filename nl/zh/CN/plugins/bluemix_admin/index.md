---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-21"

keywords: cli, ibmcloud admin cli, admin cli plugin, admin plugin, cloud foundry admin cli plugin, adding users, buildpack, security groups, cf ba

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# {{site.data.keyword.cloud_notm}} 管理 CLI
{: #bluemixadmincli}

您可以使用带有 {{site.data.keyword.cloud_notm}} 管理 CLI 插件的 Cloud Foundry 命令行界面 (CLI) 来管理 {{site.data.keyword.cloud_notm}} Local 或 {{site.data.keyword.cloud_notm}} Dedicated 环境。 例如，可以从 LDAP 注册表添加用户。

开始之前，请先安装 Cloud Foundry CLI。{{site.data.keyword.cloud_notm}} 管理 CLI 插件需要 `cf` V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面](https://github.com/cloudfoundry/cli/releases){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")

Cygwin 不支持 Cloud Foundry CLI。请在非 Cygwin 命令行窗口中使用 Cloud Foundry CLI。

{{site.data.keyword.cloud_notm}} 管理 CLI 仅用于 {{site.data.keyword.cloud_notm}} Local 和 {{site.data.keyword.cloud_notm}} Dedicated 环境。{{site.data.keyword.cloud_notm}} Public 不支持该管理 CLI。
{: note}

## 添加 {{site.data.keyword.cloud_notm}} 管理 CLI 插件
{: #add-admin-cli}

安装 Cloud Foundry CLI 后，可以添加 {{site.data.keyword.cloud_notm}} 管理 CLI 插件。

如果先前安装了 {{site.data.keyword.cloud_notm}} 管理插件，那么可能需要卸载此插件，删除存储库，然后再次安装以获取最新更新。
{: tip}

完成以下步骤来添加存储库并安装该插件：

1. 要添加 {{site.data.keyword.cloud_notm}} 管理插件存储库，请运行以下命令：
  ```
  cf add-plugin-repo IBMCloudAdmin https://<customer_console_endpoint>.bluemix.net/cli
  ```
  {: codeblock}

  您可以在管理控制台 CLI 页面上查找与实际端点相同的命令：`https://<customer_console_endpoint>.bluemix.net/cli`。
  {: note}

2. 要安装 {{site.data.keyword.cloud_notm}} 管理 CLI 插件，请运行以下命令：
  ```
  cf install-plugin IBMCloudAdminCLI -r IBMCloudAdmin
  ```
  {: codeblock}

## 卸载 {{site.data.keyword.cloud_notm}} 管理 CLI 插件
{: #remove-admin-cli}

要卸载插件，请完成以下步骤。 

1. 卸载插件：
  ```
  cf uninstall-plugin IBMCloudAdminCLI
  ```
  {: codeblock}

2. 除去插件存储库：
  ```
  cf remove-plugin-repo IBMCloudAdmin
  ```
  {: codeblock}

然后，可以添加更新的存储库并安装最新的插件。

## 使用 {{site.data.keyword.cloud_notm}} 管理 CLI 插件
{: #using-admin-cli}

您可以使用 {{site.data.keyword.cloud_notm}} 管理 CLI 插件来添加或除去用户、向组织分配或取消分配用户，以及执行其他管理任务。

要查看命令的列表，请运行以下命令：
```
cf plugins
```
{: codeblock}

有关命令的更多帮助，请使用 `-help` 选项。

### 连接并登录到 {{site.data.keyword.cloud_notm}}
{: #connecting-ibm-cloud}

1. 要连接到 {{site.data.keyword.cloud_notm}} API 端点，请运行以下命令：
  ```
  cf api api.us-south.cf.cloud.ibm.com
  ```
  {: codeblock}
  
  虽然旧的 `api..bluemix.net` Cloud Foundry API 端点仍可用，但您也可以更新脚本和基础架构自动化，以针对您的区域使用以下更新的 Cloud Foundry API 端点：

  * api.us-south.cf.cloud.ibm.com（先前为 api.ng.bluemix.net）
  * api.eu-gb.cf.cloud.ibm.com（先前为 api.eu-gb.bluemix.net）
  * api.us-east.cf.cloud.ibm.com（先前为 api.us-east.bluemix.net）
  * api.eu-de.cf.cloud.ibm.com（先前为 api.eu-de.bluemix.net）
  * api.au-syd.cf.cloud.ibm.com（先前为 api.au-syd.bluemix.net）

  您可以查看管理控制台的“资源和信息”页面，以获取正确的 URL。此 URL 显示在“API 信息”部分的 **API URL** 字段中。

2. 通过运行以下命令，登录到 {{site.data.keyword.cloud_notm}}：
  ```
cf login
```
  {: codeblock}

## 管理用户
{: #admin_users}

### 添加用户
{: #admin_add_user}

要将用户从环境的用户注册表添加到 {{site.data.keyword.cloud_notm}} 环境，请使用以下命令：
```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

要向特定组织添加用户，您必须是具有 users.write（或 Superuser）许可权的管理员。如果您是组织管理者，那么还可以通过 Superuser 来运行 **`enable-managers-add-users`** 命令，以向组织添加用户。有关更多信息，请参阅[允许管理者添加用户](#clius_emau)。

|选项|描述
| 
| -------| ------------|
| _userName_ |LDAP 注册表中用户的名称。|
| _organization_ |要向其添加用户的 {{site.data.keyword.cloud_notm}} 组织的名称或 GUID。|
| _firstName_ |要添加到组织的用户的名字。| 
| _lastName_ |要添加到组织的用户的姓氏。| 
{: caption="表 1. cf ba add-user 命令选项" caption-side="top"}

**`ba add-user`** 命令名较长，您还可以使用 **`ba au`** 作为其别名。
{: tip}

### 邀请 {{site.data.keyword.Bluemix_dedicated_notm}} 中的用户
{: #admin_dedicated_invite_public}

每个 {{site.data.keyword.Bluemix_dedicated_notm}} 环境在 {{site.data.keyword.cloud_notm}} 中都有一个客户机拥有的公共企业帐户。为了使 Dedicated 环境中的用户可使用 {{site.data.keyword.containershort}} 创建集群，管理员必须将这些用户添加到此公共企业帐户。将用户添加到公共企业帐户后，其 Dedicated 帐户和公共帐户会链接在一起。然后，用户可以使用其 IBM 标识同时登录到 Dedicated 帐户和公共帐户，并且可以通过 Dedicated 界面在公共帐户中创建资源。有关更多信息，请参阅[在 Dedicated 上设置 IBM Cloud Container Service](/docs/containers?topic=containers-dedicated#dedicated_setup)。要邀请 Dedicated 用户加入公共帐户，请运行以下命令：
```
cf ba invite-users-to-public -userid=<user_email> -organization=<dedicated_org_id> -apikey=<public_api_key> -public_org_id=<public_org_id>
```
{: pre}

要将 Dedicated 环境用户添加到 {{site.data.keyword.cloud_notm}} 公共帐户，您必须是 Dedicated 帐户的管理员。

|选项|描述
| 
| -------| ------------|
| -userid |如果要邀请单个用户，请使用该用户的电子邮件。|
| -organization |如果要邀请当前位于 Dedicated 帐户组织中的所有用户，请使用 Dedicated 帐户组织标识。|
| -apikey |用于邀请用户加入公共帐户的 API 密钥。此密钥必须由公共帐户的管理员来生成。| 
| -public_org_id |要邀请用户加入的公共帐户组织的标识。| 
{: caption="表 2. cf ba invite-users-to-public 命令选项" caption-side="top"}

### 列出邀请的 {{site.data.keyword.Bluemix_dedicated_notm}} 用户
{: #admin_dedicated_list}

如果已使用 [**`invite-users-to-public`** 命令](#admin_dedicated_invite_public)邀请 Dedicated 环境用户加入 {{site.data.keyword.Bluemix_notm}} 帐户，那么可以列出帐户中的用户以查看他们的邀请状态。具有现有 IBM 标识的受邀用户的状态为“活动”。没有现有 IBM 标识的受邀用户的状态为“暂挂”或“活动”，具体取决于他们是否已接受加入帐户的邀请。要列出 {{site.data.keyword.Bluemix_notm}} 帐户中的用户，请运行以下命令：

```
cf ba invite-users-status -apikey=<public_api_key>
```
{: pre}

要将 Dedicated 环境用户添加到 {{site.data.keyword.Bluemix_notm}} 公共帐户，您必须是 Dedicated 帐户的管理员。

<dl class="parml">
<dt class="pt dlterm">&lt;public_api_key&gt;</dt>
<dd class="pd">用于邀请用户加入帐户的 API 密钥。此密钥必须由公共帐户的管理员来生成。</dd>
</dl>

<!-- staging-only commands start. Live for interconnect -->

### 搜索用户
{: #admin_search_user}

要搜索用户，请将以下命令与可选的搜索过滤参数（name、permission、organization 和 role）配合使用：

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| -name |用户的名称。|
| -permission |分配给用户的许可权。可用的许可权为 admin（或 superuser）、login（或 basic）、catalog.read、catalog.write、reports.read、reports.write、users.read 或 users.write。不能将此参数与 organization 参数用于同一查询中。|
| -organization |用户所属的组织名称。不能将此参数与 permission 参数用于同一查询中。| 
| -role |分配给用户的组织角色。可用的角色为 auditors、managers 和 billing_managers。使用此参数时必须指定组织。| 
{: caption="表 3. cf ba search-users 命令选项" caption-side="top"}

**`ba search-users`** 命令名较长，您还可以使用 **`ba su`** 作为其别名。
{: tip}

### 为用户设置许可权
{: #admin_setperm_user}

要为指定用户设置许可权，请使用以下命令：
```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _userName_ |用户的名称。|
| _permission_ |设置分配给用户的许可权。可用的许可权为 admin（或 superuser）、login（或 basic）、catalog.read、catalog.write、reports.read、reports.write、users.read 或 users.write。不能将此参数与 organization 参数用于同一查询中。|
| _access_ |对于 catalog、reports 或 user 许可权，还必须将访问级别设置为 `read` 或 `write`。|  
{: caption="表 4. cf ba set-permissions 命令选项" caption-side="top"}

一次只能设置一个许可权。

**`ba set-permissions`** 命令名较长，您还可以使用 **`ba sp`** 作为其别名。
{: tip}

<!-- staging-only commands end -->

### 除去用户
{: #admin_remov_user}

要从 {{site.data.keyword.Bluemix_notm}} 环境除去用户，请使用以下命令：

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>

</dl>

**`ba remove-user`** 命令名较长，您还可以使用 **`ba ru`** 作为其别名。
{: tip}

### 允许管理员添加用户
{: #clius_emau}

如果您在 {{site.data.keyword.Bluemix_notm}} 环境中有 Superuser 许可权，那么可以允许组织管理者向其管理的组织添加用户。要使管理者能够添加用户，请使用以下命令：

```
cf ba enable-managers-add-users
```
{: codeblock}

**`ba enable-managers-add-users`** 命令名较长，您还可以使用 **`ba emau`** 作为其别名。
{: tip}

### 禁止管理者添加用户
{: #clius_dmau}

如果在 {{site.data.keyword.Bluemix_notm}} 环境中已允许组织管理者通过 **`enable-managers-add-users`** 命令向其管理的组织添加用户，并且您有 Superuser 许可权，那么可以除去此设置。要禁止管理者添加用户，请使用以下命令：

```
cf ba disable-managers-add-users
```
{: codeblock}

**`ba disable-managers-add-users`** 命令名较长，您还可以使用 **`ba dmau`** 作为其别名。
{: tip}

## 管理组织
{: #admin_orgs}

### 添加组织
{: #admin_add_org}

要添加组织，请使用以下命令：

```
cf ba create-org <organization> <manager>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |要添加的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID|
| _manager_ |组织的管理者的用户名。|
{: caption="表 5. cf ba create-org 命令选项" caption-side="top"}

**`ba create-org`** 命令名较长，您还可以使用 **`ba co`** 作为其别名。
{: tip}

### 删除组织
{: #admin_delete_org}

要删除组织，请使用以下命令：

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要删除的 {{site.data.keyword.cloud_notm}} 组织的名称或 GUID。</dd>
</dl>

**`ba delete-org`** 命令名较长，您还可以使用 **`ba do`** 作为其别名。
{: tip}

### 向组织分配用户
{: #admin_ass_user_org}

要将 {{site.data.keyword.cloud_notm}} 环境中的用户分配给特定组织，请使用以下命令：

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _userName_ |用户的名称。|
| _organization_ |要向其分配用户的 {{site.data.keyword.cloud_notm}} 组织的名称或 GUID。|
| _role_ |用户的角色。有效值为 `OrgManager`、`BillingManager` 和 `OrgAuditor`。有关角色描述，请参阅 [角色](/docs/iam?topic=iam-userroles#userroles)。|  
{: caption="表 6. cf ba set-org 命令选项" caption-side="top"}

**`ba set-org`** 命令名较长，您还可以使用 **`ba so`** 作为其别名。
{: tip}

### 从组织中取消分配用户
{: #admin_unass_user_org}

要将 {{site.data.keyword.cloud_notm}} 环境中的用户取消分配给特定组织，请使用以下命令：

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _userName_ |用户的名称。|
| _organization_ |{{site.data.keyword.cloud_notm}} 组织的名称或 GUID。|
| _role_ |用户的角色。有效值为 `OrgManager`、`BillingManager` 和 `OrgAuditor`。有关角色描述，请参阅 [角色](/docs/iam?topic=iam-userroles#userroles)。|  
{: caption="表 7. cf ba unset-org 命令选项" caption-side="top"}

**`ba unset-org`** 命令名较长，您还可以使用 **`ba uo`** 作为其别名。
{: tip}

### 设置组织的配额
{: #admin_set_org_quota}

要为特定组织设置使用量配额，请使用以下命令：

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |要为其设置配额的 {{site.data.keyword.cloud_notm}} 组织的名称或 GUID。|
| _plan_ |组织的配额计划。|  
{: caption="表 8. cf ba set-quota 命令选项" caption-side="top"}

**`ba set-quota`** 命令名较长，您还可以使用 **`ba sq`** 作为其别名。
{: tip}


### 查找组织的容器配额
{: #admin_find_containquotas}

要查找组织的容器配额，请使用以下命令：

```
cf ibmcloud-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">IBM Cloud 中组织的名称或标识。此参数是必需的。</dd>
</dl>

**`ibmcloud-admin containers-quota`** 命令名较长，您还可以使用 **`ba cq`** 作为其别名。
{: tip}

### 设置组织的容器配额
{: #admin_set_containquotas}

要设置组织中容器的配额，请使用以下命令并至少包含其中一个选项：

```
cf ibmcloud-admin set-containers-quota <organization> <options>
```
{: codeblock}

您可以包含多个选项，但必须至少包含一个选项。
{: note}

|选项|描述
| 
| -------| ------------|
| _organization_ |要为其设置配额的 {{site.data.keyword.cloud_notm}} 组织的名称或标识。|
| _options_ |选项为 **`floating-ips-max value`**（短名称 **`fim`**）、**`floating-ips-space-default value`**（短名称 **`fisd`**）、**`memory-max value`**（短名称 **`mm`**）、**`memory-space-default value`**（短名称 **`msd`**）或 **`image-limit value`**（短名称 **`il`**）。该值必须为整数。|  
{: caption="表 9. cf ibmcloud-admin set-containers-quota 命令选项" caption-side="top"}

（可选）可以提供一个在有效 JSON 对象中包含特定配置参数的文件。如果使用 **`-file`** 选项，那么会优先使用此选项并忽略其他选项。要提供文件，而不设置选项，请使用以下命令：

```
cf ibmcloud-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

JSON 文件的格式应该如以下示例中所示：

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**`ibmcloud-admin set-containers-quota`** 命令名较长，您还可以使用 **`ba scq`** 作为其别名。
{: tip}

## 管理空间
{: #admin_spaces}

### 向组织添加空间

要在组织中添加空间，请使用以下命令：

```
cf ibmcloud-admin create-space <organization> <space_name>
```

{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |要向其添加空间的组织的名称或 GUID。|
| _spaceName_ |要添加到组织的空间的名称。|  
{: caption="表 10. cf ibmcloud-admin create-space 命令选项" caption-side="top"}

**`ba create-space`** 命令名较长，您还可以使用 **`ba cs`** 作为其别名。
{: tip}

### 从组织中删除空间

要从组织中除去空间，请使用以下命令：

```
cf ibmcloud-admin delete-space <organization> <space_name>
```

{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |要从中除去空间的组织的名称或 GUID。|
| _spaceName_ |要从组织中除去的空间的名称。|  
{: caption="表 11. cf ibmcloud-admin delete-space 命令选项" caption-side="top"}

**`ba delete-space`** 命令名较长，您还可以使用 **`ba cs`** 作为其别名。
{: tip}

### 向空间添加具有角色的用户

要在空间中创建具有指定角色的用户，请使用以下命令：

```
cf ibmcloud-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |要向其添加用户的组织的名称或 GUID。|
| _spaceName_ |要向其添加用户的空间的名称。|
| _userName_ |用户的名称。|
| _role_ |用户的角色。有效值为 `Manager`、`Developer` 或 `Auditor`。|  
{: caption="表 12. cf ibmcloud-admin set-space 命令选项" caption-side="top"}

**`ba set-space`** 命令名较长，您还可以使用 **`ba ss`** 作为其别名。
{: tip}


### 除去空间中用户的角色

要除去空间中用户的角色，请使用以下命令：

```
cf ibmcloud-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

|选项|描述
| 
| -------| ------------|
| _organization_ |用户所属组织的名称或 GUID。|
| _spaceName_ |用户所属空间的名称。|
| _userName_ |用户的名称。|
| _role_ |用户的角色。有效值为 `Manager`、`Developer` 或 `Auditor`。|  
{: caption="表 13. cf ibmcloud-admin unset-space 命令选项" caption-side="top"}

**`ba unset-space`** 命令名较长，您还可以使用 **`ba us`** 作为其别名。
{: tip}

## 管理目录
{: #admin_catalog}

### 对所有组织启用服务
{: #admin_ena_service_org}

要允许某个服务在所有组织的 {{site.data.keyword.cloud_notm}}“目录”中显示，请使用以下命令：

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
</dl>

**`ba enable-service-plan`** 命令名较长，您还可以使用 **`ba esp`** 作为其别名。
{: tip}

### 对所有组织禁用服务
{: #admin_dis_service_org}

要禁止某个服务在所有组织的 {{site.data.keyword.Bluemix_notm}}“目录”中显示，请使用以下命令：

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
</dl>

**`ba disable-service-plan`** 命令名较长，您还可以使用 **`ba dsp`** 作为其别名。
{: tip}

### 添加组织的服务可视性
{: #admin_addvis_service_org}

可以在能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表中添加组织。要允许某个组织在目录中查看特定服务，请使用以下命令：

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _planIdentifier_ |要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。|
| _organization_ |要添加到服务的可视性列表的组织的名称或 GUID。|  
{: caption="表 14. cf ba add-service-plan-visibility 命令选项" caption-side="top"}

**`ba add-service-plan-visibility`** 命令名较长，您还可以使用 **`ba aspv`** 作为其别名。
{: tip}

### 除去组织的服务可视性
{: #admin_remvis_service_org}

可以从能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表中除去组织。要在某个组织的目录中除去某个服务的可视性，请使用以下命令：

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _planIdentifier_ |要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。|
| _organization_ |要从服务的可视性列表中除去的组织的名称或 GUID。|  
{: caption="表 15. cf ba remove-service-plan-visibility 命令选项" caption-side="top"}

**`ba remove-service-plan-visibility`** 命令名较长，您还可以使用 **`ba rspv`** 作为其别名。
{: tip}

### 编辑组织的服务可视性
{: #admin_editvis_service_org}

您可以编辑和替换特定组织可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看的服务的列表。要替换一个组织或多个组织的所有现有可视服务，请使用以下命令：

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

此命令会将指定组织的现有可视服务替换为在命令中指定的服务。

|选项|描述
| 
| -------| ------------|
| _planIdentifier_ |要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。|
| _organization_ |要为其添加可视性的组织的名称或 GUID。可以通过在命令中输入更多组织名称或 GUID，对多个组织启用服务可视性。|  
{: caption="表 16. cf ba edit-service-plan-visibs 命令选项" caption-side="top"}

**`ba edit-service-plan-visibility`** 命令名较长，您还可以使用 **`ba espv`** 作为其别名。
{: tip}

## 管理报告
{: #admin_add_report}

### 添加报告
{: #admin_adding_report}

要添加安全报告，请使用以下命令：

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

如果您拥有报告的写访问权，那么可以使用用户接受的任何格式，创建新类别并添加报告。输入 **`category`** 参数的新类别名称，或者添加新报告到现有类别。

|选项|描述
| 
| -------| ------------|
| _category_ |报告的类别。如果名称中有空格，请使用引号。|
| _date_ |报告日期，格式为 YYYYMMDD。|  
| _filePath_ |要上传的报告 PDF、文本文件或日志文件的路径。|
| _RTF_ |用于包含富文本格式 (RTF) 版本的 PDF 的选项。仅当包含报告 PDF 的路径时，此选项才适用。RTF 版本用于建立索引和执行搜索。|
{: caption="表 17. cf ba add-report 命令选项" caption-side="top"}

**`ba add-report`** 命令名较长，您还可以使用 **`ba ar`** 作为其别名。
{: tip}

### 删除报告
{: #admin_del_report}

要删除安全报告，请使用以下命令：

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _category_ |报告的类别。如果名称中有空格，请使用引号。|
| _date_ |报告日期，格式为 YYYYMMDD。|  
| _name_ |报告的名称。|
{: caption="表 18. cf ba delete-report 命令选项" caption-side="top"}

**`ba delete-report`** 命令名较长，您还可以使用 **`ba dr`** 作为其别名。
{: tip}

### 检索报告
{: #admin_retr_report}

要检索安全报告，请使用以下命令：

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">报告的文件名。如果名称中有空格，请使用引号将名称括起。</dd>
</dl>

**`ba retrieve-report`** 命令名较长，您还可以使用 **`ba rr`** 作为其别名。
{: tip}

## 查看资源度量值信息
{: #cliresourceusage}

您可以查看资源度量值信息，包括内存、磁盘和 CPU 使用率。可以查看可用物理资源和保留资源的摘要，以及物理资源和保留资源使用情况的摘要。此外，还可以查看 Droplet Execution Agent (DEA) 和单元（Diego 体系结构）使用情况数据。要查看资源度量值信息，请使用以下命令：

```
cf ba resource-metrics
```

**`ba resource-metrics`** 命令名较长，您还可以使用 **`ba rsm`** 作为其别名。
{: tip}

## 查看资源度量值历史记录
{: #cliresourceusagehistory}

您可以检索内存和磁盘使用情况的资源度量值历史记录。返回的度量值包括使用的资源量占可用总量的比例，包括物理资源和预留资源。内存和磁盘使用情况的历史记录数据可以按小时、按天或按月显示。您可以指定开始和结束日期，以便在某个特定的日期范围内检索数据。在未指定日期的情况下，缺省的历史记录数据是最近 48 小时内的每小时内存数据。数据按降序显示，较新的日期显示在前边。要查看资源度量值历史记录信息，请使用以下命令：

```
cf ba resource-metrics-history <hourly|daily|monthly>  <memory|disk >  <start|end>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| --hourly | View the historical data for the last 48 hours. This is the default value. |
| --daily | View the historical data daily average for the last 30 days. |  
| --monthly | View the historical data monthly average for the last 6 months. |
| --memory | View the used and total reserved and physical memory. |
| --disk | View the used and total reserved and physical disk. | 
| --start | Specify a start date for daily or monthly in the format of mm-dd-yyyy, or start date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
| --end | Specify an end date for daily or monthly in the format of mm-dd-yyyy, or end date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
{: caption="表 19： cf ba resource-metrics-history 命令选项" caption-side="top"}

**示例**

```
cf ibmcloud-admin resource-metrics-history
cf ibmcloud-admin resource-metrics-history --daily --disk --start=07-04-2017
cf ibmcloud-admin resource-metrics-history --monthly --memory
cf ibmcloud-admin resource-metrics-history --hourly --start="06-01-2017 00:00:00 EDT" --end="06-30-2017 23:59:00 EDT
```
{: codeblock}

您可以使用以下命令来查看上面的命令参数和示例列表：

```
cf ba resource-metrics-history -help
```

**`ba resource-metrics-history`** 命令名较长，您还可以使用 **`ba rsmh`** 作为其别名。
{: tip}

## 管理服务代理程序
{: #admin_servbro}

### 列出服务代理程序
{: #clilistservbro}

要列出服务代理程序，请使用以下命令：

```
cf ba service-brokers <broker_name>
```
{: codeblock}

要列出所有服务代理程序，请输入不带 **`broker_name`** 参数的命令。

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">定制服务代理程序的名称。如果要获取特定服务代理程序的信息，请使用此参数。可选。</dd>
</dl>

**`ba service-brokers`** 命令名较长，您还可以使用 **`ba sb`** 作为其别名。
{: tip}

### 添加服务代理程序
{: #cliaddservbro}

要添加服务代理程序，以便可以将定制服务添加到 {{site.data.keyword.Bluemix_notm}}“目录”，请使用以下命令：

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _brokerName_ |定制服务代理程序的名称。|
| _userName_ |有权访问服务代理程序的帐户的用户名。|  
| _password_ |有权访问服务代理程序的帐户的密码。|
| _brokerURL_ |服务代理程序的 URL。|
{: caption="表 20. cf ba add-service-broker 命令选项" caption-side="top"}

**`ba add-service-broker`** 命令名较长，您还可以使用 **`ba asb`** 作为其别名。
{: tip}

### 删除服务代理程序
{: #clidelservbro}

要删除服务代理程序，以从 {{site.data.keyword.Bluemix_notm}}“目录”中除去定制服务，请使用以下命令：

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">定制服务代理程序的名称或 GUID。</dd>
</dl>

**`ba delete-service-broker`** 命令名较长，您还可以使用 **`ba dsb`** 作为其别名。
{: tip}

### 更新服务代理程序
{: #cliupdservbro}

要更新服务代理程序，请使用以下命令：

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _brokerName_ |定制服务代理程序的名称。|
| _userName_ |有权访问服务代理程序的帐户的用户名。|  
| _password_ |有权访问服务代理程序的帐户的密码。|
| _brokerURL_ |服务代理程序的 URL。|
{: caption="表 21. cf ba update-service-broker 命令选项" caption-side="top"}

**`ba update-service-broker`** 命令名较长，您还可以使用 **`ba usb`** 作为其别名。
{: tip}

## 管理应用程序安全组
{: #admin_secgro}

要使用应用程序安全组 (ASG)，您必须是具有本地或专用环境完全访问权的管理员。对于命令的目标组织，环境的所有用户都可以列出可用的 ASG。但是，要创建、更新或绑定 ASG，您必须是 {{site.data.keyword.Bluemix_notm}} 环境的管理员。

ASG 的功能类似虚拟防火墙，可控制 {{site.data.keyword.cloud_notm}} 环境中应用程序的出站流量。每一个 ASG 都包含一个规则列表，允许与外部网络相互进行特定流量传输和通信。您可以将一个或多个 ASG 绑定到特定安全组集（例如，用于应用全局访问的组集），或者绑定到 {{site.data.keyword.Bluemix_notm}} 环境中某个组织内的空间。

{{site.data.keyword.Bluemix_notm}} 最初设置时其对外部网络的所有访问都受到限制。当您将两个 IBM 创建的安全组 `public_networks` 和 `dns` 绑定到缺省 Cloud Foundry 安全组集时，这两个安全组会启用对外部网络的全局访问。Cloud Foundry 中用于应用全局访问的两个安全组为 **Default Staging** 和 **Default Running** 组集。这两个组集会应用允许向所有正在运行的应用程序或所有正在编译打包的应用程序进行流量传输的规则。如果您不想绑定到这两个安全组集，那么您可以从 Cloud Foundry 组集取消绑定，然后将安全组绑定到特定空间。有关更多信息，请参阅[绑定应用程序安全组](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")。

如果取消**缺省编译打包**或**缺省运行**组集与 IBM 创建的两个安全组 `public_networks` 和 `dns` 之间的绑定，那么将禁用对外部网络的全局访问。请慎用取消绑定，应了解取消绑定对环境中正在运行和编译打包的应用程序的潜在影响。
{: important}

您可以使用以下命令来处理安全组，这些命令基于 Cloud Foundry V1.6。有关更多信息（包括必填和可选字段），请参阅有关[创建应用程序安全组](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标") 的 Cloud Foundry 信息。


### 列出安全组
{: #clilissecgro}

要列出所有安全组，请使用以下命令：

```
cf ba security-groups
```
{: codeblock}

要显示特定安全组的详细信息，请使用以下命令：

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba security-groups`** 命令名较长，您还可以使用 **`ba sg`** 作为其别名。
{: tip}

### 创建安全组
{: #clicreasecgro}

要创建安全组，请使用以下命令：
```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

您创建的每一个安全组其名称前都添加了 `adminconsole_` 前缀，用于与 IBM 创建的安全组加以区分。

|选项|描述
| 
| -------| ------------|
| _groupName_ |安全组的名称。|
| _filePath_ |规则文件的绝对或相对路径。|  
{: caption="表 22. cf ba create-security-group 命令选项" caption-side="top"}

**`ba create-security-group`** 命令名较长，您还可以使用 **`ba csg`** 作为其别名。
{: tip}

有关创建安全组和规则来定义传出流量的更多信息，请参阅[创建应用程序安全组](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")。

### 更新安全组
{: #cliupdsecgro}

要更新安全组，请使用以下命令：

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _groupName_ |安全组的名称。|
| _filePath_ |规则文件的绝对或相对路径。|  
{: caption="表 23. cf ba update-security-group 命令选项" caption-side="top"}

**`ba update-security-group`** 命令名较长，您还可以使用 **`ba usg`** 作为其别名。
{: tip}

### 删除安全组
{: #clidelsecgro}

要删除安全组，请使用以下命令：
```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba delete-security-group`** 命令名较长，您还可以使用 **`ba dsg`** 作为其别名。
{: tip}

### 绑定安全组
{: #clibindsecgro}

要绑定 Default Staging 安全组集，请使用以下命令：

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba bind-staging-security-group`** 命令名较长，您还可以使用 **`ba bssg`** 作为其别名。
{: tip}

要绑定 Default Running 安全组集，请使用以下命令：

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba bind-running-security-group`** 命令名较长，您还可以使用 **`ba brsg`** 作为其别名。
{: tip}

要将安全组绑定到空间，请使用以下命令：

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _groupName_ |安全组的名称。|
| _org_ |要将安全组绑定到的组织的名称。|
| _space_ |要将安全组绑定到的组织内空间的名称。|
{: caption="表 24. cf ba bind-security-group 命令选项" caption-side="top"}

**`ba bind-security-group`** 命令名较长，您还可以使用 **`ba bsg`** 作为其别名。
{: tip}

有关绑定安全组的更多信息，请参阅[绑定应用程序安全组 ](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")。

### 取消绑定安全组
{: #cliunbindsecgro}

如果取消“缺省编译打包”组集与 IBM 创建的两个安全组 `public_networks` 和 `dns` 之间的绑定，那么将禁用对外部网络的全局访问，因此必须慎用，还要了解这样对环境中所有正在编译打包的应用程序的可能影响。要取消绑定 Default Staging 安全组集，请使用以下命令：

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba unbind-staging-security-group`** 命令名较长，您还可以使用 **`ba ussg`** 作为其别名。
{: tip}

如果取消“缺省运行”组集与 IBM 创建的两个安全组 `public_networks` 和 `dns` 之间的绑定，那么将禁用对外部网络的全局访问，因此必须慎用，还要了解这样对环境中所有正在运行的应用程序的可能影响。要取消绑定 Default Running 安全组集，请使用以下命令：

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**`ba unbind-running-security-group`** 命令名较长，您还可以使用 **`ba brsg`** 作为其别名。
{: tip}

要将安全组取消绑定到空间，请使用以下命令：

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _groupName_ |安全组的名称。|
| _org_ |要取消绑定安全组的组织的名称。|
| _space_ |要取消绑定安全组的组织内空间的名称。|
{: caption="表 25. cf ba unbind-security-group 命令选项" caption-side="top"}

**`ba unbind-security-group`** 命令名较长，您还可以使用 **`ba usg`** 作为其别名。
{: tip}

有关取消绑定安全组的更多信息，请参阅[取消绑定应用程序安全组](https://docs.cloudfoundry.org/concepts/asg.html#unbinding-groups){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")。

## 管理 buildpack
{: #admin_buildpack}

### 列出 buildpack
{: #clilistbuildpack}

如果您有应用程序目录写许可权，那么可以列出 buildpack。要列出所有 buildpack 或查看特定 buildpack，请使用以下命令：

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">可选参数，用于指定要查看的特定 buildpack。</dd>
</dl>

**`ba buildpacks`** 命令名较长，您还可以使用 **`ba lb`** 作为其别名。
{: tip}

### 创建并上传 buildpack
{: #clicreupbuildpack}

如果您有应用程序目录写许可权，那么可以创建并上传 buildpack。可以上传文件类型为 `.zip` 的任何压缩文件。要上传 buildpack，请使用以下命令：

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _name_ |要上传的 buildpack 的名称。|
| _filePath_ |buildpack 压缩文件的路径。|
| _position_ |在 buildpack 自动检测期间检查 buildpack 的顺序。|
{: caption="表 26. cf ba create-buildpack 命令选项" caption-side="top"}

**`ba create-buildpack`** 命令名较长，您还可以使用 **`ba cb`** 作为其别名。
{: tip}

### 更新 buildpack
{: #cliupdabuildpack}

如果您有应用程序目录写许可权，那么可以更新现有 buildpack。要更新 buildpack，请使用以下命令：
```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

|选项|描述
| 
| -------| ------------|
| _name_ |要更新的 buildpack 的名称。|
| _position_ |在 buildpack 自动检测期间检查 buildpack 的顺序。|
| _enabled_ |指示 buildpack 是否用于编译打包。|
| _locked_ |指示 buildpack 是否已锁定以阻止更新。| 
{: caption="表 27. cf ba update-buildpack 命令选项" caption-side="top"}

**`ba update-buildpack`** 命令名较长，您还可以使用 **`ba ub`** 作为其别名。
{: tip}

### 删除 buildpack
{: #clidelbuildpack}

如果您有应用程序目录写许可权，那么可以删除现有 buildpack。要删除 buildpack，请使用以下命令：
```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">要删除的 buildpack 的名称。</dd>
</dl>

**`ba delete-buildpack`** 命令名较长，您还可以使用 **`ba db`** 作为其别名。
{: tip}
