---



copyright:

  years: 2015, 2019
lastupdated: "2019-01-03"

---


{:shortdesc: .shortdesc}
{:gif: data-image-type='gif'}
{:new_window: target="_blank"}
{:tip: .tip}



# Einführung in die {{site.data.keyword.Bluemix_notm}}-CLI
{: #getting-started}

Es wird empfohlen, die {{site.data.keyword.Bluemix_notm}}-CLI und alle empfohlenen Abhängigkeiten mithilfe der [hier](/docs/cli/index.html) beschriebenen Methode zu installieren.
{: tip}


Die {{site.data.keyword.Bluemix_notm}}-CLI stellt die Befehlszeilenschnittstelle zum Verwalten von Anwendungen, Containern, Infrastrukturen, Services und anderen Ressourcen in {{site.data.keyword.Bluemix_notm}} zur Verfügung.


Gehen Sie wie folgt vor, um Ihre ersten Schritte nur mit der {{site.data.keyword.Bluemix_notm}}-CLI zu machen:

1. Wählen Sie das Installationsprogramm für Ihr Betriebssystem zum Herunterladen aus.

   Mac OS X 64 Bit: [Installationsprogramm](https://clis.ng.bluemix.net/download/bluemix-cli/latest/osx){: new_window} / [sha1sums](https://clis.ng.bluemix.net/download/bluemix-cli/latest/osx/checksum){: new_window} <br>
   Windows 64 Bit: [Installationsprogramm](https://clis.ng.bluemix.net/download/bluemix-cli/latest/win64){: new_window} / [sha1sums](https://clis.ng.bluemix.net/download/bluemix-cli/latest/win64/checksum){: new_window} <br>
   Linux X86 64 Bit: [Installationsprogramm](https://clis.ng.bluemix.net/download/bluemix-cli/latest/linux64){: new_window} / [sha1sums](https://clis.ng.bluemix.net/download/bluemix-cli/latest/linux64/checksum){: new_window} <br>
   Linux LE 64 Bit (ppc64le): [Installationsprogramm](https://clis.ng.bluemix.net/download/bluemix-cli/latest/ppc64le){: new_window} / [sha1sums](https://clis.ng.bluemix.net/download/bluemix-cli/latest/ppc64le/checksum){: new_window} <br>

   **32-Bit-Releases und Vorgängerversionen finden Sie [hier.](/docs/cli/reference/ibmcloud/all_versions.html)

1. Führen Sie das Installationsprogramm aus.
   * Für Mac OS und Windows führen Sie einfach das Installationsprogramm aus.
   * Für Linux müssen Sie das Paket extrahieren und das Script `install_bluemix_cli` ausführen.

1. Wählen Sie einen API-Endpunkt als Ziel aus und melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

  ![Beispiel](example.gif){: gif}

Jetzt können Sie {{site.data.keyword.Bluemix_notm}}-Ressourcen verwalten. Geben Sie `ibmcloud help` ein, damit Beschreibungen der einzelnen Befehle angezeigt werden.

Wenn Sie eine föderierte ID verwenden, folgen Sie den [hier](/docs/iam/login_fedid.html#federated_id) angegebenen Anweisungen zur Anmeldung mit einem einmaligen Kenncode oder einem API-Schlüssel.
{: tip}

## Links mit weiterführenden Informationen zur {{site.data.keyword.Bluemix_notm}}-CLI

* [Weitere Optionen zum Herunterladen und Installieren der {{site.data.keyword.Bluemix_notm}}-CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Leistungsspektrum der {{site.data.keyword.Bluemix_notm}}-CLI mit Plug-ins erweitern](/docs/cli/reference/ibmcloud/extend_cli.html)
* [Alle Versionen für die {{site.data.keyword.Bluemix_notm}}-CLI und Informationen zum Release](/docs/cli/reference/ibmcloud/all_versions.html)
* [Dokument zur {{site.data.keyword.Bluemix_notm}}-CLI-Befehlssyntax](/docs/cli/reference/ibmcloud/bx_cli.html)


## Probleme melden und Feedback abgeben
{: #issues}

Verwenden Sie die folgenden Optionen, um Probleme zu melden oder Anforderungen für neue Features abzuschicken:
 * Erstellen Sie Problemmeldungen in [GitHub](https://github.com/IBM-Bluemix/bluemix-cli-release/issues){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg)
 * Hinterlassen Sie Nachrichten im [Slack-Kanal](https://dwopen.slack.com/messages/bluemix-cli/){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg)
