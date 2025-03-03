---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-10"

keywords: cli, general commands, ibmcloud commands, ibmcloud api, ibmcloud, cli commands, regions, target, update, ibmcloud sl

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:note: .note}
{:codeblock: .codeblock}

# General CLI (ibmcloud) commands
{: #ibmcloud_cli}

The {{site.data.keyword.cloud_notm}} command-line interface (CLI) provides a set of commands that are grouped by namespace for users to interact with {{site.data.keyword.cloud_notm}}.
{: shortdesc}

{{site.data.keyword.cloud_notm}} command line client bundles a Cloud Foundry command line client in its installation. If you have your own Cloud Foundry CLI installed, don't use both {{site.data.keyword.cloud_notm}} CLI commands and Cloud Foundry CLI commands of your own installation in the same context. Instead, use **`ibmcloud cf [command]`** if you want to use the Cloud Foundry CLI to manage Cloud Foundry resources in {{site.data.keyword.cloud_notm}} CLI context. Note that **`ibmcloud cf api/login/logout/target`** isn't allowed, and you must use **`ibmcloud api/login/logout/target`** instead.

As of May 2018 the {{site.data.keyword.cloud_notm}} CLI commands have changed from **`bluemix`** and **`bx`** to **`ibmcloud`**. However, you can still use the **`bluemix`** and **`bx`** CLI commands until they're removed later.
{: tip}

The following lists detailed commands that are supported by the {{site.data.keyword.cloud_notm}} CLI, including their names, arguments, options, prerequisites, descriptions, and examples.

Prerequisites list which actions are required before using the command, and might include one or more of the following actions:

<dl>
<dt>Docker</dt>
<dd>Install the Docker CLI.</dd>
<dt>Endpoint</dt>
<dd>Use the **`ibmcloud api`** command to set an API endpoint.</dd>
<dt>Log in</dt>
<dd>Use the **`ibmcloud login`** command to log in. If you are logging in with a federated ID, use the **`--sso`** option to authenticate with a one time passcode, or use the **`--apikey`** option to authenticate with an API key.</dd>
<dt>Target</dt>
<dd>Use the **`ibmcloud target`** command to set an org and space.</dd>
</dl>

## ibmcloud help
{: #ibmcloud_help}

Displays the general help for first-level built-in commands and supported namespaces of {{site.data.keyword.cloud_notm}} CLI, or the help for a specific built-in command or namespace.

```
ibmcloud help [COMMAND|NAMESPACE]
```

### Prerequisites
{: #help-prereqs}

None.

### Command options
{: #help-options}

<dl>
<dt>COMMAND|NAMESPACE</dt>
<dd>The command or namespace that help is displayed for. If not specified, the general help for {{site.data.keyword.cloud_notm}} CLI is shown. Optional.</dd>
</dl>

### Examples
{: #help-examples}

Display general help for the {{site.data.keyword.cloud_notm}} CLI:
```
ibmcloud help
```
{: codeblock}

Display help for the **`dev`** command:
```
ibmcloud help dev
```
{: codeblock}

## ibmcloud api
{: #ibmcloud_api}

Set or view the {{site.data.keyword.cloud_notm}} API endpoint.
```
ibmcloud api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

### Prerequisites
{: #api-prereqs}

None.

### Command options
{: #api-options}

<dl>
<dt>API_ENDPOINT</dt>
<dd>The API endpoint that is targeted, for example, `https://cloud.ibm.com`. If both the **`API_ENDPOINT`** and **`--unset`** options aren't specified, the current API endpoint is displayed. Optional.</dd>
<dt>--skip-ssl-validation</dt>
<dd>Bypass SSL validation of HTTP requests. Optional.</dd>
<dt>--unset</dt>
<dd>Remove the API endpoint setting.</dd>
</dl>

### Examples
{: #api-examples}

Set the API endpoint to cloud.ibm.com:
```
ibmcloud api cloud.ibm.com
```
{: codeblock}

```
ibmcloud api https://cloud.ibm.com --skip-ssl-validation
```
{: codeblock}

View the current API endpoint:
```
ibmcloud api
```
{: codeblock}

Remove the API endpoint:
```
ibmcloud api --unset
```
{: codeblock}

## ibmcloud config
{: #ibmcloud_config}

Writes default values to the configuration file.

```
ibmcloud config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

### Prerequisites
{: #config-prereqs}

None.

### Command options
{: #config-options}

<dl>
<dt>--check-version</dt>
<dd>Enable or disable CLI version checking. Valid values are `true` or `false`.</dd>
<dt>--color</dt>
<dd>Enable or disable color output. This option is disabled by default. Valid values are `true` or `false`.</dd>
<dt>--http-timeout</dt>
<dd>The timeout value for HTTP requests in seconds. The default value is 60 seconds.</dd>
<dt>--locale</dt>
<dd>Set a default locale. If no value is specified, the previous locale is deleted. </dd>
<dt>--trace </dt>
<dd>Trace HTTP requests to the terminal or specified file. Valid values are `true` or `false`.</dd>
</dl>

You can specify only one of the options at a time.
{: tip}

### Examples
{: #config-examples}

Set HTTP request timeout to 30 seconds:
```
ibmcloud config --http-timeout 30
```
{: codeblock}

Enable trace output for HTTP requests:
```
ibmcloud config --trace true
```
{: codeblock}

Trace HTTP requests to the `/home/usera/my_trace` file:
```
ibmcloud config --trace /home/usera/my_trace
```
{: codeblock}

Disable color output:
```
ibmcloud config --color false
```
{: codeblock}

Set the locale to zh_Hans:
```
ibmcloud config --locale zh_Hans
```
{: codeblock}

Clear the locale settings:
```
ibmcloud config --locale CLEAR
```
{: codeblock}

## ibmcloud info
{: #ibmcloud_info}

The **`ibmcloud info`** command is no longer available as of CLI version 0.14. To install the latest CLI version, see [Installing the stand-alone {{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli#install-ibmcloud-cli).

## ibmcloud cf
{: #ibmcloud_cf}

Invoke the embedded Cloud Foundry CLI.
```
ibmcloud [-q, --quiet] cf COMMAND...
```

### Prerequisites
{: #info-prereqs}

None.

### Command options
{: #info-options}

<dl>
  <dt>-q, --quiet</dt>
  <dd>Do not display the invoking message.</dd>
</dl>

### Examples
{: #info-examples}

List the Cloud Foundry apps:

```
ibmcloud cf apps
```

List the Cloud Foundry services without displaying the `Invoking cf command...` message:
```
ibmcloud -q cf services
```
{: codeblock}

## ibmcloud cf install
{: #ibmcloud_cf_install}

Install a Cloud Foundry CLI for IBM Cloud CLI
```
ibmcloud cf install [-v, --version VERSION] [--restore] [-f, --force]
```

### Prerequisites
{: #cfinstall-prereqs}

None.

### Command options
{: #cfinstall-options}

<dl>
  <dt>-v, --version</dt>
  <dd>Specify version of Cloud Foundry CLI to install</dd>
  <dt>--restore</dt>
  <dd>Restore to pre-bundled version of Cloud Foundry CLI</dd>
  <dt>-f, --force</dt>
  <dd>Force installation without confirmation</dd>
</dl>

### Examples
{: #cfinstall-examples}

Install Cloud Foundry CLI `6.44.1`:

```
ibmcloud cf install -v 6.44.1
```

Install latest version of Cloud Foundry CLI without confirmation:

```
ibmcloud cf install -f
```

Recover to default bundled Cloud Foundry CLI:

```
ibmcloud cf install --restore
```

## ibmcloud login
{: #ibmcloud_login}

Log in to the {{site.data.keyword.cloud_notm}} CLI.

```
ibmcloud login [-a API_ENDPOINT] [--sso] [-u USERNAME] [-p PASSWORD] [--apikey KEY | @KEY_FILE] [--no-iam] [-c ACCOUNT_ID | --no-account] [-g RESOURCE_GROUP] [-r REGION | --no-region] [-o ORG] [-s SPACE]
```
### Prerequisites
{: #login-prereqs}

None.

### Command options
{: #login-options}

<dl>
<dt>-a API_ENDPOINT</dt>
<dd>The API endpoint, for example, `cloud.ibm.com`. </dd>
<dt>--apikey API_KEY or @API_KEY_FILE_PATH</dt>
<dd>The API key content or the path of an API key file that is indicated by the @ symbol.</dd>
<dt>-u USER_NAME</dt>
<dd>The user name. Optional.</dd>
<dt>-p PASS_WORD</dt>
<dd>The user password. Optional.</dd>
<dt>-c ACCOUNT_ID</dt>
<dd>The ID of the target account. This option is exclusive with the **`--no account`** option.</dd>
<dt>--no-account</dt>
<dd>Forced login without the account. This option isn't recommended, and it is exclusive with the **`-c`** option.</dd>
<dt>-g RESOURCE_GROUP</dt>
<dd>The name of the target resource group. Optional.</dd>
<dt>-r REGION</dt>
<dd>The name of the target region, for example, us-south or eu-gb.</dd>
<dt>--no-region</dt>
<dd>Forced login without targeting a region.</dd>
<dt>-o ORG</dt>
<dd>The name of the target organization. This option is deprecated. Use **`ibmcloud target -o org_name`** instead. Optional.</dd>
<dt>-s SPACE</dt>
<dd>The name of the target space. This option is deprected. Use **`ibmcloud target -s space_name`** instead. Optional.</dd>
<dt>--no-iam</dt>
<dd>Force authentication with the login server instead of the public IAM.</dd>
<dt>--skip-ssl-validation</dt>
<dd>Bypass the SSL validation of HTTP requests. This option isn't recommended.</dd>
</dl>

### Examples
{: #login-examples}

Log in interactively.

```
ibmcloud login
```
{: codeblock}

Log in with a user name and password, and set a target account, org, and space:
```
ibmcloud login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

Log in with a one time passcode, and set a target account, org, and space:
```
ibmcloud login --sso -c MyAccountID -o MyOrg -s MySpace
```

Set your Cloud Found org and space. You can run the following command to interactively identify the org and space:

```
ibmcloud target --cf
```
{: codeblock}

Or, if you know which org and space that the service belongs to, you can use the following command:

```
ibmcloud target -o <value> -s <value>
```
{: codeblock}

Use an API key with an associated account:

```
ibmcloud login --apikey api-key-string -o MyOrg -s MySpace
```

```
ibmcloud login --apikey @filename -o MyOrg -s MySpace
```

Use an API key with no associated account:

```
ibmcloud login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
ibmcloud login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

If the API Key has an associated account, switching to another account isn't supported.
{: note}

Use a one time passcode:

```
ibmcloud login -u UserID --sso
```
{: codeblock}

Then, the CLI provides a URL link and prompts you for the passcode:

```
One Time Code (Get one at https://URL_Link_To_Obtain_Passcode):
```
{: screen}

Open the link in a browser to get a passcode. Enter the given passcode in the console to log in.

## ibmcloud logout
{: #ibmcloud_logout}

Log out of the CLI.

```
ibmcloud logout
```
{: codeblock}

### Prerequisites
{: #logout-prereqs}

None.

## ibmcloud regions
{: #ibmcloud_regions}

View the information for all regions on {{site.data.keyword.cloud_notm}}.

```
ibmcloud regions
```
{: codeblock}

### Prerequisites
{: #regions-prereqs}

Use the **`ibmcloud api`** command to set an API endpoint.

## ibmcloud target
{: #ibmcloud_target}

Set or view the target account, region, organization, or space.

```
ibmcloud target [-r REGION_NAME | --unset-region] [-c ACCOUNT_ID] [-g RESOURCE_GROUP | --unset-resource-group] [--cf] [--cf-api ENDPOINT] [-o ORG] [-s SPACE] [--output FORMAT]
```

### Prerequisites
{: #target-prereqs}

* Use the **`ibmcloud api`** command to set an API endpoint.
* Use the **`ibmcloud login`** command to log in. If you are logging in with a federated ID, use the **`--sso`** option to authenticate with a one time passcode, or use the **`--apikey`** option to authenticate with an API key.

### Command options
{: #target-options}

<dl>
<dt>-c ACCOUNT_ID</dt>
<dd>The ID of the target account. Optional.</dd>
<dt>-r REGION</dt>
<dd>The name of the target region, for example, us-south or eu-gb. Optional.</dd>
<dt>-g RESOURCE_GROUP</dt>
<dd>The name of the target resource group. Optional.</dd>
<dt>--cf</dt>
<dd>Interactively specify the target org and space.</dd>
<dt>--cf-api</dt>
<dd>The Cloud Foundry API endpoint.</dd>
<dt>-o ORG</dt>
<dd>The name of the target organization. Optional.</dd>
<dt>-s SPACE</dt>
<dd>The name of the target space. Optional.</dd>
<dt>--unset-region</dt>
<dd>Clear the targeted region.</dd>
<dt>--unset-resource-group</dt>
<dd>Clear the targeted resource group.</dd>
<dt>--output FORMAT</dt>
<dd>The specified output format. JSON is currently the only supported format.</dd>
</dl>

If none of the options are specified, the current account, region, org, and space are displayed.
{: note}

### Examples
{: #target-examples}

Set the current account, organization, and space:
```
ibmcloud target -c MyAccountID -o MyOrg -s MySpace
```
{: codeblock}

Switch to a new region:
```
ibmcloud target -r eu-gb
```
{: codeblock}

View the current account, region, org, and space:
```
ibmcloud target
```
{: codeblock}

## ibmcloud update
{: #ibmcloud_update}

Update the CLI to the latest version.

```
ibmcloud update [-f]
```
### Prerequisites
{: #update-prereqs}

### Command options
{: #update-options}

<dl>
  <dt>-f</dt>
  <dd>Force an update without confirmation. Root privilege is required.</dd>
</dl>

## General classic infrastructure service commands
{: #classic-service-commands}

Use classic infrastructure commands in the {{site.data.keyword.cloud_notm}} CLI to configure and manage infrastructure services.

Run the **`ibmcloud sl`** command to see the list of available commands:
```
USAGE:
   ibmcloud sl command [arguments...] [options...]

COMMANDS:
   block           Classic infrastructure Block Storage
   cdn             Classic infrastructure Content Delivery Network
   file            Classic infrastructure File Storage
   dns             Classic infrastructure Domain Name System
   globalip        Classic infrastructure Global IP addresses
   hardware        Classic infrastructure hardware servers
   image           Classic infrastructure Compute images
   ipsec           Classic infrastructure IPSEC VPN
   loadbal         Classic infrastructure Load balancers
   security        Classic infrastructure SSH Keys and SSL Certificates
   securitygroup   Classic infrastructure network security groups
   subnet          Classic infrastructure Network subnets
   ticket          Classic infrastructure Manage Tickets
   vlan            Classic infrastructure Network VLANs
   vs              Classic infrastructure Virtual Servers
   order           Classic infrastructure Orders
   user            Classic infrastructure Manage Users
   call-api        Call arbitrary API endpoints.
   help            Print command usage message
```
{: screen}

To view help information about a command, run the following command:
```
ibmcloud sl [command] -h
```

The **`ibmcloud sl init`** command is no longer available as of CLI version `0.14`. To install the latest CLI version, see [Installing the stand-alone {{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli#install-ibmcloud-cli).
{: note}

## ibmcloud sl help
{: #sl_help}

View help information for all commands to operate the classic infrastructure environment.
```
ibmcloud sl help
```
{: codeblock}

