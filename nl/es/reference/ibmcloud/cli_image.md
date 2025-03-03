---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, ibmcloud sl image, manage compute images, create compute image cli, compute image cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Creación, edición y supresión de imágenes de cálculo
{: #sl-manage-compute-images}

Utilice los mandatos siguientes para gestionar las imágenes de cálculo de {{site.data.keyword.cloud}}.
{: shortdesc}

## ibmcloud sl image delete
{: #sl_image_delete}

Suprimir una imagen.
```
ibmcloud sl image delete IDENTIFIER
```

**Ejemplos**:
```
ibmcloud sl image delete 12345678
```

Este mandato suprime la imagen con el ID `12345678`.

## ibmcloud sl image detail
{: #sl_image_detail}

Obtener detalles para una imagen.
```
ibmcloud sl image detail IDENTIFIER
```

**Ejemplos**:
```
 ibmcloud sl image detail 12345678
```

Este mandato obtiene los detalles de la imagen con ID `12345678`.

## ibmcloud sl image edit
{: #sl_image_edit}

Editar los detalles de una imagen.
```
ibmcloud sl image edit IDENTIFIER [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>--name</dt>
<dd>Nombre de la imagen.</dd>
<dt>--note</dt>
<dd>Nota adicional para la imagen.</dd>
<dt>--tag</dt>
<dd>Etiquetas para la imagen.</dd>
</dl>

*Ejemplos**:
```  
ibmcloud sl image edit 12345678 --name ubuntu16 --note testing --tag staging
```

Este mandato edita la imagen con el ID `12345678` y establece el nombre en `ubuntu16`, la nota en `testing` y la etiqueta en `staging`.

## ibmcloud sl image list
{: #sl_image_list}

Listar todas las imágenes de su cuenta.
```
ibmcloud sl image list [OPTIONS]
```

<strong>Opciones de mandato</strong>:
<dl>
<dt>--name</dt>
<dd>Filtrar en el nombre de imagen.</dd>
<dt>--public</dt>
<dd>Mostrar solo imágenes públicas.</dd>
<dt>--private</dt>
<dd>Mostrar solo imágenes privadas.</dd>
</dl>
