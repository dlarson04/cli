---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-29"

keywords: iam, iam access, api keys, service ids, access groups, authorization policy, ibmcloud iam, cli, manage keys, manage service ids, manage iam users cli, iam cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:codeblock: .codeblock}
{:note: .note}

# Gerenciando o acesso ao IAM, as chaves API, os IDs de serviço e os grupos de acesso
{: #ibmcloud_commands_iam}

Use os comandos a seguir para gerenciar chaves de API, IDs de serviço, grupos de acesso e políticas de autorização para usuários, serviços e grupos de acesso.
{: shortdesc}

## IDs de serviço iam ibmcloud
{: #ibmcloud_iam_service_ids}

Listar todos os IDs de serviço:
```
Ibmcloud iam service-ids [ -- uuid ]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>--uuid</dt>
  <dd>Mostrar somente o UUID dos IDs de serviço</dd>
</dl>

<strong>Exemplos</strong>:

Listar UUID de todos os IDs de serviço na conta atual:
```
ibmcloud iam service-ids --uuid
```
{: codeblock}

## Ibmcloud iam service-id
{: #ibmcloud_iam_service_id}

Exibir detalhes de um ID de serviço:
```
Ibmcloud iam service-id (NAME | UUID) [ -- uuid ]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço, exclusivo com UUID</dd>
  <dt>UUID (necessário)</dt>
  <dd>UUID do serviço, exclusivo com NAME</dd>
  <dt>--uuid</dt>
  <dd>Exibir o UUID do ID de serviço</dd>
</dl>

<strong>Exemplos</strong>:

Mostrar detalhes do ID de serviço `sample-test`:
```
Ibmcloud iam service-id sample-teste
```
{: codeblock}

Mostrar detalhes do ID de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-id ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976
```
{: codeblock}

## Ibmcloud iam service-id-create
{: #ibmcloud_iam_service_id_create}

Criar um ID de serviço:
```
ibmcloud iam service-id-create NAME [-d, --description DESCRIPTION] [--lock]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço</dd>
  <dt>-d, --description</dt>
  <dd>Descrição do ID de serviço</dd>
  <dt>-- bloqueio</dt>
  <dd>Bloquear o ID do serviço ao criá-lo</dd>
</dl>

<strong>Exemplos</strong>:

Criar um ID de serviço com o nome do serviço `sample-test` e a descrição `hello, world!`:
```
ibmcloud iam service-id-create sample-test -d 'hello, world!'
```
{: codeblock}

Criar um ID de serviço bloqueado com o nome do serviço `sample-test` e a descrição `hello, world!`:
```
ibmcloud iam service-id-create sample-test -d 'hello, world!' -- bloqueio
```
{: codeblock}

## Ibmcloud iam service-id-update
{: #ibmcloud_iam_service_id_update}

Atualizar um ID de serviço:
```
ibmcloud iam service-id-update (NAME|UUID) [-n, --name NEW_NAME] [-d, --description DESCRIPTION] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço, exclusivo com UUID</dd>
  <dt>UUID (necessário)</dt>
  <dd>UUID do serviço, exclusivo com NAME</dd>
  <dt>-n, --name</dt>
  <dd>Novo nome do serviço</dd>
  <dt>-d, --description</dt>
  <dd>Nova descrição do serviço</dd>
  <dt>-f, --force</dt>
  <dd>Atualizar sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Renomear o ID de serviço `sample-test` para `sample-test-2` sem confirmação:
```
ibmcloud iam service-id-update sample-test -n sample-test-2 -f
```
{: codeblock}

Atualizar a descrição de serviço `sample-test`:
```
ibmcloud iam service-id-update sample-test -d 'hello, friend!'
```
{: codeblock}

Renomear o ID de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976` para `sample-test-3` com a nova descrição:
```
ibmcloud iam service-id-update ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976 -n sample-test-3 -d 'hello, my friends!'
```
{: codeblock}

## ibmcloud iam service-id-delete
{: #ibmcloud_iam_service_id_delete}

Excluir um ID de serviço:
```
Ibmcloud iam service-id-delete (NAME | UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço, exclusivo com UUID</dd>
  <dt>UUID (necessário)</dt>
  <dd>UUID do serviço, exclusivo com NAME</dd>
  <dt>-f, --force</dt>
  <dd>Excluir sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Excluir o ID de serviço `sample-teset` sem confirmação:
```
Ibmcloud iam service-id-delete sample-teset -f
```
{: codeblock}

Excluir o ID de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-id-delete ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976
```
{: codeblock}

## ibmcloud iam service-id-lock
{: #ibmcloud_iam_service_id_lock}

Bloquear um ID de serviço:
```
Ibmcloud iam service-id-bloqueio (NAME | UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço, exclusivo com UUID</dd>
  <dt>UUID (necessário)</dt>
  <dd>UUID do serviço, exclusivo com NAME</dd>
  <dt>-f, --force</dt>
  <dd>Bloquear sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

bloqueie o ID do serviço `sample-teset` sem confirmação:
```
ibmcloud iam service-id-lock sample-teset -f
```
{: codeblock}

Bloquear ID de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-id-de bloqueio ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976
```
{: codeblock}

## ibmcloud iam service-id-unlock
{: #ibmcloud_iam_service_id_unlock}

Desbloquear um ID de serviço:
```
ibmcloud iam service-id-unlock (NAME|UUID) [-f, --force]
```
{: codeblock}

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do serviço, exclusivo com UUID</dd>
  <dt>UUID (necessário)</dt>
  <dd>UUID do serviço, exclusivo com NAME</dd>
  <dt>-f, --force</dt>
  <dd>Desbloquear sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

desbloqueie o ID de serviço `sample-teset` sem confirmação:
```
Ibmcloud iam service-id-unlock sample-teset -f
```
{: codeblock}

Desbloquear o ID de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-id-desbloquear ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976
```
{: codeblock}

## ibmcloud iam api-keys
{: #ibmcloud_iam_api_keys}

Listar todas as chaves de API da plataforma do {{site.data.keyword.Bluemix_notm}}:
```
ibmcloud iam api-keys
```
{: codeblock}

<strong>Pré-requisitos</strong>: Terminal, Login

## Ibmcloud iam api-key-create
{: #ibmcloud_iam_api_key_create}

Criar uma nova chave de API da plataforma {{site.data.keyword.cloud_notm}}:
```
ibmcloud iam api-key-create NAME [-d DESCRIPTION] [--file FILE] [--lock]
```

Usar o login da CLI do {{site.data.keyword.cloud_notm}} com uma Chave de API não funciona com a chave de API de SL anterior localizada em `control.softlayer.com`. Uma Conta do {{site.data.keyword.cloud_notm}} submetida a upgrade em que a Infraestrutura é gerenciada por meio de [cloud.ibm.com](https://cloud.ibm.com/registration){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo") é necessária para o login da CLI do {{site.data.keyword.cloud_notm}} com uma chave de API.
{: note}

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser criada.</dd>
<dt>-d <i>DESCRIPTION</i> (opcional)</dt>
<dd>Descrição da chave de API</dd>
<dt>--file <i>FILE</i></dt>
<dd>Salve as informações da chave API para o arquivo especificado.</dd>
<dt>-- bloqueio</dt>
<dd>Bloquear a chave API ao criá-la</dd>
</dl>

<strong>Exemplos</strong>:

Criar uma chave de API e salvar em um arquivo:
```
ibmcloud iam api-key-create MyKey -d "this is my API key" --file key_file
```
{: codeblock}

Criar uma chave de API bloqueada com o nome "test-key":
```
Ibmcloud iam api-key-create test-key -- bloqueio
```
{: codeblock}

## Ibmcloud iam api-key-update
{: #ibmcloud_iam_api_key_update}

Atualizar uma chave de API da plataforma {{site.data.keyword.Bluemix_notm}}:
```
ibmcloud iam api-key-update (NAME|UUID) [-n name] [-d description]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>O nome antigo da chave API a ser atualizada, exclusivo com UUID</dd>
<dt>UUID (necessário)</dt>
<dd>O UUID da chave API a ser atualizada, exclusivo com NAME</dd>
<dt>-n <i>NAME</i> (opcional)</dt>
<dd>O nome novo da chave API</dd>
<dt>-d <i>DESCRIPTION</i> (opcional)</dt>
<dd>A nova descrição da chave API</dd>
</dl>

<strong>Exemplos</strong>:

Atualizar a descrição de uma chave API:
```
ibmcloud iam api-key-update MyKey -d "the new description of my key"
```
{: codeblock}

## Ibmcloud api-key-delete
{: #ibmcloud_iam_api_key_delete}

Excluir uma chave de API da plataforma {{site.data.keyword.Bluemix_notm}}:
```
Ibmcloud iam api-key-delete (NAME | UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser excluída, exclusivo com UUID</dd>
<dt>UUID (necessário)</dt>
<dd>UUID da chave API a ser excluída, exclusivo com NAME</dd>
<dt>-f, --force</dt>
<dd>Force a exclusão sem confirmação.</dd>
</dl>

## Ibmcloud api-key-bloqueio
{: #ibmcloud_iam_api_key_lock}

Bloqueie uma chave de API da plataforma:
```
Ibmcloud iam api-key-bloqueio (NAME | UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser bloqueada, exclusivo com UUID</dd>
<dt>UUID (necessário)</dt>
<dd>UUID da chave API a ser bloqueada, exclusivo com NAME</dd>
<dt>-f, --force</dt>
<dd>Forçar a fechadura sem confirmação.</dd>
</dl>

<strong>Exemplos</strong>:

Bloquear a chave de API test-api-key:
```
Ibmcloud iam api-key-bloqueio de teste api-key
```
{: codeblock}

Bloquear a chave de API com o UUID fornecido sem confirmação:
```
ibmcloud iam api-key-lock ApiKey-18f773b0-db53-43f1-ad68-92c667c218fe --force
```
{: codeblock}s

## Ibmcloud api-key-desbloquear
{: #ibmcloud_iam_api_key_unlock}

Desbloquear uma chave de API da plataforma:
```
Ibmcloud iam api-key-desbloquear (NAME | UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser desbloqueada, exclusivo com UUID</dd>
<dt>UUID (necessário)</dt>
<dd>UUID da chave API a ser desbloqueada, exclusivo com NAME</dd>
<dt>-f, --force</dt>
<dd>Forçar o desbloqueio sem confirmação.</dd>
</dl>

<strong>Exemplos</strong>:

Desbloquear a chave de API test-api-key:
```
Ibmcloud iam api-key-unlock-api-chave de teste
```
{: codeblock}

Desbloquear a chave de API com o UUID fornecido sem confirmação:
```
Ibmcloud iam api-key-desbloquear ApiKey-18f773b0-db53-43f1-ad68-92c667c218fe -- force
```
{: codeblock}

## Ibmcloud iam service-api-keys
{: #ibmcloud_iam_service_api_keys}

Listar todas as chaves de API de um serviço:
```
Ibmcloud iam service-api-keys (SERVICE_ID_NAME | SERVICE_ID_UUID) [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-f, --force</dt>
  <dd>Exibir as chaves API de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Liste todas as chaves API do serviço `sample-service`:
```
Ibmcloud iam service-api-keys sample-service
```
{: codeblock}

## Ibmcloud iam service-api-key
{: #ibmcloud_iam_service_api_key}

Listar detalhes de uma chave de API de serviço:
```
ibmcloud iam service-api-key (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [--uuid] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>APIKEY_NAME (necessário)</dt>
  <dd>Nome da chave API, exclusivo com APIKEY_UUID</dd>
  <dt>APIKEY_UUID (necessário)</dt>
  <dd>UUID da chave API, exclusivo com APIKEY_NAME</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>--uuid</dt>
  <dd>Exibir o UUID da chave API de serviço</dd>
  <dt>-f, --force</dt>
  <dd>Exibir a chave API de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Mostrar detalhes da chave API de serviço `sample-key` do serviço `sample-serviço`:
```
Ibmcloud iam service-api-key sample-key sample-service
```
{: codeblock}

## ibmcloud iam service-api-key-create
{: #ibmcloud_iam_service_api_key_create}

Criar uma chave de API de serviço:
```
ibmcloud iam service-api-key-create NAME (SERVICE_ID_NAME|SERVICE_ID_UUID) [-d, --description DESCRIPTION] [--file FILE] [-f, --force] [--lock]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>NAME (necessário)</dt>
  <dd>Nome do ID do serviço ou da chave API de serviço recém-criada</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-d, --description</dt>
  <dd>Descrição da chave de API</dd>
  <dt>--file</dt>
  <dd>Salve as informações da chave API para o arquivo especificado.</dd>
  <dt>-f, --force</dt>
  <dd>Forçar a criação sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Criar uma chave API de serviço `sample-key` para o serviço
`sample-service` sem confirmação:
```
Ibmcloud iam service-api-key-create sample-key sample-service -f
```
{: codeblock}

## Ibmcloud iam service-api-key-update
{: #ibmcloud_iam_service_api_key_update}

Atualizar uma chave de API de serviço:
```
ibmcloud iam service-api-key-update (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID)  [-n, --name NEW_NAME] [-d, --description DESCRIPTION] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>APIKEY_NAME (necessário)</dt>
  <dd>Nome da chave API, exclusivo com APIKEY_UUID</dd>
  <dt>APIKEY_UUID (necessário)</dt>
  <dd>UUID da chave API, exclusivo com APIKEY_NAME</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-n, --name</dt>
  <dd>Novo nome da chave API de serviço</dd>
  <dt>-d, --description</dt>
  <dd>Nova descrição da chave API de serviço</dd>
  <dt>-f, --force</dt>
  <dd>Atualizar sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Renomeie a chave API de serviço `sample-key` para `new-sample-key`:
```
ibmcloud iam service-api-key-update sample-key sample-service -n new-sample-key
```
{: codeblock}

## Ibmcloud iam service-api-key-delete
{: #ibmcloud_iam_service_api_key_delete}

Excluir uma chave de API de serviço:
```
ibmcloud iam service-api-key-delete (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>APIKEY_NAME (necessário)</dt>
  <dd>Nome da chave API, exclusivo com APIKEY_UUID</dd>
  <dt>APIKEY_UUID (necessário)</dt>
  <dd>UUID da chave API, exclusivo com APIKEY_NAME</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-f, --force</dt>
  <dd>Excluir sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Excluir a chave API de serviço `sample-key` do ID de serviço `sample-serviço`:
```
Ibmcloud iam service-api-key-delete sample-key sample-service
```
{: codeblock}

## ibmcloud iam service-api-key-lock
{: #ibmcloud_iam_service_api_key_lock}

Bloquear uma chave de API de serviço:
```
ibmcloud iam service-api-key-lock (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>APIKEY_NAME (necessário)</dt>
  <dd>Nome da chave API, exclusivo com APIKEY_UUID</dd>
  <dt>APIKEY_UUID (necessário)</dt>
  <dd>UUID da chave API, exclusivo com APIKEY_NAME</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-f, --force</dt>
  <dd>Bloquear sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Bloquear a chave API de serviço `sample-key` do ID do serviço `sample-service`:
```
Ibmcloud iam service-api-key-bloqueio sample-key sample-service
```
{: codeblock}

## Ibmcloud iam service-api-key-desbloquear
{: #ibmcloud_iam_service_api_key_unlock}

Desbloquear uma chave de API de serviço:
```
ibmcloud iam service-api-key-unlock (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>APIKEY_NAME (necessário)</dt>
  <dd>Nome da chave API, exclusivo com APIKEY_UUID</dd>
  <dt>APIKEY_UUID (necessário)</dt>
  <dd>UUID da chave API, exclusivo com APIKEY_NAME</dd>
  <dt>SERVICE_ID_NAME (necessário)</dt>
  <dd>Nome do ID do serviço, exclusivo com SERVICE_ID_UUID</dd>
  <dt>SERVICE_ID_UUID (necessário)</dt>
  <dd>UUID do ID do serviço, exclusivo com SERVICE_ID_NAME</dd>
  <dt>-f, --force</dt>
  <dd>Desbloquear sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Desbloquear a chave API de serviço `sample-key` do ID do serviço `sample-service`:
```
Ibmcloud iam service-api-key-desbloquear sample-key sample-service
```
{: codeblock}

## Ibmcloud iam user-policies
{: #ibmcloud_iam_user_policies}

Listar as políticas do usuário `name@example.com`:
```
ibmcloud iam user-policies name@example.com
```

<strong>Pré-requisitos</strong>: terminal, login, conta de destino

<strong>Opções de comando</strong>:
<dl>
<dt>USER_NAME ((necessário))</dt>
<dd>Nome do usuário ao qual as políticas pertencem</dd>
</dl>

<strong>Exemplos</strong>:

Listar as políticas do usuário `name@example.com`:
```
ibmcloud iam user-policies name@example.com
```

## Ibmcloud iam user-policy
{: #ibmcloud_iam_user_policy}

Exibir detalhes de uma política do usuário:
```
Ibmcloud iam user-policy USER_NAME POLICY_ID
```

<strong>Pré-requisitos</strong>: terminal, login, conta de destino

<strong>Opções de comando</strong>:
<dl>
<dt>USER_NAME ((necessário))</dt>
<dd>Nome do usuário ao qual a política pertence</dd>
<dt>POLICY_ID (necessário)</dt>
<dd>ID da política</dd>
</dl>

<strong>Exemplos</strong>:

Liste a política `0bb730daa` do usuário `name@example.com`:
```
Ibmcloud iam user-policy name@example.com 0bb730daa
```

## Ibmcloud iam user-policy-create
{: #ibmcloud_iam_user_policy_create}

Criar uma política de usuário:
```
ibmcloud iam user-policy-create USER_NAME {--file JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```

<strong>Pré-requisitos</strong>: terminal, login, conta de destino

<strong>Opções de comando</strong>:
<dl>
<dt>USER_NAME ((necessário))</dt>
<dd>Nome do usuário ao qual a política pertence</dd>
<dt>--file <i>FILE</i> (opcional)</dt>
<dd>Arquivo JSON de definição de política</dd>
<dt>--roles <i>ROLE_NAME1,ROLE_NAME2...</i> (opcional)</dt>
<dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
<dt>--service-name <i>SERVICE_NAME</i> (opcional)</dt>
<dd>Nome do serviço da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>-- serivce-instance <i>SERVICE_INSTANCE_GUID</i> (opcional)</dt>
<dd>GUID da instância de serviço da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--region <i>REGION</i> (opcional)</dt>
<dd>Região da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource-type <i>RESOURCE_TYPE</i> (opcional)</dt>
<dd>Tipo de recurso da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource <i>RESOURCE</i> (opcional)</dt>
<dd>Recurso da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource-group-name <i>RESOURCE_GROUP_NAME</i> (opcional)</dt>
<dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Isso é exclusivo com as sinalizações `--file`, `--resource` e `--resource-group-id`.</dd>
<dt>--resource-group-id <i>RESOURCE_GROUP_ID</i> (opcional)</dt>
<dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Isso é exclusivo com as sinalizações `--file`, `--resource` e `--resource-group-name`.</dd>
</dl>

<strong>Exemplos</strong>:

Crie a política de usuário para o usuário `name@example.com` do arquivo JSON de política `policy.json`:
```
Ibmcloud iam user-policy-create name@example.com -- file
```

Dê a `name@example.com` a função `Administrator` para todos os recursos `sample-service`:
```
ibmcloud iam user-policy-create name@example.com --roles Administrator --service-name sample-service
```

Fornecer a função de `Editor` a `name@example.com` para o recurso `key123` da
instância de serviço de amostra com o GUID `d161aeea-fd02-40f8-a487-df1998bd69a9` na região `us-south`:
```
ibmcloud iam user-policy-create name@example.com --roles Editor --service-name sample-service --service-instance
d161aeea-fd02-40f8-a487-df1998bd69a9 --region us-south --resource-type key --resource key123
```

Dê a `name@example.com` a função `Operator` para o grupo de recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam user-policy-create name@example.com --roles Operator --resource-type resource-group --resource dda27e49d2a1efca58083a01dfde18f6
```

Dê a `name@example.com` a função `Viewer` para os membros do grupo de recursos `sample-resource-group`:
```
ibmcloud iam user-policy-create name@example.com --roles Viewer --resource-group-name sample-resource-group
```

Dê a `name@example.com` a função `Viewer` para os membros do grupo de recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam user-policy-create name@example.com --roles Viewer --resource-group-id dda27e49d2a1efca58083a01dfde18f6
```

## Ibmcloud iam user-policy-update
{: #ibmcloud_iam_user_policy_update}

Atualizar uma política de usuário:
```
ibmcloud iam user-policy-update USER_NAME POLICY_ID {--file JSON_FILE | [--roles ROLE_NAME1,ROLE_NAME2...] [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```

<strong>Pré-requisitos</strong>: terminal, login, conta de destino

<strong>Opções de comando</strong>:
<dt>USER_NAME ((necessário))</dt>
<dd>Nome do usuário ao qual a política pertence</dd>
<dt>POLICY_ID (necessário)</dt>
<dd>ID da política a ser atualizada</dd>
<dt>--file <i>FILE</i> (opcional)</dt>
<dd>Arquivo JSON de definição de política</dd>
<dt>--roles <i>ROLE_NAME1,ROLE_NAME2...</i> (opcional)</dt>
<dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
<dt>--service-name <i>SERVICE_NAME</i> (opcional)</dt>
<dd>Nome do serviço da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>-- serivce-instance <i>SERVICE_INSTANCE_GUID</i> (opcional)</dt>
<dd>GUID da instância de serviço da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--region <i>REGION</i> (opcional)</dt>
<dd>Região da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource-type <i>RESOURCE_TYPE</i> (opcional)</dt>
<dd>Tipo de recurso da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource <i>RESOURCE</i> (opcional)</dt>
<dd>Recurso da definição de política; isso é exclusivo com a sinalização `--file`.</dd>
<dt>--resource-group-name <i>RESOURCE_GROUP_NAME</i> (opcional)</dt>
<dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Isso é exclusivo com as sinalizações `--file`, `--resource` e `--resource-group-id`.</dd>
<dt>--resource-group-id <i>RESOURCE_GROUP_ID</i> (opcional)</dt>
<dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Isso é exclusivo com as sinalizações `--file`, `--resource` e `--resource-group-name`.</dd>
</dl>

<strong>Exemplos</strong>:

Atualize a política de usuário com aquela do arquivo JSON
```
ibmcloud iam user-policy-update name@example.com 0bb730daa --file @policy.json
```

Atualize a política de usuário para dar a `name@example.com` a função `Administrator` para todos os recursos `sample-service`：
```
ibmcloud iam user-policy-update name@example.com user-policy-id --roles Administrator --service-name sample-service
```

Atualizar a política do usuário para fornecer a função de `Editor` a `name@example.com` para
o recurso `key123` da instância de serviço de amostra com o GUID `d161aeea-fd02-40f8-a487-df1998bd69a9`
na região `us-south`:
```
ibmcloud iam user-policy-update name@example.com --roles Editor --service-name sample-service --service-instance d161aeea-fd02-40f8-a487-df1998bd69a9 --region us-south --resource-type key --resource key123
```

Atualize a política de usuário para dar a `name@example.com` a função `Operator` para o grupo de recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam user-policy-update name@example.com user-policy-id --roles Operator --resource-type resource-group --resource dda27e49d2a1efca58083a01dfde18f6
```

Atualize a política de usuário para dar a `name@example.com` a função `Viewer` para os membros do grupo de recursos `sample-resource-group`:
```
ibmcloud iam user-policy-update name@example.com user-policy-id --roles Viewer --resource-group-name sample-resource-group
```

Atualize a política de usuário para dar a `name@example.com` a função `Viewer` para membros do grupo de recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam user-policy-update name@example.com user-policy-id --roles Viewer --resource-group-id dda27e49d2a1efca58083a01dfde18f6
```

## Ibmcloud iam user-policy-delete
{: #ibmcloud_iam_user_policy_delete}

Excluir uma política do usuário
```
ibmcloud iam user-policy-delete USER_ID POLICY_ID [-f, --force]
```

<strong>Pré-requisitos</strong>: terminal, login, conta de destino

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Exclua a política do usuário sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Excluir as políticas `user-policy-id` do usuário `name@example.com`:
```
Delete-ibmcloud iam user-policy name@example.com user-policy-id
```

Excluir as políticas `user-policy-id` do usuário `name@example.com` sem confirmação:
```
Ibmcloud iam user-policy-delete name@example.com user-policy-id -f
```

## As políticas de serviço iam ibmcloud
{: #ibmcloud_iam_service_policies}

Listar todas as políticas de serviço do serviço especificado:
```
ibmcloud iam service-policies SERVICE_ID [--output FORMAT] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID (necessário)</dt>
  <dd>Nome ou UUID do ID do serviço</dd>
  <dt>-- output FORMAT (opcional)</dt>
  <dd>Especifica o formato de saída de políticas de serviço. Apenas JSON é suportado agora.</dd>
  <dt>-f, -- force (opcional)</dt>
  <dd>Exibir políticas de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Liste políticas do serviço `test`:
```
ibmcloud iam service-policies test
```

Listar políticas de serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-policies ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976
```

## Ibmcloud iam service-policy
{: #ibmcloud_iam_service_policy}

Exibir detalhes de uma política de serviço:
```
ibmcloud iam service-policy SERVICE_ID POLICY_ID [--output FORMAT] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID (necessário)</dt>
  <dd>Nome ou UUID do ID do serviço</dd>
  <dt>POLICY_ID (necessário)</dt>
  <dd>ID da política de serviço<dd>
  <dt>-- output FORMAT (opcional)</dt>
  <dd>Especifica o formato de saída da política de serviço. Apenas JSON é suportado agora.</dd>
  <dt>-f, -- force (opcional)</dt>
  <dd>Exibir política de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Mostre a política `140798e2-8ea7db3` do serviço `test`:
```
Ibmcloud iam service-policies test 140798e2-8ea7db3
```

Mostrar a política `140798e2-8ea7db3` de serviço
`ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-policies ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976 140798e2-8ea7db3
```

## Ibmcloud iam service-policy-create
{: #ibmcloud_iam_service_policy_create}

Criar uma política de serviço:
```
ibmcloud iam service-policy-create SERVICE_ID {--file JSON_FILE | -r, --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID] [--account-management]} [-f, --force]",
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID (necessário)</dt>
  <dd>Nome ou UUID do ID do serviço</dd>
  <dt>--file</dt>
  <dd>Arquivo JSON de definição de política. Isso é exclusivo com as sinalizações `-r, --roles`, `--service-name`, `--service-instance`, `--region`, `--resource-type`, `--resource`, `--resource-group-name` e `--resource-group-id`.</dd>
  <dt>-r, --roles</dt>
  <dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
  <dt>--service-name</dt>
  <dd>Nome do serviço da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-- service-instance <i>SERVICE_INSTANCE_GUID</i></dt>
  <dd>GUID da instância de serviço da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-region</dt>
  <dd>Região da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>--resource-type</dt>
  <dd>Tipo de recurso da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>--resource</dt>
  <dd>Recurso da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>--resource-group-name</dt>
  <dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-id`.</dd>
  <dt>--resource-group-id </dt>
  <dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-name`.</dd>
  <dt>--account-management (opcional)</dt>
  <dd>Conceder acesso a todos os serviços de gerenciamento de conta</dd>
  <dt>-f, --force</dt>
  <dd>Criar política de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Crie a política de serviço do arquivo JSON para o serviço `test`:
```
ibmcloud iam service-policy-create test --file @policy.json
```

Criar a política de serviço por meio do arquivo JSON para o serviço
`ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-policy-create ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976 -- file
```

Conceda ao serviço `test` a função `Administrator` para todos os serviços de gerenciamento de conta:
```
ibmcloud iam service-policy-create test --roles Administrator --account-management
```

Conceda ao serviço `test` a função `Viewer` para todos os recursos na conta:
```
ibmcloud iam service-policy-create test -- roles Viewer
```

## Ibmcloud iam service-policy-update
{: #ibmcloud_iam_service_policy_update}

Atualizar uma política de serviço:
```
ibmcloud iam service-policy-update SERVICE_ID POLICY_ID {--file JSON_FILE | [-r, --roles ROLE_NAME1,ROLE_NAME2...] [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID] [--account-management]} [-f, --force]",
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID (necessário)</dt>
  <dd>Nome ou UUID do ID do serviço</dd>
  <dt>POLICY_ID (necessário)</dt>
  <dd>ID da política de serviço<dd>
  <dt>--file</dt>
  <dd>Arquivo JSON de definição de política. Isso é exclusivo com as sinalizações `-r, --roles`, `--service-name`, `--service-instance`, `--region`, `--resource-type`, `--resource`, `resource-group-name` e `resource-group-id`.</dd>
  <dt>-r, --roles</dt>
  <dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
  <dt>-service-name</dt>
  <dd>Nome do serviço da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-service-instance <i>SERVICE_INSTANCE_GUID</i></dt>
  <dd>GUID da instância de serviço da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-region</dt>
  <dd>Região da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-resource-type</dt>
  <dd>Tipo de recurso da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>-resource</dt>
  <dd>Recurso da definição de política. Isso é exclusivo com a sinalização `--file`.</dd>
  <dt>--resource-group-name</dt>
  <dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-id`.</dd>
  <dt>--resource-group-id </dt>
  <dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-name`.</dd>
  <dt>--account-management (opcional)</dt>
  <dd>Conceder acesso a todos os serviços de gerenciamento de conta</dd>
  <dt>-f, --force</dt>
  <dd>Atualizar a política de serviço sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Atualize a política de serviço `140798e2-8ea7db3` do arquivo JSON para o serviço `test`:
```
ibmcloud iam service-policy-update test 140798e2-8ea7db3 --file @policy.json
```

Atualize a política de serviço `140798e2-8ea7db3` do arquivo JSON para o serviço `test`:
```
ibmcloud iam service-policy-update test 140798e2-8ea7db3 --file @policy.json
```

Atualize a política de serviço `140798e2-8ea7db3` para conceder ao serviço `test` a função `Administrator` para todos os serviços de gerenciamento de conta:
```
ibmcloud iam service-policy-update test 140798e2-8ea7db3 --roles Administrator --account-management
```

Atualize a política de serviço `140798e2-8ea7db3` para conceder ao serviço `test` a função `Viewer` para todos os recursos na conta:
```
ibmcloud iam service-policy-update test 140798e2-8ea7db3 --roles Viewer
```

## Ibmcloud iam service-policy-delete
{: #ibmcloud_iam_service_policy_delete}

Excluir uma política de serviço:
```
ibmcloud iam service-policy-delete SERVICE_ID POLICY_ID [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SERVICE_ID (necessário)</dt>
  <dd>Nome ou UUID do ID do serviço</dd>
  <dt>POLICY_ID (necessário)</dt>
  <dd>ID da política de serviço<dd>
  <dt>-f, --force</dt>
  <dd>Excluir sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Excluir a política `140798e2-8ea7db3` de serviço `test`:
```
Ibmcloud iam service-policy-delete test 140798e2-8ea7db3
```

Excluir política `140798e2-8ea7db3` do serviço `ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976`:
```
Ibmcloud iam service-policy-delete ServiceId-cb258cb9-8de3-4ac0-9aec-b2b2d27ac976 140798e2-8ea7db3
```

## ibmcloud iam oauth-tokens
{: #ibmcloud_iam_oauth_tokens}

Recupere e exiba os tokens OAuth para a sessão atual:
```
ibmcloud iam oauth-tokens
```
{: codeblock}

<strong>Pré-requisitos</strong>: Login, Destino

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Atualizar e exibir tokens OAuth:
```
ibmcloud iam oauth-tokens
```
{: codeblock}

## Ibmcloud iam dedicated-id-disconnect
{: #ibmcloud_iam_dedicated_id_disconnect}

Desconecte o IBMid público com o não IBMid dedicado:
```
Ibmcloud iam dedicated-id-disconnect [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Forçar desconexão sem confirmação</dd>
</dl>

## ibmcloud iam authorization-policy-create
{: #ibmcloud_iam_authorization_policy_create}

Criar uma política de autorização para permitir a uma instância de serviço o acesso a outra instância de serviço:
```
ibmcloud iam authorization-policy-create SOURCE_SERVICE_NAME TARGET_SERVICE_NAME ROLE_NAME1,ROLE_NAME2... [—-source-service-instance-name SOURCE_SERVICE_INSTANCE_NAME | --source-service-instance-id SOURCE_SERVICE_INSTANCE_ID] [--source-resource-type RESOURCE_TYPE] [—-target-service-instance-name TARGET_SERVICE_INSTANCE_NAME] [--target-resource-type RESOURCE_TYPE | --target-service-instance-id TARGET_SERVICE_INSTANCE_ID] [--output FORMAT]
```

<strong>Pré-requisitos</strong>: Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>SOURCE_SERVICE_NAME</dt>
  <dd>Serviço de origem que pode ser autorizado para acesso.</dd>
  <dt>TARGET_SERVICE_NAME</dt>
  <dd>Serviço de destino que o serviço de origem pode ser autorizado a acessar.</dd>
  <dt>ROLE_NAME1,ROLE_NAME2...</dt>
  <dd>As funções que fornecem acesso para o serviço de origem.</dd>  
  <dt>--source-service-instance-name SOURCE_SERVICE_INSTANCE_NAME</dt>
  <dd>Nome da instância de serviço de origem, mutuamente exclusivo com `--source-service-instance-id`. Se não for especificado, todas as instâncias do serviço de origem serão autorizadas a acessar.</dd>
  <dt>--source-service-instance-id SOURCE_SERVICE_INSTANCE_ID</dt>
  <dd>Instanceid de serviço de origem, mutuamente exclusivo com `--source-service-instance-name`. Se não for especificado, todas as instâncias do serviço de origem serão autorizadas a acessar.</dd>
  <dt>--source-resource-type</dt>
  <dd>Tipo de recurso do serviço de origem</dd>
  <dt>--target-service-instance-name TARGET_SERVICE_INSTANCE_NAME</dt>
  <dd>Nome da instância de serviço de destino, mutuamente exclusivo com `--target-service-instance-id`. Se não for especificado, todas as instâncias do serviço de destino serão autorizadas a acessar.</dd>
  <dt>--target-service-instance-id TARGET_SERVICE_INSTANCE_ID</dt>
  <dd>ID da instância de serviço de destino, mutuamente exclusivo com `--target-service-instance-name`. Se não for especificado, todas as instâncias do serviço de destino serão autorizadas a acessar.</dd>
  <dt>--target-resource-type</dt>
  <dd>Tipo de recurso do serviço de destino</dd>
</dl>

## Ibmcloud iam authorization-policy-delete
{: #ibmcloud_iam_authorization_policy_delete}

Excluir uma política de autorização:
```
Ibmcloud iam authorization-policy-delete AUTHORIZATION_POLICY_ID [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>AUTHORIZATION_POLICY_ID</dt>
  <dd>ID da política de autorização para exclusão.</dd>
  <dt>-f, --force</dt>
  <dd>Forçar exclusão sem confirmação.</dd>
</dl>

## Ibmcloud iam authorization-policy
{: #ibmcloud_iam_authorization_policy}

Mostrar detalhes de uma política de autorização:
```
Ibmcloud iam authorization-policy AUTHORIZATION_POLICY_ID
```

<strong>Pré-requisitos</strong>: Login, Destino

<strong>Opções de comando</strong>:
<dl>
  <dt>AUTHORIZATION_POLICY_ID</dt>
  <dd>ID da política de autorização para exibição.</dd>
</dl>

## ibmcloud iam authorization-policies
{: #ibmcloud_iam_authorization_policies}

Listar políticas de autorização sob a conta atual:
```
ibmcloud iam authorization-policies
```
{: codeblock}

<strong>Pré-requisitos</strong>: Login, Destino

## ibmcloud iam access-groups
{: #ibmcloud_iam_access_groups}

Listar grupos de acesso sob a conta atual:
```
ibmcloud iam access-groups [-u USER_NAME | -s SERVICE_ID_NAME]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-u</dt>
  <dd>Listar grupos de acesso aos quais o usuário pertence. Essa sinalização é exclusiva para '-s'.</dd>
  <dt>-s</dt>
  <dd>Listar grupos de acesso aos quais o ID de serviço pertence. Essa sinalização é exclusiva para '-u'.</dd>
</dl>

<strong>Exemplos</strong>:

Listar todos os grupos de acesso:
```
ibmcloud iam access-groups
```
{: codeblock}

## Grupo de acesso iam ibmcloud
{: #ibmcloud_iam_access_group}

Mostrar detalhes de um grupo de acesso:
```
Grupo de acesso iam ibmcloud GROUP_NAME [ -- id ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-id</dt>
  <dd>Mostrar somente o ID</dd>
</dl>

<strong>Exemplos</strong>:

Mostrar detalhes do grupo de acesso `example_group`:
```
Ibmcloud iam access-group example_group
```

## ibmcloud iam access-group-create
{: #ibmcloud_iam_access_group_create}

Crie um grupo de acesso:
```
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-d, --description</dt>
  <dd>Descrição de grupo de acesso</dd>
</dl>

<strong>Exemplos</strong>:

Criar um grupo de acesso `example_group`:
```
ibmcloud iam access-group-create example_group -d "example access group"
```

## Ibmcloud iam access-group-update
{: #ibmcloud_iam_access_group_update}

Atualizar um grupo de acesso:
```
ibmcloud iam access-group-update GROUP_NAME [-n, --name NEW_NAME] [-d, --description NEW_DESCRIPTION] [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-n, --name</dt>
  <dd>O novo nome do grupo de acesso</dd>
  <dt>-d, --description</dt>
  <dd>Nova descrição</dd>
  <dt>-f, --force</dt>
  <dd>Forçar atualização sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Renomear o grupo de acesso `example_group` para `hello_world_group`:
```
Ibmcloud iam access-group-update example_group -- name "hello_world_group"
```

## Ibmcloud iam access-group-delete
{: #ibmcloud_iam_access_group_delete}

Excluir um grupo de acesso

```
ibmcloud iam access-group-delete GROUP_NAME [-f, --force] [-r, --recursive]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Forçar exclusão sem confirmação</dd>
  <dt>-r, --recursive</dt>
  <dd>Excluir grupo de acesso e seus membros</dd>
</dl>

<strong>Exemplos</strong>:

Excluir acesso ao grupo `example_group`:
```
Ibmcloud iam access-group-delete example_group -- force
```

## Ibmcloud iam access-group-users
{: #ibmcloud_iam_access_group_users}

Listar usuários em um grupo de acesso:
```
Ibmcloud iam access-group-users GROUP_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Listar todos os usuários no grupo de acesso `example_group`:
```
Ibmcloud iam access-group-users example_group
```

## Ibmcloud iam access-group-user-add
{: #ibmcloud_iam_access_group_user_add}

Incluir usuário(s) em um grupo de acesso:
```
Ibmcloud iam access-group-user-add GROUP_NAME USER_NAME [ USER_NAME2 ...]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Incluir o usuário `name@example.com` ao grupo de acesso
`example_group`:
```
Ibmcloud iam access group-user-add example_group name@example.com
```

## Ibmcloud iam access-group-user-remove
{: #ibmcloud_iam_access_group_user_remove}

Remover um usuário de um grupo de acesso:
```
Ibmcloud iam access-group-user-remove GROUP_NAME USER_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Remover o usuário `name@example.com` do grupo de acesso `example_group`:
```
Ibmcloud iam access-group-user-remove example_group name@example.com
```

## Ibmcloud iam access-group-user-purge
{: #ibmcloud_iam_access_group_user_purge}

Remover usuário de todos os grupos de acesso:
```
Ibmcloud iam access-group-user-purge USER_NAME [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Excluir sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Remover usuário `name@example.com` de todos os grupos de acesso:
```
ibmcloud iam access-group-user-purge name@example.com -f
```

## Ibmcloud iam access-group-service-ids
{: #ibmcloud_iam_access_group_service_ids}

Listar IDs de serviço em um grupo de acesso:
```
ibmcloud iam access-group-service-ids GROUP_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Listar todos os IDs de serviço no grupo de acesso `example_group`:
```
Ibmcloud iam access-group-service-ids example_group
```

## Ibmcloud iam access-group-service-id-add
{: #ibmcloud_iam_access_group_service_id_add}

Inclua o ID de serviço em um grupo de acesso:
```
Ibmcloud iam access-group-service-id-add GROUP_NAME SERVICE_ID_NAME [ SERVICE_ID_NAME2 ...]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Incluir o ID de serviço `exemple-service` no grupo de acesso
`example_group`:
```
Ibmcloud iam access-group-service-id-add example_group example-service
```

## Ibmcloud iam access-group-service-id-remove
{: #ibmcloud_iam_access_group_service_id_remove}

Remover um ID de serviço de um grupo de acesso:
```
Ibmcloud iam access-group-service-id-remove GROUP_NAME SERVICE_ID_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Remover o ID de serviço `example-service` do grupo de acesso
`example_group`:
```
Ibmcloud iam access-group-service-id-remove example_group example-service
```

## Ibmcloud iam access-group-service-id-purge
{: #ibmcloud_iam_access_group_service_id_purge}

Remover o ID de serviço de todos os grupos de acesso:
```
Ibmcloud iam access-group-service-id-purge SERVICE_ID_NAME [ -f, -- force ]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Excluir sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Remover o ID de serviço `example-service` de todos os grupos de acesso:

```
Ibmcloud iam access-group-service-id-purge example -- force
```

## Ibmcloud iam access-group-policies
{: #ibmcloud_iam_access_group_policies}

Listar políticas de um grupo de acesso:
```
Ibmcloud iam access-group-policies GROUP_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Liste todas as políticas do grupo de acesso `example_group`:
```
Ibmcloud iam access-group-policies example_group
```

## Ibmcloud iam access-group-policy
{: #ibmcloud_iam_access_group_policy}

Mostrar detalhes de uma política de grupo de acesso:
```
Ibmcloud iam access-group-policy GROUP_NAME POLICY_ID
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
</dl>

<strong>Exemplos</strong>:

Mostrar detalhes de política `51b9717e-76b0-4f6a-bda7-b8132431f926` do grupo de acesso
`example_group`:
```
Ibmcloud iam access-group-policy example_group 51b9717e-76b0-4f6a-bda7-b8132431f926
```

## Ibmcloud iam access-group-policy-create
{: #ibmcloud_iam_access_group_policy_create}

Criar uma política de grupo de acesso:
```
ibmcloud iam access-group-policy-create GROUP_NAME {--file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>--file</dt>
  <dd>Arquivo JSON de definição de política</dd>
  <dt>-roles</dt>
  <dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
  <dt>-service-name</dt>
  <dd>Nome do serviço da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-service-instance <i>SERVICE_INSTANCE_GUID</i></dt>
  <dd>GUID da instância de serviço da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-region</dt>
  <dd>Região da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource-type</dt>
  <dd>Tipo de recurso da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource</dt>
  <dd>Recurso da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource-group-name</dt>
  <dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-id`.</dd>
  <dt>-resource-group-id</dt>
  <dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-name`.</dd>
</dl>

<strong>Exemplos</strong>:

Criar uma política de grupo de acesso por meio de um arquivo JSON:
```
Ibmcloud iam access-group-policy-create example_group -f @policy.json
```

Fornecer ao `example_group` a função `Administrator` para todos
os recursos do `sample-service`:
```
ibmcloud iam access-group-policy-create example_group --roles Administrator --service-name sample-service
```

Fornecer a função de `Editor` a `example_group` para o recurso `key123` da
instância `sample-service` com a GUID `d161aeea-fd02-40f8-a487-df1998bd69a9` na região `us-south`:
```
ibmcloud iam access-group-policy-create example_group --roles Editor --service-name sample-service --service-instance
d161aeea-fd02-40f8-a487-df1998bd69a9 --region us-south --resource-type key --resource key123
```

Fornecer ao `example_group` a função `Operator` para o grupo de
recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam access-group-policy-create example_group --roles Operator --resource-type resource-group --resource dda27e49d2a1efca58083a01dfde18f6
```

Fornecer ao `example_group` a função `Viewer` para os membros do grupo
de recursos `sample-resource-group`:
```
ibmcloud iam access-group-policy-create example_group --roles Viewer --resource-group-name sample-resource-group
```

Fornecer ao `example_group` a função `Viewer` para os membros do
grupo de recursos com ID `dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam access-group-policy-create example_group --roles Viewer --resource-group-id dda27e49d2a1efca58083a01dfde18f6
```

## ibmcloud iam access-group-policy-update
{: #ibmcloud_iam_access_group_policy_update}

Atualizar uma política de grupo de acesso:
```
ibmcloud iam access-group-policy-update GROUP_NAME POLICY_ID {--file JSON_FILE | [--roles ROLE_NAME1,ROLE_NAME2...] [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE_GUID] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>--file</dt>
  <dd>Arquivo JSON de definição de política</dd>
  <dt>-- roles</dt>
  <dd>Os nomes de função da definição de política. Para funções suportadas de um serviço específico, execute `ibmcloud iam roles --service SERVICE_NAME`. Essa opção é exclusiva com `--file`.</dd>
  <dt>-service-name</dt>
  <dd>Nome do serviço da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-service-instance <i>SERVICE_INSTANCE_GUID</i></dt>
  <dd>GUID da instância de serviço da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-region</dt>
  <dd>Região da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource-type</dt>
  <dd>Tipo de recurso da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource</dt>
  <dd>Recurso da definição de política. Essa opção é exclusiva com `--file`.</dd>
  <dt>-resource-group-name</dt>
  <dd>Nome do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-id`.</dd>
  <dt>-resource-group-id</dt>
  <dd>ID do grupo de recursos. `*` significa todos os grupos de recursos. Essa opção é exclusiva com `--file` e `--resource-group-name`.</dd>
</dl>

<strong>Exemplos</strong>:

Atualizar a política de grupo de acesso com aquela no arquivo JSON de política:
```
ibmcloud iam access-group-policy-update example_group b8638ceb-5c4d-4d58-ae06-7ad95a10c4d4 -f @policy.json
```

Atualizar a política de grupo de acesso para fornecer a função `Administrator`
do `example_group` para todos os recursos do `sample-service`:
```
ibmcloud iam access-group-policy-update example_group b8638ceb-5c4d-4d58-ae06-7ad95a10c4d4 --roles Administrator --service-name sample-service
```

Atualizar a política de grupo de acesso para fornecer a função de `Editor` a `example_group` para o recurso `key123` da instância `sample-service` com a GUID
`d161aeea-fd02-40f8-a487-df1998bd69a9` na região `us-south`:
```
ibmcloud iam access-group-policy-update example_group --roles Editor --service-name sample-service --service-instance d161aeea-fd02-40f8-a487-df1998bd69a9 --region us-south
```

Atualizar a política de grupo de acesso para fornecer ao `example_group`
a função `Operator` para o grupo de recursos com ID
`dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam access-group-policy-update example_group b8638ceb-5c4d-4d58-ae06-7ad95a10c4d4 --roles Operator --resource-type resource-group --resource dda27e49d2a1efca58083a01dfde18f6
```

Atualizar a política do grupo de acesso para fornecer ao `example_group`
a função `Viewer` para os membros do grupo de recursos
`sample-resource-group`:
```
ibmcloud iam access-group-policy-update example_group b8638ceb-5c4d-4d58-ae06-7ad95a10c4d4 --roles Viewer --resource-group-name sample-resource-group
```

Atualizar a política de grupo de acesso para fornecer ao `example_group`
a função `Viewer` para membros do grupo de recursos com ID
`dda27e49d2a1efca58083a01dfde18f6`:
```
ibmcloud iam access-group-policy-update example_group b8638ceb-5c4d-4d58-ae06-7ad95a10c4d4 --roles Viewer --resource-group-id dda27e49d2a1efca58083a01dfde18f6
```

## Ibmcloud iam access-group-policy-delete
{: #ibmcloud_iam_access_group_policy_delete}

Excluir uma política de grupo de acesso:
```
ibmcloud iam access-group-policy-delete GROUP_NAME POLICY_ID [-f, --force]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>-f, --force</dt>
  <dd>Forçar exclusão sem confirmação</dd>
</dl>

<strong>Exemplos</strong>:

Excluir a política `51b9717e-76b0-4f6a-bda7-b8132431f926` do grupo de acesso
`example_group`:
```
Ibmcloud iam access-group-policy-delete example_group 51b9717e-76b0-4f6a-bda7-b8132431f926 -f
```
