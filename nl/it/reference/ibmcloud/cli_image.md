---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, ibmcloud sl image, manage compute images, create compute image cli, compute image cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Creazione, modifica ed eliminazione di immagini di calcolo
{: #sl-manage-compute-images}

Utilizza i seguenti comandi per gestire le immagini di calcolo {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl image delete
{: #sl_image_delete}

Elimina un'immagine.
```
ibmcloud sl image delete IDENTIFICATIVO
```

**Esempi**:
```
ibmcloud sl image delete 12345678
```

Questo comando elimina l'immagine con ID `12345678`.

## ibmcloud sl image detail
{: #sl_image_detail}

Ottieni i dettagli per un'immagine.
```
ibmcloud sl image detail IDENTIFICATIVO
```

**Esempi**:
```
 ibmcloud sl image detail 12345678
```

Questo comando ottiene i dettagli per l'immagine con ID `12345678`.

## ibmcloud sl image edit
{: #sl_image_edit}

Modifica i dettagli di un'immagine.
```
ibmcloud sl image edit IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--name</dt>
<dd>Nome dell'immagine.</dd>
<dt>--note</dt>
<dd>Nota supplementare per l'immagine.</dd>
<dt>--tag</dt>
<dd>Le tag per l'immagine.</dd>
</dl>

*Esempi**:
```  
ibmcloud sl image edit 12345678 --name ubuntu16 --note testing --tag staging
```

Questo comando modifica l'immagine con ID `12345678` e imposta il suo nome su `ubuntu16`, la nota su `testing` e la tag su `staging`.

## ibmcloud sl image list
{: #sl_image_list}

Elenca tutte le immagini per il tuo account.
```
ibmcloud sl image list [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--name</dt>
<dd>Filtra il nome dell'immagine.</dd>
<dt>--public</dt>
<dd>Visualizza solo le immagini pubbliche.</dd>
<dt>--private</dt>
<dd>Visualizza solo le immagini private.</dd>
</dl>
