---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, manage security groups, ingress, egress, traffic, virtual server cli, classic infrastructure cli, securitygroup, ibmcloud sl securitygroup, security group cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Managing security groups for virtual server traffic
{: #sl-manage-securitygroups}

A security group is a set of IP filter rules that define how to handle incoming (ingress) and outgoing (egress) traffic to both the public and private interfaces of a virtual server instance. The rules that you add to a security group are known as security group rules.

Use the following commands to manage a security group using the {{site.data.keyword.cloud}} classic infrastructure Security Group service.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

Create a security group.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-n, --name</dt>
<dd>The name of the security group.</dd>
<dt>-d, --description</dt>
<dd>The description of the security group.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

Delete the given security group.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Force operation without confirmation.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

Get details about a security group.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

Edit details of a security group.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-n, --name</dt>
<dd>The name of the security group.</dd>
<dt>-d, --description</dt>
<dd>The description of the security group.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

Attach an interface to a security group.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>The network component ID to associate with the security group.</dd>
<dt>-s, --server</dt>
<dd>The server ID to associate with the security group.</dd>
<dt>-i, --interface</dt>
<dd>The interface of the server to associate (public/private).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

List interfaces associated with security group.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>--sortby</dt>
<dd>Column to sort by, options are: id,virtualServerId,hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

Detach an interface from a security group.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>The network component to remove from the security group.</dd>
<dt>-s, --server</dt>
<dd>The server ID to remove from the security group.</dd>
<dt>-i, --interface</dt>
<dd>The interface of the server to remove (public/private).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

List security groups.
```
List security groups
```

<strong>Command options</strong>:
<dl>
<dt>--sortby</dt>
<dd>Column to sort by, options are: id,name,description,created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

Add a security group rule to a security group.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>The remote IP/CIDR to enforce.</dd>
<dt>-s, --remote-group</dt>
<dd>The ID of the remote security group to enforce.</dd>
<dt>-d, --direction</dt>
<dd>The direction of traffic to enforce (ingress,egress), required.</dd>
<dt>-e, --ether-type</dt>
<dd>The ethertype (IPv4 or IPv6) to enforce, default is IPv4 if not specified.</dd>
<dt>-M, --port-max</dt>
<dd>The upper port bound to enforce.</dd>
<dt>-m, --port-min</dt>
<dd>The lower port bound to enforce.</dd>
<dt>-p, --protocol</dt>
<dd>The protocol (icmp, tcp, udp) to enforce.</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

Edit a security group rule in a security group.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>The remote IP/CIDR to enforce.</dd>
<dt>-s, --remote-group</dt>
<dd>The ID of the remote security group to enforce.</dd>
<dt>-d, --direction</dt>
<dd>The direction of traffic to enforce (ingress,egress), required.</dd>
<dt>-e, --ether-type</dt>
<dd>The ethertype (IPv4 or IPv6) to enforce, default is IPv4 if not specified.</dd>
<dt>-M, --port-max</dt>
<dd>The upper port bound to enforce.</dd>
<dt>-m, --port-min</dt>
<dd>The lower port bound to enforce.</dd>
<dt>-p, --protocol</dt>
<dd>The protocol (icmp, tcp, udp) to enforce.</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

List security group rules.
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>--sortby</dt>
<dd>Column to sort by, options are: id,remoteIp,remoteGroupId,direction,ethertype,portRangeMin,portRangeMax,protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

Remove a rule from a security group.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Command options</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Force operation without confirmation.</dd>
</dl>
