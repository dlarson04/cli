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

# Managing classic infrastructure VLANs
{: #manage-classic-vlans}

Virtual Local Area Networks (VLANs) are used by {{site.data.keyword.cloud}} to isolate broadcast traffic on the public and private networks. VLANs are assigned as needed to fulfill other offerings.

Use the following commands to manage classic infrastructure VLANs.
{: shortdesc}

## ibmcloud sl vlan create
{: #sl_vlan_create}

Create a new VLAN.
```
ibmcloud sl vlan create [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-t, --vlan-type</dt>
<dd>The type of the VLAN, either public or private.</dd>
<dt>-r, --router</dt>
<dd>The hostname of the router.</dd>
<dt>-d, --datacenter</dt>
<dd>The short name of the datacenter.</dd>
<dt>-n, --name</dt>
<dd>The name of the VLAN.</dd>
<dt>-f, --force</dt>
<dd>Force operation without confirmation.</dd>
</dl>

**Examples**:
```
ibmcloud sl vlan create -t public -d dal09 -s 16 -n myvlan
```
{: codeblock}

This command creates a public vlan located at datacenter `dal09` with 16 IP addresses and name is `myvlan`.

## ibmcloud sl vlan cancel
{: #sl_vlan_cancel}

Cancel a VLAN:
```
ibmcloud sl vlan cancel IDENTIFIER [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Force operation without confirmation.</dd>
</dl>

**Examples**:
```
ibmcloud sl vlan cancel 12345678 -f
```
{: codeblock}

This command cancels vlan with ID `12345678` without asking for confirmation.

## ibmcloud sl vlan detail
{: #sl_vlan_detail}

Get details about a VLAN.
```
ibmcloud sl vlan detail IDENTIFIER [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>--no-vs</dt>
<dd>Hide virtual server listing.</dd>
<dt>--no-hardware</dt>
<dd>Hide hardware listing.</dd>
</dl>

**Examples**:
```
ibmcloud sl vlan detail 12345678  --no-vs --no-hardware
```
{: codeblock}

This command shows details of vlan with ID `12345678`, and not list virtual server or hardware server.

## ibmcloud sl vlan edit
{: #sl_vlan_edit}

Edit the details about a VLAN.
```
ibmcloud sl vlan edit IDENTIFIER [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-n, --name</dt>
<dd>The name of the VLAN.</dd>
</dl>

**Examples**:
```
ibmcloud sl vlan edit 12345678 -n myvlan-rename
```
{: codeblock}

This command updates vlan with `ID 12345678` and gives it a new name `myvlan-rename`.

## ibmcloud sl vlan list
{: #sl_vlan_list}

List all the VLANs on your account.
```
ibmcloud sl vlan list [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>--sortby</dt>
<dd>Column to sort by, options are: id,number,name,firewall,datacenter,hardware,virtual_servers,public_ips.</dd>
<dt>-d, --datacenter</dt>
<dd>Filter by datacenter shortname.</dd>
<dt>-n, --number</dt>
<dd>Filter by VLAN number.</dd>
<dt>--name</dt>
<dd>Filter by VLAN name.</dd>
<dt>--order</dt>
<dd>Filter by ID of the order that purchased the VLAN.</dd>
</dl>

**Examples**:
```
ibmcloud sl vlan list -d dal09 --sortby number
```
This commands lists all vlans on current account filtering by datacenter equals to `dal09`, and sort them by vlan number.

## ibmcloud sl vlan options
{: #sl_vlan_options}

List all the options for creating VLAN.
```
ibmcloud sl vlan options
```
{: codeblock}

**Examples**:
```
ibmcloud sl vlan options
```
{: codeblock}

This command lists all options for creating a vlan, eg. vlan type, datacenters, subnet size, routers, etc.
