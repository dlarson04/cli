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

# Gestione delle VLAN dell'infrastruttura classica
{: #manage-classic-vlans}

Le VLAN (Virtual Local Area Network) vengono utilizzate da {{site.data.keyword.cloud}} per isolare il traffico broadcast sulle reti pubbliche e private. Le VLAN vengono assegnate come necessario per soddisfare altre offerte.

Utilizza i seguenti comandi per gestire le VLAN dell'infrastruttura classica.
{: shortdesc}

## ibmcloud sl vlan create
{: #sl_vlan_create}

Crea una nuova VLAN.
```
ibmcloud sl vlan create [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-t, --vlan-type</dt>
<dd>Il tipo della VLAN, pubblica o privata.</dd>
<dt>-r, --router</dt>
<dd>Il nome host del router.</dd>
<dt>-d, --datacenter</dt>
<dd>Il nome breve del datacenter.</dd>
<dt>-n, --name</dt>
<dd>Il nome della VLAN.</dd>
<dt>-f, --force</dt>
<dd>Forza l'operazione senza conferma.</dd>
</dl>

**Esempi**:
```
ibmcloud sl vlan create -t public -d dal09 -s 16 -n myvlan
```
{: codeblock}

Questo comando crea una vlan pubblica ubicata nel datacenter `dal09` con 16 indirizzi IP e con il nome `myvlan`.

## ibmcloud sl vlan cancel
{: #sl_vlan_cancel}

Annulla una VLAN:
```
ibmcloud sl vlan cancel IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forza l'operazione senza conferma.</dd>
</dl>

**Esempi**:
```
ibmcloud sl vlan cancel 12345678 -f
```
{: codeblock}

Questo comando annulla la vlan con ID `12345678` senza richiedere conferma.

## ibmcloud sl vlan detail
{: #sl_vlan_detail}

Ottieni i dettagli di una VLAN.
```
ibmcloud sl vlan detail IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--no-vs</dt>
<dd>Nascondi elenco server virtuali.</dd>
<dt>--no-hardware</dt>
<dd>Nascondi elenco hardware.</dd>
</dl>

**Esempi**:
```
ibmcloud sl vlan detail 12345678  --no-vs --no-hardware
```
{: codeblock}

Questo comando mostra i dettagli della vlan con ID `12345678` e non elenca il server virtuale o il server hardware.

## ibmcloud sl vlan edit
{: #sl_vlan_edit}

Modifica i dettagli di una VLAN.
```
ibmcloud sl vlan edit IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-n, --name</dt>
<dd>Il nome della VLAN.</dd>
</dl>

**Esempi**:
```
ibmcloud sl vlan edit 12345678 -n myvlan-rename
```
{: codeblock}

Questo comando aggiorna la vlan con `ID 12345678` e le fornisce un nuovo nome `myvlan-rename`.

## ibmcloud sl vlan list
{: #sl_vlan_list}

Elenca tutte le VLAN per il tuo account.
```
ibmcloud sl vlan list [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--sortby</dt>
<dd>Colonna da ordinare, le opzioni sono: id, number, name, firewall, datacenter, hardware, virtual_servers, public_ips.</dd>
<dt>-d, --datacenter</dt>
<dd>Filtra per nome breve del datacenter.</dd>
<dt>-n, --number</dt>
<dd>Filtra in base al numero della VLAN.</dd>
<dt>--name</dt>
<dd>Filtra in base al nome della VLAN.</dd>
<dt>--order</dt>
<dd>Filtra in base all'ID dell'ordine che ha acquistato la VLAN.</dd>
</dl>

**Esempi**:
```
ibmcloud sl vlan list -d dal09 --sortby number
```
Questo comando elenca tutte le vlan sull'account corrente eseguendo il filtro per un datacenter uguale a `dal09` e le ordina per numero di vlan.

## ibmcloud sl vlan options
{: #sl_vlan_options}

Elenca tutte le opzioni per la creazione della VLAN.
```
ibmcloud sl vlan options
```
{: codeblock}

**Esempi**:
```
ibmcloud sl vlan options
```
{: codeblock}

Questo comando elenca tutte le opzioni per la creazione di una vlan, ad es. il tipo di vlan, i datacenter, la dimensione della sottorete, i router, ecc
