---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-21"

keywords: cli, manage resources, resource group, ibmcloud resource group, ibmcloud resource, service-instance, quotas, resource group cli, resource cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# Gestione di risorse e gruppi di risorse
{: #ibmcloud_commands_resource}

Un gruppo di risorse è un modo per organizzare le risorse dell'account in raggruppamenti personalizzabili. Utilizza i seguenti comandi per gestire le risorse {{site.data.keyword.cloud}} in un gruppo di risorse.
{: shortdesc}

## ibmcloud resource groups
{: #ibmcloud_resource_groups}

Elenca i gruppi di risorse.
```
ibmcloud resource groups [--default] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--default</dt>
  <dd>Richiama il gruppo predefinito dell'account corrente.</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON.</dd>
</dl>

<strong>Esempi</strong>:

Elenca tutti i gruppi di risorse nell'account attualmente selezionato:
```
ibmcloud resource groups
```
{: codeblock}

Elenca il gruppo predefinito dell'account attualmente selezionato:
```
ibmcloud resource groups --default
```
{: codeblock}

## ibmcloud resource group
{: #ibmcloud_resource_group}

Mostra i dettagli di un gruppo di risorse
```
ibmcloud resource group NOME [--id] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--id</dt>
  <dd>Mostra solo l'ID</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON.</dd>
</dl>

<strong>Esempi</strong>:

Mostra il gruppo di risorse `example-group`:
```
ibmcloud resource group example-group
```
{: codeblock}

Mostra solo l'ID del gruppo di risorse `example-group`:
```
ibmcloud resource group example-group --id
```
{: codeblock}

## ibmcloud resource group-create
{: #ibmcloud_resource_group_create}

Crea un gruppo di risorse:
```
ibmcloud resource group-create NOME
```
{: codeblock}

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome del gruppo di risorse</dd>
</dl>

<strong>Esempi</strong>:

Crea un gruppo di risorse `example-group`:
```
ibmcloud resource group-create example-group
```
{: codeblock}

## ibmcloud resource group-update
{: #ibmcloud_resource_group_update}

Aggiorna un gruppo di risorse esistente
```
ibmcloud resource group-update NOME [-n, --name NUOVO_NOME] [-q, --quota NOME_NUOVA_QUOTA]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome del gruppo di risorse di destinazione</dd>
  <dt>-n, --name</dt>
  <dd>Nuovo nome del gruppo di risorse</dd>
  <dt>-q, --quota</dt>
  <dd>Nome della nuova definizione di quota</dd>
  <dt>-f</dt>
  <dd>Forza l'aggiornamento senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Rinomina il gruppo di risorse `example-group` come `trial-group`:
```
ibmcloud resource group-update example-group -n trial-group
```
{: codeblock}

Modifica la quota del gruppo di risorse `example-group` come `free`:
```
ibmcloud resource group-update example-group -q free
```
{: codeblock}

## ibmcloud resource quotas
{: #ibmcloud_resource_quotas}

Elenca tutte le definizioni di quota.
```
ibmcloud resource quotas
```
{: codeblock}

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
</dl>

<strong>Esempi</strong>:

Elenca tutte le definizioni di quota:
```
ibmcloud resource quotas
```
{: codeblock}

## ibmcloud resource quota
{: #ibmcloud_resource_quota}

Mostra i dettagli di una definizione di quota.
```
ibmcloud resource quota NOME
```
{: codeblock}

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome della quota</dd>
</dl>

<strong>Esempi</strong>:

Mostra i dettagli della quota `free`:
```
ibmcloud resource quota free
```
{: codeblock}

## ibmcloud resource cf-service-instance-migrate
{: #ibmcloud_resource_cf_service_instance_migrate}

Migrazione di un'istanza del servizio Cloud Foundry in un gruppo di risorse
```
ibmcloud resource cf-service-instance-migrate (NOME_ISTANZA_SERVIZIO | ID_ISTANZA_SERVIZIO) [--resource-group-name NOME_GRUPPO_RISORSE | --resource-group-id ID_GRUPPO_RISORSE] [-f, --force]
```

<strong>Prerequisiti</strong>: Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ISTANZA_SERVIZIO o ID_ISTANZA_SERVIZIO (obbligatorio)</dt>
  <dd>Nome o ID dell'istanza del servizio</dd>
  <dt>--resource-group-name</dt>
  <dd>Nome del gruppo di risorse. Questa opzione è esclusiva con '--resource-group-id'. Se non viene specificata alcuna di tali opzioni, viene utilizzato come valore predefinito il gruppo di risorse attualmente di destinazione.</dd>
  <dt>--resource-group-id</dt>
  <dd>ID del gruppo di risorse. Questa opzione è esclusiva con '--resource-group-name'. Se non viene specificata alcuna di tali opzioni, viene utilizzato come valore predefinito il gruppo di risorse attualmente di destinazione.</dd>
  <dt>-f, --force</dt>
  <dd>Migra senza conferma</dd>
</dl>

## ibmcloud resource service-instances
{: #ibmcloud_resource_service_instances}

Elenca le istanze del servizio.
```
ibmcloud resource service-instances [--service-name NOME_SERVIZIO] [--location UBICAZIONE] [--type TIPO_ISTANZA] [-g GRUPPO_RISORSE] [--long] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--service-name <i>NOME_SERVIZIO</i></dt>
  <dd>Nome del servizio di appartenenza</dd>
  <dt>--location <i>UBICAZIONE</i></dt>
  <dd>Filtra per ubicazione</dd>
  <dt>--type <i>TIPO_ISTANZA</i></dt>
  <dd>Il tipo di istanza. Se non specificato, viene utilizzato il tipo `service_instance`, utilizza ALL per elencare tutti i tipi di istanza.</dd>
  <dt>-g <i>GRUPPO_RISORSE</i></dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--long</dt>
  <dd>Mostra dei campi aggiuntivi nell'output</dd>
  <dt>--output <i>FORMATO</i></dt>
  <dd>Specifica il formato di output, al momento è supportato solo JSON. </dd>
</dl>

<strong>Esempi</strong>:

Elenca le istanze del servizio `test-service`:
```
ibmcloud resource service-instances --service-name test-service
```
{: codeblock}

## ibmcloud resource service-instance
{: #ibmcloud_resource_service_instance}

Mostra i dettagli di un'istanza del servizio.

```
ibmcloud resource service-instance (NOME|ID) [--location UBICAZIONE] [--id] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio), esclusivo con ID</dt>
  <dd>Nome dell'istanza del servizio</dd>
  <dt>ID (obbligatorio), esclusivo con NOME</dt>
  <dd>ID dell'istanza del servizio</dd>
  <dt>--location</dt>
  <dd>Filtra per ubicazione</dd>
  <dt>--id</dt>
  <dd>Visualizza l'ID dell'istanza del servizio</dd>
  <dt>--output</dt>
  <dd>Specifica il formato di output, al momento è supportato solo JSON. Questa opzione è esclusiva con '--id'.</dd>
</dl>

<strong>Esempi</strong>:

Mostra i dettagli dell'istanza del servizio `my-service-instance`:
```
ibmcloud resource service-instance my-service-instance
```
{: codeblock}

## ibmcloud resource service-instance-create
{: #ibmcloud_resource_service_instance_create}

Crea un'istanza del servizio.
```
ibmcloud resource service-instance-create NOME (NOME_SERVIZIO | ID_SERVIZIO) NOME_PIANO_SERVIZIO UBICAZIONE [-d, --deployment NOME_DISTRIBUZIONE] [-p, --parameters @FILE_JSON | STRINGA_JSON ] [-g GRUPPO_RISORSE] [--service-endpoints TIPO_ENDPOINT_SERVIZIO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome dell'istanza del servizio</dd>
  <dt>NOME_SERVIZIO o ID_SERVIZIO (obbligatorio)</dt>
  <dd>Nome o ID del servizio. Per elencare le offerte di servizio, utilizza il [comando](/docs/cli/reference/ibmcloud/cli_catalog.html#ibmcloud_catalog_service_marketplace)`ibmcloud catalog service-marketplace`.</dd>
  <dt>NOME_PIANO_SERVIZIO o ID_PIANO_SERVIZIO (obbligatorio)</dt>
  <dd>Nome o ID del piano di servizio</dd>
  <dt>LOCATION (obbligatorio)</dt>
  <dd>Ubicazione o ambiente di destinazione per creare l'istanza del servizio</dd>
  <dt>-d, --deployment <i>NOME_DISTRIBUZIONE</i></dt>
  <dd>Nome della distribuzione</dd>
  <dt>-p, --parameters <i>@FILE_JSON o STRINGA_JSON</i></dt>
  <dd>File JSON o stringa JSON di parametri per creare l'istanza del servizio</dd>
  <dt>-g <i>GRUPPO_RISORSE</i></dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--service-endpoints <i>TIPO_ENDPOINT_SERVIZIO</i></dt>
  <dd>Tipi di endpoint del servizio</dd>
</dl>

<strong>Esempi</strong>:

Crea un'istanza del servizio denominata `my-service-instance` utilizzando il piano di servizio `test-service-plan` del servizio `test-service` nell'ubicazione `eu-gb`:
```
ibmcloud resource service-instance-create my-service-instance test-service test-service-plan eu-gb
```
{: codeblock}

## ibmcloud resource service-instance-update
{: #ibmcloud_resource_service_instance_update}

Aggiorna l'istanza del servizio.
```
ibmcloud resource ( NOME | ID ) [-n, --name NUOVO_NOME] [--service-plan-id ID_PIANO_SERVIZIO] [-p, --parameters @FILE_JSON | STRINGA_JSON ] [-g GRUPPO_RISORSE] [--service-endpoints TIPO_ENDPOINT_SERVIZIO] [-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>Nome (obbligatorio)</dt>
  <dd>Nome dell'istanza del servizio, esclusivo con ID</dd>
  <dt>ID (obbligatorio)</dt>
  <dd>ID dell'istanza del servizio, esclusivo con NOME</dd>
  <dt>-n, --name <i>NUOVO_NOME</i></dt>
  <dd>Nuovo nome dell'istanza del servizio</dd>
  <dt>--service-plan-id <i>ID_PIANO_SERVIZIO</i></dt>
  <dd>Nuovo ID del piano di servizio</dd>
  <dt>-p, --parameters <i>@FILE_JSON | STRINGA_JSON</i></dt>
  <dd>File JSON o stringa JSON di parametri per creare l'istanza del servizio</dd>
  <dt>-g <i>GRUPPO_RISORSE</i></dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--service-endpoints <i>TIPO_ENDPOINT_SERVIZIO</i></dt>
  <dd>Tipi di endpoint del servizio</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'aggiornamento senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Aggiorna l'istanza del servizio `my-service-instance` e modificane il nome in `new-service-instance`:
```
ibmcloud resource service-instance-update my-service-instance -n new-service-instance
```

## ibmcloud resource service-instance-delete
{: #ibmcloud_resource_service_instance_delete}

Elimina l'istanza del servizio.
```
ibmcloud resource service-instance-delete (NOME|ID) [-f, --force] [--recursive]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>Nome (obbligatorio)</dt>
  <dd>Nome dell'istanza del servizio, esclusivo con ID</dd>
  <dt>ID (obbligatorio)</dt>
  <dd>ID dell'istanza del servizio, esclusivo con NOME</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'eliminazione senza conferma</dd>
  <dt>--recursive</dt>
  <dd>Elimina tutte le risorse di appartenenza</dd>
</dl>

<strong>Esempi</strong>:

Elimina la risorsa service-instance `my-service-instance`:
```
ibmcloud resource service-instance-delete my-service-instance
```
{: codeblock}

## ibmcloud resource service-bindings
{: #ibmcloud_resource_service_bindings}

Mostra le associazioni mediante bind all'alias del servizio,
```
ibmcloud resource service-bindings ALIAS_SERVIZIO [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>ALIAS_SERVIZIO (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON.</dd>
</dl>

<strong>Esempi</strong>:

Mostra le associazioni mediante bind delle risorse all'alias del servizio `my-service-alias`:
```
ibmcloud resource bindings my-service-alias
```

## ibmcloud resource service-binding
{: #ibmcloud_resource_service_binding}

Mostra i dettagli di un'associazione mediante bind del servizio.
```
ibmcloud resource service-binding NOME_ALIAS NOME_APPLICAZIONE [--id] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>NOME_APPLICAZIONE</dt>
  <dd>Nome applicazione CloudFoundry</dd>
  <dt>--id</dt>
  <dd>Visualizza solo l'ID. Tutto l'altro output per il bind del servizio viene eliminato. Questa opzione è esclusiva con '--output'.</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON. Questa opzione è esclusiva con '--id'.</dd>
</dl>

<strong>Esempi</strong>:

Mostra i dettagli dell'associazione mediante bind del servizio tra l'alias del servizio `my-service-alias` e l'applicazione `my-app`:
```
ibmcloud resource bindings my-service-alias my-app
```
{: codeblock}

## ibmcloud resource service-binding-create
{: #ibmcloud_resource_service_binding_create}

Crea un'associazione mediante bind del servizio.
```
ibmcloud resource service-binding-create NOME_ALIAS_SERVIZIO NOME_APPLICAZIONE NOME_RUOLO [-n NOME_BIND] [--service-id ID_SERVIZIO] [-p, --parameters @FILE_JSON | TESTO_JSON] [--service-endpoint TIPO_ENDPOINT_SERVIZIO] [-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS_SERVIZIO (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>NOME_APPLICAZIONE (obbligatorio)</dt>
  <dd>Nome applicazione CloudFoundry</dd>
  <dt>NOME_RUOLO (obbligatorio)</dt>
  <dd>Nome del ruolo utente</dd>
  <dt>--service-id <i>ID_SERVIZIO</i></dt>
  <dd>Nome o UUID dell'ID servizio a cui appartiene il ruolo</dd>
  <dt>-p, --parameter <i>@FILE_JSON | TESTO_JSON</i></dt>
  <dd>File JSON o stringa JSON dei parametri</dd>
  <dt>--service-endpoint <i>TIPO_ENDPOINT_SERVIZIO</i></dt>
  <dd>Tipo di endpoint del servizio</dd>
  <dt>-f, --force</dt>
  <dd>Forza la creazione senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Crea un'associazione mediante bind del servizio tra l'alias del servizio `my-service-alias` e l'applicazione `my-app` con il ruolo `Administrator`:
```
ibmcloud resource service-binding-create my-service-alias my-app Administrator
```
{: codeblock}

## ibmcloud resource service-binding-delete
{: #ibmcloud_resource_service_binding_delete}

Elimina un'associazione mediante bind del servizio.
```
ibmcloud resource service-binding-delete ALIAS_SERVIZIO NOME_APPLICAZIONE [-f, --force]
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS_SERVIZIO (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>NOME_APPLICAZIONE</dt>
  <dd>Nome applicazione CloudFoundry</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'eliminazione senza conferma</dd>
</dl>

<strong>Esempi</strong>:
Elimina il bind del servizio tra l'alias di servizio `my-service-alias` e l'applicazione `my-app`:
```
ibmcloud resource service-binding-delete my-service-alias my-app
```
{: codeblock}

## ibmcloud resource service-keys
{: #ibmcloud_resource_service_keys}

Elenca le chiavi di servizio dell'istanza del servizio o dell'alias del servizio.
```
ibmcloud resource service-keys [ --instance-id ID | --instance-name NOME | --alias-id ID | --alias-name NOME ] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--instance-id</dt>
  <dd>ID istanza del servizio</dd>
  <dt>--instance-name</dt>
  <dd>Nome istanza del servizio</dd>
  <dt>--alias-id</dt>
  <dd>ID alias del servizio</dd>
  <dt>--alias-name</dt>
  <dd>Nome alias del servizio</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON.</dd>
</dl>

<strong>Esempi</strong>:

Elenca le chiavi di servizio dell'istanza del servizio `my-service-instance`:
```
ibmcloud resource service-keys --instance-name my-service-instance  [--output FORMATO]
```

## ibmcloud resource service-key
{: #ibmcloud_resource_service_key}

Visualizza i dettagli di qualsiasi numero di chiavi di servizio, dove i primi *n* caratteri del nome della chiave del servizio corrispondono al NOME_CHIAVE fornito.
```
ibmcloud resource service-key (NOME | ID) [-g GRUPPO_RISORSE] [--id] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME</dt>
  <dd>Nome della chiave</dd>
  <dt>ID</dt>
  <dd>ID della chiave</dd>
  <dt>-g</dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--id</dt>
  <dd>Visualizza l'ID della chiave di servizio. Questa opzione è esclusiva con '--output'.</dd>
  <dt>-g GRUPPO_RISORSE</dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>Specifica il formato di output, al momento è supportato solo JSON. Questa opzione è esclusiva con '--id'.</dd>
</dl>

<strong>Esempi</strong>:

Mostra i dettagli delle chiavi di servizio `my-service-key`:
```
ibmcloud resource service-key my-service-key
```
<strong>Esempi</strong>:
mostra i dettagli della chiave di servizio con ID `crn:v1:bluemix:public:cloudantnosqldb:us-south:a/537860630a5ba7115be954e8d5aa5689:cc2a6d6c-8f5e-4038-b975-b09b51d1d8dc:resource-key:9057f12e-fbf5-421d-8865-764422217a79`:

```
ibmcloud resource service-key crn:v1:bluemix:public:cloudantnosqldb:us-south:a/537860630a5ba7115be954e8d5aa5689:cc2a6d6c-8f5e-4038-b975-b09b51d1d8dc:resource-key:9057f12e-fbf5-421d-8865-764422217a79
```

## ibmcloud resource service-key-create
{: #ibmcloud_resource_service_key_create}

Crea una chiave di servizio.
```
ibmcloud resource service-key-create NOME NOME_RUOLO ( --instance-id ID_ISTANZA_SERVIZIO | --instance-name NOME_ISTANZA_SERVIZIO | --alias-id ID_ALIAS_SERVIZIO | --alias-name NOME_ALIAS_SERVIZIO) [--service-id ID_SERVIZIO] [-p, --parameters @FILE_JSON | TESTO_JSON] [-g GRUPPO_RISORSE] [--service-endpoint TIPO_ENDPOINT_SERVIZIO] [-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME (obbligatorio)</dt>
  <dd>Nome della chiave</dd>
  <dt>NOME_RUOLO (obbligatorio)</dt>
  <dd>Nome del ruolo utente</dd>
  <dt>--instance-id <i>ID_ISTANZA_SERVIZIO</i></dt>
  <dd>ID istanza del servizio</dd>
  <dt>--instance-name <i>NOME_ISTANZA_SERVIZIO</i></dt>
  <dd>Nome istanza del servizio</dd>
  <dt>--alias-id <i>ID_ALIAS_SERVIZIO</i></dt>
  <dd>ID alias del servizio</dd>
  <dt>--alias-name <i>NOME_ALIAS_SERVIZIO</i></dt>
  <dd>Nome alias del servizio</dd>
  <dt>--service-id <i>ID_SERVIZIO</i></dt>
  <dd>Nome o UUID dell'ID servizio a cui appartiene il ruolo</dd>
  <dt>-p, --parameters <i>@FILE_JSON | TESTO_JSON</i></dt>
  <dd>File JSON o stringa JSON dei parametri</dd>
  <dt>-g <i>GRUPPO_RISORSE</i></dt>
  <dd>Nome del gruppo di risorse</dd>
  <dt>--service-endpoint <i>TIPO_ENDPOINT_SERVIZIO</i></dt>
  <dd>Tipo di endpoint del servizio</dd>
  <dt>-f, --force</dt>
  <dd>Forza la creazione senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Crea una chiave di servizio denominata `my-service-key` con il ruolo `Administrator` per l'istanza del servizio `my-service-instance`:
```
ibmcloud resource service-key-create my-service-key Administrator --instance-name my-service-instance
```

## ibmcloud resource service-key-update
{: #ibmcloud_resource_service_key_update}

Aggiorna una chiave di servizio.
```
ibmcloud resource service-key-update ( NOME | ID ) [-n, --name NUOVO_NOME] [-g GRUPPO_RISORSE] [-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME | ID</dt>
  <dd>Nome o ID della chiave</dd>
  <dt>-n, --name NUOVO_NOME</dt>
  <dd>Nuovo nome della chiave</dd>
  <dt>-g GRUPPO_RISORSE</dt>
  <dd>ID del gruppo di risorse a cui appartiene la chiave</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'aggiornamento senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Aggiorna una chiave di servizio denominata `my-service-key` e forniscile un nuovo nome `my-service-key-2`:
```
ibmcloud resource service-key-update my-service-key -n my-service-key-2
```

## ibmcloud resource service-key-delete
{: #ibmcloud_resource_service_key_delete}

Elimina una chiave di servizio.
```
ibmcloud resource service-key-delete ( NOME_CHIAVE | ID_CHIAVE ) [-f, --forece]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_CHIAVE | ID_CHIAVE</dt>
  <dd>Il nome o l'ID della chiave</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'eliminazione senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Elimina la chiave di servizio `my-service-key`:
```
ibmcloud resource service-key-delete my-service-key
```

## ibmcloud resource service-aliases
{: #ibmcloud_resource_service_aliases}

Elenca gli alias per un'istanza del servizio.
```
ibmcloud resource service-aliases [ --instance-id ID | --instance-name NOME ] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--instance-id</dt>
  <dd>ID dell'istanza del servizio di appartenenza.</dd>
  <dt>--instance-name</dt>
  <dd>Nome dell'istanza del servizio di appartenenza.</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON.</dd>
</dl>

<strong>Esempi</strong>:

Elenca gli alias del servizio per l'istanza del servizio `my-service-instance`:
```
ibmcloud resource service-aliases my-service-instance
```

## ibmcloud resource service-alias
{: #ibmcloud_resource_service_alias}

Mostra i dettagli di un alias del servizio.
```
ibmcloud resource service-alias NOME_ALIAS [--id] [--output FORMATO]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>--id</dt>
  <dd>Visualizza solo l'ID dell'alias del servizio fornito. Tutto l'altro output per l'alias viene eliminato. Questa opzione è esclusiva con '--output'.</dd>
  <dt>--output FORMATO (facoltativo)</dt>
  <dd>--output valore  Specifica il formato di output, al momento è supportato solo JSON. Questa opzione è esclusiva con '--id'.</dd>
</dl>

<strong>Esempi</strong>:

Mostra i dettagli dell'alias del servizio `my-service-alias`:
```
ibmcloud resource service-alias  my-service-alias
```

## ibmcloud resource service-alias-create
{: #ibmcloud_resource_service_alias_create}

Crea un alias di un'istanza del servizio.
```
ibmcloud resource service-alias-create NOME_ALIAS ( --instance-id ID | --instance-name NOME ) [-s NOME_SPAZIO] [-t, --tags TAG] [-p, --parameters @FILE_JSON | TESTO_JSON]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>--instance-id</dt>
  <dd>ID dell'istanza del servizio di appartenenza.</dd>
  <dt>--instance-name</dt>
  <dd>Nome dell'istanza del servizio di appartenenza.</dd>
  <dt>-s</dt>
  <dd>Nome dello spazio in cui l'alias viene creato. Il valore predefinito è lo spazio corrente.</dd>
  <dt>-t, --tags</dt>
  <dd>Elenco delle tag.</dd>
  <dt>-p, --parameters</dt>
  <dd>File JSON o stringa JSON dei parametri.</dd>
</dl>

<strong>Esempi</strong>:

Crea un alias del servizio denominato `my-service-alias` dell'istanza del servizio `my-service-instance`:
```
ibmcloud resource service-alias-create my-service-alias --instance-name my-service-instance
```

## ibmcloud resource service-alias-update
{: #ibmcloud_resource_service_alias_update}

Aggiorna un alias del servizio.
```
ibmcloud resource service-alias-update NOME_ALIAS [-n, --name NUOVO_NOME] [-t, --tags TAG] [-p, --parameters @FILE_JSON | STRINGA_JSON ][-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>-n, --name</dt>
  <dd>Nuovo nome dell'alias del servizio.</dd>
  <dt>-t, --tags</dt>
  <dd>Elenco delle tag.</dd>
  <dt>-p, --parameters</dt>
  <dd>File JSON o stringa JSON dei parametri.</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'aggiornamento senza conferma dell'utente.</dd>
</dl>

<strong>Esempi</strong>:

Aggiorna l'alias del servizio `my-service-alias` e modificane il nome in `new-service-alias`:
```
ibmcloud resource service-alias-update my-service-alias -n new-service-alias
```

## ibmcloud resource service-alias-delete
{: #ibmcloud_resource_service_alias_delete}

Elimina un alias del servizio.
```
ibmcloud resource service-alias-delete NOME_ALIAS [-f, --force]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
<dl>
  <dt>NOME_ALIAS (obbligatorio)</dt>
  <dd>Nome dell'alias del servizio</dd>
  <dt>-f, --force</dt>
  <dd>Forza l'eliminazione senza conferma</dd>
</dl>

<strong>Esempi</strong>:

Elimina l'alias del servizio `my-service-alias`:
```
ibmcloud resource service-alias-delete my-service-alias
```

## ibmcloud resource search
{: #ibmcloud_resource_search}

Cerca le risorse utilizzando la sintassi di query Lucene.
```
ibmcloud search QUERY_LUCENE [-o, --offset OFFSET] [-l, --limit LIMITE] [-s, --sort-by (name, family, region, type, crn)] [-p, --provider PROVIDER]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
<dl>
  <dt>-o, -offset</dt>
  <dd>Avvio numero posizione risorsa</dd>
  <dt>-l, -limit</dt>
  <dd>Numero di risorse da restituire (massimo 10000)</dd>
  <dt>-s, --sort-by</dt>
  <dd>Proprietà in base a cui ordinare. Gli input accettati sono `name`, `family`, `region`, `type`, `crn`.</dd>
  <dt>-p, --provider</dt>
  <dd>Visualizza le risorse dell'infrastruttura classica; il solo valore consentito è: classic-infrastructure</dd>
</dl>

<strong>Attributi ricercabili</strong>:
Puoi cercare i seguenti attributi:

<dl>
  <dt>name</dt>
  <dd>Il nome definito dall'utente della risorsa.</dd>
  <dt>region</dt>
  <dd>L'ubicazione geografica dove viene eseguito il provisioning della risorsa. Ad esempio: us-south, us-east, au-syd, eu-gb, eu-de, and jp-tok.</dd>
  <dt>service_name</dt>
  <dd>Il nome del servizio come si presenta nella colonna Name dell'output di 'ibmcloud catalog service-marketplace'.</dd>
  <dt>family</dt>
  <dd>Il componente cloud a cui appartiene la tua risorsa. I valori consentiti sono cloud_foundry, containers,  resource_controller, vmware o ims.</dd>
  <dt>organization_id</dt>
  <dd>Il GUID organizzazione Cloud Foundry.</dd>
  <dt>doc.space_id</dt>
  <dd>Il GUID spazio Cloud Foundry.</dd>
  <dt>doc.resource_group_id</dt>
  <dd>L'ID del gruppo di risorse.</dd>
  <dt>type</dt>
  <dd>Il tipo di risorsa. I valori consentiti sono k8-cluster, cf-service-instance, cf-user-provided-service-instance, cf-organization, cf-service-binding, cf-space, cf-application, resource-instance, resource-alias, resource-binding, resource-group, vmware-solutions, cloud-objects-storage-infrastructure, block-storage, file-storage, cloud-backup.</dd>
  <dt>creation_date</dt>
  <dd>La data in cui viene creata la risorsa.</dd>
  <dt>modification_date</dt>
  <dd>La data dell'ultima modifica della risorsa. È nel formato aaaa-mm-ggThh:mm:ssZ </dd>
  <dt>_objectType</dt>
  <dd>Il tipo della risorsa dell'infrastruttura classica. I valori consentiti sono SoftLayer_Virtual_DedicatedHost, SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress, SoftLayer_Network_Vlan, SoftLayer_Network_Vlan_Firewall and SoftLayer_Virtual_Guest. </dd>
  <dt>tags, tagReferences.tag.name</dt>
  <dd>La tag collegata a una risorsa. Utilizza tagReferences.tag.name quando cerchi le tag collegate alle risorse dell'infrastruttura classica </dd> 
</dl>

<strong>Esempi</strong>:

Cerca le applicazioni Cloud Foundry il cui nome inizia con uno testo specifico: 
```
ibmcloud resource search "name:my* AND type:cf-application"
```

Ricerca le istanze del servizio Cloud Foundry del servizio del nome servizio specificato:
```
ibmcloud resource search "service_name:messagehub AND type:cf-service-instance"
```

Ricerca i bind del servizio Cloud Foundry nell'organizzazione con l'ID specificato:
```
ibmcloud resource search "organization_guid:5b82c134-afb3-4f69-b1e0-3cbe4a13a205 AND type:cf-service-binding"
```

Ricerca gli spazi Cloud Foundry con il nome specificato e ubicati in una delle due regioni specificate:
```
ibmcloud resource search "name:dev AND type:cf-space AND region:(us-south OR eu-gb)"
```

Ricerca le risorse il cui nome contiene la parola dev nello spazio Cloud Foundry con l'ID specificato:
```
ibmcloud resource search "name:*dev* AND doc.space_guid:a07181ca-f917-4ee6-af22-b2c0c2a2d5d7"
```

Ricerca le risorse del controller delle risorse nell'ubicazione specificata (ad esempio la regione us-south):
```
ibmcloud resource search "region:us-south AND family:resource_controller"
```

Ricerca le risorse o gli alias nel gruppo di risorse con l'ID specificato:
```
ibmcloud resource search "(type:resource-instance OR type:resource-alias) AND (doc.resource_group_id:c900d9671b235c00461c5e311a8aeced)"
```

Ricerca i gruppi di risorse con il nome predefinito:
```
ibmcloud resource search "name:default AND type:resource-group"
```

Ricerca i bind della risorsa per il nome servizio specificato:
```
ibmcloud resource search "service_name:cloud-object-storage AND type:resource-binding"
```

Ricerca una risorsa con il CRN (Cloud Resource Name) specificato:
```
ibmcloud resource search "crn:\"crn:v1:bluemix:public:cloudantnosqldb:us-south:s/4948af7e-cc78-4321-998a-e549dd5e9210:41a031cd-e9e5-4c46-975d-9e4a6391322e:cf-service-instance:\""
```

Ricerca una risorsa con la tag specificata:
```
ibmcloud resource search "tags:\"mykey:myvalue\""
```
{: codeblock}

Cerca la risorsa Virtual Guest dell'infrastruttura classica con l'ID specificato (solo con -p classic-infrastructure):
```
ibmcloud resource search "id:12345678 _objectType:SoftLayer_Virtual_Guest"
```
{: codeblock}

Cerca la risorsa hardware dell'infrastruttura classica con il nome tag specificato (solo con -p classic-infrastructure):
```
ibmcloud resource search "tagReferences.tag.name:name _objectType:SoftLayer_Hardware"
```
{: codeblock}

## ibmcloud resource tags
{: #ibmcloud_resource_tags}

Elenca tutte le tag nel tuo account di fatturazione

```
ibmcloud resource tags [-o, --offset OFFSET] [-l, --limit LIMITE] [-p, --provider classic-infrastructure] [-d, --details true]
```
<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
<dl>
  <dt>-o, -offset</dt>
  <dd>Numero della posizione della tag iniziale</dd>
  <dt>-l, -limit</dt>
  <dd>Numero di tag da restituire (massimo 1000, valore predefinito 100)</dd>
  <dt>-p; --provider</dt> 
  <dd>Specifica classic-infrastructure quando cerchi le tag dell'infrastruttura classica</dd>
  <dt>-d, --details</dt>
  <dd>Mostra il numero di risorse con tag.</dd>
</dl>


## ibmcloud resource tag-attach
{: #ibmcloud_resource_tag_attach}

Collega una o più tag a una risorsa:
```
ibmcloud resource tag-attach --tag-names TAG_NAMES (--resource-name NAME | --resource-id RESOURCE_ID ) [--resource-type RESOURCE_TYPE]
```
<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--tag-names (obbligatorio)</dt>
  <dd>Elenco separato da virgole di nomi di tag</dd>
  <dt>--resource-name</dt>
  <dd>Il nome della risorsa a cui devono essere collegate le tag. Questa opzione non può essere utilizzata con le risorse dell'infrastruttura classica. </dd>
  <dt>--resource-id</dt>
  <dd>Il CRN della risorsa a cui verranno collegate le tag; per le risorse dell'infrastruttura classica, è l'ID della risorsa. Puoi ottenere il CRN o l'ID della risorsa utilizzando il comando 'ibmcloud resource search'.</dd>
  <dt>--resource-type</dt>
  <dd>Il tipo della risorsa dell'infrastruttura classica a cui verranno collegate le tag; questo parametro è obbligatorio se si collega una tag a una risorsa dell'infrastruttura classica. I valori possibili per --resource-type sono: SoftLayer_Virtual_DedicatedHost, SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress, SoftLayer_Network_Vlan, SoftLayer_Network_Vlan_Firewall e SoftLayer_Virtual_Guest. </dd>
</dl>

<strong>Esempi</strong>:

* Per collegare la tag `MyTag` a un cluster Kubernetes denominato `MyCluster`, per prima cosa cerca il CRN del cluster a cui vuoi applicare la tag:
  ```
  ibmcloud resource search 'type:k8\-cluster AND name:MyCluster'
  ```
  {: codeblock}

  Prendi nota del CRN, che è una stringa simile al seguente esempio: 
  ```
  crn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a::
  ```
  {: screen}

  Per collegare la tag, immetti il seguente comando:
  ```
  ibmcloud resource tag-attach --tag-names MyTag --resource-id rn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a:: 
  ```
  {: codeblock}

* Per collegare la tag `MyTag` ai nomi della risorsa `MyResource`:
  ```
  ibmcloud resource tag-attach --tag-name MyTag --resource-name  'MyResource'
  ```
  {: codeblock}
  
  
* Per collegare la tag `MyTag` a un guest virtuale dell'infrastruttura classica denominato `MyVM`, per prima cosa cerca l'ID del guest virtuale a cui vuoi applicare la tag:
  ```
  ibmcloud resource search 'fullyQualifiedDomainName:MyVM  _objectType:SoftLayer_Virtual_Guest' -p classic-infrastructure
  ```
  {: codeblock}

  Prendi nota dell'ID, che è una stringa simile a `48373549`.

  Per collegare la tag, immetti il seguente comando:
  ```
  ibmcloud resource tag-attach --tag-names MyTag --resource-id 48373549 --resource-type SoftLayer_Virtual_Guest  
  ```
  {: codeblock}

## ibmcloud resource tag-detach
{: #ibmcloud_resource_tag_detach}

Scollegamento di una o più tag da una risorsa:
```
ibmcloud resource tag-detach  --tag-names TAG_NAMES (--resource-name NAME | --resource-id RESOURCE_ID ) [--resource-type RESOURCE_TYPE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--tag-names (obbligatorio)</dt>
  <dd>Elenco separato da virgole di nomi di tag</dd>
  <dt>--resource-name</dt>
  <dd>Il nome della risorsa da cui devono essere scollegate le tag. Questa opzione non può essere utilizzata con le risorse dell'infrastruttura classica. </dd>
  <dt>--resource-id</dt>
  <dd>Il CRN della risorsa da cui verranno scollegate le tag; per le risorse dell'infrastruttura classica, è l'ID della risorsa. Puoi ottenere il CRN o l'ID della risorsa utilizzando il comando 'ibmcloud resource search'.</dd>
  <dt>--resource-type</dt>
  <dd>Il tipo della risorsa dell'infrastruttura classica da cui verranno scollegate le tag; questo parametro è obbligatorio se si collega una tag a una risorsa dell'infrastruttura classica. I valori possibili per --resource-type sono: SoftLayer_Virtual_DedicatedHost, SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress, SoftLayer_Network_Vlan, SoftLayer_Network_Vlan_Firewall e SoftLayer_Virtual_Guest. </dd>
</dl>


## ibmcloud resource tag-delete
{: #ibmcloud_resource_tag_delete}

Eliminazione di una tag:
```
ibmcloud resource tag-delete --tag-name NOME_TAG [-p, --provider PROVIDER]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
<dl>
  <dt>--tag-name (obbligatorio)</dt>
  <dd>Il nome della tag da eliminare.</dd>
  <dt>-p; --provider</dt> 
  <dd>Specifica classic-infrastructure quando elimini una tag dell'infrastruttura classica</dd>
</dl>

Una tag può essere eliminata solo se non è collegata ad alcuna risorsa.
