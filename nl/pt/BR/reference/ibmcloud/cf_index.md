---

copyright:
  years: 2016, 2019
lastupdated: "2019-04-10"

keywords: cli, cf commands, cloud foundry commands, cloud foundry cli, cf apps, cf help, cf logs, cf api

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:note: .note}

# Trabalhando com o Cloud Foundry (cf commands)
{: #cf}

A interface da linha de comandos (CLI) do Cloud Foundry (cf) fornece um conjunto de comandos para gerenciar seus apps. As informações a seguir listam os comandos cf usados mais comumente para gerenciar apps e inclui seus nomes, opções, uso, pré-requisitos, descrições e exemplos. Para listar todos os comandos cf e informações de ajuda associadas, use `cf help`. Use `cf command_name -h` para visualizar informações detalhadas da ajuda para um comando específico.
{: shortdesc}

Para obter mais detalhes sobre como começar com a CLI do Cloud Foundry, consulte [Introdução](https://github.com/cloudfoundry/cli#getting-started){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

Para obter uma lista mais detalhada de comandos `cf CLI`, consulte a comunidade [Guia de referência da CLI do Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/cf-help.html){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

Se a sua rede contém um servidor proxy HTTP entre o host que executa os comandos cf e o terminal de API Cloud Foundry,
deve-se especificar o nome do host ou endereço IP do servidor proxy, configurando a variável de ambiente
`HTTP_PROXY`. Para obter detalhes, consulte [Usando a CLI do cf com um servidor proxy](https://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").
{: note}

## Índice de comandos da CLI do Cloud Foundry
{: #CLIname_commands_index}

Use o índice na tabela a seguir para se referir aos comandos do Cloud Foundry usados frequentemente:

<table summary="Comandos gerais do Cloud Foundry ordenados alfabeticamente que têm links que levam a mais informações sobre o comando">
<caption>Tabela 1. Comandos gerais do Cloud Foundry</caption>
 <thead>
 <th colspan="6">Comandos gerais do Cloud Foundry</th>
 </thead>
 <tbody>
 <tr>
 <td>[api
](#cf_api)</td>
 <td>[help](#cf_help)</td>
 <td>[login](#cf_login)</td>
 <td>[stacks](#cf_stacks)</td>
 <td>[target](#cf_target)</td>
 <td>[ -v ](#cf_v)</td>
 </tr>
   </tbody>
 </table>

<table summary="Comandos ordenados alfabeticamente para gerenciar apps, espaços e serviços. Cada comando tem um link que leva a mais informações sobre ele.">
<caption>Tabela 2. Comandos para gerenciar apps, espaços e serviços</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar aplicativos, espaços e serviços</th>
 </thead>
 <tbody>
 <tr>
 <td>[aplicativos
](#cf_apps)</td>
 <td>[bind-service](#cf_bind-service)</td>
 <td>[create-service](#cf_create-service)</td>
 <td>[create-space](#cf_create-space)</td>
 <td>[excluir](#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](#cf_delete-space)</td>
 <td>[eventos](#cf_events)</td>
 <td>[Registros do](#cf_logs)</td>
 <td>[mercado de trabalho](#cf_marketplace)</td>
 <td>[push](#cf_push)</td>
  </tr>
 <tr>
 <td>[escalar](#cf_scale)</td>
 <td>[services](#cf_services)
 <td>[set-env](#cf_set-env)</td>
 <td>[ssh](#cf_ssh)</td>
 <td>[stop](#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

Use este comando para exibir ou especificar a URL do terminal de API do {{site.data.keyword.cloud}}.
```
cf api [URL] [--skip-ssl-validation] [--unset]
```

<strong>Pré-requisitos</strong>: nenhum.

<strong>Opções de comando</strong>:

   <dl>
   <dt>URL (opcional)</dt>
   <dd>A URL do terminal da API do {{site.data.keyword.cloud_notm}} que você deve especificar quando se conectar ao {{site.data.keyword.cloud_notm}}. Geralmente, essa URL é `https://api.<REGION>.cf.{DomainName}`.
   Se você desejar exibir a URL do terminal de API que está usando atualmente, não será necessário especificar esse parâmetro para o comando cf api.</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>Desativa o processo de validação SSL. O uso desse parâmetro pode causar problemas de segurança.</dd>
   <dt>* --unset</dt>
   <dd>Remove as informações de conexão para todos os terminais API.</dd>
   </dl>

<strong>Exemplos</strong>:

Para visualizar o terminal de API atual:
```
cf api
```
{: codeblock}

Remova a conexão com todos os terminais de API para api.us-south.cf.cloud.ibm.com:
```
cf api api.us-south.cf.cloud.ibm.com -- unset
```
{: codeblock}

Desative o processo de validação de SSL para api.us-south.cf.cloud.ibm.com:
```
cf api api.us-south.cf.cloud.ibm.com --skip-ssl-validation
```
{: codeblock}

## cf apps
{: #cf_apps}

Lista todos os aplicativos que você implementou no espaço atual. O
status de cada aplicativo também é exibido.

Suponha que tenha uma instância para um app, na coluna de instâncias da resposta do comando cf apps, você verá 1/1 se seu app estiver ativo e 0/1 se seu app estiver inativo. Se você vir ?/1, que indica que o estado da instância do app é desconhecido, será possível copiar a URL do app para o seu navegador
para verificar se o app responde ou acompanhar o log pelo comando `cf logs appname` para ver se o app
está gerando conteúdo de log.

```
cf apps
```
{: codeblock}

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

## cf bind-service
{: #cf_bind-service}

Liga uma instância de serviço existente ao seu aplicativo.

```
cf bind-service appname service_instance
```
{: codeblock}

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

   <dl>
   <dt>appname (obrigatório)</dt>
   <dd>O nome do aplicativo.</dd>
   <dt>service_instance (obrigatório)</dt>
   <dd>O nome da instância de serviço existente.</dd>
    </dl>

<strong>Exemplos</strong>:

Ligue uma instância de serviço chamada `my_dataworks` ao seu app chamado `my_app`.
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

Cria uma instância de serviço.

```
cf create-service service_name service_plan service_instance
```
{: codeblock}

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

   <dl>
   <dt>service_name (obrigatório)</dt>
   <dd>O nome do serviço.</dd>
   <dt>service_plan (obrigatório)</dt>
   <dd>O nome do plano de serviço.</dd>
   <dt>service_instance (obrigatório)</dt>
   <dd>O nome que você deseja usar para a nova instância de serviço que você criar.</dd>
    </dl>

<strong>Exemplos</strong>:

Cria uma instância do serviço {{site.data.keyword.dataworks_short}} com um plano `free`.
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

Cria um espaço.

```
cf create-space space_name [-o] [-q]
```

<strong>Pré-requisitos</strong>: `cf api`, `cf login`

<strong>Opções de comando</strong>:

   <dl>
   <dt>space_name (obrigatório)</dt>
   <dd>O nome do espaço.</dd>
   <dt>*-o* (opcional)</dt>
   <dd>O nome da organização dentro do qual você deseja criar um espaço.</dd>
   <dt>*-q* (opcional)</dt>
   <dd>A cota para designar ao espaço recentemente criado. Se não especificado, uma cota padrão será designada automaticamente.</dd>
    </dl>

<strong>Exemplos</strong>:

Criar um espaço chamado new_space
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

Exclui um aplicativo existente.

```
cf delete appname [-f] [-r]
```

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

   <dl>
   <dt>appname (obrigatório)</dt>
   <dd>O nome do aplicativo.</dd>
   <dt>*-f* (opcional)</dt>
   <dd>Força a exclusão do aplicativo sem nenhuma confirmação.</dd>
   <dt>*-r* (opcional)</dt>
   <dd>Exclui todos os nomes de domínio que são associados com o aplicativo. </dd>
    </dl>

<strong>Exemplos</strong>:

Exclui um aplicativo que é denominado `my_app` (requer confirmação).
```
cf delete my_app
```
{: codeblock}

Exclui um aplicativo chamado `my_app` sem requerer confirmação.
```
cf delete my_app -f
```
{: codeblock}

Exclui um aplicativo chamado `my_app` e todos os nomes de domínio associados a `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Exclui um aplicativo chamado `my_app` e todos os nomes de domínio associados a `my_app` sem requerer confirmação.
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

Exclui um espaço.
```
cf delete-space space_name [-f]
```

<strong>Pré-requisitos</strong>: `cf api`, `cf login`

<strong>Opções de comando</strong>:

   <dl>
   <dt>space_name (obrigatório)</dt>
   <dd>O nome do espaço.</dd>
   <dt>*-f* (opcional)</dt>
   <dd>Força a exclusão do espaço sem nenhuma confirmação.</dd>
   *Nota:* A exclusão de um espaço é uma operação irreversível.
   </dl>

<strong>Exemplos</strong>:

Exclui um aplicativo que é denominado `my_app` (requer confirmação).
```
cf delete my_app
```
{: codeblock}

Exclui um aplicativo chamado `my_app` sem requerer confirmação.
```
cf delete my_app -f
```
{: codeblock}

Exclui um aplicativo chamado `my_app` e todos os nomes de domínio associados a `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Exclui um aplicativo que é denominado `my_app` e todos os nomes de domínio associados a `my_app` sem requerer confirmação.
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

Exibe eventos de tempo de execução que estão relacionados a um aplicativo.

```
cf events [appname]
```
{: codeblock}

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

   <dl>
   <dt>appname</dt>
   <dd>O nome do aplicativo.</dd>
   </dl>

<strong>Exemplos</strong>:

Exibe os eventos para um aplicativo chamado `my_app`.
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

Exibe informações da ajuda para todos os comandos cf ou para um comando cf específico.

```
cf help [command_name]
```
{: codeblock}

<strong>Pré-requisitos</strong>: nenhum.

<strong>Opções de comando</strong>:

   <dl>
   <dt>command_name (opcional)</dt>
   <dd>O nome de um comando.</dd>
    </dl>

<strong>Exemplos</strong>:

Exiba as informações da ajuda para todos os comandos cf.
```
cf help
```
{: codeblock}

Exiba as informações da ajuda para o comando de eventos.
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

Efetua seu login no {{site.data.keyword.cloud_notm}}. Se você estiver efetuando login com um ID federado, deverá usar o parâmetro de conexão única (SSO) para efetuar login.

Também é possível usar uma chave de API da Plataforma do {{site.data.keyword.cloud_notm}} para efetuar login. Use o nome de usuário `apikey` e seu valor de chave API como a senha. Para obter mais informações sobre como criar uma chave de API, consulte [Entendendo chaves API](/docs/iam?topic=iam-manapikey#manapikey).
{: note}

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>Pré-requisitos</strong>: nenhum.

<strong>Opções de comando</strong>:

<dl>
<dt>*-a* https://api.<REGION>.cf.{DomainName} (opcional)</dt>
<dd>A URL do terminal da API do {{site.data.keyword.cloud_notm}}.</dd>
<dt>*-u* user_name (opcional)</dt>
<dd>Seu nome de usuário.</dd>
<dt>*-p* password (opcional)</dt>
<dd>Sua senha.</dd>
<dd>*Importante:* Se você fornecer sua senha usando o parâmetro *-p* na interface de linha de comandos, a senha poderá ser registrada no histórico da linha de comandos. Por motivos de segurança, evite fornecer a senha usando o parâmetro -p. Em vez disso, insira a senha quando a interface da linha de comandos solicitar.</dd>
<dt>*-sso*</dt>
<dd>Deve-se usar a opção de conexão única (SSO) ao efetuar login com um ID federado. Isso não é necessário ao efetuar login com um IBMid. Se você tentar se conectar com um ID federado e não especificar o parâmetro de SSO, será solicitado em um prompt que o inclua. Usar o parâmetro SSO solicita que você insira a senha descartável após o login.</dd>
<dt>*-o* organization_name</dt>
<dd>O nome da organização na qual você deseja efetuar login.</dd>
<dt>*-s* space_name</dt>
<dd>O nome do espaço no qual você deseja efetuar login.</dd>
<dt>*--skip-ssl-validation* (opcional)</dt>
<dd>Desativa o processo de validação SSL. O uso desse parâmetro pode causar problemas de segurança.</dd>
</dl>

*Nota:* Se você fornecer a sua senha no parâmetro *-p* desse comando, sua senha poderá ser registrada no arquivo histórico do comando shell e poderá ser visível para outros usuários do sistema operacional local.

<strong>Exemplos</strong>:

Efetue login no {{site.data.keyword.cloud_notm}}.
```
cf login
```
{: codeblock}

Efetue login no {{site.data.keyword.cloud_notm}} com um terminal definido de `https://api.us-south.cf.cloud.ibm.com`.
```
cf login -a https://api.us-south.cf.cloud.ibm.com
```
{: codeblock}

Efetue login no {{site.data.keyword.cloud_notm}} com um terminal definido de `https://api.us-south.cf.cloud.ibm.com`, um nome do usuário de `user_name` e nenhuma senha especificada por razões de segurança.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u user_name
```
{: codeblock}

Efetue login no {{site.data.keyword.cloud_notm}} com um terminal definido de `https://api.us-south.cf.cloud.ibm.com`, um nome do usuário de `user_name`, nenhuma senha especificada por motivos de segurança e um nome de organização de `org_name` e o nome de espaço de `space_name`.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u user_name -o org_name -s space_name
```
{: codeblock}

Efetue login no {{site.data.keyword.cloud_notm}} com um terminal definido de `https://api.us-south.cf.cloud.ibm.com` usando uma chave de API. Use `apikey` como o nome do usuário e a chave API real como a senha.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u apikey -p ThisValueIsYourAPIKey
```
{: codeblock}

É possível efetuar login nos terminais de API do Cloud Foundry regionais a seguir:
* api.us-south.cf.cloud.ibm.com (anteriormente api.ng.bluemix.net)
* api.eu-gb.cf.cloud.ibm.com (anteriormente api.eu-gb.bluemix.net)
* api.us-east.cf.cloud.ibm.com (anteriormente api.us-east.bluemix.net)
* api.eu-de.cf.cloud.ibm.com (anteriormente api.eu-de.bluemix.net)
* api.au-syd.cf.cloud.ibm.com (anteriormente api.au-syd.bluemix.net)

Os terminais de API do Cloud Foundry anteriores "api.<REGION>.bluemix.net" ainda são válidos, mas em breve serão descontinuados.
{: note}

## cf logs
{: #cf_logs}

Exibe os fluxos de log STDOUT e STDERR de um aplicativo.

```
cf logs appname [--recent]
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>*--recent* (opcional)</dt>
<dd>Recupera logs recentes.</dd>
</dl>

<strong>Exemplos</strong>:

Exiba os fluxos de log para um aplicativo chamado `my_app`.
```
cf logs my_app
```
{: codeblock}

Exiba os fluxos de log recentes para um aplicativo chamado `my_app`.
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

Lista todos os serviços que estão disponíveis no mercado. Os serviços listados por esse comando também são mostrados no Catálogo do {{site.data.keyword.cloud_notm}}.

```
cf marketplace
```
<strong>Pré-requisitos</strong>: `cf api`

<strong>Opções de comando</strong>: nenhuma.

<strong>Exemplos</strong>:

Liste todos os serviços no mercado de trabalho
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

Implementa um novo aplicativo para
{{site.data.keyword.cloud_notm}} ou atualiza um aplicativo existente no {{site.data.keyword.cloud_notm}}.

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

<dl>
<dt>appname (obrigatório)</dt>
<dd>O nome do aplicativo.</dd>
<dt>*-b* buildpack_name (opcional)</dt>
<dd>O nome do buildpack. O buildpack_name pode ser um buildpack customizado por nome (por exemplo, liberty-for-java) ou uma URL de Git (por exemplo, https://github.com/cloudfoundry/java-buildpack) ou uma URL de Git com uma ramificação ou tag (por exemplo, https://github.com/cloudfoundry/java-buildpack#v3.3.0 para a tag v3.3.0).</dd>
<dt>*-c* start_command (opcional)</dt>
<dd>O comando start do seu aplicativo. Para usar o comando inicial padrão, especifique um valor de null para essa opção. </dd>
<dt>*-f* manifest_path (opcional)</dt>
<dd>O caminho do arquivo de manifesto. O arquivo manifest padrão é manifest.yml sob o diretório-raiz de seu aplicativo.</dd>
<dt>*-i* instance_number (opcional)</dt>
<dd>O número de instâncias.</dd>
<dt>*-k* disk_limit (opcional)</dt>
<dd>O limite de disco para o aplicativo. Os valores possíveis são *256M*, *1024M* ou *1G*.</dd>
<dt>*-m* memory_limit (opcional)</dt>
<dd>O limite de memória para o aplicativo. Os valores possíveis são *256M*, *1024M* ou *1G*.</dd>
<dt>*-n* host_name (opcional)</dt>
<dd>O nome do host para o aplicativo, por exemplo, *my-subdomain*.</dd>
<dt>*-p* app_path (opcional)</dt>
<dd>O caminho para o diretório do aplicativo ou o archive do aplicativo</dd>
<dt>*-s* stack_name (opcional)</dt>
<dd>A pilha para executar os apps. Uma pilha é um sistema de arquivos pré-construído que inclui o sistema operacional. Use `cf stacks` para visualizar as pilhas disponíveis no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-t* tempo limite (opcional)</dt>
<dd>Tempo máximo, em segundos, para o aplicativo iniciar. Outros tempos-limite do lado do servidor podem substituir esse valor.</dd>
<dt>*--no-hostname* (opcional)</dt>
<dd>Mapeia o domínio do sistema {{site.data.keyword.cloud_notm}} para esse aplicativo.</dd>
<dt>*--no-manifest* (opcional)</dt>
<dd>Ignora o arquivo de manifesto padrão.</dd>
<dt>*--no-route* (opcional)</dt>
<dd>Não mapeia uma rota para este aplicativo.</dd>
<dt>*--no-start* (opcional)</dt>
<dd>Não inicia o aplicativo depois que o aplicativo é implementado.</dd>
<dt>*--random-route* (opcional)</dt>
<dd>Cria uma rota aleatória para o aplicativo.</dd>
</dl>

<strong>Exemplos</strong>:

Inicie um aplicativo chamado `my_app` com o comando inicial padrão.
```
cf push `my_app` -c null
```
{: codeblock}

Inicie um aplicativo chamado `my_app` com a opção para executar um arquivo de script chamado `run.sh`.
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

Exibe ou muda o número da instância, o limite de espaço em disco e o limite de memória para um aplicativo.

```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

<dl>
<dt>appname (obrigatório)</dt>
<dd>O nome do aplicativo.</dd>
<dt>*-i* instance_number (opcional)</dt>
<dd>O número de instâncias.</dd>
<dt>*-k* disk_limit (opcional)</dt>
<dd>O limite de disco para o aplicativo; os valores possíveis são `256M`, `1024M` ou `1G`.</dd>
<dt>*-m* memory_limit (opcional)</dt>
<dd>O limite de memória para o aplicativo; os valores possíveis são `256M`, `1024M` ou `1G`.</dd>
<dt>*-f* (opcional)</dt>
<dd>Força o aplicativo a reiniciar sem prompt.</dd>
</dl>

<strong>Exemplos</strong>:

Exiba o número da instância, o limite de espaço em disco e o limite de memória para um aplicativo chamado `my_app`.
```
cf scale my_app
```
{: codeblock}

Modifique o número da instância para `1234`, o limite de espaço em disco para `1G` e o limite de memória para `1G` para um app chamado `my_app`.
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

Lista todos os serviços que estão disponíveis no espaço atual.

```
cf services
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>: nenhuma.

<strong>Exemplos</strong>:

Liste todos os serviços no espaço atual.
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

Configura uma variável de ambiente para um aplicativo

```
cf set-env appname var_name var_value
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

<dl>
<dt>appname (obrigatório)</dt>
<dd>O nome do aplicativo.</dd>
<dt>var_name (obrigatório)</dt>
<dd>O nome da variável de ambiente.</dd>
<dt>var_value (obrigatório)</dt>
<dd>O valor da variável de ambiente.</dd>
</dl>

<strong>Exemplos</strong>:

Configure uma variável de ambiente chamada `variable_a` com um valor de `123` para o aplicativo chamado `my_app`.
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

Acessar com segurança o contêiner de aplicativo. O comando `cf ssh` pode ser usado para configurar uma sessão SSH interativa, executar comandos remotos, transferir arquivos e configurar o encaminhamento de porta com uma instância de contêiner de aplicativo específica.

```
cf ssh
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

Por padrão, o acesso SSH fica ativado para aplicativos Diego. É possível usar o comando `cf ssh-enabled` para
verificar se o acesso SSH está ativado ou o comando `cf enable-ssh` para ativar o acesso se foi desativado.

<strong>Opções de comando</strong>:

<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>-c</dt>
<dd>Especifica um comando remoto a ser executado.</dd>
<dt>-i</dt>
<dd>Destina uma instância específica de um aplicativo. Se não especificada, a primeira instância do aplicativo será usada (uma instância com índice 0).</dd>
<dt>-L</dt>
<dd>Ativa o encaminhamento de porta local, que liga uma porta de saída em sua máquina a uma porta de entrada na VM do aplicativo.</dd>
<dt>-N</dt>
<dd>Não executa um comando remoto.</dd>
<dt>-t, -tt ou -T</dt>
<dd>Permite executar uma sessão SSH no modo pseudo-tty em vez de gerar a saída de linha de terminal.<dd>
</dl>

<strong>Exemplos</strong>:

Iniciar uma sessão SSH interativa com a instância do contêiner executando o aplicativo `my_app`.
```
$ cf ssh my_app
```
{: codeblock}

Executar um único comando na instância de contêiner de aplicativo `my_app`.
```
$ cf ssh my_app -c "ls -l"
```

Transferir um único arquivo da instância de contêiner de aplicativo `my_app`.
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

Configurar o encaminhamento de porta da porta 7777 na máquina local para a porta 8888 na instância de contêiner de aplicativo `my_app`.
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

Lista todas as pilhas. Uma pilha é um sistema de arquivos pré-construído, incluindo um sistema operacional que pode executar apps.

```
cf stacks
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`

<strong>Opções de comando</strong>: nenhuma.

<strong>Exemplos</strong>:

Liste todas as pilhas.
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

Para um aplicativo

```
cf stop appname
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opções de comando</strong>:

<dl>
<dt>appname (obrigatório)</dt>
<dd>O nome do aplicativo.</dd>
</dl>

<strong>Exemplos</strong>:

Pare o aplicativo chamado `my_app`.
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

Configura ou visualiza a organização ou espaço de destino

```
cf target [-o org_name] [-s space_name]
```
<strong>Pré-requisitos</strong>: `cf api`, `cf login`

<strong>Opções de comando</strong>:

<dl>
<dt>-o *org_name* (opcional)</dt>
<dd>O nome da organização na qual o espaço está localizado.</dd>
<dt>-s *space_name* (opcional)</dt>
<dd>O nome do espaço.</dd>
</dl>

<strong>Exemplos</strong>:

Configure o destino para a organização chamada "my_org" e o espaço chamado "my_space".
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

Exibe a versão da interface da linha de comandos do Cloud Foundry.

```
cf -v
```
<strong>Pré-requisitos</strong>: nenhum.

<strong>Opções de comando</strong>: nenhuma.

<strong>Exemplos</strong>:

Exiba a versão da interface da linha de comandos do Cloud Foundry.
```
cf -v
```
{: codeblock}


## Links Relacionados
{: #cf-related}

* [Download da CLI do Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")
* [Cartão de referência rápida - comandos cf](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")
