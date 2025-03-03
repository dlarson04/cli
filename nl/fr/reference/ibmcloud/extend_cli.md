---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-15"

keywords: extend cli, ibmcloud repo-plugins, repo-plugins, plug-in, plugin, ibmcloud cli, ibmcloud, ibmcloud dev, cli, command line, command-line, developer tools, plugin install

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Extension de l'interface de ligne de commande {{site.data.keyword.cloud_notm}} avec des plug-in
{: #plug-ins}

L'interface de ligne de commande {{site.data.keyword.cloud}} prend en charge une structure de plug-in destinée à étendre ses fonctionnalités. Vous pouvez installer un plug-in depuis un référentiel, une URL WEB, ou installer localement un fichier binaire de plug-in.

Le [{{site.data.keyword.cloud_notm}} référentiel de plug-in d'interface de ligne de commande](https://plugins.cloud.ibm.com/ui/repository.html){: new_window} ![Icône de lien externe](../../../icons/launch-glyph.svg) est le référentiel officiel d'hébergement des plug-in.

Pour explorer d'autres commandes de gestion de plug-in, exécutez `ibmcloud plugin` afin d'afficher les messages d'aide.
{: tip}

## Installation d'un plug-in à partir du référentiel de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}
{: #install-from-repo}

### Etape 1 : Rechercher le plug-in
{: #step1-search-plugin}

1. Utilisez la commande `ibmcloud plugin repo-plugins -r REPO_NAME` pour rechercher un plug-in dans le référentiel.
2. Le référentiel officiel de l'interface de ligne de commande {{site.data.keyword.cloud_notm}} est nommé IBM Cloud ; vous pouvez rechercher les plug-in officiels comme indiqué dans l'exemple suivant :
```
ibmcloud plugin repo-plugins -r "IBM Cloud"
```
{: codeblock}

```
Status             Name                                   Versions                       Description   
Update Available   container-service/kubernetes-service   0.2.99, 0.2.95, 0.2.80...      IBM Cloud Kubernetes Service for management of Kubernetes clusters   
Update Available   cloud-functions                        1.0.30, 1.0.29, 1.0.28...      IBM Cloud CLI plug-in for IBM Cloud Functions   
...
```
{: screen}

### Etape 2 : Installer le plug-in
{: step2-install-plugin}

Utilisez la commande `ibmcloud plugin install PLUGIN_NAME -r REPO_NAME` pour installer le plug-in. Par exemple, utilisez la commande suivante pour installer un plug-in à partir du référentiel de plug-in IBM officiel 'IBM Cloud' :

```
ibmcloud plugin install auto-scaling
```
{: codeblock}

```
Looking up 'auto-scaling' from repository 'IBM Cloud'...
Plug-in 'auto-scaling 0.2.7' found in repository 'IBM Cloud'
Attempting to download the binary file...
 7.28 MiB / 7.28 MiB [============================================] 100.00% 1s
7636608 bytes downloaded
Installing binary...
OK
Plug-in 'auto-scaling 0.2.7' was successfully installed into /Users/username/.bluemix/plugins/auto-scaling. Use 'ibmcloud plugin show auto-scaling' to show its details.
```
{: screen}

## Installation locale d'un plug-in
{: #install-plugin-locally}

Utilisez la commande `ibmcloud plugin install LOCAL_FILE_NAME` pour installer un fichier binaire de plug-in sur votre poste local. Par exemple :

```
ibmcloud plugin install ./auto-scaling-darwin-amd64-0.2.7
```
{: codeblock}

```
Installing plugin './auto-scaling-darwin-amd64-0.2.7'...
OK
Plug-in 'auto-scaling 0.2.7' was successfully installed into /Users/username/.bluemix/plugins/auto-scaling. Use 'ibmcloud plugin show auto-scaling' to show its details.
$
```
{: screen}

## Installation d'un plug-in à partir d'une URL Web
{: install-plugin-from-url}

Utilisez la commande `ibmcloud plugin install URL` pour installer un plug-in directement à partir d'une URL Web. Par exemple :
```
ibmcloud plugin install https://plugins.cloud.ibm.com/downloads/bluemix-plugins/auto-scaling/0.2.7/auto-scaling-darwin-amd64-0.2.7
```
{: codeblock}

Sortie :
```
Attempting to download the binary file...
 7.28 MiB / 7.28 MiB [===========================================] 100.00% 0s
7636608 bytes downloaded
Installing binary...
OK
Plug-in 'auto-scaling 0.2.7' was successfully installed into /Users/username/.bluemix/plugins/auto-scaling. Use 'ibmcloud plugin show auto-scaling' to show its details.
$
```
{: screen}
