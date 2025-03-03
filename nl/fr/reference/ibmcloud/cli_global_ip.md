---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, ibmcloud sl globalip, globalip, global ip addresses, assign global ip

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gestion des adresses IP globales
{: #sl-manage-global-ip}

Une adresse IP globale est un sous-réseau secondaire statique spécialisé. Il vous est distribué en tant que sous-réseau /32 (en d'autres termes, une seule adresse IP) qui peut être routé vers n'importe quelle autre adresse IP sur votre compte.

Les commandes suivantes permettent de gérer une adresse IP globale dans le service Global IP de l'infrastructure classique {{site.data.keyword.Bluemix}}.
{: shortdesc}

## ibmcloud sl globalip assign
{: #sl_globalip_assign}

Permet d'affecter une adresse IP globale à un routeur ou un périphérique cible.
```
ibmcloud sl globalip assign IDENTIFIER TARGET
```

**Exemples** :
```
ibmcloud sl globalip assign 12345678 9.111.123.456
```

Cette commande affecte une adresse IP portant l'ID `12345678` à une unité cible dont l'adresse IP est `9.111.123.456`.

## ibmcloud sl globalip cancel
{: #sl_globalip_cancel}

Permet d'annuler une adresse IP globale.
```
ibmcloud sl globalip cancel IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>

**Exemples** :
```
ibmcloud sl globalip cancel 12345678
```

Cette commande annule une adresse IP portant l'ID `12345678`.

 ## ibmcloud sl globalip create
{: #sl_globalip_create}

Permet de créer une adresse IP globale.
```
ibmcloud sl globalip create [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--v6</dt>
<dd>Commandez une adresse IP IPv6.</dd>
<dt>--test</dt>
<dd>Indique qu'une commande doit être testée.</dd>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>

**Exemples** :
```
ibmcloud sl globalip create --v6
```

Cette commande crée une adresse IP V6.

## ibmcloud sl globalip list
{: #sl_globalip_list}

Permet de répertorier toutes les adresses IP globale sur votre compte.
```
ibmcloud sl globalip list [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--v4</dt>
<dd>Afficher uniquement les éléments IPv4.</dd>
<dt>--v6</dt>
<dd>Afficher uniquement les éléments IPv6.</dd>
<dt>--order</dt>
<dd>Filtrer par ID de commande utilisé pour acheter cette adresse IP.</dd>
</dl>

**Exemples** :
```
ibmcloud sl globalip list --v4
```

Cette commande répertorie toutes les adresses IP V4 sur le compte en cours.

## ibmcloud sl globalip unassign
{: #sl_globalip_unassign}

Permet d'annuler l'affectation d'une adresse IP globale à partir d'un routeur ou d'un périphérique cible.
```
ibmcloud sl globalip unassign IDENTIFIER
```


**Exemples** :
```
ibmcloud sl globalip unassign 12345678
```

Cette commande annule l'affectation à l'unité cible d'une adresse IP portant l'ID `12345678`.
