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

# Sicherheitsgruppen für Datenverkehr mit virtuellen Servern verwalten
{: #sl-manage-securitygroups}

Eine Sicherheitsgruppe ist eine Gruppe aus IP-Filterregeln, von denen definiert wird, wie eingehender (Ingress) und ausgehender (Egress) Datenverkehr an öffentliche und private Schnittstellen einer Instanz eines virtuellen Servers verarbeitet werden soll. Die Regeln, die Sie zu einer Sicherheitsgruppe hinzufügen, werden als Sicherheitsgruppenregeln bezeichnet.

Verwenden Sie die folgenden Befehle, um eine Sicherheitsgruppe über den Service für Sicherheitsgruppen der klassischen {{site.data.keyword.cloud}}-Infrastruktur zu verwalten.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

Eine Sicherheitsgruppe erstellen.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-n, --name</dt>
<dd>Der Name der Sicherheitsgruppe.</dd>
<dt>-d, --description</dt>
<dd>Die Beschreibung der Sicherheitsgruppe.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

Die angegebene Sicherheitsgruppe löschen.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Operation ohne Bestätigung erzwingen.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

Details zu einer Sicherheitsgruppe abrufen.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

Details einer Sicherheitsgruppe bearbeiten.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-n, --name</dt>
<dd>Der Name der Sicherheitsgruppe.</dd>
<dt>-d, --description</dt>
<dd>Die Beschreibung der Sicherheitsgruppe.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

Eine Schnittstelle zu einer Sicherheitsgruppe zuordnen.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>Die ID der Netzkomponente, die der Sicherheitsgruppe zugeordnet werden soll.</dd>
<dt>-s, --server</dt>
<dd>Die Server-ID, die der Sicherheitsgruppe zugeordnet werden soll.</dd>
<dt>-i, --interface</dt>
<dd>Die Schnittstelle des Servers, die zugeordnet werden soll (öffentlich/privat).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

Die Schnittstellen auflisten, die der Sicherheitsgruppe zugeordnet sind.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>--sortby</dt>
<dd>Spalte, nach der sortiert werden soll. Optionen: id,virtualServerId,hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

Die Zuordnung einer Schnittstelle zu einer Sicherheitsgruppe aufheben.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>Die Netzkomponente, die von der Sicherheitsgruppe entfernt werden soll.</dd>
<dt>-s, --server</dt>
<dd>Die Server-ID, die von der Sicherheitsgruppe entfernt werden soll.</dd>
<dt>-i, --interface</dt>
<dd>Die Schnittstelle des Servers, die entfernt werden soll (öffentlich/privat).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

Sicherheitsgruppen auflisten.
```
List security groups
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>--sortby</dt>
<dd>Spalte, nach der sortiert werden soll. Optionen: id,name,description,created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

Sicherheitsgruppenregel zu einer Sicherheitsgruppe hinzufügen.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>Die zu erzwingende ferne IP/CIDR.</dd>
<dt>-s, --remote-group</dt>
<dd>Die ID der zu erzwingenden fernen Sicherheitsgruppe.</dd>
<dt>-d, --direction</dt>
<dd>Die zu erzwingende Richtung des Datenverkehrs (ingress,egress), erforderlich.</dd>
<dt>-e, --ether-type</dt>
<dd>Der zu erzwingende Ethernet-Typ (IPv4 oder IPv6), Standard ist IPv4, falls keine andere Angabe erfolgt.</dd>
<dt>-M, --port-max</dt>
<dd>Die zu erzwingende obere Portgrenze.</dd>
<dt>-m, --port-min</dt>
<dd>Die zu erzwingende untere Portgrenze.</dd>
<dt>-p, --protocol</dt>
<dd>Das zu erzwingende Protokoll (icmp, tcp, udp).</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

Sicherheitsgruppenregel in einer Sicherheitsgruppe bearbeiten.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>Die zu erzwingende ferne IP/CIDR.</dd>
<dt>-s, --remote-group</dt>
<dd>Die ID der zu erzwingenden fernen Sicherheitsgruppe.</dd>
<dt>-d, --direction</dt>
<dd>Die zu erzwingende Richtung des Datenverkehrs (ingress,egress), erforderlich.</dd>
<dt>-e, --ether-type</dt>
<dd>Der zu erzwingende Ethernet-Typ (IPv4 oder IPv6), Standard ist IPv4, falls keine andere Angabe erfolgt.</dd>
<dt>-M, --port-max</dt>
<dd>Die zu erzwingende obere Portgrenze.</dd>
<dt>-m, --port-min</dt>
<dd>Die zu erzwingende untere Portgrenze.</dd>
<dt>-p, --protocol</dt>
<dd>Das zu erzwingende Protokoll (icmp, tcp, udp).</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

Sicherheitsgruppenregeln auflisten.
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>--sortby</dt>
<dd>Spalte, nach der sortiert werden soll. Optionen sind: id,remoteIp,remoteGroupId,direction,ethertype,portRangeMin,portRangeMax,protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

Regel aus einer Sicherheitsgruppe entfernen.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Befehlsoptionen</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Operation ohne Bestätigung erzwingen.</dd>
</dl>
