---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, security cli, ssh keys cli, ssl cli, ibmcloud sl security, certificate cli, ibmcloud sl, sshkey-add, manage security cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# Gestione di chiavi SSH di sicurezza e certificati SSL
{: #sl-manage-security-keys}

Le chiavi SSH consentono l'accesso a un dispositivo senza utilizzare una password dai client corrispondenti per ogni chiave pubblica implementata sul dispositivo. Aggiungendo una chiave SSH a un dispositivo, il dispositivo a cui è stata fornita la chiave SSH accede al dispositivo per la chiave corrispondente senza l'utilizzo di una password.

I certificati SSL sono abilitati dai siti web come una misura di sicurezza per proteggere l'utente. Sono generalmente utilizzati quando devi trasmettere informazioni riservate a un sito web.

Utilizza i seguenti comandi per gestire i certificati e le chiavi SSH dell'infrastruttura classica {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl security sshkey-add
{: #sl_security_sshkey_add}

Aggiungi un nuova chiave SSH.
```
ibmcloud sl security sshkey-add ETICHETTA [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-f, --in-file</dt>
<dd>Il file id_rsa.pub da importare per questa chiave.</dd>
<dt>-k, --key</dt>
<dd>La chiave SSH effettiva.</dd>
<dt>--note</dt>
<dd>Nota aggiuntiva che verrà associata alla chiave.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security sshkey-add -f ~/.ssh/id_rsa.pub --note mykey
```
{: codeblock}

Questo comando aggiunge una chiave SSH dal file: ~/.ssh/id_rsa.pub con una nota "mykey".

## ibmcloud sl security sshkey-edit
{: #sl_security_sshkey_edit}

Modifica una chiave SSH.
```
ibmcloud sl security sshkey-edit IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--label</dt>
<dd>La nuova etichetta per la chiave.</dd>
<dt>--note</dt>
<dd>Nuove note per la chiave.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security sshkey-edit 12345678 --label ibmcloud --note testing
```
{: codeblock}

Questo comando aggiorna la chiave SSH con ID `12345678` e imposta l'etichetta su `ibmcloud` e la nota su `testing`.

## ibmcloud sl security sshkey-list
{: #sl_security_sshkey_list}

Elenca le chiavi SSH per il tuo account.
```
ibmcloud sl security sshkey-list [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--sortby</dt>
<dd>Colonna in base a cui ordinare; le opzioni sono: id,label,fingerprint,notes.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security sshkey-list --sortby label
```
{: codeblock}

Questo comando elenca tutte le chiavi SSH sull'account corrente e le ordina per etichetta.

## ibmcloud sl security sshkey-print
{: #sl_security_sshkey_print}

Stampa una chiave SSH sulla schermata.
```
ibmcloud sl security sshkey-print IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-f, --out-file</dt>
<dd>La chiave SSH pubblica verrà scritta in questo file.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security sshkey-print 12345678 -f ~/mykey.pub
```
{: codeblock}

Questo comando mostra l'ID, l'etichetta e le note della chiave SSH con ID 12345678 e scrive la chiave pubblica nel file: ~/mykey.pub.

## ibmcloud sl security sshkey-remove
{: #sl_security_sshkey_remove}

Rimuovi permanentemente una chiave SSH.
```
ibmcloud sl security sshkey-remove IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forza l'operazione senza conferma.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security sshkey-remove 12345678 -f
```
{: codeblock}

Questo comando rimuove la chiave SSH con ID `12345678` senza richiedere conferma.

## ibmcloud sl security cert-add
{: #sl_security_cert_add}

Aggiungi e carica i dettagli del certificato SSL.
```
ibmcloud sl security cert-add [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--crt</dt>
<dd>File del certificato.</dd>
<dt>--csr</dt>
<dd>File di richiesta di firma certificato.</dd>
<dt>--icc</dt>
<dd>File del certificato intermedio.</dd>
<dt>--key</dt>
<dd>File della chiave privata</dd>
<dt>--notes</dt>
<dd>Note aggiuntive.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security cert-add --crt ~/ibm.com.cert --key ~/ibm.com.key
```
This command adds certificate file: ~/ibm.com.cert and private key file ~/ibm.com.key for domain ibm.com.

## ibmcloud sl security cert-edit
{: #sl_security_cert_edit}

Modifica il certificato SSL.
```
ibmcloud sl security cert-edit IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--crt</dt>
<dd>File del certificato.</dd>
<dt>--csr</dt>
<dd>File di richiesta di firma certificato.</dd>
<dt>--icc</dt>
<dd>File del certificato intermedio.</dd>
<dt>--key</dt>
<dd>File della chiave privata</dd>
<dt>--notes</dt>
<dd>Note aggiuntive.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security cert-edit 12345678 --key ~/ibm.com.key
```
This command edits certificate with ID 12345678 and updates its private key with file: ~/ibm.com.key.

## ibmcloud sl security cert-download
{: #sl_security_cert_download}

Scarica i file di chiave e i certificati SSL.
```
ibmcloud sl security cert-download IDENTIFICATIVO
```


**Esempi**:
```
ibmcloud sl security cert-download 12345678
```
Questo comando scarica 4 file nella directory corrente per il certificato con ID 12345678. I 4 file sono: il file del certificato, il file della richiesta di firma del certificato, il file del certificato intermedio e il file della chiave privata.

## ibmcloud sl security cert-list
{: #sl_security_cert_list}

Elenca i certificati SSL per il tuo account.
```
ibmcloud sl security cert-list [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>--status</dt>
<dd>Mostra i certificati con questo stato; il valore predefinito è: all; le opzioni sono: all,valid,expired.</dd>
<dt>--sortby</dt>
<dd>Colonna in base a cui ordinare; le opzioni sono: id,common_name,days_until_expire,notes.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security cert-list --status valid --sortby days_until_expire
```
Questo comando elenca tutti i certificati validi sull'account corrente e li ordina per giorni di validità.

## ibmcloud sl security cert-remove
{: #sl_security_cert_remove}

Rimuovi il certificato SSL.
```
ibmcloud sl security cert-remove IDENTIFICATIVO [OPZIONI]
```

<strong>Opzioni del comando</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forza l'operazione senza conferma.</dd>
</dl>

**Esempi**:
```
ibmcloud sl security cert-remove 12345678
```
Questo comando rimuove il certificato con ID 12345678.
