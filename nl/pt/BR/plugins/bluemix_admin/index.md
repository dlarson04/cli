---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-21"

keywords: cli, ibmcloud admin cli, admin cli plugin, admin plugin, cloud foundry admin cli plugin, adding users, buildpack, security groups, cf ba

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# CLI do administrador do {{site.data.keyword.cloud_notm}}
{: #bluemixadmincli}

É possível gerenciar o ambiente do {{site.data.keyword.cloud_notm}} Local ou do {{site.data.keyword.cloud_notm}} Dedicated usando a interface da linha de comandos (CLI) do Cloud Foundry com o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}. Por
exemplo, é possível incluir usuários a partir de um registro LDAP.

Antes de iniciar, instale a CLI do Cloud Foundry. O plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}
requer `cf` versão 6.11.2 ou mais recente. [Fazer download da interface da linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")

A CLI do Cloud Foundry não é suportada pelo Cygwin. Use a CLI do Cloud Foundry em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

A CLI do administrador do {{site.data.keyword.cloud_notm}} é usada apenas para o {{site.data.keyword.cloud_notm}} Local e o ambiente do {{site.data.keyword.cloud_notm}} Dedicated. Ele não é suportado pelo {{site.data.keyword.cloud_notm}} Public.
{: note}

## Incluindo o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}
{: #add-admin-cli}

Depois de instalar a CLI do Cloud Foundry, é possível incluir o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}.

Se anteriormente você instalou o plug-in do administrador do {{site.data.keyword.cloud_notm}}, poderá ser necessário desinstalar o plug-in, excluir o repositório e, em seguida, instalar novamente para obter as atualizações mais recentes.
{: tip}

Conclua as etapas a seguir para incluir o repositório e instalar
o plug-in:

1. Para incluir o repositório do plug-in de administrador do {{site.data.keyword.cloud_notm}}, execute o comando a seguir:
  ```
  cf add-plugin-repo IBMCloudAdmin https://<customer_console_endpoint>.bluemix.net/cli
  ```
  {: codeblock}

  É possível localizar o mesmo comando com o terminal real em sua página da CLI do console do administrador: `https://<customer_console_endpoint>.bluemix.net/cli`.
  {: note}

2. Para instalar o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}, execute o comando a seguir:
  ```
  cf install-plugin IBMCloudAdminCLI -r IBMCloudAdmin
  ```
  {: codeblock}

## Desinstalando o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}
{: #remove-admin-cli}

Conclua as etapas a seguir para desinstalar o plug-in. 

1. Desinstale o plug-in:
  ```
  cf uninstall-plugin IBMCloudAdminCLI
  ```
  {: codeblock}

2. Remova o repositório de plug-in:
  ```
  cf remove-plugin-repo IBMCloudAdmin
  ```
  {: codeblock}

Em seguida, é possível incluir o repositório atualizado e instalar o plug-in mais recente.

## Usando o Plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}}
{: #using-admin-cli}

É possível usar o plug-in da CLI do administrador do {{site.data.keyword.cloud_notm}} para incluir ou remover usuários, designar ou remover a designação de usuários das organizações e executar outras tarefas de gerenciamento.

Para ver uma lista de comandos, execute o comando
a seguir:
```
cf plugins
```
{: codeblock}

Para obter mais ajuda para um comando, use a opção `-help`.

### Conectando e efetuando login no {{site.data.keyword.cloud_notm}}
{: #connecting-ibm-cloud}

1. Para conectar-se ao terminal da API do {{site.data.keyword.cloud_notm}}, execute o comando a seguir:
  ```
  cf api api.us-south.cf.cloud.ibm.com
  ```
  {: codeblock}
  
  Embora os terminais de API anteriores do Cloud Foundry `api.*.bluemix.net` ainda estejam disponíveis, é possível atualizar os scripts e a automação de infraestrutura para usar os terminais de API atualizados do Cloud Foundry a seguir para sua região:

  * api.us-south.cf.cloud.ibm.com (anteriormente api.ng.bluemix.net)
  * api.eu-gb.cf.cloud.ibm.com (anteriormente api.eu-gb.bluemix.net)
  * api.us-east.cf.cloud.ibm.com (anteriormente api.us-east.bluemix.net)
  * api.eu-de.cf.cloud.ibm.com (anteriormente api.eu-de.bluemix.net)
  * api.au-syd.cf.cloud.ibm.com (anteriormente api.au-syd.bluemix.net)

  É possível verificar a página Recursos e informações do console do administrador da URL correta. A URL é mostrada na seção Informações da API no campo **URL da API**.

2. Efetue login no {{site.data.keyword.cloud_notm}} executando o comando a seguir:
  ```
  cf login
  ```
  {: codeblock}

## Administrando Usuários
{: #admin_users}

### Incluindo um usuário
{: #admin_add_user}

Para incluir um usuário em seu ambiente do {{site.data.keyword.cloud_notm}} a partir do
registro do usuário de seu ambiente, use o comando a seguir:
```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

Para incluir um usuário em uma organização específica, deve-se ser um administrador com a permissão users.write (ou Superusuário). Se você for um gerenciador de organização, também poderá ser fornecido a você o recurso para incluir usuários em sua organização por um Superusuário que executa o comando **`enable-managers-add-users`**. Para obter mais informações, consulte [Ativando gerenciadores para incluir usuários](#clius_emau).

| Opção | Descrição | 
| -------| ------------|
| _userName_ | O nome do usuário no registro LDAP. |
| _organization_ | O nome ou GUID da organização do {{site.data.keyword.cloud_notm}} na qual incluir o usuário. |
| _firstName_ | O nome do usuário a ser incluído na organização. | 
| _lastName_ | O sobrenome do usuário a ser incluído na organização. | 
{: caption="Tabela 1. Opções do comando cf ba add-user" caption-side="top"}

Também é possível usar **`ba au`** como um alias para o nome de comando mais longo **`ba add-user`**.
{: tip}

### Convidando um usuário do {{site.data.keyword.Bluemix_dedicated_notm}}
{: #admin_dedicated_invite_public}

Cada ambiente do {{site.data.keyword.Bluemix_dedicated_notm}} tem uma conta pública, corporativa ou de propriedade do cliente no {{site.data.keyword.cloud_notm}}. Para que os usuários no ambiente Dedicated criem clusters com o {{site.data.keyword.containershort}}, o administrador deve incluir os usuários nessa conta corporativa pública. Quando os usuários são incluídos na conta corporativa pública, suas contas Dedicated e públicas são vinculadas. Os usuários podem então usar seu IBMid para efetuar login no Dedicated ou público simultaneamente e podem criar recursos na conta pública da interface Dedicated. Para obter mais informações, veja [Configurando o IBM Cloud Container Service no Dedicated](/docs/containers?topic=containers-dedicated#dedicated_setup). Para convidar usuários do Dedicated para a conta pública:
```
cf ba invite-users-to-public -userid=<user_email> -organization=<dedicated_org_id> -apikey=<public_api_key> -public_org_id=<public_org_id>
```
{: pre}

Para incluir usuários do ambiente Dedicado em sua conta pública do {{site.data.keyword.cloud_notm}}, deve-se ser um Administrador da conta Dedicada.

| Opção | Descrição | 
| -------| ------------|
| -userid | Se você estiver convidando um único usuário, o e-mail do usuário. |
| -organization | Se você estiver convidando todos os usuários atualmente em uma organização da conta Dedicated, o ID da organização da conta Dedicated. |
| -apikey | Uma chave API para convidar usuários para a conta pública. Ela deve ser gerada pelo administrador da conta pública. | 
| -public_org_id | O ID da organização da conta pública para qual você está convidando usuários. | 
{: caption="Tabela 2. Opções do comando cf ba invite-users-to-public" caption-side="top"}

### Listando usuários que são convidados do {{site.data.keyword.Bluemix_dedicated_notm}}
{: #admin_dedicated_list}

Se você convidou usuários do ambiente Dedicado para sua conta do {{site.data.keyword.Bluemix_notm}} com o [**comando `invite-users-to-public`**](#admin_dedicated_invite_public), será possível listar os usuários em sua conta para ver seus status de convites. Os usuários convidados que têm um IBMid existente têm um status de ACTIVE. Os usuários convidados que não tinham um IBMid existente têm um status de PENDING ou ACTIVE, dependendo se já aceitaram o convite para a conta. Para listar os usuários em sua conta do {{site.data.keyword.Bluemix_notm}}:

```
cf ba invite-users-status -apikey=<public_api_key>
```
{: pre}

Para incluir usuários do ambiente Dedicado em sua conta pública do {{site.data.keyword.Bluemix_notm}}, deve-se ser um administrador da conta Dedicada.

<dl class="parml">
<dt class="pt dlterm">&lt;public_api_key&gt;</dt>
<dd class="pd">A chave API que foi usada para convidar os usuários para a conta. Ela deve ser gerada pelo administrador da conta pública. </dd>
</dl>

<!-- staging-only commands start. Live for interconnect -->

### Procurando um usuário
{: #admin_search_user}

Para procurar um usuário, use o comando a seguir com os parâmetros de filtro de procura opcionais (nome, permissão,
organização e função):

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| -name | O nome do usuário. |
| -permission | A permissão que é designada ao usuário. As permissões disponíveis são admin (ou superusuário), login (ou básico), catalog.read, catalog.write, reports.read, reports.write, users.read ou users.write. Não é possível usar esse parâmetro com o parâmetro de organização na mesma consulta. |
| -organization | O nome da organização à qual o usuário pertence. Não é possível usar esse parâmetro com o parâmetro de permissão na mesma consulta. | 
| -role | A função de organização que é designada ao usuário. As funções disponíveis são auditores, gerenciadores e billing_managers. Deve-se especificar a organização com esse parâmetro. | 
{: caption="Tabela 3. Opções do comando cf ba search-users" caption-side="top"}

Também é possível usar **`ba su`** como um alias para o nome de comando mais longo **`ba search-users`**.
{: tip}

### Configurando permissões para um usuário
{: #admin_setperm_user}

Para configurar permissões para um usuário especificado, use o comando a seguir:
```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _userName_ | O nome do usuário. |
| _permission_ | Configure a permissão designada ao usuário. As permissões disponíveis são admin (ou superusuário), login (ou básico), catalog.read, catalog.write, reports.read, reports.write, users.read ou users.write. Não é possível usar esse parâmetro com o parâmetro de organização na mesma consulta. |
| _access_ | Para o catálogo, relatórios ou permissões de usuário, deve-se também configurar o nível de acesso como `read` ou `write`. |  
{: caption="Tabela 4. Opções do comando cf ba set-permissions" caption-side="top"}

É possível configurar uma permissão de cada vez.

Também é possível usar **`ba sp`** como um alias para o nome de comando mais longo **`ba set-permissions`**.
{: tip}

<!-- staging-only commands end -->

### Removendo um usuário
{: #admin_remov_user}

Para remover um usuário de seu ambiente do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

Também é possível usar o **`ba ru`** como um alias para o nome de comando mais longo **`ba remove-user`**.
{: tip}

### Ativando gerenciadores para incluir usuários
{: #clius_emau}

Se você tiver a permissão Superusuário em seu ambiente do {{site.data.keyword.Bluemix_notm}}, será possível ativar os gerenciadores de organização para incluir usuários nas organizações que eles gerenciam. Para
permitir que os gerenciadores incluam usuários, use o comando a seguir:

```
cf ba enable-managers-add-users
```
{: codeblock}

Também é possível usar o **`ba emau`** como um alias para o nome de comando mais longo **`ba enable-managers-add-users`**.
{: tip}

### Desativando gerenciadores de incluir usuários
{: #clius_dmau}

Se os gerenciadores de organização estiverem ativados para incluir usuários nas organizações que gerenciam em seu ambiente do {{site.data.keyword.Bluemix_notm}} com o comando **`enable-managers-add-users`** e se você tiver a permissão Superusuário, será possível remover essa configuração. Para desativar os usuários de incluírem usuários, use o comando a seguir:

```
cf ba disable-managers-add-users
```
{: codeblock}

Também é possível usar o comando **`ba dmau`** como um alias para o nome de comando mais longo **`ba disable-managers-add-users`**.
{: tip}

## Administrando as organizações
{: #admin_orgs}

### Incluindo uma Organização
{: #admin_add_org}

Para incluir uma organização, use o comando a seguir:

```
cf ba create-org <organization> <manager>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização do {{site.data.keyword.Bluemix_notm}} a ser incluída |
| _manager_ | O nome do usuário do gerenciador para a organização. |
{: caption="Tabela 5. Opções do comando cf ba create-org" caption-side="top"}

Também é possível usar **`ba co`** como um alias para o nome de comando mais longo **`ba create-org`**.
{: tip}

### Excluindo uma Organização
{: #admin_delete_org}

Para excluir uma organização, use o comando a seguir:

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.cloud_notm}} a ser excluída.</dd>
</dl>

Também é possível usar **`ba do`** como um alias para o nome de comando mais longo **`ba delete-org`**.
{: tip}

### Designando um usuário a uma organização
{: #admin_ass_user_org}

Para designar um usuário em seu ambiente do {{site.data.keyword.cloud_notm}} para uma
determinada organização, use o comando a seguir:

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _userName_ | O nome do usuário. |
| _organization_ | O nome ou GUID da organização do {{site.data.keyword.cloud_notm}} para a qual designar o usuário. |
| _role_ | A função do usuário. Os valores válidos são `OrgManager`, `BillingManager`, `OrgAuditor`. Consulte [Funções](/docs/iam?topic=iam-userroles#userroles) para obter as descrições de função. |  
{: caption="Tabela 6. Opções do comando cf ba set-org" caption-side="top"}

Também é possível usar **`ba so`** como um alias para o nome de comando mais longo **`ba set-org`**.
{: tip}

### Removendo a designação de um usuário de uma organização
{: #admin_unass_user_org}

Para remover a designação de um usuário em seu ambiente do {{site.data.keyword.cloud_notm}} de
uma determinada organização, use o comando a seguir:

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _userName_ | O nome do usuário. |
| _organization_ | O nome ou o GUID da organização do {{site.data.keyword.cloud_notm}}. |
| _role_ | A função do usuário. Os valores válidos são `OrgManager`, `BillingManager`, `OrgAuditor`. Consulte [Funções](/docs/iam?topic=iam-userroles#userroles) para obter as descrições de função. |  
{: caption="Tabela 7. Opções do comando cf ba unset-org" caption-side="top"}

Também é possível usar **`ba uo`** como um alias para o nome de comando mais longo **`ba unset-org`**.
{: tip}

### Configurando uma cota para uma organização
{: #admin_set_org_quota}

Para configurar a cota de uso para uma determinada organização, use o comando a seguir:

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização {{site.data.keyword.cloud_notm}} para a qual configurar a cota. |
| _plan_ | O plano da cota para uma organização. |  
{: caption="Tabela 8. Opções do comando cf ba set-quota" caption-side="top"}

Também é possível usar **`ba sq`** como um alias para o nome de comando mais longo **`ba set-quota`**.
{: tip}


### Localizando cotas de contêiner para uma organização
{: #admin_find_containquotas}

Para localizar a cota para contêineres para uma organização, use o comando a seguir:

```
cf ibmcloud-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o ID da organização no IBM Cloud. Esse parâmetro
é obrigatório.</dd>
</dl>

Também é possível usar **`ba cq`** como um alias para o nome de comando mais longo **`ibmcloud-admin containers-quota`**.
{: tip}

### Configurando cotas de contêiner para uma organização
{: #admin_set_containquotas}

Para configurar a cota para contêineres em uma organização, use o comando a seguir com pelo menos uma das opções incluídas:

```
cf ibmcloud-admin set-containers-quota <organization> <options>
```
{: codeblock}

É possível incluir várias opções, mas deve-se incluir pelo menos uma.
{: note}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o ID da organização do {{site.data.keyword.cloud_notm}} para a qual configurar a cota. |
| _options_ | As opções são **`floating-ips-max value`** (nome abreviado **`fim`**), **`floating-ips-space-default value`** (nome abreviado **`fisd`**), **`memory-max value`** (nome abreviado **`mm`**), **`memory-space-default value`** (nome abreviado **`msd`**) ou **`image-limit value`** (nome abreviado **`il`**). O valor deve ser um número inteiro.  |  
{: caption="Tabela 9. Opções do comando cf ibmcloud-admin set-containers-quota" caption-side="top"}

Opcionalmente, é possível fornecer um arquivo que contém parâmetros de configuração específicos em um objeto JSON válido. Se você usar a opção **`-file`**, ela terá precedência e as outras opções serão ignoradas. Para
fornecer um arquivo em vez de configurar as opções, use o comando a seguir:

```
cf ibmcloud-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

O arquivo JSON deve ter o formato que é mostrado no exemplo a seguir:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

Também é possível usar **`ba scq`** como um alias para o nome de comando mais longo **`ibmcloud-admin set-containers-quota`**.
{: tip}

## Administrando Espaços
{: #admin_spaces}

### Incluindo um espaço na organização

Para incluir um espaço na organização, use o comando a seguir:

```
cf ibmcloud-admin create-space <organization> <space_name>
```

{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização na qual incluir o espaço. |
| _spaceName_ | O nome do espaço que você está incluindo na organização. |  
{: caption="Tabela 10. Opções do comando cf ibmcloud-admin create-space" caption-side="top"}

Também é possível usar **`ba cs`** como um alias para o nome de comando mais longo **`ba create-space`**.
{: tip}

### Excluindo um espaço da organização

Para remover um espaço da organização, use o comando a seguir:

```
cf ibmcloud-admin delete-space <organization> <space_name>
```

{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização da qual o espaço deve ser removido. |
| _spaceName_ | O nome do espaço que você está removendo da organização. |  
{: caption="Tabela 11. Opções do comando cf ibmcloud-admin delete-space" caption-side="top"}

Também é possível usar **`ba cs`** como um alias para o nome de comando mais longo **`ba delete-space`**.
{: tip}

### Incluindo um usuário em um espaço com uma função

Para criar um usuário em um espaço com uma função especificada, use o comando a seguir:

```
cf ibmcloud-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização na qual o usuário está sendo incluído. |
| _spaceName_ | O nome do espaço no qual o usuário está sendo incluído. |
| _userName_ | O nome do usuário. |
| _role_ | A função do usuário. Os valores válidos são `Manager`, `Developer` ou `Auditor`. |  
{: caption="Tabela 12. Opções do comando cf ibmcloud-admin set-space" caption-side="top"}

Também é possível usar **`ba ss`** como um alias para o nome de comando mais longo **`ba set-space`**.
{: tip}


### Removendo a função de um usuário em um espaço

Para remover a função de um usuário em um espaço, use o comando a seguir:

```
cf ibmcloud-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _organization_ | O nome ou o GUID da organização à qual o usuário pertence. |
| _spaceName_ | O nome do espaço ao qual o usuário pertence. |
| _userName_ | O nome do usuário. |
| _role_ | A função do usuário. Os valores válidos são `Manager`, `Developer` ou `Auditor`. |  
{: caption="Tabela 13. Opções do comando cf ibmcloud-admin unset-space" caption-side="top"}

Também é possível usar **`ba us`** como um alias para o nome de comando mais longo **`ba unset-space`**.
{: tip}

## Administrando o catálogo
{: #admin_catalog}

### Ativando serviços para todas as organizações
{: #admin_ena_service_org}

Para ativar um serviço para ser exibido no catálogo do {{site.data.keyword.cloud_notm}} para todas as
organizações, use o comando a seguir:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você inserir um nome do plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico," serão solicitados os planos de serviço dos quais escolher. Para identificar um nome de plano de serviço, selecione a categoria do serviço na página inicial, em seguida, selecione **Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de serviços
que estão disponíveis para esse serviço. </dd>
</dl>

Também é possível usar **`ba esp`** como um alias para o nome de comando mais longo **`ba enable-service-plan`**.
{: tip}

### Desativando serviços para todas as organizações
{: #admin_dis_service_org}

Para desativar um serviço de ficar visível no catálogo do {{site.data.keyword.Bluemix_notm}} para todas as
organizações, use o comando a seguir:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você inserir um nome do plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico," serão solicitados os planos de serviço dos quais escolher. Para identificar um nome de plano de serviço, selecione a categoria do serviço na página inicial, em seguida, selecione **Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de
serviços que estão disponíveis para esse serviço.</dd>
</dl>

Também é possível usar **`ba dsp`** como um alias para o nome de comando mais longo **`ba disable-service-plan`**.
{: tip}

### Incluindo a visibilidade de serviço para organizações
{: #admin_addvis_service_org}

É possível incluir uma organização da lista de organizações que podem ver um serviço específico no catálogo do {{site.data.keyword.Bluemix_notm}}. Para permitir que uma organização visualize um serviço específico no catálogo, use o comando a seguir:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _planIdentifier_ | O nome ou o GUID do plano de serviço que você deseja ativar. Se você inserir um nome do plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico," serão solicitados os planos de serviço dos quais escolher. Para identificar um nome de plano de serviço, selecione a categoria do serviço na página inicial, em seguida, selecione **Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de serviços
que estão disponíveis para esse serviço. |
| _organization_ | O nome ou GUID da organização a ser incluída na lista de visibilidade do serviço. |  
{: caption="Tabela 14. Opções do comando cf ba add-service-plan-visibility" caption-side="top"}

Também é possível usar **`ba aspv`** como um alias para o nome de comando mais longo **`ba add-service-plan-visibility`**.
{: tip}

### Removendo a visibilidade de serviço para organizações
{: #admin_remvis_service_org}

É possível remover uma organização da lista de organizações que podem ver um serviço específico no catálogo do {{site.data.keyword.Bluemix_notm}}. Para remover a visibilidade de um serviço no catálogo para uma organização, use o comando a seguir:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _planIdentifier_ | O nome ou o GUID do plano de serviço que você deseja ativar. Se você inserir um nome do plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico," serão solicitados os planos de serviço dos quais escolher. Para identificar um nome de plano de serviço, selecione a categoria do serviço na página inicial, em seguida, selecione **Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de serviços
que estão disponíveis para esse serviço. |
| _organization_ | O nome ou o GUID da organização a ser removida da lista de visibilidade do serviço. |  
{: caption="Tabela 15. Opções do comando cf ba remove-service-plan-visibility" caption-side="top"}

Também é possível usar **`ba rspv`** como um alias para o nome de comando mais longo **`ba remove-service-plan-visibility`**.
{: tip}

### Editando a visibilidade de serviço para organizações
{: #admin_editvis_service_org}

É possível editar e substituir a lista de serviços que as organizações específicas podem ver no catálogo do {{site.data.keyword.Bluemix_notm}}. Para substituir todos os serviços visíveis existentes para uma organização ou múltiplas organizações, use o comando a seguir:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

Esse
comando substitui os serviços visíveis existentes para as organizações especificadas pelo serviço que você especifica no comando.

| Opção | Descrição | 
| -------| ------------|
| _planIdentifier_ | O nome ou o GUID do plano de serviço que você deseja ativar. Se você inserir um nome do plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico," serão solicitados os planos de serviço dos quais escolher. Para identificar um nome de plano de serviço, selecione a categoria do serviço na página inicial, em seguida, selecione **Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de serviços
que estão disponíveis para esse serviço. |
| _organization_ | O nome ou o GUID da organização para a qual incluir visibilidade. É
possível ativar a visibilidade do serviço para mais de uma organização, inserindo mais nomes da organização ou GUIDs no comando. |  
{: caption="Tabela 16. Opções do comando cf ba edit-service-plan-visibilities" caption-side="top"}

Também é possível usar **`ba espv`** como um alias para o nome de comando mais longo **`ba edit-service-plan-visibility`**.
{: tip}

## Administrando relatórios
{: #admin_add_report}

### Incluindo Relatórios
{: #admin_adding_report}

Para incluir um relatório de segurança, use o comando a seguir:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

Se você tiver acesso de gravação para a permissão de relatórios, será possível criar uma nova categoria e incluir um relatório em qualquer um dos formatos aceitos para os seus usuários. Insira
o novo nome da categoria para o parâmetro **`category`** ou inclua o seu novo relatório em uma categoria existente.

| Opção | Descrição | 
| -------| ------------|
| _category_ | A categoria para o relatório. Se houver um espaço no nome, use aspas. |
| _date_ | A data do relatório no formato de AAAAMMDD. |  
| _filePath_ | O caminho para o PDF do relatório, arquivo de texto ou arquivo de log para upload. |
| _RTF_ | Uma opção para incluir uma versão do Rich Text Format (RTF) do PDF. Essa opção se aplicará apenas se você incluir um caminho no PDF do relatório. A versão RTF é usada para indexação e procura. |
{: caption="Tabela 17. Opções do comando cf ba add-report" caption-side="top"}

Também é possível usar **`ba ar`** como um alias para o nome de comando mais longo **`ba add-report`**.
{: tip}

### Excluindo relatórios
{: #admin_del_report}

Para excluir um relatório de segurança, use o comando a seguir:

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _category_ | A categoria para o relatório. Se houver um espaço no nome, use aspas. |
| _date_ | A data do relatório no formato de AAAAMMDD. |  
| _name_ | O nome do relatório. |
{: caption="Tabela 18. Opções do comando cf ba delete-report" caption-side="top"}

Também é possível usar **`ba d`r** como um alias para o nome de comando mais longo **`ba delete-report`**.
{: tip}

### Recuperando relatórios
{: #admin_retr_report}

Para recuperar um relatório de segurança, use o comando a seguir:

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">O nome do arquivo do relatório. Se houver um espaço no nome, use as aspas em torno do nome.</dd>
</dl>

Também é possível usar **`ba rr`** como um alias para o nome de comando mais longo **`ba retrieve-report`**.
{: tip}

## Visualizando informações de métrica de recurso
{: #cliresourceusage}

É possível visualizar informações de métrica de recurso, incluindo memória, disco e uso de CPU. É possível ver um resumo dos recursos físicos e reservados disponíveis, bem como o uso de recursos físicos e reservados. Também é possível ver dados de uso de Droplet Execution Agents (DEAs) e células (arquitetura Diego). Para visualizar as informações de métrica de recurso, use o comando a seguir:

```
cf ba resource-metrics
```

Também é possível usar **`ba rsm`** como um alias para o nome de comando mais longo **`ba resource-metrics`**.
{: tip}

## Visualizando o histórico de métrica de recurso
{: #cliresourceusagehistory}

É possível recuperar o histórico de métrica de recurso para uso de memória e disco. As métricas retornadas incluem a quantia
de recursos que são usados fora do total disponível para ambos os recursos, físico e reservado. Os dados históricos para uso de memória e disco podem ser exibidos por hora, diariamente ou mensalmente. É possível especificar datas de início e de encerramento para recuperar dados dentro de um intervalo de data específico. Os dados históricos padrão, quando nenhuma data é especificada, são dados de memória por hora para as últimas 48 horas. Os dados são exibidos em ordem decrescente, com as datas mais recentes mostradas primeiro. Para visualizar as informações de histórico de métrica de recurso, use o comando a seguir:

```
cf ba resource-metrics-history <hourly|daily|monthly>  <memory|disk >  <start|end>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| --hourly | View the historical data for the last 48 hours. This is the default value. |
| --daily | View the historical data daily average for the last 30 days. |  
| --monthly | View the historical data monthly average for the last 6 months. |
| --memory | View the used and total reserved and physical memory. |
| --disk | View the used and total reserved and physical disk. | 
| --start | Specify a start date for daily or monthly in the format of mm-dd-yyyy, or start date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
| --end | Specify an end date for daily or monthly in the format of mm-dd-yyyy, or end date and time for hourly in the format of mm-dd-yyyy hh:mm:ss time zone. |
{: caption="Tabela 19. Opções do comando cf ba resource-metrics-history" caption-side="top"}

**Exemplos**

```
cf ibmcloud-admin resource-metrics-history
cf ibmcloud-admin resource-metrics-history --daily --disk --start=07-04-2017
cf ibmcloud-admin resource-metrics-history --monthly --memory
cf ibmcloud-admin resource-metrics-history --hourly --start="06-01-2017 00:00:00 EDT" --end="06-30-2017 23:59:00 EDT
```
{: codeblock}

É possível visualizar a lista anterior de parâmetros de comando e exemplos usando o comando a seguir:

```
cf ba resource-metrics-history -help
```

Também é possível usar **`ba rsmh`** como um alias para o nome de comando mais longo **`ba resource-metrics-history`**.
{: tip}

## Administrando brokers de serviço
{: #admin_servbro}

### Listando brokers de serviço
{: #clilistservbro}

Para listar brokers de serviço, use o comando a seguir:

```
cf ba service-brokers <broker_name>
```
{: codeblock}

Para listar todos os brokers de serviço, insira o comando sem o parâmetro **`broker_name`**.

<dl class="parml">
<dt class="pt dlterm">&lt;nome_do_servidor_intermediário&gt;</dt>
<dd class="pd">O nome do broker de serviço customizado. Use esse parâmetro se desejar obter informações de um broker de serviço específico. Opcional.</dd>
</dl>

Também é possível usar **`ba sb`** como um alias para o nome de comando mais longo **`ba service-brokers`**.
{: tip}

### Incluindo um broker de serviço
{: #cliaddservbro}

Para incluir um broker de serviço para que seja possível incluir um serviço customizado no catálogo do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _brokerName_ | O nome do broker de serviço customizado. |
| _userName_ | O nome do usuário para a conta que tem acesso ao broker de serviço. |  
| _password_ | A senha para a conta que tem acesso ao broker de serviço. |
| _brokerURL_ | A URL para o broker de serviço. |
{: caption="Tabela 20. Opções do comando cf ba add-service-broker" caption-side="top"}

Também é possível usar **`ba asb`** como um alias para o nome de comando mais longo **`ba add-service-broker`**.
{: tip}

### Excluindo um broker de serviço
{: #clidelservbro}

Para excluir um broker de serviço que remove o serviço customizado do
catálogo do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">O nome ou o GUID do broker de serviço customizado.</dd>
</dl>

Também é possível usar **`ba dsb`** como um alias para o nome de comando mais longo **`ba delete-service-broker`**.
{: tip}

### Atualizando um broker de serviço
{: #cliupdservbro}

Para atualizar um broker de serviço, use o comando a seguir:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _brokerName_ | O nome do broker de serviço customizado. |
| _userName_ | O nome do usuário para a conta que tem acesso ao broker de serviço. |  
| _password_ | A senha para a conta que tem acesso ao broker de serviço. |
| _brokerURL_ | A URL para o broker de serviço. |
{: caption="Tabela 21. Opções do comando cf ba update-service-broker" caption-side="top"}

Também é possível usar **`ba usb`** como um alias para o nome de comando mais longo **`ba update-service-broker`**.
{: tip}

## Administrando grupos de segurança do aplicativo
{: #admin_secgro}

Para trabalhar com grupos de segurança do aplicativo (ASGs), você deve ser um
administrador com acesso total para o ambiente local ou dedicado. Todos os usuários do
ambiente podem listar os ASGs disponíveis para a organização que está sendo alvo com o
comando. No entanto, para criar, atualizar ou ligar ASGs, você deve ser um
administrador do ambiente {{site.data.keyword.Bluemix_notm}}.

Os ASGs funcionam como firewalls virtuais que controlam o tráfego de saída dos apps em seu ambiente do {{site.data.keyword.cloud_notm}}. Cada ASG consiste
em uma lista de regras que permitem tráfego e comunicação específicos de/para a
rede externa. É possível ligar um ou mais ASGs a um conjunto de grupos de segurança
específicos, por exemplo, um conjunto de grupos usado para aplicar acesso global ou
você pode ligar aos espaços dentro de uma organização em seu ambiente do
{{site.data.keyword.Bluemix_notm}}.

O {{site.data.keyword.Bluemix_notm}} é configurado inicialmente com todos
os acessos à rede externa restrita. Dois grupos de segurança criados pela IBM,
`public_networks` e `dns`, permitem acesso global à
rede externa quando você liga esses grupos aos conjuntos de grupos de segurança padrão do
Cloud Foundry. Os dois conjuntos de grupos de segurança no Cloud Foundry que são usados
para aplicar acesso global são **Preparação padrão** e
**Execução padrão**. Esses conjuntos de grupos aplicam as regras para
permitir o tráfego para todos os apps em execução ou todos os apps de preparação. Se você
não desejar ligar a esses dois conjuntos grupos de segurança, poderá desvincular dos
conjuntos de grupos do Cloud Foundry e depois ligar o grupo de segurança a um espaço
específico. Para obter mais informações, consulte [Ligando grupos de segurança do aplicativo](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

A desvinculação dos conjuntos de grupos **Preparação padrão** ou **Execução padrão** dos dois grupos de segurança criados pela IBM, `public_networks` e `dns`, desativa o acesso global à rede externa. Use a desvinculação com cuidado e reconhecimento de seu impacto potencial nos apps em execução e de preparação em seu ambiente.
{: important}

Os comandos a seguir que permitem que você trabalhe com grupos de segurança são baseados na versão 1.6 do Cloud Foundry. Para obter mais informações, incluindo campos obrigatórios e opcionais, consulte as informações do Cloud Foundry sobre [Criando grupos de segurança do aplicativo](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

### Listando grupos de segurança
{: #clilissecgro}

Para listar todos os grupos de segurança, use o comando a seguir:

```
cf ba security-groups
```
{: codeblock}

Para exibir detalhes para um grupo de segurança específico, use o comando a seguir:

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba sg`** como um alias para o nome de comando mais longo **`ba security-groups`**.
{: tip}

### Criando um Grupo de Segurança
{: #clicreasecgro}

Para criar um grupo de segurança, use o comando a seguir:
```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

Cada grupo
de segurança que você cria tem o prefixo `adminconsole_` incluído no
nome para distingui-lo dos grupos de segurança criados pela IBM.

| Opção | Descrição | 
| -------| ------------|
| _groupName_ | O nome do grupo de segurança. |
| _filePath_ | O caminho absoluto ou relativo para um arquivo de regras. |  
{: caption="Tabela 22. Opções do comando cf ba create-security-group" caption-side="top"}

Também é possível usar **`ba csg`** como um alias para o nome de comando mais longo **`ba create-security-group`**.
{: tip}

Para obter mais informações sobre a criação de grupos de segurança e as regras que definem o tráfego de saída, consulte [Criando grupos de segurança do aplicativo](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

### Atualizando um grupo de segurança
{: #cliupdsecgro}

Para atualizar um grupo de segurança, use o comando a seguir:

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _groupName_ | O nome do grupo de segurança. |
| _filePath_ | O caminho absoluto ou relativo para um arquivo de regras. |  
{: caption="Tabela 23. Opções do comando cf ba update-security-group" caption-side="top"}

Também é possível usar **`ba usg`** como um alias para o nome de comando mais longo **`ba update-security-group`**.
{: tip}

### Excluindo um Grupo de Segurança
{: #clidelsecgro}

Para excluir um grupo de segurança, use o comando a seguir:
```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba dsg`** como um alias para o nome de comando mais longo **`ba delete-security-group`**.
{: tip}

### Ligando grupos de segurança
{: #clibindsecgro}

Para ligar ao conjunto de grupos de segurança de Preparação padrão, use o comando a seguir:

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba bssg`** como um alias para o nome de comando mais longo **`ba bind-staging-security-group`**.
{: tip}

Para ligar ao conjunto de grupos de segurança de Execução padrão, use o comando a seguir:

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba brsg`** como um alias para o nome de comando mais longo **`ba bind-running-security-group`**.
{: tip}

Para ligar um grupo de segurança a um espaço, use o comando a seguir:

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _groupName_ | O nome do grupo de segurança. |
| _org_ | O nome da organização à qual ligar o grupo de segurança. |
| _space_ | O nome do espaço dentro da organização à qual ligar o grupo de segurança. |
{: caption="Tabela 24. Opções do comando cf ba bind-security-group" caption-side="top"}

Também é possível usar **`ba bsg`** como um alias para o nome de comando mais longo **`ba bind-security-group`**.
{: tip}

Para obter mais informações sobre como ligar grupos de segurança, consulte [Ligando grupos de segurança do aplicativo](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

### Desvinculando grupos de segurança
{: #cliunbindsecgro}

A desvinculação do conjunto de grupos Preparação padrão dos dois grupos de segurança criados pela IBM, `public_networks` e `dns`, desativa o acesso global à rede externa e deve ser usada com cuidado e entendimento das ramificações que têm em todos os apps de preparação em seu ambiente. Para desvincular de um conjunto de grupos de segurança de Preparação padrão, use o comando a seguir:

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba ussg`** como um alias para o nome de comando mais longo **`ba unbind-staging-security-group`**.
{: tip}

A desvinculação do conjunto de grupos Execução padrão dos dois grupos de segurança criados pela IBM, `public_networks` e `dns`, desativa o acesso global à rede externa e deve ser usada com cuidado e entendimento das ramificações que têm em todos os apps em execução em seu ambiente. Para desvincular de um conjunto de grupos de segurança de Execução padrão, use o comando a seguir:

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

Também é possível usar **`ba brsg`** como um alias para o nome de comando mais longo **`ba unbind-running-security-group`**.
{: tip}

Para desvincular um grupo de segurança de um espaço, use o comando a seguir:

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _groupName_ | O nome do grupo de segurança. |
| _org_ | O nome da organização da qual desvincular o grupo de segurança. |
| _space_ | O nome do espaço dentro da organização da qual desvincular o grupo de segurança. |
{: caption="Tabela 25. Opções do comando cf ba unbind-security-group" caption-side="top"}

Também é possível usar **`ba usg`** como um alias para o nome de comando mais longo **`ba unbind-security-group`**.
{: tip}

Para obter mais informações sobre a desvinculação de grupos de segurança, consulte [Desvinculando grupos de segurança do aplicativo](https://docs.cloudfoundry.org/concepts/asg.html#unbinding-groups){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo").

## Administrando buildpacks
{: #admin_buildpack}

### Listando buildpacks
{: #clilistbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível listar os buildpacks. Para listar todos os buildpacks ou visualizar um buildpack
específico, use o comando a seguir:

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Um parâmetro opcional para especificar um buildpack específico para visualizar.</dd>
</dl>

Também é possível usar **`ba lb`** como um alias para o nome de comando mais longo **`ba buildpacks`**.
{: tip}

### Criando e fazendo upload de um buildpack
{: #clicreupbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível criar e fazer upload de um buildpack. É possível fazer upload de qualquer arquivo compactado que tenha um tipo de arquivo `.zip`. Para
fazer upload de um buildpack, use o comando a seguir:

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _name_ | O nome do buildpack a ser transferido por upload. |
| _filePath_ | O caminho para o arquivo compactado buildpack. |
| _position_ | A ordem na qual os buildpacks são verificados durante a detecção automática de buildpack. |
{: caption="Tabela 26. Opções do comando cf ba create-buildpack" caption-side="top"}

Também é possível usar **`ba cb`** como um alias para o nome de comando mais longo **`ba create-buildpack`**.
{: tip}

### Atualizando um buildpack
{: #cliupdabuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível atualizar um buildpack existente. Para atualizar um buildpack, use o comando a
seguir:
```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

| Opção | Descrição | 
| -------| ------------|
| _name_ | O nome do buildpack a ser atualizado. |
| _position_ | A ordem na qual os buildpacks são verificados durante a detecção automática de buildpack. |
| _enabled_ | Indica se o buildpack é usado para preparação. |
| _locked_ | Indica se o buildpack está bloqueado para evitar atualizações. | 
{: caption="Tabela 27. Opções do comando cf ba update-buildpack" caption-side="top"}

Também é possível usar **`ba ub`** como um alias para o nome de comando mais longo **`ba update-buildpack`**.
{: tip}

### Excluindo um buildpack
{: #clidelbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível excluir um buildpack existente. Para excluir um buildpack, use o comando a seguir:
```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">O nome do buildpack a ser excluído.</dd>
</dl>

Também é possível usar **`ba db`** como um alias para o nome de comando mais longo **`ba delete-buildpack`**.
{: tip}
