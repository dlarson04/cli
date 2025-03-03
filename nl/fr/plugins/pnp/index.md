---

copyright:
  years: 2016, 2018
lastupdated: "2019-03-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Plug-in d'appairage de réseau privé pour l'interface de ligne de commande {{site.data.keyword.cloud_notm}}
{: #private_network_cli}

Utilisez l'interface de ligne de commande d'appairage de réseau privé pour configurer et gérer l'appairage de réseau privé entre deux espaces {{site.data.keyword.cloud}}. L'appairage de réseau privé est pris en charge pour IBM Containers (conteneurs Docker). Les espaces {{site.data.keyword.cloud_notm}} peuvent se trouver dans des zones de disponibilité différentes dans une même région ou dans différentes régions. Le plug-in d'interface de ligne de commande d'appairage de réseau privé peut être utilisé avec le plug-in d'interface de ligne de commande {{site.data.keyword.cloud_notm}}.

Le plug-in d'interface de ligne de commande d'appairage de réseau privé est disponible pour les systèmes d'exploitation Windows, MAC et Linux. Assurez-vous d'utiliser le plug-in qui vous convient.

Avant de commencer, créez des espaces {{site.data.keyword.cloud_notm}}. Assurez-vous que chaque conteneur dans un espace dispose d'une adresse IP provenant d'un réseau différent.

**Remarque :** si vous avez utilisé l'appairage de réseau privé avec un espace {{site.data.keyword.cloud_notm}} et devez supprimer l'espace, supprimez d'abord les connexions d'appairage de réseau privé dans cet espace.

Pour commencer, installez l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Pour plus d'informations, voir [Interface de ligne de commande IBM Cloud](/docs/cli?topic=cloud-cli-ibmcloud-cli).

## Installation du plug-in d'interface de ligne de commande d'appairage de réseau privé

**Remarque** : si une version précédente du plug-in est installée, vous devez la désinstaller. Utilisez la commande suivante pour désinstaller le plug-in :
```
ibmcloud plugin uninstall private-network-peering
```
{: codeblock}

### Installation locale
Téléchargez le plug-in d'appairage de réseau privé pour votre plateforme depuis le [référentiel de plug-in d'interface de ligne de commande {{site.data.keyword.cloud_notm}}](https://plugins.cloud.ibm.com/ui/repository.html){: new_window} ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe").

Installez le plug-in d'appairage de réseau privé avec la commande suivante :

**Remarque** : placez-vous à l'emplacement du plug-in ou spécifiez le chemin d'accès à l'emplacement du plug-in.

* Pour le système d'exploitation Microsoft Windows :
```
ibmcloud plugin install private-network-peering-windows-amd64.exe
```
{: codeblock}

* Pour le système d'exploitation MAC OS :
```
ibmcloud plugin install private-network-peering-darwin-amd64
```
{: codeblock}

* Pour le système d'exploitation Linux :
```
ibmcloud plugin install private-network-peering-linux-amd64
```
{: codeblock}

**Remarque** : lorsque vous installez le plug-in pour le système d'exploitation Linux, si un message d'erreur signale que vous ne disposez pas des droits appropriés, exécutez la commande suivante et changez les droits :
```
chmod a+x ./private-network-peering-linux-amd64
```
{: codeblock}

### Installation depuis le référentiel {{site.data.keyword.cloud_notm}}

Pour installer le plug-in depuis le référentiel {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. Ajoutez le noeud final de registre de plug-in {{site.data.keyword.cloud_notm}} :
	```
	ibmcloud plugin repo-add IBMCloud http://plugins.cloud.ibm.com
	```
	{: codeblock}

2. Exécutez la commande suivante :
	```
	ibmcloud plugin install private-network-peering -r IBMCloud
	```
	{: codeblock}

## Liste des commandes d'appairage de réseau privé
Les commandes ci-après sont prises en charge. Utilisez la commande `ibmcloud network` pour consulter la liste des commandes disponibles :

| Commande     | Description                                    |
|-------------|------------------------------------------------|
| pnp-routers | Liste de tous les routeurs disponibles pour l'appairage        |
| pnp-create  | Crée une connexion d'appairage de réseau privé   |
| pnp-delete  | Supprime une connexion d'appairage de réseau privé   |
| pnp-show    | Répertorie toutes les connexions d'appairage de réseau privé  |
{: caption="Tableau 1. Commandes d'appairage de réseau privé" caption-side="top"}


### Syntaxe de la commande
Pour afficher les informations d'aide sur les commandes, exécutez : `ibmcloud network [commande] -h`.

#### Liste de tous les routeurs disponibles pour l'appairage
```
ibmcloud network pnp-routers [--verbose (ou -v)]
```

#####Paramètres facultatifs
{: #op1}

* **--verbose (ou -v)** (indicateur) : affichez les informations de réseau détaillées pour chaque routeur.

######Exemple de commande
{: #ex1}

Afin d'afficher les informations réseau pour tous les routeurs :

$ ibmcloud network pnp-routers
	Listing available routers ...
	OK

IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3

Afin d'afficher les informations réseau détaillées pour tous les routeurs :

$ ibmcloud network pnp-routers -v
	Listing available routers ...
	OK

Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
FIELD          VALUE
IP             129.41.234.246
Name           default-router
Compute        Container
Region         US-South
Organization   ywu@us.ibm.com
Space          demo1
Networks       172.31.0.0/16

Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
FIELD          VALUE
IP             129.41.237.172
Name           default-router
Compute        Container
Region         US-South
Organization   ywu@us.ibm.com
Space          demo2
Networks       172.25.0.0/16
...


#### Création d'une connexion d'appairage de réseau privé en utilisant les adresses IP
```
ibmcloud network pnp-create <router_ip> <router_ip> <name>
```

#####Paramètres
{: #p1}

* **router_ip** : adresses IP des deux routeurs à connecter. Vous pouvez les identifier avec la commande suivante : `ibmcloud network pnp-routers`
* **nom** : nom de la connexion d'appairage de réseau privé.

######Exemple de commande
{: #ex2}

$ ibmcloud network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
OK

Private network peering connection 'demo' created.


####Création d'une connexion d'appairage de réseau privé avec le nom de connexion

```
ibmcloud network pnp-create -i <nom>
```

#####Paramètres
{: #p2}

* **--interactive (-i)** (indicateur) : mode interactif pour sélectionner les routeurs.
* **nom** : nom de la connexion d'appairage de réseau privé.

######Exemple de commande
{: #ex3}

$ ibmcloud network pnp-create -i demo
	Creating private network peering connection 'demo' ...
List of available routers (select TWO for peering):

#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

Select first router for peering> 1
	Select second router for peering> 2

Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
OK

Private network peering connection 'demo' created.


#### Liste de toutes les connexions d'appairage de réseau privé
```
ibmcloud network pnp-show [--verbose (ou -v)]
```

#####Paramètres facultatifs
{: #op2}

* **--verbose (ou -v)** (indicateur) : affichez les informations de réseau détaillées pour chaque routeur.

######Exemple de commande
{: #ex4}

Affichez les informations de base :

$ ibmcloud network pnp-show
	Listing private network peering connections ...
	OK

ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

Affichez les informations détaillées :

$ ibmcloud network pnp-show -v
	Listing private network peering connections ...
	OK

Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
FIELD              VALUE
Name               demo
Status             Active
Router1 IP         129.41.234.246
Router1 Networks   172.31.0.0/16
Router2 Name       default-router
Router2 IP         129.41.237.172
Router2 Networks   172.25.0.0/16

#### Suppression d'une connexion d'appairage de réseau privé
```
ibmcloud network pnp-delete [--force (or -f)] <connection_id>
```
#####Paramètres
{: #p3}
* **connection_id** : un ou plusieurs ID de connexion séparés par une virgule.

#####Paramètres facultatifs
{: #op3}

* **--force (ou -f)** (indicateur) : supprime la connexion sans demander confirmation.

######Exemple de commande :
{: #ex5}

Supprimez une connexion :

$ ibmcloud network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
Are you sure you want to delete the connection? (yes/no)> yes

Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
OK

Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.

Supprimez plusieurs connexions :
```
ibmcloud network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
