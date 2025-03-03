---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-21"

keywords: cli, IBM Cloud Developer Tools CLI, ibmcloud cli, download cli, ibmcloud dev, cloud cli, dev plugin, dev plug-in, cloud command line, developer tools, dev tools, install cloud cli, getting started cli

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:note: .note}

# Introdução à CLI do {{site.data.keyword.cloud_notm}}
{: #ibmcloud-cli}

Neste tutorial, você instala um conjunto de ferramentas do {{site.data.keyword.cloud}} desenvolvedor, verifica a instalação e configura o ambiente. O {{site.data.keyword.dev_cli_notm}} oferece uma abordagem de linha de comandos para criar, desenvolver e implementar aplicativos em nuvem.
{: shortdesc}

O comando de instalação neste tutorial instala a versão mais recente da CLI do {{site.data.keyword.cloud_notm}} independente disponível, além das ferramentas a seguir:

* `Homebrew` (somente Mac)
* `Git`
* `Docker`
* `Helm`
* `kubectl`
* `curl`
* Plug-in do {{site.data.keyword.dev_cli_notm}}
* Plug-in do {{site.data.keyword.IBM_notm}} {{site.data.keyword.openwhisk_short}}
* Plug-in do {{site.data.keyword.registrylong_notm}}
* Plug-in do {{site.data.keyword.containerlong_notm}}
* Plug-in do `sdk-gen`

## Antes de começar
{: #idt-prereq}

É necessária uma conta do [{{site.data.keyword.cloud_notm}} ](https://cloud.ibm.com/){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") e os requisitos do sistema a seguir:

* Se você estiver executando o Windows&trade;, algumas funções não serão suportadas, a
menos que esteja executando o Windows&trade; 10 Pro.
* Deve-se usar o canal estável para o Docker com uma versão mínima de 1.13.1.

## Etapa 1. Execute o comando de instalação
{: #step1-install-idt}

A versão mais recente da CLI do {{site.data.keyword.cloud_notm}} será instalada quando
você executar o comando.

* Para Mac e Linux&trade;, execute o comando a seguir:
  ```
  curl -sL https://ibm.biz/idt-installer | bash
  ```
  {: codeblock}

* Para o Windows&trade; 10 Pro, execute o comando a seguir como um administrador:
  ```
  [Net.ServicePointManager]::SecurityProtocol = "Tls12"; iex(New-Object Net.WebClient).DownloadString('https://ibm.biz/idt-win-installer')
  ```
  {: codeblock}

  Clique com o botão direito do mouse no ícone do Windows&trade; PowerShell e selecione **Executar como administrador**.
  {: tip}

Também é possível fazer download do script do instalador por meio desse [repositório do GitHub](https://github.com/IBM-Cloud/ibm-cloud-developer-tools){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

Se for necessário usar uma versão de 32 bits da CLI ou uma versão anterior diferente da
mais recente para ambientes {{site.data.keyword.cloud_notm}} Dedicados, veja [Liberações da CLI do {{site.data.keyword.cloud_notm}}](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: new_window}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
{: note}

## Etapa 2. Verificar a instalação
{: #step2-verify-idt}

Para verificar se a CLI e as ferramentas do Desenvolvedor foram instaladas com êxito, execute o comando `help`:
```
ibmcloud dev help
```
{: codeblock}

A saída lista as instruções de uso, a versão atual e os comandos suportados.

## Etapa 3. Configure seu ambiente
{: #step3-configure-idt-env}

1. Efetue login no {{site.data.keyword.cloud_notm}} com seu IBMid. Se você tiver múltiplas contas, deverá selecionar qual conta usar. Se você não especificar uma região com a sinalização `-r`, deverá também escolher uma região.
  ```
  ibmcloud login
  ```
  {: codeblock}
  
  Se as suas credenciais forem rejeitadas, talvez você esteja usando um ID federado. Para efetuar login com uma identidade federada, use a sinalização `--sso`. Consulte
[Efetuando login com um ID federado](/docs/iam/federated_id?topic=iam-federated_id#federated_id) para obter mais detalhes.
  {: tip}

2. Para acessar os serviços do Cloud Foundry, deve-se especificar uma organização e um espaço do Cloud Foundry. É possível executar o comando a seguir para identificar interativamente a organização e o espaço:
  ```
  ibmcloud target --cf
  ```
  {: codeblock}

  Ou, se você souber a qual organização e a qual espaço o serviço pertence, será possível usar o comando a seguir:
  ```
  ibmcloud target -o <value> -s <value>
  ```
  {: codeblock}

## Próximas Etapas
{: #next-steps}

* Agora você está pronto para desenvolver e implementar seu primeiro app. Para obter mais informações, consulte [Criando e implementando aplicativos usando a CLI](/docs/apps?topic=creating-apps-create-deploy-app-cli#create-deploy-app-cli).

* É possível receber notificações sobre novas liberações da CLI do {{site.data.keyword.cloud_notm}}. Assine o [repositório de liberações de CLI do {{site.data.keyword.cloud_notm}}](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: new_window}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")
