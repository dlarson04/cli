---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: cli, local app debug, java debug, node debug, debug, cli debug, local cli, ibmcloud dev, dev debug

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Depuración de apps locales para la CLI de {{site.data.keyword.dev_cli_notm}}
{: #local-debug}

Existen herramientas para ayudarle a depurar la aplicación en Java&trade; y Node.js en {{site.data.keyword.cloud_notm}}.

## Depuración de apps Java
{: #java}

Pasos para habilitar la herramienta de depuración para una app Java&trade;:

1. Desde el directorio raíz del proyecto de su app, ejecute el mandato siguiente:

  ```
  ibmcloud dev debug
  ```
  {: codeblock}

2. Conexión del depurador a su app:

	* Eclipse
      1. Importe el **Proyecto maven existente** en Eclipse.
      2. Cree una configuración de depuración de [app Java&trade; remota](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm){: new_window} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo").
         1. Especifique la dirección IP o `localhost:<port>`  
         2. Escriba `7777` como número de puerto.
         3. Especifique el nombre del proyecto que ha importado.
      6. Defina un punto de interrupción en el IDE.
      7. Ejecute la configuración de depuración.
      8. Acceda al punto final con un navegador para volver a crear el problema.  
	   
	   El puerto predeterminado es `9080` para el punto final de microservicios básicos de Java&trade;.
	   {: note}

	* [IntelliJ](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html){: new_window} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")
	* [VSCode](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugger){: new_window} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")
	* Línea de mandatos de JDK: `jdb -attach <host:port>`

## Depuración de apps Node.js
{: #idt-node-debug}

Pasos para habilitar la herramienta de depuración para una app Node.js:

1. Desde el directorio raíz del proyecto de app, ejecute el mandato siguiente:
  ```
  ibmcloud dev debug
  ```
  {: codeblock}

2. Conexión del depurador a su app:
	* [VSCode](https://blog.docker.com/2016/07/live-debugging-docker/){: new_window} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")
	* [WebStorm](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/){: new_window} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")


<!--
## Swift app debugging - content from mike tunnicliffe
{: #swift}

Steps to enable debug for a Swift app:  

1. On the App server (or system where the Swift app will execute), you should start the 'lldb server':
 - `lldb-server platform -->
<!-- listen <port number>`
2. On the App server, build the Kitura-based server app using the debug configuration:
 - `swift build debug`
3. On the App server, start the Kitura-based server app:
 - `./build/debug/Kitura-Starter`
4. On the client system (also known as the host system), start the 'lldb client':
 - `lldb`
5. Configure lldb client to connect to lldb-server:
 - `(lldb) platform select remote-linux`
 - `(lldb) platform connect connect://<ip address server>:<port number server>`
6. Execute commands to debug remote program:
 - `(lldb) process attach -->
<!--pid 3626`
-->
