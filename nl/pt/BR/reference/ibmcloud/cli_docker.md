---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-21"

keywords: cli, docker, docker container, ibmcloud docker, docker run, docker pull, ibmcloud cli, dockerfile, ibmcloud login

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Usando o {{site.data.keyword.dev_cli_notm}} por meio de um contêiner do Docker
{: #using-idt-from-docker}

Com o contêiner do Docker do {{site.data.keyword.dev_cli_notm}}, você obtém a CLI do
{{site.data.keyword.cloud}}, além das ferramentas a seguir:

* `Git`
* `Helm`
* `kubectl`
* `curl`
* Plug-in do {{site.data.keyword.dev_cli_notm}}
* Plug-in do {{site.data.keyword.IBM_notm}} {{site.data.keyword.openwhisk_short}}
* Plug-in do {{site.data.keyword.registrylong_notm}}
* Plug-in do {{site.data.keyword.containerlong_notm}}
* Plug-in do `sdk-gen`

## Antes de começar
{: #idt-docker-prereq}

É necessária uma [conta do {{site.data.keyword.cloud_notm}}](https://{DomainName}/login){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo") e deve-se instalar a versão estável do Docker mais recente antes de executar as etapas a seguir.

## Etapa 1. Puxe a imagem do Docker do hub do Docker.
{: #step1-pull-docker-image}

```
docker pull ibmcom/ibm-cloud-developer-tools-amd64
```
{: codeblock}

## Etapa 2. Inicie o contêiner do Docker.
{: #step2-start-docker}

Use o comando a seguir para iniciar o contêiner do Docker do {{site.data.keyword.dev_cli_notm}}.

```
docker run -ti ibmcom/ibm-cloud-developer-tools-amd64
```
{: codeblock}

## Etapa 3. Efetue login no {{site.data.keyword.cloud_notm}} com o IBMid.
{: #step3-ibmcloud-login}

```
ibmcloud login
```
{: codeblock}

Se as suas credenciais forem rejeitadas, talvez você esteja usando um ID federado. Consulte
[Efetuando login com um ID federado](/docs/iam?topic=iam-federated_id#federated_id) para obter mais detalhes.
{: tip}

O plug-in da CLI do {{site.data.keyword.dev_cli_notm}} usa dois contêineres para facilitar a construção e o teste de seu aplicativo. O primeiro é o contêiner de ferramentas, que contém os utilitários necessários para construir e testar seu app. O `Dockerfile` para esse contêiner é definido pelo parâmetro [`dockerfile-tools`](/docs/cli/idt?topic=cloud-cli-idt-cli#command-parameters). Você pode pensar nele como um contêiner de desenvolvimento, pois ele contém as ferramentas que são normalmente usadas para o desenvolvimento de um tempo de execução específico.

O segundo contêiner é o contêiner de execução, que simula de perto o ambiente de tempo de execução real do aplicativo quando ele é implementado na nuvem. Esse contêiner está em um formato que é adequado para ser implementado para o uso no {{site.data.keyword.cloud_notm}}, por exemplo. Como resultado, é definido um ponto de entrada que inicia seu app. Quando você seleciona a execução do seu app por meio da CLI do Plug-in da CLI do {{site.data.keyword.dev_cli_notm}}, ele usa esse contêiner. O `Dockerfile` para esse contêiner é definido pelo parâmetro
[`dockerfile-run`](/docs/cli/idt?topic=cloud-cli-idt-cli#run-parameters).

Agora você está pronto para usar o {{site.data.keyword.dev_cli_notm}} para gerenciar os recursos do {{site.data.keyword.cloud_notm}}, desenvolver e implementar seus apps.
