---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: cli, sdk generator, open api, ibmcloud sdk, ibmcloud sdk generate, generate, sdk validate, sdk list, cloud foundry, rest api 

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Générateur de SDK
{: #sdk-cli}

Le plug-in {{site.data.keyword.IBM}} SDK Generator peut être installé dans [l'interface de ligne de commande](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) {{site.data.keyword.cloud_notm}}.

En tant que développeur sous {{site.data.keyword.cloud_notm}}, vous pouvez utiliser ce plug-in pour générer des SDK depuis votre définition d'API REST conforme à la [spécification Open API ](https://www.openapis.org/){: new_window} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe"). Lorsque vous apportez des modifications à votre définition d'API REST, vous pouvez utiliser ce plug-in pour ne régénérer que le SDK au lieu de régénérer l'ensemble du projet.

Vous pouvez aussi voir si vos applications Cloud Foundry dans un espace donné disposent de définitions d'API REST valides pour la génération de SDK. Enfin, vous pouvez
utiliser le plug-in de générateur de SDK {{site.data.keyword.IBM_notm}} pour
valider les définitions d'API REST afin de vous assurer qu'elles sont conformes aux
exigences du générateur de SDK.

Ce plug-in de générateur de SDK {{site.data.keyword.IBM_notm}}
vous permet d'intégrer facilement vos services de back end à votre application avec un SDK généré. Lorsqu'un changement se produit dans une API REST, vous pouvez générer à nouveau le SDK et remplacer l'ancien pour une mise à niveau transparente du SDK. Vous pouvez également intégrer l'interface de ligne de commande dans un pipeline devops et vous assurer que le SDK est toujours cohérent avec la spécification d'API chaque fois que l'application est générée.

La définition d'API REST doit être valide et hébergée sur un noeud final de serveur opérationnel de votre système. Si la définition d'API REST est hébergée, l'URL relative doit être définie dans la variable d'environnement `OPENAPI_SPEC`.

## Exigences
{: #prereqs}

Vérifiez que vous répondez bien aux exigences suivantes :

* Vous disposez d'un compte [{{site.data.keyword.cloud_notm}}](https://{DomainName}/login){: new_window} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe").
* Vous disposez d'une définition d'API valide conforme à la spécification [Open API ](https://www.openapis.org/){: new_window} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe").

## Installation
{: #sdk-installation}

Installez les [{{site.data.keyword.cloud_notm}}outils de développement](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

## Commandes
{: #commands}

Utilisez les commandes ci-après pour générer un SDK, valider des fichiers de définition Open API ou répertorier les applications Cloud Foundry.

### Génération d'un SDK
{: #gen}

Utilisez `ibmcloud sdk generate [arguments...] [command options]`.

#### Arguments
{: #gen-args}

* `APP_NAME` - nom de l'application Cloud Foundry dans votre
espace en cours
* `OPENAPI_DOC_LOCATION` - URL ou chemin d'accès relatif au fichier de définition d'API REST brut JSON ou Yaml
* `GENERATED_SDK_NAME` (facultatif) - nom du SDK généré


#### Options
{: #gen-options}

* `PLATFORM` (requis)
   * `--android` - génère un SDK Android
   * `--ios` - génère un SDK Swift iOS
   * `--swift` - generate a Swift server SDK
   * `--js` - génère un SDK JavaScript
* `LOCATION` (requis) - spécifie le type pour `OPENAPI_DOC_LOCATION`
   * `-r` - adresse URL distante
   * `-f` - fichier
   * `-a` - application s'exécutant dans {{site.data.keyword.cloud_notm}}
   * `-l` - adresse URL de localhost
* `--output "YOUR_RELATIVE_PATH"` (facultatif) - place le SDK généré dans le répertoire qui est spécifié par `YOUR_RELATIVE_PATH` (remplace le SDK existant, le cas échéant)
* `--unzip` (facultatif) - extrait le SDK généré (remplace les artefacts de SDK existants, le cas échéant)


#### Syntaxe
{: #gen-usage}

Pour générer un SDK depuis une application Cloud Foundry qui s'exécute dans
{{site.data.keyword.cloud_notm}}, vous pouvez utiliser le nom de l'application en tant que paramètre dans l'interface de ligne de commande de l'application. La
commande suivante utilise le nom de l'application comme nom de SDK `SDK_Name`.

```
ibmcloud sdk generate [APP_NAME] [LOCATION] [PLATFORM]
```
{: codeblock}

Pour générer un SDK depuis une URL dans un fichier de définition Open API ou un fichier yaml ou JSON local, utilisez la commande suivante :

```
ibmcloud sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [LOCATION] [PLATFORM]
```
{: codeblock}


### Validation des définitions Open API
{: #validating}

Utilisez `ibmcloud sdk validate [argument]`.


#### Arguments
{: #val-args}

* `APP_NAME` - nom de l'application Cloud Foundry dans votre
espace en cours
* `OPENAPI_DOC_LOCATION` - URL ou chemin d'accès relatif au fichier de définition d'API REST brut JSON ou Yaml


#### Syntaxe
{: #val-usage}

Pour valider une spécification d'API d'une application Cloud Foundry qui s'exécute dans {{site.data.keyword.cloud_notm}}, vous pouvez utiliser le nom de l'application en tant que paramètre dans l'interface de ligne de commande de l'application.

```
ibmcloud sdk validate [APP_NAME] [LOCATION]
```
{: codeblock}

Pour valider un SDK depuis l'URL dans un document de spécification d'API ou un fichier yaml ou JSON local, utilisez la commande suivante.

```
ibmcloud sdk validate [OPENAPI_DOC_LOCATION] [LOCATION]
```
{: codeblock}



### Liste des applications (Cloud Foundry)
{: #list-apps}

Utilisez `ibmcloud sdk list [argument] [option]` pour répertorier les applications et valider les spécifications d'API. La variable d'environnement `OPENAPI_SPEC` doit être définie par rapport au chemin de l'URL relative hébergeant votre spécification.


#### Arguments
{: #list-args}

* `SPACE_NAME` (facultatif) - nom de l'espace Cloud
Foundry dans votre organisation en cours dans lequel vous voulez rechercher des
applications. Si aucune valeur n'est fournie, l'espace en cours est exploré.


#### Options
{: #list-options}

* `--url` (facultatif) - pour afficher une URL complète dans la définition Open API pour chaque application de la liste.


#### Syntaxe
{: #list-usage}

Pour répertorier les applications de l'espace en cours, utilisez la commande
suivante :

```
ibmcloud sdk list
```
{: codeblock}

Pour répertorier les applications de l'espace en cours et afficher l'URL de
spécification d'API, utilisez la commande suivante :

```
ibmcloud sdk list --url
```
{: codeblock}

Pour répertorier les applications d'un espace spécifique, utilisez la commande suivante.

```
ibmcloud sdk list [SPACE_NAME]
```
{: codeblock}

Pour répertorier les applications d'un espace spécifique et afficher L'URL de spécification d'API, utilisez la commande suivante.

```
ibmcloud sdk list [SPACE_NAME] --url
```
{: codeblock}
