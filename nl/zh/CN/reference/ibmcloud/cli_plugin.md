---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-04"

keywords: cli, add cli plug-in, remove cli plug-in, cli plug-in, ibmcloud plugin, repo-add, repo-remove, plugin uninstall, plugin update

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# 添加和除去 {{site.data.keyword.cloud_notm}} CLI 插件
{: #ibmcloud_commands_settings}

{{site.data.keyword.cloud}} 支持通过插件框架来扩展其功能。使用以下命令可管理 {{site.data.keyword.cloud_notm}} CLI 插件。
{: shortdesc}

## ibmcloud plugin repos
{: #ibmcloud_plugin_repos}

列出 {{site.data.keyword.cloud_notm}} CLI 中注册的所有插件存储库。
```
ibmcloud plugin repos
```
{: codeblock}

<strong>先决条件</strong>：无

## ibmcloud plugin repo-add
{: #ibmcloud_plugin_repo_add}

将新的插件存储库添加到 {{site.data.keyword.cloud_notm}} CLI 中。
```
ibmcloud plugin repo-add REPO_NAME REPO_URL
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>REPO_NAME（必需）</dt>
   <dd>要添加的存储库的名称。可以为每个存储库定义您自己的名称。</dd>
   <dt>REPO_URL（必需）</dt>
   <dd>要添加的存储库的 URL。存储库 URL 必须包含协议（例如，https://plugins.cloud.ibm.com，而不是 plugins.cloud.ibm.com）。https://plugins.cloud.ibm.com 是 {{site.data.keyword.cloud_notm}} CLI 的官方插件存储库。</dd>
    </dl>


<strong>示例</strong>：

将 {{site.data.keyword.cloud_notm}} CLI 的官方插件存储库添加为 `ibmcloud-repo`：
```
ibmcloud plugin repo-add ibmcloud-repo https://plugins.cloud.ibm.com
```
{: codeblock}

## ibmcloud plugin repo-remove
{: #ibmcloud_plugin_repo_remove}

从 {{site.data.keyword.cloud_notm}} CLI 中除去插件存储库。
```
ibmcloud plugin repo-remove REPO_NAME
```
{: codeblock}

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
   <dl>
   <dt>REPO_NAME（必需）</dt>
   <dd>要除去的存储库的名称。</dd>
   </dl>

<strong>示例</strong>：

从 {{site.data.keyword.cloud_notm}} CLI 中除去 `ibmcloud-repo` 存储库：
```
ibmcloud plugin repo-remove ibmcloud-repo
```
{: codeblock}

## ibmcloud plugin repo-plugins
{: #ibmcloud_plugin_repo_plugins}

列出所有添加的存储库或特定存储库中的所有可用插件。
```
ibmcloud plugin repo-plugins [-r REPO_NAME]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>-r <i>REPO_NAME</i>（可选）</dt>
   <dd>仅列出指定存储库中的插件。</dd>
   </dl>

<strong>示例</strong>：

列出所有添加的存储库中的所有插件：

```
ibmcloud plugin repo-plugins
```

列出 `ibmcloud-repo` 存储库中的所有插件：

```
ibmcloud plugin repo-plugins -r ibmcloud-repo
```

## ibmcloud plugin repo-plugin
{: #ibmcloud_plugin_repo_plugin}

显示存储库中插件的详细信息。

```
ibmcloud plugin repo-plugin PLUGIN_NAME [-r REPO_NAME]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>-r <i>REPO_NAME</i>（可选）</dt>
   <dd>存储库的名称。如果未指定存储库，此命令将使用缺省插件存储库。</dd>
   </dl>

<strong>示例</strong>：

列出存储库“sample-repo”中插件“IBM-Containers”的详细信息：

```
ibmcloud plugin repo-plugin IBM-Containers -r sample-repo
```

列出缺省存储库中插件“IBM-Containers”的详细信息

```
ibmcloud plugin repo-plugin IBM-Containers -r sample-repo
```

## ibmcloud plugin list
{: #ibmcloud_plugin_list}

列出 {{site.data.keyword.cloud_notm}} CLI 中的所有已安装插件。
```
ibmcloud plugin list
```
{: codeblock}

<strong>先决条件</strong>：无

## ibmcloud plugin show
{: #ibmcloud_plugin_show}

显示已安装插件的详细信息。
```
ibmcloud plugin show PLUGIN-NAME
```

<strong>先决条件</strong>：无

## ibmcloud plugin install
{: #ibmcloud_plugin_install}

从指定的路径或存储库将特定版本的插件安装到 {{site.data.keyword.cloud_notm}} CLI 中。
```
ibmcloud plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

```
ibmcloud plugin install LOCAL-PATH/TO/PLUGIN | URL [-f]
```

如果未指定存储库，此命令将使用缺省插件存储库“Bluemix”。如果未指定版本，此命令将选择可用的最新版本进行安装。

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME（必需）</dt>
   <dd>如果未指定 -r <i>REPO_NAME</i>，那么将从指定的本地路径或远程 URL 安装插件。</dd>
   <dt>-r <i>REPO_NAME</i>（可选）</dt>
   <dd>插件二进制文件所在的存储库的名称。如果未指定存储库，此命令将使用缺省插件存储库“Bluemix”。</dd>
   <dt>-v <i>VERSION</i>（可选）</dt>
   <dd>要安装的插件的版本。如果未提供，将安装插件的最新版本。此选项仅对从存储库安装插件有效。</dd>
   <dt>-f</dt>
   <dd>强制安装插件而不确认。</dd>
    </dl>


{{site.data.keyword.cloud_notm}} CLI 具有官方存储库名称 `Bluemix`。

<strong>示例</strong>：

从本地文件安装插件：

```
ibmcloud plugin install /downloads/new_plugin
```

从远程 URL 安装插件：

```
ibmcloud plugin install https://plugins.cloud.ibm.com/downloads/bluemix-plugins/new_plugin
```

从“Bluemix”存储库安装最新版本的“container-service”插件：

```
ibmcloud plugin install container-service -r Bluemix
```

或者简单地指定为：

```
ibmcloud plugin install container-service
```

从官方插件存储库安装版本“0.1.425”的“container-service”插件：

```
ibmcloud plugin install container-service -v 0.1.425
```

## ibmcloud plugin update
{: #ibmcloud_plugin_update}

从存储库升级插件。

```
ibmcloud plugin update [PLUGIN NAME] [-r REPO_NAME] [-v VERSION] [--all]
```

如果未指定存储库，此命令将使用缺省插件存储库“Bluemix”。如果未指定版本，此命令将选择可用的最新版本进行安装。

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
<dl>
 <dt>PLUGIN NAME</dt>
 <dd>要更新的插件的名称。如果未指定，此命令将检查安装的所有插件的升级。</dd>
 <dt>-r REPO_NAME</dt>
 <dd>插件二进制文件所在的存储库的名称。如果未指定，此命令将使用缺省插件存储库“Bluemix”。</dd>
 <dt>-v <i>VERSION</i>（可选）</dt>
 <dd>要更新到的插件版本。如果未提供，那么将插件更新到最新可用版本。</dd>
 <dt>--all</dt>
 <dd>更新所有可用的插件</dd>
</dl>

<strong>示例</strong>：

检查官方插件存储库“Bluemix”中所有可用的升级：

```
ibmcloud plugin update -r Bluemix
```

或者简单地指定为：

```
ibmcloud plugin update
```

将官方插件存储库中的插件“container-service”升级到最新版本：

```
ibmcloud plugin update container-service
```

将官方插件存储库中的插件“container-service”更新到版本“0.1.440”：

```
ibmcloud plugin update container-service -v 0.1.440
```

## ibmcloud plugin uninstall
{: #ibmcloud_plugin_uninstall}

从 {{site.data.keyword.cloud_notm}} CLI 中卸载指定的插件。

```
ibmcloud plugin uninstall PLUGIN_NAME
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>PLUGIN_NAME（必需）</dt>
   <dd>要卸载的插件的名称。</dd>
    </dl>

<strong>示例</strong>：

卸载先前安装的“container-service”插件：

```
ibmcloud plugin uninstall container-service
```
