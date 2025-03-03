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

# Gestión de grupos de seguridad para el tráfico de servidor virtual
{: #sl-manage-securitygroups}

Un grupo de seguridad es un conjunto de reglas de filtro de IP que definen cómo manejar tráfico entrante (ingreso) y saliente (egreso) a las interfaces públicas y privadas de una instancia de servidor virtual. Las reglas que se añaden a un grupo de seguridad se conocen como reglas de grupo de seguridad.

Utilice los mandatos siguientes para gestionar un grupo de seguridad mediante el servicio Security Group de la infraestructura clásica de {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

Crear un grupo de seguridad.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-n, --name</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>-d, --description</dt>
<dd>Descripción del grupo de seguridad.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

Suprimir el grupo de seguridad determinado.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forzar la operación sin confirmación.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

Obtener detalles sobre un grupo de seguridad.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

Editar detalles de un grupo de seguridad.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-n, --name</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>-d, --description</dt>
<dd>Descripción del grupo de seguridad.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

Adjuntar una interfaz a un grupo de seguridad.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>El ID de componente de red para asociar con el grupo de seguridad.</dd>
<dt>-s, --server</dt>
<dd>El ID de servidor para asociar con el grupo de seguridad.</dd>
<dt>-i, --interface</dt>
<dd>La interfaz del servidor a asociar (público/privado).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

Listar interfaces asociadas con el grupo de seguridad.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>--sortby</dt>
<dd>Columna por la que se debe ordenar. Las opciones son: id,virtualServerId,hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

Desconectar una interfaz de un grupo de seguridad.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>El componente de red que va a eliminar del grupo de seguridad.</dd>
<dt>-s, --server</dt>
<dd>El ID de servidor que va a eliminar del grupo de seguridad.</dd>
<dt>-i, --interface</dt>
<dd>La interfaz del servidor que va a eliminar (público/privado).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

Listar grupos de seguridad.
```
Listar grupos de seguridad
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>--sortby</dt>
<dd>Columna para ordenar por las opciones: id,name,description,created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

Añadir una regla de grupo de seguridad a un grupo de seguridad.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>El IP/CIDR remoto a imponer.</dd>
<dt>-s, --remote-group</dt>
<dd>El ID del grupo de seguridad remoto a imponer.</dd>
<dt>-d, --direction</dt>
<dd>La dirección de tráfico a imponer (entrada, salida), obligatorio.</dd>
<dt>-e, --ether-type</dt>
<dd>El ethertype (IPv4 o IPv6) a imponer, el valor predeterminado es IPv4 si no se especifica.</dd>
<dt>-M, --port-max</dt>
<dd>El puerto superior obligado a imponerse.</dd>
<dt>-m, --port-min</dt>
<dd>El puerto inferior obligado a imponerse.</dd>
<dt>-p, --protocol</dt>
<dd>El protocolo (icmp, tcp, udp) a imponerse.</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

Editar una regla de grupo de seguridad en un grupo de seguridad.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>El IP/CIDR remoto a imponer.</dd>
<dt>-s, --remote-group</dt>
<dd>El ID del grupo de seguridad remoto a imponer.</dd>
<dt>-d, --direction</dt>
<dd>La dirección de tráfico a imponer (entrada, salida), obligatorio.</dd>
<dt>-e, --ether-type</dt>
<dd>El ethertype (IPv4 o IPv6) a imponer, el valor predeterminado es IPv4 si no se especifica.</dd>
<dt>-M, --port-max</dt>
<dd>El puerto superior obligado a imponerse.</dd>
<dt>-m, --port-min</dt>
<dd>El puerto inferior obligado a imponerse.</dd>
<dt>-p, --protocol</dt>
<dd>El protocolo (icmp, tcp, udp) a imponerse.</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

Listar reglas de grupo de seguridad.
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>--sortby</dt>
<dd>Columna por la que se debe ordenar. Las opciones son: id,remoteIp,remoteGroupId,direction,ethertype,portRangeMin,portRangeMax,protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

Eliminar una regla de un grupo de seguridad.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>-f, --force</dt>
<dd>Forzar la operación sin confirmación.</dd>
</dl>
