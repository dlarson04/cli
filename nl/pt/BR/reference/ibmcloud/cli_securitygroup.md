---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, manage security groups, ingress, egress, traffic, virtual server cli, classic infrastructure cli, securitygroup, ibmcloud sl securitygroup, security group cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gerenciando grupos de segurança para tráfego de servidor virtual
{: #sl-manage-securitygroups}

Um grupo de segurança é um conjunto de regras de filtro IP que definem como manipular o tráfego recebido
(ingresso) e de saída (egresso) para as interfaces públicas e privadas de uma instância de servidor virtual. As regras que você inclui em um grupo de segurança são conhecidas como regras
do grupo de segurança.

Use os comandos a seguir para gerenciar um grupo de segurança usando o serviço do Grupo de segurança de infraestrutura clássica do {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

Crie um grupo de segurança.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-n, --name</dt>
<dd>O nome do grupo de segurança.</dd>
<dt>-d, --description</dt>
<dd>A descrição do grupo de segurança.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

Excluir o grupo de segurança especificado.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forçar a operação sem confirmação.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

Obter detalhes sobre um grupo de segurança.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

Editar detalhes de um grupo de segurança.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-n, --name</dt>
<dd>O nome do grupo de segurança.</dd>
<dt>-d, --description</dt>
<dd>A descrição do grupo de segurança.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

Conectar uma interface a um grupo de segurança.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>O ID de componente de rede para associar com o grupo de segurança.</dd>
<dt>-s, --server</dt>
<dd>O ID do servidor para associar com o grupo de segurança.</dd>
<dt>-i, --interface</dt>
<dd>A interface do servidor para associar (pública/privada).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

Listar as interfaces associadas ao grupo de segurança.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--sortby</dt>
<dd>Coluna pela qual classificar; as opções são: id, virtualServerId, hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

Remover uma interface de um grupo de segurança.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>O componente de rede para remover do grupo de segurança.</dd>
<dt>-s, --server</dt>
<dd>O ID do servidor para remover do grupo de segurança.</dd>
<dt>-i, --interface</dt>
<dd>A interface do servidor para remover (pública/privada).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

Listar grupos de segurança.
```
Listar grupos de segurança
```

<strong>Opções de comando</strong>:
<dl>
<dt>--sortby</dt>
<dd>Coluna pela qual classificar, as opções são: id, name, description, created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

Incluir uma regra de grupo de segurança em um grupo de segurança.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>O IP/CIDR remoto a cumprir.</dd>
<dt>-s, --remote-group</dt>
<dd>O ID do grupo de segurança remoto a cumprir.</dd>
<dt>-d, --direction</dt>
<dd>A direção do tráfego a cumprir (ingresso, egresso), obrigatória.</dd>
<dt>-e, --ether-type</dt>
<dd>O ethertype (IPv4 ou IPv6) a cumprir, caso não seja especificado, o padrão é IPv4.</dd>
<dt>-M, --port-max</dt>
<dd>A ligação de porta superior a cumprir.</dd>
<dt>-m, --port-min</dt>
<dd>A ligação de porta inferior a cumprir.</dd>
<dt>-p, --protocol</dt>
<dd>O protocolo (icmp, tcp, udp) a cumprir.</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

Editar uma regra de grupo de segurança em um grupo de segurança.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>O IP/CIDR remoto a cumprir.</dd>
<dt>-s, --remote-group</dt>
<dd>O ID do grupo de segurança remoto a cumprir.</dd>
<dt>-d, --direction</dt>
<dd>A direção do tráfego a cumprir (ingresso, egresso), obrigatória.</dd>
<dt>-e, --ether-type</dt>
<dd>O ethertype (IPv4 ou IPv6) a cumprir, caso não seja especificado, o padrão é IPv4.</dd>
<dt>-M, --port-max</dt>
<dd>A ligação de porta superior a cumprir.</dd>
<dt>-m, --port-min</dt>
<dd>A ligação de porta inferior a cumprir.</dd>
<dt>-p, --protocol</dt>
<dd>O protocolo (icmp, tcp, udp) a cumprir.</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

Listar regras de grupo de segurança.
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--sortby</dt>
<dd>Coluna pela qual classificar, as opções são: id, remoteIp, remoteGroupId, direction, ethertype, portRangeMin, portRangeMax,
protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

Remova uma regra de um grupo de segurança.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Opções de comando</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forçar a operação sem confirmação.</dd>
</dl>
