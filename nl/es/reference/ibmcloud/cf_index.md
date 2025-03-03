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

# Cómo trabajar con Cloud Foundry (mandatos cf)
{: #cf}

La interfaz de línea de mandatos (CLI) de Cloud Foundry (cf) proporciona un conjunto de mandatos para gestionar las apps. En la siguiente información se indican los mandatos cf más comúnmente utilizados para gestionar apps e incluye sus nombres, opciones, uso, requisitos previos, descripciones y ejemplos. Para ver una lista de todos los mandatos cf y su información de ayuda asociada, utilice `cf help`. Utilice `cf nombre_mandato -h` para ver información de ayuda detallada sobre un determinado mandato.
{: shortdesc}

Para obtener más detalles sobre cómo iniciarse en la CLI de Cloud Foundry, consulte
[Iniciación](https://github.com/cloudfoundry/cli#getting-started){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

Para obtener una lista más detallada de mandatos `cf CLI`, consulte la [Guía de referencia de CLI de Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/cf-help.html){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo") de la comunidad.

Si la red contiene un servidor proxy HTTP entre el host que ejecuta los mandatos cf y el punto final de la API de
Cloud Foundry, debe especificar el nombre de host o la dirección IP del servidor proxy mediante la variable de entorno `HTTP_PROXY`. Para obtener detalles, consulte [Utilización de la CLI cf con un servidor proxy](https://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").
{: note}

## Índice de mandatos de CLI de Cloud Foundry
{: #CLIname_commands_index}

Utilice el índice de la siguiente tabla para hacer referencia a los mandatos de Cloud Foundry utilizados con frecuencia:

<table summary="Mandatos de Cloud Foundry generales ordenados alfabéticamente que tienen enlaces que le proporcionan más información para el mandato">
<caption>Tabla 1. Mandatos generales de Cloud Foundry</caption>
 <thead>
 <th colspan="6">Mandatos de Cloud Foundry generales</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](#cf_api)</td>
 <td>[help](#cf_help)</td>
 <td>[login](#cf_login)</td>
 <td>[stacks](#cf_stacks)</td>
 <td>[target](#cf_target)</td>
 <td>[-v](#cf_v)</td>
 </tr>
   </tbody>
 </table>

<table summary="Mandatos ordenados alfabéticamente para gestionar apps, espacios y servicios. Cada mandato tiene un enlace que le proporciona más información para el mandato.">
<caption>Tabla 2. Mandatos para gestionar apps, espacios y servicios</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar apps, espacios y servicios</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](#cf_apps)</td>
 <td>[bind-service](#cf_bind-service)</td>
 <td>[create-service](#cf_create-service)</td>
 <td>[create-space](#cf_create-space)</td>
 <td>[delete](#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](#cf_delete-space)</td>
 <td>[events](#cf_events)</td>
 <td>[logs](#cf_logs)</td>
 <td>[marketplace](#cf_marketplace)</td>
 <td>[enviar por push](#cf_push)</td>
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

Utilice este mandato para visualizar o especificar el URL del punto final de la API de {{site.data.keyword.cloud}}.
```
cf api [URL] [--skip-ssl-validation] [--unset]
```

<strong>Requisitos previos</strong>: Ninguno.

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>URL (opcional)</dt>
   <dd>El URL del punto final API de {{site.data.keyword.cloud_notm}}
que debe especificar al conectarse a {{site.data.keyword.cloud_notm}}. Normalmente, este URL es `https://api.<REGION>.cf.{DomainName}`.
   Si desea visualizar el URL del punto final API que está utilizando actualmente no tiene que especificar este parámetro para el mandato cf api.</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>Inhabilita el proceso de validación de SSL. El uso de este parámetro puede ocasionar problemas de seguridad.</dd>
   <dt>* --unset</dt>
   <dd>Elimina información de conexión para todos los puntos finales de la API.</dd>
   </dl>

<strong>Ejemplos</strong>:

Para ver el punto final de API actual:
```
cf api
```
{: codeblock}

Eliminar la conexión con todos los puntos finales de la API para api.us-south.cf.cloud.ibm.com:
```
cf api api.us-south.cf.cloud.ibm.com --unset
```
{: codeblock}

Inhabilitar el proceso de validación de SSL para api.us-south.cf.cloud.ibm.com:
```
cf api api.us-south.cf.cloud.ibm.com --skip-ssl-validation
```
{: codeblock}

## cf apps
{: #cf_apps}

Lista todas las aplicaciones desplegadas en el espacio actual. También se visualiza el estado de cada aplicación.

Suponga que tiene una instancia para una app, en la columna instancias de la respuesta desde el mandato cf apps, verá 1/1 si la app está activa y 0/1 si la app está desactivada. Si ve ?/1, lo que indica que el estado de la instancia de la app es desconocido, puede copiar el URL de la app en su navegador para comprobar si la app responde, o puede poner el registro en cola mediante el mandato `cf logs nombre_app` para ver si la app está generando contenido de registro.

```
cf apps
```
{: codeblock}

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

## cf bind-service
{: #cf_bind-service}

Enlaza una instancia de servicio existente a su aplicación.

```
cf bind-service nombre_app instancia_servicio
```
{: codeblock}

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>appname (necesario)</dt>
   <dd>El nombre de la aplicación.</dd>
   <dt>service_instance (necesario)</dt>
   <dd>El nombre de la instancia de servicio existente.</dd>
    </dl>

<strong>Ejemplos</strong>:

Enlace una instancia de servicio denominada `my_dataworks` a su app denominada `my_app`.
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

Crea una instancia de servicio.

```
cf create-service nombre_servicio plan_servicio instancia_servicio
```
{: codeblock}

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>service_name (necesario)</dt>
   <dd>El nombre del servicio.</dd>
   <dt>service_plan (necesario)</dt>
   <dd>El nombre del plan del servicio.</dd>
   <dt>service_instance (necesario)</dt>
   <dd>El nombre que desea utilizar para la nueva instancia del servicio que cree.</dd>
    </dl>

<strong>Ejemplos</strong>:

Crear una instancia del servicio de {{site.data.keyword.dataworks_short}} con un plan `free`.
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

Crea un espacio.

```
cf create-space space_name [-o] [-q]
```

<strong>Requisitos previos</strong>: `cf api`, `cf login`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>space_name (necesario)</dt>
   <dd>El nombre del espacio.</dd>
   <dt>*-o* (opcional)</dt>
   <dd>El nombre de la organización en la que desea crear un espacio.</dd>
   <dt>*-q* (opcional)</dt>
   <dd>Cuota para asignar al espacio recién creado. Si no se especifica, se asignará automáticamente una cuota predeterminada.</dd>
    </dl>

<strong>Ejemplos</strong>:

Crear un espacio denominado new_space
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

Suprima una aplicación existente.

```
cf delete appname [-f] [-r]
```

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>appname (necesario)</dt>
   <dd>El nombre de la aplicación.</dd>
   <dt>*-f* (opcional)</dt>
   <dd>Fuerza la supresión de la aplicación sin ninguna confirmación.</dd>
   <dt>*-r* (opcional)</dt>
   <dd>Suprime todos los nombres de dominio asociados a la aplicación. </dd>
    </dl>

<strong>Ejemplos</strong>:

Suprime una aplicación que se denomina `my_app` (se requiere confirmación).
```
cf delete my_app
```
{: codeblock}

Suprime una aplicación denominada `my_app` sin exigir confirmación.
```
cf delete my_app -f
```
{: codeblock}

Suprime una aplicación llamada `my_app` y todos los nombres de dominio asociados con `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Suprime una aplicación denominada `my_app` y todos los nombres de dominio asociados con `my_app` sin exigir confirmación.
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

Suprime un espacio.
```
cf delete-space space_name [-f]
```

<strong>Requisitos previos</strong>: `cf api`, `cf login`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>space_name (necesario)</dt>
   <dd>El nombre del espacio.</dd>
   <dt>*-f* (opcional)</dt>
   <dd>Fuerza la supresión del espacio sin ninguna confirmación.</dd>
   *Nota:* La supresión de un espacio en una operación irreversible.
   </dl>

<strong>Ejemplos</strong>:

Suprime una aplicación que se denomina `my_app` (se requiere confirmación).
```
cf delete my_app
```
{: codeblock}

Suprime una aplicación denominada `my_app` sin exigir confirmación.
```
cf delete my_app -f
```
{: codeblock}

Suprime una aplicación llamada `my_app` y todos los nombres de dominio asociados con `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Suprime una aplicación que se denomina `my_app` y todos los nombres de dominio asociados con `my_app` sin exigir información.
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

Muestra los sucesos de tiempo de ejecución relacionados con una aplicación.

```
cf events [appname]
```
{: codeblock}

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>nombre_app</dt>
   <dd>El nombre de la aplicación.</dd>
   </dl>

<strong>Ejemplos</strong>:

Muestra los sucesos para una aplicación denominada `my_app`.
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

Visualizar información de ayuda para todos los mandatos cf o para un mandato cf específico.

```
cf help [command_name]
```
{: codeblock}

<strong>Requisitos previos</strong>: Ninguno.

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>command_name (opcional)</dt>
   <dd>El nombre de un mandato.</dd>
    </dl>

<strong>Ejemplos</strong>:

Visualizar la información de ayuda para todos los mandatos cf.
```
cf help
```
{: codeblock}

Visualizar la información de ayuda para el mandato events.
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

Se inicia la sesión
en {{site.data.keyword.cloud_notm}}. Si va a iniciar sesión con un ID federado, debe utilizar el parámetro de inicio de sesión único (SSO) para iniciar la sesión.

También puede utilizar una clave de una API de la plataforma de {{site.data.keyword.cloud_notm}} para iniciar una sesión. Utilice el nombre de usuario `apikey` y su valor de clave de API como contraseña. Para obtener más información sobre la creación de claves de API, consulte [Visión general de las claves de API](/docs/iam?topic=iam-manapikey#manapikey).
{: note}

```
cf login [-a url] [-u nombre_usuario] [-p contraseña] [-sso] [-o nombre_organización] [-s nombre_espacio] [--skip-ssl-validation]
```

<strong>Requisitos previos</strong>: Ninguno.

<strong>Opciones de mandato</strong>:

<dl>
<dt>*-a* https://api.<REGION>.cf.{NombreDominio} (opcional)</dt>
<dd>El URL del punto final API de {{site.data.keyword.cloud_notm}}.</dd>
<dt>*-u* nombre_usuario (opcional)</dt>
<dd>Su nombre de usuario.</dd>
<dt>*-p* contraseña (opcional)</dt>
<dd>Su contraseña.</dd>
<dd>*Importante:* Si especifica la contraseña con el parámetro *-p* en la interfaz de línea de mandatos, es posible que la contraseña quede registrada en el historial de línea de mandatos. Por motivos de seguridad, evite especificar la contraseña con el parámetro -p. Escriba en su lugar la contraseña cuando se lo solicite la interfaz de línea de mandatos.</dd>
<dt>*-sso*</dt>
<dd>Debe utilizar la opción de inicio de sesión único (SSO) al iniciar sesión con un ID federado. Esto no es necesario al iniciar sesión con un IBMid. Si intenta iniciar sesión con un ID federado y no especifica el parámetro SSO, se le solicitará que lo incluya. Al utilizar el parámetro SSO se le solicitará que especifique el código de acceso de un solo uso tras iniciar la sesión.</dd>
<dt>*-o* nombre_organización</dt>
<dd>El nombre de la organización en la que desea iniciar sesión.</dd>
<dt>*-s* nombre_espacio</dt>
<dd>El nombre del espacio en el que desea iniciar sesión.</dd>
<dt>*--skip-ssl-validation* (opcional)</dt>
<dd>Inhabilita el proceso de validación de SSL. El uso de este parámetro puede ocasionar problemas de seguridad.</dd>
</dl>

*Nota:* Si proporciona la contraseña en el parámetro *-p* de este mandato, es posible que quede registrada en el archivo histórico del mandato de shell
y lo vean otros usuarios del sistema operativo local.

<strong>Ejemplos</strong>:

Iniciar sesión en {{site.data.keyword.cloud_notm}}.
```
cf login
```
{: codeblock}

Iniciar sesión en {{site.data.keyword.cloud_notm}} con un punto final definido de `https://api.us-south.cf.cloud.ibm.com`.
```
cf login -a https://api.us-south.cf.cloud.ibm.com
```
{: codeblock}

Iniciar sesión en {{site.data.keyword.cloud_notm}} con un punto final definido de `https://api.us-south.cf.cloud.ibm.com`, un nombre de usuario de `nombre_usuario`, y sin contraseña especificada por motivos de seguridad.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u nombre_usuario
```
{: codeblock}

Iniciar sesión en {{site.data.keyword.cloud_notm}} con un punto final definido de `https://api.us-south.cf.cloud.ibm.com`, un nombre de usuario de `user_name`, sin contraseña especificada por motivos de seguridad, y un nombre de organización de `nombre_org` y un nombre de espacio de `nombre_espacio`.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u nombre_usuario -o nombre_org -s nombre_espacio
```
{: codeblock}

Iniciar una sesión en {{site.data.keyword.cloud_notm}} con un punto final definido de `https://api.us-south.cf.cloud.ibm.com` utilizando una clave de API. Utilice `apikey` como el nombre de usuario y la clave de API real como contraseña.
```
cf login -a https://api.us-south.cf.cloud.ibm.com -u apikey -p ThisValueIsYourAPIKey
```
{: codeblock}

Puede iniciar sesión en los puntos finales de API de Cloud Foundry regionales siguientes:
* api.us-south.cf.cloud.ibm.com  (anteriormente api.ng.bluemix.net)
* api.eu-gb.cf.cloud.ibm.com     (anteriormente api.eu-gb.bluemix.net)
* api.us-east.cf.cloud.ibm.com   (anteriormente api.us-east.bluemix.net)
* api.eu-de.cf.cloud.ibm.com     (anteriormente api.eu-de.bluemix.net)
* api.au-syd.cf.cloud.ibm.com    (anteriormente api.au-syd.bluemix.net)

Los puntos finales de API de Cloud Foundry "api.<REGION>.bluemix.net" heredados siguen siendo válidos pero pronto quedarán en desuso.
{: note}

## cf logs
{: #cf_logs}

Visualizar las
corrientes de anotaciones cronológicas STDOUT y STDERR de una aplicación.

```
cf logs appname [--recent]
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

<dl>
<dt>nombre_app</dt>
<dd>El nombre de la aplicación.</dd>
<dt>*--recent* (opcional)</dt>
<dd>Recupera los registros recientes.</dd>
</dl>

<strong>Ejemplos</strong>:

Visualizar las corrientes de registros para una aplicación denominada `my_app`.
```
cf logs my_app
```
{: codeblock}

Visualizar las corrientes de registros recientes para una aplicación denominada `my_app`.
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

Lista todos los
servicios disponibles en el mercado. Los servicios que muestra este mandato también se pueden ver en el catálogo de {{site.data.keyword.cloud_notm}}.

```
cf marketplace
```
<strong>Requisitos previos</strong>: `cf api`

<strong>Opciones de mandatos</strong>: Ninguna.

<strong>Ejemplos</strong>:

Listar todos los servicios del mercado
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

Desplegar una aplicación nueva
en {{site.data.keyword.cloud_notm}}
o actualiza una aplicación existente en {{site.data.keyword.cloud_notm}}.

```
cf push appname [-b nombre_paquete_compilación] [-c mandato_inicio] [-f vía_acceso_manifiesto] [-i número_instancia] [-k límite_disco] [-m límite_memoria] [-n nombre_host] [-p vía_acceso_app] [-s nombre_pila] [-t longitud_tiempo_espera] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

<dl>
<dt>appname (necesario)</dt>
<dd>El nombre de la aplicación.</dd>
<dt>*-b* nombre_paquete_compilación (opcional)</dt>
<dd>El nombre del paquete de compilación. El nombre_paquete_compilación puede ser un paquete de compilación personalizado por nombre (por ejemplo liberty-for-java), un URL de Git (por ejemplo https://github.com/cloudfoundry/java-buildpack) o un URL de Git con una ramificación o etiqueta (por ejemplo https://github.com/cloudfoundry/java-buildpack#v3.3.0 para la etiqueta v3.3.0).</dd>
<dt>*-c* mandato_inicio (opcional)</dt>
<dd>El mandato de inicio de la aplicación. Para utilizar el mandato de inicio predeterminado
debe especificar un valor null para esta opción. </dd>
<dt>*-f* vía_acceso_manifiesto (opcional)</dt>
<dd>La vía de acceso al archivo de manifiesto. El archivo de manifiesto predeterminado es manifest.yml y se encuentra en el directorio raíz de la aplicación.</dd>
<dt>*-i* número_instancia (opcional)</dt>
<dd>El número de instancias.</dd>
<dt>*-k* límite_disco (opcional)</dt>
<dd>El límite de disco de la aplicación. Los valores posibles son *256M*, *1024M* o *1G*.</dd>
<dt>*-m* límite_memoria (opcional)</dt>
<dd>El límite de memoria para la aplicación. Los valores posibles son *256M*, *1024M* o *1G*.</dd>
<dt>*-n* nombre_host (opcional)</dt>
<dd>El nombre de host de la aplicación, como por ejemplo *mi-subdominio*.</dd>
<dt>*-p* vía_acceso_app (opcional)</dt>
<dd>La vía de acceso al directorio de la aplicación o el archivo de archivado de la aplicación.</dd>
<dt>*-s* nombre_pila (opcional)</dt>
<dd>La pila para ejecutar las apps. Una pila es un sistema de archivos preconstruido, incluido el sistema operativo. Utilice `cf stacks` para ver las pilas disponibles en {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-t* tiempo_espera (opcional)</dt>
<dd>Tiempo máximo en segundos para que se inicie la aplicación. Es posible que otros tiempos de espera de lado del servidor
sustituyan este valor.</dd>
<dt>*--no-hostname* (opcional)</dt>
<dd>Correlaciona el dominio de sistema de {{site.data.keyword.cloud_notm}}
a esta aplicación.</dd>
<dt>*--no-manifest* (opcional)</dt>
<dd>Ignora el archivo de manifiesto predeterminado.</dd>
<dt>*--no-route* (opcional)</dt>
<dd>No correlaciona ninguna ruta a esta aplicación.</dd>
<dt>*--no-start* (opcional)</dt>
<dd>No inicia la aplicación tras su despliegue.</dd>
<dt>*--random-route* (opcional)</dt>
<dd>Crea una ruta aleatoria para la aplicación.</dd>
</dl>

<strong>Ejemplos</strong>:

Iniciar una aplicación denominada `my_app` con el mandato de inicio predeterminado.
```
cf push `my_app` -c null
```
{: codeblock}

Iniciar una aplicación denominada `my_app` con la opción para ejecutar un archivo de script denominada `run.sh`.
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

Mostrar o cambiar el número de instancia, el límite de espacio de disco y el límite de memoria de una aplicación.

```
cf scale appname [-i número_instancia] [-k límite_disco] [-m límite_memoria] [-f]
```

<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

<dl>
<dt>appname (necesario)</dt>
<dd>El nombre de la aplicación.</dd>
<dt>*-i* número_instancia (opcional)</dt>
<dd>El número de instancias</dd>
<dt>*-k* límite_disco (opcional)</dt>
<dd>El límite de disco de la aplicación; los valores posibles son `256M`, `1024M`, o `1G`.</dd>
<dt>*-m* límite_memoria (opcional)</dt>
<dd>El límite de memoria para la aplicación; los valores posibles son `256M`, `1024M` o `1G`.</dd>
<dt>*-f* (opcional)</dt>
<dd>Fuerza el reinicio de la aplicación sin ninguna solicitud.</dd>
</dl>

<strong>Ejemplos</strong>:

Mostrar el número de instancia, el límite de espacio de disco y el límite de memoria para una aplicación denominada `my_app`.
```
cf scale my_app
```
{: codeblock}

Modifique el número de instancia a `1234`, el límite de espacio de disco a `1G`, y el límite de memoria a `1G` para una app denominada `my_app`.
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

Lista todos los
servicios disponibles en el espacio actual.

```
cf services
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandatos</strong>: Ninguna.

<strong>Ejemplos</strong>:

Listar todos los servicios del espacio actual.
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

Establece una variable de entorno para una aplicación

```
cf set-env nombre_app nombre_variable valor_variable
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

<dl>
<dt>appname (necesario)</dt>
<dd>El nombre de la aplicación.</dd>
<dt>nombre_variable (necesario)</dt>
<dd>El nombre de la variable de entorno.</dd>
<dt>valor_variable (necesario)</dt>
<dd>El valor de la variable de entorno.</dd>
</dl>

<strong>Ejemplos</strong>:

Defina una variable de entorno denominada `variable_a` con un valor de `123` para la aplicación denominada `my_app`.
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

Accede de forma segura al contenedor de aplicaciones. Se puede utilizar el mandato `cf ssh` para configurar una sesión SSH interactiva, ejecutar mandatos remotos, transferir archivos y configurar el reenvío de puertos con una determinada instancia del contenedor de aplicaciones.

```
cf ssh
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

De forma predeterminada, el acceso SSH está habilitado para aplicaciones Diego. Puede utilizar el mandato `cf ssh-enabled` para verificar si se ha habilitado el acceso SSH o el mandato `cf enable-ssh` para habilitar el acceso, en caso de que estuviese inhabilitado.

<strong>Opciones de mandato</strong>:

<dl>
<dt>nombre_app</dt>
<dd>El nombre de la aplicación.</dd>
<dt>-c</dt>
<dd>Especifica el mandato remoto que se va a ejecutar.</dd>
<dt>-i</dt>
<dd>Destinado a una instancia específica de una aplicación. Si no se especifica, se utiliza la primera instancia de la aplicación (una instancia con índice 0).</dd>
<dt>-L</dt>
<dd>Permite el reenvío de puerto local, que vincula un puerto de salida de la máquina con un puerto de entrada de la VM de la aplicación.</dd>
<dt>-N</dt>
<dd>No ejecutar un mandato remoto.</dd>
<dt>-t, -tt, o -T</dt>
<dd>Le permite ejecutar una sesión SSH en modalidad pseudo tty en lugar de generar salida de línea de terminal.<dd>
</dl>

<strong>Ejemplos</strong>:

Inicio de una sesión SSH interactiva con una instancia del contenedor que ejecuta la aplicación `my_app`.
```
$ cf ssh my_app
```
{: codeblock}

Ejecución de un solo mandato en la instancia del contenedor de aplicaciones `my_app`.
```
$ cf ssh my_app -c "ls -l"
```

Transferencia de un solo archivo desde la instancia del contenedor de aplicaciones `my_app`.
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

Configuración del reenvío de puertos del puerto 7777 de la máquina local al puerto 8888 de la instancia del contenedor de aplicaciones `my_app`.
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

Lista todas las pilas. Una pila es un sistema de archivos predefinido, incluido un sistema operativo que pueda ejecutar apps.

```
cf stacks
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`

<strong>Opciones de mandatos</strong>: Ninguna.

<strong>Ejemplos</strong>:

Listar todas las pilas.
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

Detiene una aplicación

```
cf stop nombre_app
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`, `cf target`

<strong>Opciones de mandato</strong>:

<dl>
<dt>appname (necesario)</dt>
<dd>El nombre de la aplicación.</dd>
</dl>

<strong>Ejemplos</strong>:

Detener la aplicación denominada `my_app`.
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

Establece o visualiza el espacio o la organización de destino

```
cf target [-o nombre_org] [-s nombre_espacio]
```
<strong>Requisitos previos</strong>: `cf api`, `cf login`

<strong>Opciones de mandato</strong>:

<dl>
<dt>-o *nombre_org* (opcional)</dt>
<dd>El nombre de la organización donde se ubica el espacio.</dd>
<dt>-s *nombre_espacio* (opcional)</dt>
<dd>El nombre del espacio.</dd>
</dl>

<strong>Ejemplos</strong>:

Establezca el destino en la organización denominada "my_org" y el espacio denominado "my_space".
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

Muestra la versión de la interfaz de línea de mandatos de Cloud Foundry.

```
cf -v
```
<strong>Requisitos previos</strong>: Ninguno.

<strong>Opciones de mandatos</strong>: Ninguna.

<strong>Ejemplos</strong>:

Visualice la versión de la interfaz de línea de mandatos de Cloud Foundry.
```
cf -v
```
{: codeblock}


## Enlaces relacionados
{: #cf-related}

* [Descargar CLI de Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")
* [Tarjeta de referencia rápida - Mandatos cf](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")
