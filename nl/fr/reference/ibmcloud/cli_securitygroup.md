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

# Gestion des groupes de sécurité pour le trafic de serveur virtuel
{: #sl-manage-securitygroups}

Un groupe de sécurité est un ensemble de règles de filtrage d'adresses IP qui détermine la manière de gérer le trafic entrant (ingress) et sortant (egress) tant au niveau des interfaces publiques qu'au niveau des interfaces privées d'une instance de serveur virtuel. Les règles que vous ajoutez à un groupe de sécurité sont dénommées règles de groupe de sécurité.

Les commandes suivantes permettent de gérer un groupe de sécurité à l'aide du service Security Group de l'infrastructure classique {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

Créer un groupe de sécurité.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-n, --name</dt>
<dd>Nom du groupe de sécurité.</dd>
<dt>-d, --description</dt>
<dd>Description du groupe de sécurité.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

Supprimer le groupe de sécurité indiqué.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

Obtenir des détails sur un groupe de sécurité.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

Modifier les détails d'un groupe de sécurité.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-n, --name</dt>
<dd>Nom du groupe de sécurité.</dd>
<dt>-d, --description</dt>
<dd>Description du groupe de sécurité.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

Associer une interface à un groupe de sécurité.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-n, --network-component</dt>
<dd>ID de composant réseau à associer au groupe de sécurité.</dd>
<dt>-s, --server</dt>
<dd>ID de serveur à associer au groupe de sécurité.</dd>
<dt>-i, --interface</dt>
<dd>Interface du serveur à associer (public/privé).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

Répertorier les interfaces associées au groupe de sécurité.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--sortby</dt>
<dd>Options de tri des colonnes : id, virtualServerId, hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

Déconnecter une interface d'un groupe de sécurité.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-n, --network-component</dt>
<dd>Composant réseau à retirer du groupe de sécurité.</dd>
<dt>-s, --server</dt>
<dd>ID de serveur à retirer du groupe de sécurité.</dd>
<dt>-i, --interface</dt>
<dd>Interface du serveur à retirer (public/privé).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

Répertorier les groupes de sécurité.
```
Répertorier les groupes de sécurité
```

<strong>Options de commande</strong> :
<dl>
<dt>--sortby</dt>
<dd>Options de tri des colonnes : id, name, description, created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

Ajouter une règle de groupe de sécurité à un groupe de sécurité.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-r, --remote-ip</dt>
<dd>IP/CIDR distant à appliquer.</dd>
<dt>-s, --remote-group</dt>
<dd>ID du groupe de sécurité distant à appliquer.</dd>
<dt>-d, --direction</dt>
<dd>Direction du trafic à appliquer (entrant,sortant), élément requis.</dd>
<dt>-e, --ether-type</dt>
<dd>Ethertype (IPv4 ou IPv6) à appliquer, la valeur par défaut est IPv4.</dd>
<dt>-M, --port-max</dt>
<dd>Port supérieur lié à appliquer.</dd>
<dt>-m, --port-min</dt>
<dd>Port inférieur lié à appliquer.</dd>
<dt>-p, --protocol</dt>
<dd>Protocole (icmp, tcp, udp) à appliquer.</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

Modifier une règle de groupe de sécurité dans un groupe de sécurité.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-r, --remote-ip</dt>
<dd>IP/CIDR distant à appliquer.</dd>
<dt>-s, --remote-group</dt>
<dd>ID du groupe de sécurité distant à appliquer.</dd>
<dt>-d, --direction</dt>
<dd>Direction du trafic à appliquer (entrant,sortant), élément requis.</dd>
<dt>-e, --ether-type</dt>
<dd>Ethertype (IPv4 ou IPv6) à appliquer, la valeur par défaut est IPv4.</dd>
<dt>-M, --port-max</dt>
<dd>Port supérieur lié à appliquer.</dd>
<dt>-m, --port-min</dt>
<dd>Port inférieur lié à appliquer.</dd>
<dt>-p, --protocol</dt>
<dd>Protocole (icmp, tcp, udp) à appliquer.</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

Répertorier les règles de groupe de sécurité
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--sortby</dt>
<dd>Les options de tri des colonnes sont les suivantes : id, remoteIp, remoteGroupId, direction, ethertype, portRangeMin, portRangeMax, protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

Retirer une règle d'un groupe de sécurité.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>
