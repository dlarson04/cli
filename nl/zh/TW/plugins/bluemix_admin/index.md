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

您可以搭配使用 Cloud Foundry 指令行介面 (CLI) 與 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式，來管理 {{site.data.keyword.cloud_notm}} Local 或 {{site.data.keyword.cloud_notm}} Dedicated 環境。例如，您可以從 LDAP 登錄新增使用者。

開始之前，請先安裝 Cloud Foundry CLI。「{{site.data.keyword.cloud_notm}} 管理 CLI」外掛程式需要 `cf` 6.11.2 版或更新版本。[下載 Cloud Foundry 指令行介面](https://github.com/cloudfoundry/cli/releases){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")

Cygwin 不支援 Cloud Foundry CLI。請在非 Cygwin 指令行視窗的指令行視窗中使用 Cloud Foundry CLI。

{{site.data.keyword.cloud_notm}} 管理 CLI 僅適用於 {{site.data.keyword.cloud_notm}} Local 及 {{site.data.keyword.cloud_notm}} Dedicated 環境。{{site.data.keyword.cloud_notm}} Public 則不予支援。
{: note}

## 新增 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式
{: #add-admin-cli}

在安裝 Cloud Foundry CLI 之後，您可以新增 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式。

如果您先前已安裝 {{site.data.keyword.cloud_notm}} 管理外掛程式，則可能需要解除安裝外掛程式、刪除儲存庫，然後重新安裝以取得最新更新項目。
{: tip}

完成下列步驟以新增儲存庫並安裝外掛程式：

1. 若要新增 {{site.data.keyword.cloud_notm}} 管理外掛程式儲存庫，請執行下列指令：
  ```
  cf add-plugin-repo IBMCloudAdmin https://<customer_console_endpoint>.bluemix.net/cli
  ```
  {: codeblock}

  您可以在管理主控台 CLI 頁面上找到與實際端點相同的指令：`https://<customer_console_endpoint>.bluemix.net/cli`。
  {: note}

2. 若要安裝 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式，請執行下列指令：
  ```
  cf install-plugin IBMCloudAdminCLI -r IBMCloudAdmin
  ```
  {: codeblock}

## 解除安裝 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式
{: #remove-admin-cli}

請完成下列步驟，以解除安裝外掛程式。 

1. 解除安裝外掛程式：
  ```
  cf uninstall-plugin IBMCloudAdminCLI
  ```
  {: codeblock}

2. 移除外掛程式儲存庫：
  ```
  cf remove-plugin-repo IBMCloudAdmin
  ```
  {: codeblock}

然後，您可以新增已更新的儲存庫並安裝最新的外掛程式。

## 使用 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式
{: #using-admin-cli}

您可以使用 {{site.data.keyword.cloud_notm}} 管理 CLI 外掛程式來新增或移除使用者、對組織指派或取消指派使用者，以及執行其他管理作業。

若要查看指令清單，請執行下列指令：

```
cf plugins
```
{: codeblock}

如需指令的其他說明，請使用 `-help` 選項。

### 連接並登入 {{site.data.keyword.cloud_notm}}
{: #connecting-ibm-cloud}

1. 若要連接至 {{site.data.keyword.cloud_notm}} API 端點，請執行下列指令：
  ```
  cf api api.us-south.cf.cloud.ibm.com
  ```
  {: codeblock}
  
  雖然舊式 `api.*.bluemix.net` Cloud Foundry API 端點仍然可用，但您可以更新 Script 及基礎架構自動化，以使用您地區的下列已更新 Cloud Foundry API 端點：

  * api.us-south.cf.cloud.ibm.com（之前是 api.ng.bluemix.net）
  * api.eu-gb.cf.cloud.ibm.com（之前是 api.eu-gb.bluemix.net）
  * api.us-east.cf.cloud.ibm.com（之前是 api.us-east.bluemix.net）
  * api.eu-de.cf.cloud.ibm.com（之前是 api.eu-de.bluemix.net）
  * api.au-syd.cf.cloud.ibm.com（之前是 api.au-syd.bluemix.net）

  您可以檢查管理主控台的「資源及資訊」頁面，以取得正確的 URL。URL 顯示在「API 資訊」區段的 **API URL** 欄位中。

2. 執行下列指令，以登入 {{site.data.keyword.cloud_notm}}：
  ```
  cf login
  ```
  {: codeblock}

## 管理使用者
{: #admin_users}

### 新增使用者
{: #admin_add_user}

若要從環境的使用者登錄中，將使用者新增至 {{site.data.keyword.cloud_notm}} 環境，請使用下列指令：
```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

若要將使用者新增至特定組織，您必須是具有 users.write（或「超級使用者」）許可權的管理者。如果您是組織管理員，則透過「超級使用者」執行 **`enable-managers-add-users`** 指令，您也可以具有將使用者新增至組織的功能。如需相關資訊，請參閱[允許管理員新增使用者](#clius_emau)。

| 選項 | 說明                                                  | 
| -------| ------------|
| _userName_ |LDAP 登錄中的使用者名稱。|
| _organization_ |要新增使用者之 {{site.data.keyword.cloud_notm}} 組織的名稱或 GUID。|
| _firstName_ |要新增至組織之使用者的名字。| 
| _lastName_ |要新增至組織之使用者的姓氏。| 
{: caption="表 1. cf ba add-user 指令選項" caption-side="top"}

您也可以使用 **`ba au`** 作為 **`ba add-user`** 這個較長指令名稱的別名。
{: tip}

### 從 {{site.data.keyword.Bluemix_dedicated_notm}} 邀請使用者
{: #admin_dedicated_invite_public}

每一個 {{site.data.keyword.Bluemix_dedicated_notm}} 環境都具有 {{site.data.keyword.cloud_notm}} 中由客戶擁有的公用公司帳戶。若要讓 Dedicated 環境中的使用者利用 {{site.data.keyword.containershort}} 來建立叢集，管理者必須將使用者新增至這個公用公司帳戶。將使用者新增至公用公司帳戶之後，會將其 Dedicated 及公用帳戶鏈結在一起。使用者接著可以使用其 IBM ID 同時登入 Dedicated 及公用，而且可以從 Dedicated 介面建立公用帳戶中的資源。如需相關資訊，請參閱[在 Dedicated 上設定 IBM Cloud Container Service](/docs/containers?topic=containers-dedicated#dedicated_setup)。若要邀請 Dedicated 使用者加入公用帳戶，請執行下列指令：
```
cf ba invite-users-to-public -userid=<user_email> -organization=<dedicated_org_id> -apikey=<public_api_key> -public_org_id=<public_org_id>
```
{: pre}

若要將 Dedicated 環境使用者新增至 {{site.data.keyword.cloud_notm}} Public 帳戶，您必須是 Dedicated 帳戶的管理者。

| 選項 | 說明                                                  | 
| -------| ------------|
| -userid |如果您要邀請單一使用者，則為使用者的電子郵件。|
| -organization |如果您要邀請 Dedicated 帳戶組織中目前的所有使用者，則為 Dedicated 帳戶組織 ID。|
| -apikey |用於邀請使用者加入公用帳戶的 API 金鑰。這必須由公用帳戶的管理者產生。| 
| -public_org_id |您要邀請使用者加入的公用帳戶組織的 ID。| 
{: caption="表 2. cf ba invite-users-to-public 指令選項" caption-side="top"}

### 列出從 {{site.data.keyword.Bluemix_dedicated_notm}} 邀請的使用者
{: #admin_dedicated_list}

如果您已使用 [**`invite-users-to-public`** 指令](#admin_dedicated_invite_public)來邀請 Dedicated 環境使用者加入您的 {{site.data.keyword.Bluemix_notm}} 帳戶，則可以列出您帳戶中的使用者來查看其邀請狀態。具有現有 IBM ID 的受邀使用者將具有 ACTIVE 狀態。根據是否已接受邀請加入帳戶，沒有現有 IBM ID 的受邀使用者將具有 PENDING 或 ACTIVE 狀態。若要列出您 {{site.data.keyword.Bluemix_notm}} 帳戶中的使用者，請執行下列指令：

```
cf ba invite-users-status -apikey=<public_api_key>
```
{: pre}

若要將 Dedicated 環境使用者新增至 {{site.data.keyword.Bluemix_notm}} Public 帳戶，您必須是 Dedicated 帳戶的管理者。

<dl class="parml">
<dt class="pt dlterm">&lt;public_api_key&gt;</dt>
<dd class="pd">用來邀請使用者加入帳戶的 API 金鑰。這必須由公用帳戶的管理者產生。</dd>
</dl>

<!-- staging-only commands start. Live for interconnect -->

### 搜尋使用者
{: #admin_search_user}

若要搜尋使用者，請搭配使用下列指令與選用性的搜尋過濾器參數（name、permission、organization 及 role）：

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| -name |使用者的名稱。|
| -permission |指派給使用者的許可權。可用的許可權為 admin（或 superuser）、login（或 basic）、catalog.read、catalog.write、reports.read、reports.write、users.read 或 users.write。您不能在相同的查詢中搭配使用此參數與 organization 參數。|
| -organization |使用者所屬的組織名稱。您不能在相同的查詢中搭配使用此參數與 permission 參數。| 
| -role |指派給使用者的組織角色。可用的角色為 auditors、managers 及 billing_managers。您必須使用此參數來指定組織。| 
{: caption="表 3. cf ba search-users 指令選項" caption-side="top"}

您也可以使用 **`ba su`** 作為 **`ba search-users`** 這個較長指令名稱的別名。
{: tip}

### 設定使用者的許可權
{: #admin_setperm_user}

若要設定所指定使用者的許可權，請使用下列指令：
```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _userName_ |使用者的名稱。|
| _permission_ |指派給使用者的許可權。可用的許可權為 admin（或 superuser）、login（或 basic）、catalog.read、catalog.write、reports.read、reports.write、users.read 或 users.write。您不能在相同的查詢中搭配使用此參數與 organization 參數。|
| _access_ |對於型錄、報告或使用者許可權，您還必須將存取層次設定為 `read` 或 `write`。|  
{: caption="表 4. cf ba set-permissions 指令選項" caption-side="top"}

一次可以設定一個許可權。

您也可以使用 **`ba sp`** 作為 **`ba set-permissions`** 這個較長指令名稱的別名。
{: tip}

<!-- staging-only commands end -->

### 移除使用者
{: #admin_remov_user}

若要從 {{site.data.keyword.Bluemix_notm}} 環境移除使用者，請使用下列指令：

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>

</dl>

您也可以使用 **`ba ru`** 作為 **`ba remove-user`** 這個較長指令名稱的別名。
{: tip}

### 允許管理員新增使用者
{: #clius_emau}

如果您在 {{site.data.keyword.Bluemix_notm}} 環境中具有「超級使用者」許可權，則可以允許組織管理員將使用者新增至他們所管理的組織。若要讓管理員新增使用者，請使用下列指令：

```
cf ba enable-managers-add-users
```
{: codeblock}

您也可以使用 **`ba emau`** 作為 **`ba enable-managers-add-users`** 這個較長指令名稱的別名。
{: tip}

### 禁止管理員新增使用者
{: #clius_dmau}

如果已在您的 {{site.data.keyword.Bluemix_notm}} 環境中使用 **`enable-managers-add-users`** 指令，讓組織管理員能將使用者新增至他們所管理的組織，而且您具有「超級使用者」許可權，則可以移除此設定。若要停止讓管理員新增使用者，請使用下列指令：

```
cf ba disable-managers-add-users
```
{: codeblock}

您也可以使用 **`ba dmau`** 指令作為 **`ba disable-managers-add-users`** 這個較長指令名稱的別名。
{: tip}

## 管理組織
{: #admin_orgs}

### 新增組織
{: #admin_add_org}

若要新增組織，請使用下列指令：

```
cf ba create-org <organization> <manager>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要新增之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID|
| _manager_ |組織管理員的使用者名稱。|
{: caption="表 5. cf ba create-org 指令選項" caption-side="top"}

您也可以使用 **`ba co`** 作為 **`ba create-org`** 這個較長指令名稱的別名。
{: tip}

### 刪除組織
{: #admin_delete_org}

若要刪除組織，請使用下列指令：

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要刪除之 {{site.data.keyword.cloud_notm}} 組織的名稱或 GUID。</dd>
</dl>

您也可以使用 **`ba do`** 作為 **`ba delete-org`** 這個較長指令名稱的別名。
{: tip}

### 將使用者指派至組織
{: #admin_ass_user_org}

若要將 {{site.data.keyword.cloud_notm}} 環境中的使用者指派給特定組織，請使用下列指令：

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _userName_ |使用者的名稱。|
| _organization_ |要指派使用者之 {{site.data.keyword.cloud_notm}} 組織的名稱或 GUID。|
| _role_ |使用者的角色。有效值為 `OrgManager`、`BillingManager`、`OrgAuditor`。請參閱[角色](/docs/iam?topic=iam-userroles#userroles)以取得角色說明。|  
{: caption="表 6. cf ba set-org 指令選項" caption-side="top"}

您也可以使用 **`ba so`** 作為 **`ba set-org`** 這個較長指令名稱的別名。
{: tip}

### 從組織取消指派使用者
{: #admin_unass_user_org}

若要從特定組織取消指派 {{site.data.keyword.cloud_notm}} 環境中的使用者，請使用下列指令：

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _userName_ |使用者的名稱。|
| _organization_ | {{site.data.keyword.cloud_notm}} 組織的名稱或 GUID。|
| _role_ |使用者的角色。有效值為 `OrgManager`、`BillingManager`、`OrgAuditor`。請參閱[角色](/docs/iam?topic=iam-userroles#userroles)以取得角色說明。|  
{: caption="表 7. cf ba unset-org 指令選項" caption-side="top"}

您也可以使用 **`ba uo`** 作為 **`ba unset-org`** 這個較長指令名稱的別名。
{: tip}

### 設定組織的配額
{: #admin_set_org_quota}

若要設定特定組織的用量配額，請使用下列指令：

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要設定其配額之 {{site.data.keyword.cloud_notm}} 組織的名稱或 GUID。|
| _plan_ |組織的配額方案。|  
{: caption="表 8. cf ba set-quota 指令選項" caption-side="top"}

您也可以使用 **`ba sq`** 作為 **`ba set-quota`** 這個較長指令名稱的別名。
{: tip}


### 尋找組織的容器配額
{: #admin_find_containquotas}

若要尋找組織的容器配額，請使用下列指令：

```
cf ibmcloud-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">IBM Cloud 中組織的名稱或 ID。這是必要參數。</dd>
</dl>

您也可以使用 **`ba cq`** 作為 **`ibmcloud-admin containers-quota`** 這個較長指令名稱的別名。
{: tip}

### 設定組織的容器配額
{: #admin_set_containquotas}

若要設定組織中容器的配額，請使用下列指令，並至少包括其中一個選項：

```
cf ibmcloud-admin set-containers-quota <organization> <options>
```
{: codeblock}

您可以包括多個選項，但必須至少包括一個選項。
{: note}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要設定其配額之 {{site.data.keyword.cloud_notm}} 組織的名稱或 ID。|
| _options_ |選項為 **`floating-ips-max value`**（簡稱 **`fim`**）、**`floating-ips-space-default value`**（簡稱 **`fisd`**）、**`memory-max value`**（簡稱 **`mm`**）、**`memory-space-default value`**（簡稱 **`msd`**）或 **`image-limit value`**（簡稱 **`il`**）。此值必須是整數。|  
{: caption="表 9. cf ibmcloud-admin set-containers-quota 指令選項" caption-side="top"}

您可以選擇提供一個檔案，其中包含有效 JSON 物件中的特定配置參數。如果使用 **`-file`** 選項，則會優先處理此選項，並忽略其他選項。若要提供檔案而非設定選項，請使用下列指令：

```
cf ibmcloud-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

JSON 檔案應該具有下列範例中所顯示的格式：

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

您也可以使用 **`ba scq`** 作為 **`ibmcloud-admin set-containers-quota`** 這個較長指令名稱的別名。
{: tip}

## 管理空間
{: #admin_spaces}

### 將空間新增至組織

若要在組織中新增空間，請使用下列指令：

```
cf ibmcloud-admin create-space <organization> <space_name>
```

{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要在其中新增空間之組織的名稱或 GUID。|
| _spaceName_ |您要新增至組織之空間的名稱。|  
{: caption="表 10. cf ibmcloud-admin create-space 指令選項" caption-side="top"}

您也可以使用 **`ba cs`** 作為 **`ba create-space`** 這個較長指令名稱的別名。
{: tip}

### 刪除組織中的空間

若要移除組織中的空間，請使用下列指令：

```
cf ibmcloud-admin delete-space <organization> <space_name>
```

{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要從中移除空間之組織的名稱或 GUID。|
| _spaceName_ |您要從組織中移除之空間的名稱。|  
{: caption="表 11. cf ibmcloud-admin delete-space 指令選項" caption-side="top"}

您也可以使用 **`ba cs`** 作為 **`ba delete-space`** 這個較長指令名稱的別名。
{: tip}

### 在空間中新增具有某角色的使用者

若要在空間中建立具有指定角色的使用者，請使用下列指令：

```
cf ibmcloud-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |要在其中新增使用者之組織的名稱或 GUID。|
| _spaceName_ |要在其中新增使用者之空間的名稱。|
| _userName_ |使用者的名稱。|
| _role_ |使用者的角色。有效值為 `Manager`、`Developer` 或 `Auditor`。|  
{: caption="表 12. cf ibmcloud-admin set-space 指令選項" caption-side="top"}

您也可以使用 **`ba ss`** 作為 **`ba set-space`** 這個較長指令名稱的別名。
{: tip}


### 移除空間中的使用者角色

若要移除空間中的使用者角色，請使用下列指令：

```
cf ibmcloud-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _organization_ |使用者所屬組織的名稱或 GUID。|
| _spaceName_ |使用者所屬空間的名稱。|
| _userName_ |使用者的名稱。|
| _role_ |使用者的角色。有效值為 `Manager`、`Developer` 或 `Auditor`。|  
{: caption="表 13. cf ibmcloud-admin unset-space 指令選項" caption-side="top"}

您也可以使用 **`ba us`** 作為 **`ba unset-space`** 這個較長指令名稱的別名。
{: tip}

## 管理型錄
{: #admin_catalog}

### 針對所有組織啟用服務
{: #admin_ena_service_org}

若要啟用服務，以便針對所有組織顯示在 {{site.data.keyword.cloud_notm}} 型錄中，請使用下列指令：

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要停用之服務方案的名稱或 GUID。如果輸入非唯一的服務方案名稱（例如 "Standard" 或 "Basic"），系統會提示您可從中選擇的服務方案。若要識別服務方案名稱，請從首頁選取服務種類，然後選取**新增**，以檢視該種類的服務。請按一下服務名稱，以開啟詳細資料視圖，然後您可以檢視該服務可用的服務方案名稱。</dd>
</dl>

您也可以使用 **`ba esp`** 作為 **`ba enable-service-plan`** 這個較長指令名稱的別名。
{: tip}

### 針對所有組織停用服務
{: #admin_dis_service_org}

若要讓所有組織在 {{site.data.keyword.Bluemix_notm}} 型錄中看不見服務，請使用下列指令：

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要停用之服務方案的名稱或 GUID。如果輸入非唯一的服務方案名稱（例如 "Standard" 或 "Basic"），系統會提示您可從中選擇的服務方案。若要識別服務方案名稱，請從首頁選取服務種類，然後選取**新增**，以檢視該種類的服務。請按一下服務名稱，以開啟詳細資料視圖，然後您可以檢視該服務可用的服務方案名稱。</dd>
</dl>

您也可以使用 **`ba dsp`** 作為 **`ba disable-service-plan`** 這個較長指令名稱的別名。
{: tip}

### 新增組織的服務可見性
{: #admin_addvis_service_org}

您可以從組織清單中新增可在 {{site.data.keyword.Bluemix_notm}} 型錄中看見特定服務的組織。若要容許組織在型錄中檢視特定服務，請使用下列指令：

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _planIdentifier_ |您要停用之服務方案的名稱或 GUID。如果輸入非唯一的服務方案名稱（例如 "Standard" 或 "Basic"），系統會提示您可從中選擇的服務方案。若要識別服務方案名稱，請從首頁選取服務種類，然後選取**新增**，以檢視該種類的服務。請按一下服務名稱，以開啟詳細資料視圖，然後您可以檢視該服務可用的服務方案名稱。|
| _organization_ |要新增至服務可見性清單之組織的名稱或 GUID。|  
{: caption="表 14. cf ba add-service-plan-visibility 指令選項" caption-side="top"}

您也可以使用 **`ba aspv`** 作為 **`ba add-service-plan-visibility`** 這個較長指令名稱的別名。
{: tip}

### 移除組織的服務可見性
{: #admin_remvis_service_org}

您可以從可在 {{site.data.keyword.Bluemix_notm}} 型錄看見特定服務的組織清單，移除某個組織。若要針對組織移除型錄中的服務可見性，請使用下列指令：

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _planIdentifier_ |您要停用之服務方案的名稱或 GUID。如果輸入非唯一的服務方案名稱（例如 "Standard" 或 "Basic"），系統會提示您可從中選擇的服務方案。若要識別服務方案名稱，請從首頁選取服務種類，然後選取**新增**，以檢視該種類的服務。請按一下服務名稱，以開啟詳細資料視圖，然後您可以檢視該服務可用的服務方案名稱。|
| _organization_ |要從服務可見性清單中移除之組織的名稱或 GUID。|  
{: caption="表 15. cf ba remove-service-plan-visibility 指令選項" caption-side="top"}

您也可以使用 **`ba rspv`** 作為 **`ba remove-service-plan-visibility`** 這個較長指令名稱的別名。
{: tip}

### 編輯組織的服務可見性
{: #admin_editvis_service_org}

您可以編輯及取代特定組織可在 {{site.data.keyword.Bluemix_notm}} 型錄中看到的服務清單。若要取代一個組織或多個組織的所有現有可見服務，請使用下列指令：

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

這個指令會將所指定組織的現有可見服務取代為您在指令中指定的服務。

| 選項 | 說明                                                  | 
| -------| ------------|
| _planIdentifier_ |您要停用之服務方案的名稱或 GUID。如果輸入非唯一的服務方案名稱（例如 "Standard" 或 "Basic"），系統會提示您可從中選擇的服務方案。若要識別服務方案名稱，請從首頁選取服務種類，然後選取**新增**，以檢視該種類的服務。請按一下服務名稱，以開啟詳細資料視圖，然後您可以檢視該服務可用的服務方案名稱。|
| _organization_ |要在其中新增可見性之組織的名稱或 GUID。您可以在指令中輸入其他組織名稱或 GUID，針對多個組織啟用服務的可見性。|  
{: caption="表 16. cf ba edit-service-plan-visibilities 指令選項" caption-side="top"}

您也可以使用 **`ba espv`** 作為 **`ba edit-service-plan-visibility`** 這個較長指令名稱的別名。
{: tip}

## 管理報告
{: #admin_add_report}

### 新增報告
{: #admin_adding_report}

若要新增安全報告，請使用下列指令：

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

如果您有報告許可權的寫入權，則可以建立新的種類，並以使用者可以接受的任何格式來新增報告。請在 **`category`** 參數中輸入新的種類名稱，或是將您的新報告新增至現有種類。

| 選項 | 說明                                                  | 
| -------| ------------|
| _category_ |報告的種類。如果名稱中有空格，請使用引號。|
| _date_ |報告日期，格式為 YYYYMMDD。|  
| _filePath_ |要上傳之報告 PDF、文字檔或日誌檔的路徑。|
| _RTF_ |用來包含 PDF 之「Rich Text 格式 (RTF)」版本的選項。只有在您包含報告 PDF 的路徑時，此選項才適用。RTF 版本用於編製索引及進行搜尋。|
{: caption="表 17. cf ba add-report 指令選項" caption-side="top"}

您也可以使用 **`ba ar`** 作為 **`ba add-report`** 這個較長指令名稱的別名。
{: tip}

### 刪除報告
{: #admin_del_report}

若要刪除安全報告，請使用下列指令：

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _category_ |報告的種類。如果名稱中有空格，請使用引號。|
| _date_ |報告日期，格式為 YYYYMMDD。|  
| _name_ |報告的名稱。|
{: caption="表 18. cf ba delete-report 指令選項" caption-side="top"}

您也可以使用 **`ba dr`** 作為 **`ba delete-report`** 這個較長指令名稱的別名。
{: tip}

### 擷取報告
{: #admin_retr_report}

若要擷取安全報告，請使用下列指令：

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">報告的檔名。如果名稱中有空格，請使用引號括住該名稱。</dd>
</dl>

您也可以使用 **`ba rr`** 作為 **`ba retrieve-report`** 這個較長指令名稱的別名。
{: tip}

## 檢視資源度量值資訊
{: #cliresourceusage}

您可以檢視資源度量值資訊（包括記憶體用量、磁碟用量及 CPU 用量）。您可以查看可用的實體資源與保留資源的摘要，以及實體資源與保留資源用量的摘要。您也可以查看 Droplet Execution Agent (DEA) 及 Cell（Diego 架構）用量資料。若要檢視資源度量值資訊，請使用下列指令：

```
cf ba resource-metrics
```

您也可以使用 **`ba rsm`** 作為 **`ba resource-metrics`** 這個較長指令名稱的別名。
{: tip}

## 檢視資源度量值歷程
{: #cliresourceusagehistory}

您可以擷取記憶體及磁碟用量的資源度量值歷程。傳回的度量值包括已使用的資源量佔可用總計的比例（針對實體以及保留資源）。記憶體及磁碟用量歷程資料可以每小時、每日或每月顯示。您可以指定開始及結束日期，以在特定日期範圍內擷取資料。未指定任何日期時，預設歷程資料是最新 48 小時的每小時記憶體資料。資料以遞減順序顯示，最近的日期最先顯示。若要檢視資源度量值歷程資訊，請使用下列指令：

```
cf ba resource-metrics-history <hourly|daily|monthly>  <memory|disk >  <start|end>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| --hourly | View the historical data for the last 48 hours. This is the default value. |
| --daily | View the historical data daily average for the last 30 days. |  
| --monthly | View the historical data monthly average for the last 6 months. |
| --memory | View the used and total reserved and physical memory. |
| --disk | View the used and total reserved and physical disk. | 
| --start | Specify a start date for daily or monthly in the format of mm-dd-yyyy, or start date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
| --end | Specify an end date for daily or monthly in the format of mm-dd-yyyy, or end date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
{: caption="表 19. cf ba resource-metrics-history 指令選項" caption-side="top"}

**範例**

```
cf ibmcloud-admin resource-metrics-history
cf ibmcloud-admin resource-metrics-history --daily --disk --start=07-04-2017
cf ibmcloud-admin resource-metrics-history --monthly --memory
cf ibmcloud-admin resource-metrics-history --hourly --start="06-01-2017 00:00:00 EDT" --end="06-30-2017 23:59:00 EDT
```
{: codeblock}

您可以使用下列指令來檢視先前的指令參數及範例清單：

```
cf ba resource-metrics-history -help
```

您也可以使用 **`ba rsmh`** 作為 **`ba resource-metrics-history`** 這個較長指令名稱的別名。
{: tip}

## 管理服務分配管理系統
{: #admin_servbro}

### 列出服務分配管理系統。
{: #clilistservbro}

若要列出服務分配管理系統，請使用下列指令：

```
cf ba service-brokers <broker_name>
```
{: codeblock}

若要列出所有服務分配管理系統，請輸入不含 **`broker_name`** 參數的指令。

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">自訂服務分配管理系統的名稱。如果您要取得特定服務分配管理系統的資訊，請使用此參數。選用。</dd>
</dl>

您也可以使用 **`ba sb`** 作為 **`ba service-brokers`** 這個較長指令名稱的別名。
{: tip}

### 新增服務分配管理系統
{: #cliaddservbro}

若要新增服務分配管理系統，以便您將自訂服務新增至 {{site.data.keyword.Bluemix_notm}} 型錄，請使用下列指令：

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _brokerName_ |自訂服務分配管理系統的名稱。|
| _userName_ |可存取服務分配管理系統之帳戶的使用者名稱。|  
| _password_ |可存取服務分配管理系統之帳戶的密碼。|
| _brokerURL_ |服務分配管理系統的 URL。|
{: caption="表 20. cf ba add-service-broker 指令選項" caption-side="top"}

您也可以使用 **`ba asb`** 作為 **`ba add-service-broker`** 這個較長指令名稱的別名。
{: tip}

### 刪除服務分配管理系統
{: #clidelservbro}

若要刪除服務分配管理系統，以從 {{site.data.keyword.Bluemix_notm}} 型錄移除自訂服務，請使用下列指令：

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">自訂服務分配管理系統的名稱或 GUID。</dd>
</dl>

您也可以使用 **`ba dsb`** 作為 **`ba delete-service-broker`** 這個較長指令名稱的別名。
{: tip}

### 更新服務分配管理系統
{: #cliupdservbro}

若要更新服務分配管理系統，請使用下列指令：

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _brokerName_ |自訂服務分配管理系統的名稱。|
| _userName_ |可存取服務分配管理系統之帳戶的使用者名稱。|  
| _password_ |可存取服務分配管理系統之帳戶的密碼。|
| _brokerURL_ |服務分配管理系統的 URL。|
{: caption="表 21. cf ba update-service-broker 指令選項" caption-side="top"}

您也可以使用 **`ba usb`** 作為 **`ba update-service-broker`** 這個較長指令名稱的別名。
{: tip}

## 管理應用程式安全群組
{: #admin_secgro}

若要使用應用程式安全群組 (ASG)，您必須是本端或專用環境中具有完整存取權的管理者。環境的所有使用者都可以列出可供指令設為目標之組織使用的 ASG。不過，若要建立、更新或連結 ASG，您必須是 {{site.data.keyword.Bluemix_notm}} 環境的管理者。

ASG 是當作虛擬防火牆使用，可控制 {{site.data.keyword.cloud_notm}} 環境中應用程式的出埠資料流量。每一個 ASG 都包含一份規則清單，可容許與外部網路之間的特定資料流量和通訊。您可以將一個以上的 ASG 連結至特定安全群組集（例如，用於套用廣域存取權的群組集），也可以連結至 {{site.data.keyword.Bluemix_notm}} 環境中組織內的空間。

{{site.data.keyword.Bluemix_notm}} 一開始是設定成限制外部網路的所有存取權。將 IBM 所建立的兩個安全群組（`public_networks` 及 `dns`）連結至預設 Cloud Foundry 安全群組集時，這些群組就會啟用外部網路的廣域存取權。Cloud Foundry 中用來套用廣域存取權的兩個安全群組集是 **Default Staging** 及 **Default Running** 群組集。這些群組集會套用規則，以容許對所有執行中應用程式或所有編譯打包中應用程式的資料流量。如果您不想要連結至這兩個安全群組集，則可以取消與 Cloud Foundry 群組集的連結，然後將安全群組連結至特定空間。如需相關資訊，請參閱[連結應用程式安全群組](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")。

取消連結 **Default Staging** 或 **Default Running** 群組集與兩個 IBM 建立的安全群組 `public_networks` 及 `dns`，會停用對外部網路的廣域存取。請小心使用取消連結，並瞭解它對您環境內執行中及編譯打包中的應用程式可能造成的影響。
{: important}

下列可讓您使用安全群組的指令是根據 Cloud Foundry 1.6 版。如需相關資訊（包括必要及選用欄位），請參閱有關[建立應用程式安全群組](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示") 的 Cloud Foundry 資訊。


### 列出安全群組
{: #clilissecgro}

若要列出所有安全群組，請使用下列指令：

```
cf ba security-groups
```
{: codeblock}

若要顯示特定安全群組的詳細資料，請使用下列指令：

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全群組的名稱</dd>
</dl>

您也可以使用 **`ba sg`** 作為 **`ba security-groups`** 這個較長指令名稱的別名。
{: tip}

### 建立安全群組
{: #clicreasecgro}

若要建立安全群組，請使用下列指令：
```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

您建立的每一個安全群組的名稱前面都會加上 `adminconsole_` 字首，以與 IBM 所建立的安全群組進行區別。

| 選項 | 說明                                                  | 
| -------| ------------|
| _groupName_ |安全群組的名稱。|
| _filePath_ |規則檔的絕對或相對路徑。|  
{: caption="表 22. cf ba create-security-group 指令選項" caption-side="top"}

您也可以使用 **`ba csg`** 作為 **`ba create-security-group`** 這個較長指令名稱的別名。
{: tip}

如需建立安全群組以及定義送出資料流量之規則的相關資訊，請參閱[建立應用程式安全群組](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")。

### 更新安全群組
{: #cliupdsecgro}

若要更新安全群組，請使用下列指令：

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _groupName_ |安全群組的名稱。|
| _filePath_ |規則檔的絕對或相對路徑。|  
{: caption="表 23. cf ba update-security-group 指令選項" caption-side="top"}

您也可以使用 **`ba usg`** 作為 **`ba update-security-group`** 這個較長指令名稱的別名。
{: tip}

### 刪除安全群組
{: #clidelsecgro}

若要刪除安全群組，請使用下列指令：
```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">您的安全群組名稱</dd>
</dl>

您也可以使用 **`ba dsg`** 作為 **`ba delete-security-group`** 這個較長指令名稱的別名。
{: tip}

### 連結安全群組
{: #clibindsecgro}

若要連結至 Default Staging 安全群組集，請使用下列指令：

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">您的安全群組名稱</dd>
</dl>

您也可以使用 **`ba bssg`** 作為 **`ba bind-staging-security-group`** 這個較長指令名稱的別名。
{: tip}

若要連結至 Default Running 安全群組集，請使用下列指令：

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">您的安全群組名稱</dd>
</dl>

您也可以使用 **`ba brsg`** 作為 **`ba bind-running-security-group`** 這個較長指令名稱的別名。
{: tip}

若要將安全群組連結至空間，請使用下列指令：

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _groupName_ |安全群組的名稱。|
| _org_ |要與安全群組連結的組織名稱。|
| _space_ |組織內要與安全群組連結的空間名稱。|
{: caption="表 24. cf ba bind-security-group 指令選項" caption-side="top"}

您也可以使用 **`ba bsg`** 作為 **`ba bind-security-group`** 這個較長指令名稱的別名。
{: tip}

如需連結安全群組的相關資訊，請參閱[連結應用程式安全群組](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")。

### 取消連結安全群組
{: #cliunbindsecgro}

取消連結 Default Staging 群組集與兩個 IBM 建立的安全群組 `public_networks` 及 `dns`，會停用對外部網路的廣域存取，必須小心使用取消連結，並瞭解它對您環境內所有編譯打包中的應用程式造成的結果。若要從 Default Staging 安全群組集取消連結，請使用下列指令：

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">您的安全群組名稱</dd>
</dl>

您也可以使用 **`ba ussg`** 作為 **`ba unbind-staging-security-group`** 這個較長指令名稱的別名。
{: tip}

取消連結 Default Running 群組集與兩個 IBM 建立的安全群組 `public_networks` 及 `dns`，會停用對外部網路的廣域存取，必須小心使用取消連結，並瞭解它對您環境內所有執行中的應用程式造成的結果。若要從 Default Running 安全群組集取消連結，請使用下列指令：

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">您的安全群組名稱</dd>
</dl>

您也可以使用 **`ba brsg`** 作為 **`ba unbind-running-security-group`** 這個較長指令名稱的別名。
{: tip}

若要取消安全群組與空間的連結，請使用下列指令：

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _groupName_ |安全群組的名稱。|
| _org_ |要與安全群組取消連結的組織名稱。|
| _space_ |組織內要與安全群組取消連結的空間名稱。|
{: caption="表 25. cf ba unbind-security-group 指令選項" caption-side="top"}

您也可以使用 **`ba usg`** 作為 **`ba unbind-security-group`** 這個較長指令名稱的別名。
{: tip}

如需取消連結安全群組的相關資訊，請參閱[取消連結應用程式安全群組](https://docs.cloudfoundry.org/concepts/asg.html#unbinding-groups){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")。

## 管理建置套件
{: #admin_buildpack}

### 列出建置套件
{: #clilistbuildpack}

如果您具有應用程式型錄寫入權，則可以列出建置套件。若要列出所有建置套件，或檢視特定建置套件，請使用下列指令：

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">選用性參數，可指定要檢視的特定建置套件。</dd>
</dl>

您也可以使用 **`ba lb`** 作為 **`ba buildpacks`** 這個較長指令名稱的別名。
{: tip}

### 建立及上傳建置套件
{: #clicreupbuildpack}

如果您具有應用程式型錄寫入權，則可以建立及上傳建置套件。您可以上傳任何檔案類型為 `.zip` 的壓縮檔。若要上傳建置套件，請使用下列指令：

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _name_ |要上傳之建置套件的名稱。|
| _filePath_ |建置套件壓縮檔的路徑。|
| _position_ |在建置套件自動偵測期間檢查建置套件的順序。|
{: caption="表 26. cf ba create-buildpack 指令選項" caption-side="top"}

您也可以使用 **`ba cb`** 作為 **`ba create-buildpack`** 這個較長指令名稱的別名。
{: tip}

### 更新建置套件
{: #cliupdabuildpack}

如果您具有應用程式型錄寫入權，則可以更新現有建置套件。若要更新建置套件，請使用下列指令：
```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

| 選項 | 說明                                                  | 
| -------| ------------|
| _name_ |要更新之建置套件的名稱。|
| _position_ |在建置套件自動偵測期間檢查建置套件的順序。|
| _enabled_ |指出是否將建置套件用於編譯打包。|
| _locked_ |指出是否鎖定建置套件，以防止更新。| 
{: caption="表 27. cf ba update-buildpack 指令選項" caption-side="top"}

您也可以使用 **`ba ub`** 作為 **`ba update-buildpack`** 這個較長指令名稱的別名。
{: tip}

### 刪除建置套件
{: #clidelbuildpack}

如果您具有應用程式型錄寫入權，則可以刪除現有建置套件。若要刪除建置套件，請使用下列指令：
```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">要刪除之建置套件的名稱。</dd>
</dl>

您也可以使用 **`ba db`** 作為 **`ba delete-buildpack`** 這個較長指令名稱的別名。
{: tip}
