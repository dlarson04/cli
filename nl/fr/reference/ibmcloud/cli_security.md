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

# Gestion des certificats SSL et des clés SSH de sécurité
{: #sl-manage-security-keys}

Les clés SSH permettent d'accéder à un appareil sans utiliser le mot de passe des clients correspondants pour chaque clé publique implémentée sur l'appareil. En ajoutant une clé SSH à un appareil, l'appareil fourni avec la clé SSH accède à l'appareil associé à la clé sans recourir à l'utilisation d'un mot de passe.

Les certificats SSL sont utilisés par les sites Web comme mesure de sécurité pour protéger l'utilisateur. Ils sont généralement utilisés lorsque vous devez transmettre des informations confidentielles à un site Web.

Les commandes suivantes permettent de gérer les certificats et les clés SSH de l'infrastructure classique {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl security sshkey-add
{: #sl_security_sshkey_add}

Permet d'ajouter une nouvelle clé SSH.
```
ibmcloud sl security sshkey-add LABEL [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --in-file</dt>
<dd>Fichier id_rsa.pub à importer pour cette clé.</dd>
<dt>-k, --key</dt>
<dd>Clé SSH réelle.</dd>
<dt>--note</dt>
<dd>Note supplémentaire qui sera associée à la clé.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security sshkey-add -f ~/.ssh/id_rsa.pub --note mykey
```
{: codeblock}

Cette commande ajoute une clé SSH à partir d'un fichier : ~/.ssh/id_rsa.pub with a note "mykey".

## ibmcloud sl security sshkey-edit
{: #sl_security_sshkey_edit}

Permet d'éditer une clé SSH.
```
ibmcloud sl security sshkey-edit IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--label</dt>
<dd>Nouveau libellé de la clé.</dd>
<dt>--note</dt>
<dd>Nouvelles notes pour la clé.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security sshkey-edit 12345678 --label ibmcloud --note testing
```
{: codeblock}

Cette commande met à jour la clé SSH portant l'ID `12345678` et lui affecte l'étiquette `ibmcloud` et la note `testing`.

## ibmcloud sl security sshkey-list
{: #sl_security_sshkey_list}

Permet de répertorier les clés SSH sur votre compte.
```
ibmcloud sl security sshkey-list [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--sortby</dt>
<dd>Options de tri des colonnes : id,label,fingerprint,notes.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security sshkey-list --sortby label
```
{: codeblock}

Cette commande répertorie toutes les clés SSH sur le compte en cours et les trie par libellé.

## ibmcloud sl security sshkey-print
{: #sl_security_sshkey_print}

Permet d'imprimer une clé SSH sur l'écran.
```
ibmcloud sl security sshkey-print IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --out-file</dt>
<dd>La clé SSH publique sera écrite sur ce fichier.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security sshkey-print 12345678 -f ~/mykey.pub
```
{: codeblock}

Cette commande affiche l'ID, le libellé et les notes de la clé SSH portant l'ID 12345678 et écrit la clé publique dans le fichier : ~/mykey.pub.

## ibmcloud sl security sshkey-remove
{: #sl_security_sshkey_remove}

Permet de retirer définitivement une clé SSH.
```
ibmcloud sl security sshkey-remove IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security sshkey-remove 12345678 -f
```
{: codeblock}

Cette commande retire la clé SSH portant l'ID `12345678` sans demander de confirmation.

## ibmcloud sl security cert-add
{: #sl_security_cert_add}

Permet d'ajouter et de télécharger les détails relatifs au certificat SSL.
```
ibmcloud sl security cert-add [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--crt</dt>
<dd>Fichier de certificat.</dd>
<dt>--csr</dt>
<dd>Fichier de demande de signature de certificat.</dd>
<dt>--icc</dt>
<dd>Fichier de certificat intermédiaire.</dd>
<dt>--key</dt>
<dd>Fichier de clé privée.</dd>
<dt>--notes</dt>
<dd>Notes supplémentaires.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security cert-add --crt ~/ibm.com.cert --key ~/ibm.com.key
```
Cette commande ajoute le fichier certificat ~/ibm.com.cert et le fichier de clé privée ~/ibm.com.key pour le domaine ibm.com.

## ibmcloud sl security cert-edit
{: #sl_security_cert_edit}

Permet d'éditer un certificat SSL.
```
ibmcloud sl security cert-edit IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--crt</dt>
<dd>Fichier de certificat.</dd>
<dt>--csr</dt>
<dd>Fichier de demande de signature de certificat.</dd>
<dt>--icc</dt>
<dd>Fichier de certificat intermédiaire.</dd>
<dt>--key</dt>
<dd>Fichier de clé privée.</dd>
<dt>--notes</dt>
<dd>Notes supplémentaires.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security cert-edit 12345678 --key ~/ibm.com.key
```
Cette commande modifie le certificat portant l'ID 12345678 et met à jour sa clé privée avec le fichier ~/ibm.com.key.

## ibmcloud sl security cert-download
{: #sl_security_cert_download}

Permet de télécharger des fichiers de certificat et de clé SSL.
```
ibmcloud sl security cert-download IDENTIFIER
```


**Exemples** :
```
ibmcloud sl security cert-download 12345678
```
Cette commande télécharge 4 fichiers sur le répertoire de travail pour le certificat portant l'ID 12345678. Ces 4 fichiers sont : le fichier certificat, le fichier de demande de signature de certificat, le fichier de certificat intermédiaire et le fichier de clé privée.

## ibmcloud sl security cert-list
{: #sl_security_cert_list}

Permet de répertorier les certificats SSL présents sur votre compte.
```
ibmcloud sl security cert-list [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>--status</dt>
<dd>Afficher les certificats avec ce statut. La valeur par défaut est all, les options possibles sont les suivantes : all,valid,expired.</dd>
<dt>--sortby</dt>
<dd>Options de tri des colonnes : id,common_name,days_until_expire,notes.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security cert-list --status valid --sortby days_until_expire
```
Cette commande répertorie tous les certificats valides sur le compte en cours et les trie par jours de validité.

## ibmcloud sl security cert-remove
{: #sl_security_cert_remove}

Permet de retirer un certificat SSL.
```
ibmcloud sl security cert-remove IDENTIFIER [OPTIONS]
```

<strong>Options de commande</strong> :
<dl>
<dt>-f, --force</dt>
<dd>Forcer l'opération sans qu'aucune confirmation ne soit demandée.</dd>
</dl>

**Exemples** :
```
ibmcloud sl security cert-remove 12345678
```
Cette commande retire le certificat portant l'ID 12345678.
