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

# Adding and removing {{site.data.keyword.cloud_notm}} CLI plug-ins
{: #ibmcloud_commands_settings}

{{site.data.keyword.cloud}} supports a plug-in framework to extend its capability. Use the following commands to manage the {{site.data.keyword.cloud_notm}} CLI plug-ins.
{: shortdesc}

## ibmcloud plugin repos
{: #ibmcloud_plugin_repos}

List all plug-in repositories that are registered in {{site.data.keyword.cloud_notm}} CLI.
```
ibmcloud plugin repos
```
{: codeblock}

<strong>Prerequisites</strong>:  None

## ibmcloud plugin repo-add
{: #ibmcloud_plugin_repo_add}

Add a new plug-in repository to {{site.data.keyword.cloud_notm}} CLI.
```
ibmcloud plugin repo-add REPO_NAME REPO_URL
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>REPO_NAME (required)</dt>
   <dd>The name of the repository to be added. You can define your own name for each repository.</dd>
   <dt>REPO_URL (required)</dt>
   <dd>The URL of the repository to be added. The repository URL must contain the protocol (for example, https://plugins.cloud.ibm.com instead of plugins.cloud.ibm.com). https://plugins.cloud.ibm.com is the official plug-in repository of {{site.data.keyword.cloud_notm}} CLI.</dd>
    </dl>


<strong>Examples</strong>:

Add the official plug-in repository of {{site.data.keyword.cloud_notm}} CLI as `ibmcloud-repo`:
```
ibmcloud plugin repo-add ibmcloud-repo https://plugins.cloud.ibm.com
```
{: codeblock}

## ibmcloud plugin repo-remove
{: #ibmcloud_plugin_repo_remove}

Remove a plug-in repository from {{site.data.keyword.cloud_notm}} CLI.
```
ibmcloud plugin repo-remove REPO_NAME
```
{: codeblock}

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
   <dl>
   <dt>REPO_NAME (required)</dt>
   <dd>The name of the repository to be removed.</dd>
   </dl>

<strong>Examples</strong>:

Remove `ibmcloud-repo` repository from {{site.data.keyword.cloud_notm}} CLI:
```
ibmcloud plugin repo-remove ibmcloud-repo
```
{: codeblock}

## ibmcloud plugin repo-plugins
{: #ibmcloud_plugin_repo_plugins}

List all available plug-ins in all added repositories or a specific repository.
```
ibmcloud plugin repo-plugins [-r REPO_NAME]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>List only the plugins in specified repository.</dd>
   </dl>

<strong>Examples</strong>:

List all plugins in all added repositories:

```
ibmcloud plugin repo-plugins
```

List all plug-ins in the `ibmcloud-repo` repository:

```
ibmcloud plugin repo-plugins -r ibmcloud-repo
```

## ibmcloud plugin repo-plugin
{: #ibmcloud_plugin_repo_plugin}

Show the details of a plug-in in the repository.

```
ibmcloud plugin repo-plugin PLUGIN_NAME [-r REPO_NAME]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>The name of the repository. If no repository is specified, the command uses the default plug-in repository.å</dd>
   </dl>

<strong>Examples</strong>:

List details of plug-in "IBM-Containers" in repository "sample-repo":

```
ibmcloud plugin repo-plugin IBM-Containers -r sample-repo
```

List details of plug-in "IBM-Containers" in default repository

```
ibmcloud plugin repo-plugin IBM-Containers -r sample-repo
```

## ibmcloud plugin list
{: #ibmcloud_plugin_list}

List all installed plug-ins in {{site.data.keyword.cloud_notm}} CLI.
```
ibmcloud plugin list
```
{: codeblock}

<strong>Prerequisites</strong>:  None

## ibmcloud plugin show
{: #ibmcloud_plugin_show}

Show details of an installed plug-in.
```
ibmcloud plugin show PLUGIN-NAME
```

<strong>Prerequisites</strong>:  None

## ibmcloud plugin install
{: #ibmcloud_plugin_install}

Install the specific version of plug-in to {{site.data.keyword.cloud_notm}} CLI from the specified path or repository.
```
ibmcloud plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

```
ibmcloud plugin install LOCAL-PATH/TO/PLUGIN | URL [-f]
```

If no repository is specified, the command uses the default plug-in repository 'Bluemix'.
If no version is specified, the command selects the latest available version to install.

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (required)</dt>
   <dd>If -r <i>REPO_NAME</i> is not specified, plug-in is installed from the specified local path or remote URL.</dd>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>The name of the repository where the plug-in binary is located. If no repository is specified, the command uses the default plug-in repository 'Bluemix'.</dd>
   <dt>-v <i>VERSION</i> (optional)</dt>
   <dd>The version of the plug-in to be installed. If not provided, the latest version of the plug-in is installed. This option is valid only when you install the plug-in from the repository.</dd>
   <dt>-f </dt>
   <dd>Force install of plug-in without confirmation.</dd>
    </dl>


The {{site.data.keyword.cloud_notm}} CLI has the official repository name of `Bluemix`.

<strong>Examples</strong>:

Install a plug-in from the local file:

```
ibmcloud plugin install /downloads/new_plugin
```

Install a plug-in from the remote URL:

```
ibmcloud plugin install https://plugins.cloud.ibm.com/downloads/bluemix-plugins/new_plugin
```

Install the 'container-service' plug-in of the latest version from the 'Bluemix' repository:

```
ibmcloud plugin install container-service -r Bluemix
```

or simply:

```
ibmcloud plugin install container-service
```

Install the 'container-service' plug-in with the  version '0.1.425' from the official plugin repository:

```
ibmcloud plugin install container-service -v 0.1.425
```

## ibmcloud plugin update
{: #ibmcloud_plugin_update}

Upgrade the plug-in from a repository.

```
ibmcloud plugin update [PLUGIN NAME] [-r REPO_NAME] [-v VERSION] [--all]
```

If no repository is specified, the command uses the default plug-in repository 'Bluemix'.
If no version is specified, the command selects the latest available version to install.

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
<dl>
 <dt>PLUGIN NAME</dt>
 <dd>Name of the plug-in to update. If not specified, the command checks upgrades for all plug-ins installed.</dd>
 <dt>-r REPO_NAME</dt>
 <dd>The name of the repository where the plug-in binary is located. If not specified, the command uses the default plug-in repository 'Bluemix'.</dd>
 <dt>-v <i>VERSION</i> (optional)</dt>
 <dd>The version of the plug-in to be updated to. If not provided, update the plug-in to the the latest available version.</dd>
 <dt>--all</dt>
 <dd>Update all available plug-ins</dd>
</dl>

<strong>Examples</strong>:

check for all available upgrade in the official plug-in repository 'Bluemix':

```
ibmcloud plugin update -r Bluemix
```

or simply:

```
ibmcloud plugin update
```

Upgrade plug-in 'container-service' in the official plug-in repository to the latest:

```
ibmcloud plugin update container-service
```

Update plug-in 'container-service' in the official plug-in repository to version '0.1.440':

```
ibmcloud plugin update container-service -v 0.1.440
```

## ibmcloud plugin uninstall
{: #ibmcloud_plugin_uninstall}

Uninstall the specified plug-in from {{site.data.keyword.cloud_notm}} CLI.

```
ibmcloud plugin uninstall PLUGIN_NAME
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>PLUGIN_NAME (required)</dt>
   <dd>The name of the plug-in to be uninstalled.</dd>
    </dl>

<strong>Examples</strong>:

Uninstall the 'container-service' plug-in that was previously installed:

```
ibmcloud plugin uninstall container-service
```
