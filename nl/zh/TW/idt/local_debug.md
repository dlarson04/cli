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

# {{site.data.keyword.dev_cli_notm}} CLI 的本端應用程式除錯
{: #local-debug}

在 {{site.data.keyword.cloud_notm}} 中，有一些工具可協助您針對以 Java&trade; 及 Node.js 撰寫的應用程式進行除錯。

## Java 應用程式除錯
{: #java}

針對 Java&trade; 應用程式啟用除錯工具的步驟：

1. 從應用程式專案的根目錄中，執行下列指令：

  ```
ibmcloud dev debug
```
  {: codeblock}

2. 將除錯器連接至應用程式：

	* Eclipse
      1. 將**現有 maven 專案**匯入至 Eclipse。
      2. 建立 [Java&trade; 遠端應用程式](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm){: new_window} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示") 除錯配置。
         1. 輸入 IP 位址或 `localhost:<port>`  
         2. 輸入 `7777` 作為埠號。
         3. 指定您所匯入的專案名稱。
      6. 在 IDE 中設定岔斷點。
      7. 執行除錯配置。
      8. 使用瀏覽器存取端點，以重建問題。  
	   
	   Java&trade; 基本「微服務」端點的預設埠是 `9080`。
	   {: note}

	* [IntelliJ ](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html){: new_window} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")
	* [VSCode ](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugger){: new_window} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")
	* JDK 指令行：`jdb -attach <host:port>`

## Node.js 應用程式除錯
{: #idt-node-debug}

針對 Node.js&trade; 應用程式啟用除錯工具的步驟：

1. 從應用程式專案的根目錄中，執行下列指令：
  ```
ibmcloud dev debug
```
  {: codeblock}

2. 將除錯器連接至應用程式：
	* [VSCode ](https://blog.docker.com/2016/07/live-debugging-docker/){: new_window} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")
	* [WebStorm ](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/){: new_window} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")


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
