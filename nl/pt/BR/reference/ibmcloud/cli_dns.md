---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, domain management, dns service, ibmcloud sl dns, classic infrastructure, management interface, dns, dns cli, manage dns cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gerenciando domínios com o serviço DNS
{: #sl-manage-domains}

O Domain Name Service (DNS) do {{site.data.keyword.cloud}} fornece aos clientes um local central para
visualizar e gerenciar os domínios por meio da interface de gerenciamento básica de DNS e também fornece aos usuários
a opção de gerenciar o DNS reverso e o secundário no mesmo local gratuitamente.

Use os comandos a seguir para gerenciar o serviço DNS da infraestrutura clássica do {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Sl dns import ibmcloud
{: #sl_dns_import}

Importar uma zona com base em um arquivo de zona BIND.
```
ibmcloud sl dns import ZONEFILE [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--dry-run</dt>
<dd>Não criar registros realmente.</dd>
</dl>

**Exemplos**:
```
ibmcloud sl dns import ~/ibm.com.txt
```
Esse comando importa a zona e seus registros de recurso do arquivo: ~/ibm.com.txt.


## Ibmcloud sl dns record-add
{: #sl_dns_record_add}

Incluir registro de recurso em uma zona.
```
ibmcloud sl dns record-add ZONE RECORD TYPE DATA [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--ttl</dt>
<dd>TTL (Tempo de vida) em segundos, como: 86.400, o padrão é: 7.200.</dd>
</dl>

**Exemplos**:
```
ibmcloud sl dns record-add ibm.com ftp A 127.0.0.1 --ttl 86400
```
Esse comando inclui um registro A para a zona: ibm.com, seu host é "ftp", os dados são "127.0.0.1" e ttl é 86400 segundos.


## ibmcloud sl dns record-edit
{: #sl_dns_record_edit}

Atualizar registros de recurso em uma zona.
```
Ibmcloud sl dns record-edit ZONE [ OPTIONS ]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--by-record</dt>
<dd>Editar pelo registro do host, como www.</dd>
<dt>--by-id</dt>
<dd>Editar um registro único por seu ID.</dd>
<dt>--data</dt>
<dd>Registrar dados, como um endereço IP.</dd>
<dt>--ttl</dt>
<dd>Valor TTL em segundos, como: 86400.</dd>
</dl>

**Exemplos**:
```
ibmcloud sl dns record-edit ibm.com --by-id 12345678 --data 127.0.0.2 --ttl 3600
```
Esse comando edita registros na zona: ibm.com, cujo ID é 12345678 e configura seus dados como "127.0.0.2" e ttl como 3600.


## Ibmcloud sl dns record-list
{: #sl_dns_record_list}

Listar todos os registros de recurso em uma zona.
```
Ibmcloud sl dns record-list ZONE [ OPTIONS ]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--data</dt>
<dd>Filtrar por dados do registro, como um endereço IP.</dd>
<dt>--record</dt>
<dd>Filtrar pelo registro do host, como www.</dd>
<dt>--ttl</dt>
<dd>Filtrar pelo valor TTL em segundos, como: 86400.</dd>
<dt>--type</dt>
<dd>Filtrar pelo tipo de registro, como A ou CNAME.</dd>
</dl>

**Exemplos**:
```
ibmcloud sl dns record-list ibm.com --record elasticsearch --type A --ttl 900
```
Esse comando lista todos os registros A na zona: ibm.com, filtrados pelo host é elasticsearch e ttl é 900 segundos.


## Ibmcloud sl dns record-remove
{: #sl_dns_record_remove}

Remover registro de recurso de uma zona.
```
Ibmcloud sl dns record-remove RECORD_ID
```

**Exemplos**:
```
Ibmcloud sl dns record-remove 12345678
```
Esse comando remove o registro de recurso com ID 12345678.


## Ibmcloud sl dns zone-create
{: #sl_dns_zone_create}

Criar uma zona.
```
ibmcloud sl dns zone-create ZONE
```

**Exemplos**:
```
ibmcloud sl dns zone-create ibm.com
```
Esse comando cria uma zona chamada ibm.com.


## Ibmcloud sl dns zone-delete
{: #sl_dns_zone_delete}

Excluir uma zona.
```
Ibmcloud sl dns zone-delete ZONE
```

**Exemplos**:
```
ibmcloud sl dns zone-delete ibm.com
```
Esse comando exclui uma zona chamada ibm.com.


## ibmcloud sl dns zone-list
{: #sl_dns_zone_list}

Listar todas as zonas em sua conta.
```
ibmcloud sl dns zone-list
```

**Exemplos**:
```
ibmcloud sl dns zone-list
```
Esse comando lista todas as zonas na conta atual.


## Ibmcloud sl dns zone-print
{: #sl_dns_zone_print}

Imprimir registros de zona e recurso no formato BIND.
```
Ibmcloud sl dns zone-print ZONE
```

**Exemplos**:
```
ibmcloud sl dns zone-print ibm.com
```
Esse comando imprime a zona que é denominada ibm.com no formato BIND.
