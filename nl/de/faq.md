---

copyright:
  years: 2019
lastupdated: "2019-04-04"

keywords: cli, cli faq, debug cli, cli help, ibmcloud cli help, ibmcloud help

subcollection: cloud-cli

---

# Häufig gestellte Fragen
{: #ibm-cli-faq}

## Muss ich die neueste Version der {{site.data.keyword.cloud_notm}}-CLI verwenden?
{: #cli-latest-version}

Ja, Sie müssen die neueste Version verwenden. Sie können überprüfen, welche Version Sie verwenden, indem Sie den folgenden Befehl ausführen:

```
ibmcloud -v
```
{: codeblock}

## Wie aktualisiere ich meine CLI?
{: #cli-update-version}

Führen Sie den folgenden Befehl aus, um eine Aktualisierung auf die neueste Version der Befehlszeilenschnittstelle durchzuführen:

```
ibmcloud update
```
{: codeblock}

## Kann ich über neue Releases der Befehlszeilenschnittstelle (CLI) benachrichtigt werden?
{: #cli-get-notified}

Ja, Sie bleiben so auf dem Laufenden über neue Releases der CLI und werden benachrichtigt, sobald sie verfügbar sind. Abonnieren Sie das [Release-Repository der {{site.data.keyword.cloud_notm}}-CLI](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")

## Wie ist die Dateistruktur für {{site.data.keyword.cloud_notm}}-Anwendungen?
{: #cli-file-structure}

Anwendungen, die über die CLI erstellt oder aktiviert werden, enthalten vorkonfigurierte Einstellungen, die in der Datei `cli-config.yml` zusammengefasst sind. Die Datei `cli-config.yml` enthält Standardeinträge, die von den Befehlen der CLI verwendet werden und durch an die Befehlszeile übergebene Werte überschrieben werden können.

Anwendungen, die in einer DevOps-Toolchain bereitgestellt wurden, können ebenfalls Dateien wie z. B. `toolchain.yml` und `pipeline.yml` enthalten. Anwendungen, die manuell bereitgestellt werden, können eine `manifest.yml`-Datei und Helm-Diagrammdateien enthalten (z. B. für die Bereitstellung in Cloud Foundry oder Kubernetes).

## Wie werden lokale Container verwendet?
{: #cli-faq-containers}

Das {{site.data.keyword.dev_cli_long}}-CLI-Plug-in verwendet zwei Container, um das Erstellen und Testen Ihrer Anwendung zu vereinfachen. Der erste ist der Container 'tools', der die erforderlichen Dienstprogramme zum Erstellen und Testen Ihrer Anwendung enthält. Die `Dockerfile` für diesen Container ist durch den Parameter [`dockerfile-tools`](/docs/cli/idt?topic=cloud-cli-idt-cli#command-parameters) definiert. Sie können ihn als Entwicklungscontainer ansehen, denn er enthält die Tools, die üblicherweise für die Entwicklung einer bestimmten Laufzeit verwendet werden.

Der zweite Container ist der Ausführungscontainer, der die tatsächliche Laufzeitumgebung Ihrer App recht genau abbildet, nachdem diese in der Cloud bereitgestellt wurde. Dieser Container weist ein Format auf, das beispielsweise für die Bereitstellung zur Verwendung in {{site.data.keyword.cloud_notm}} geeignet ist. In der Folge wird ein Eingangspunkt definiert, der Ihre Anwendung startet. Wenn Sie entscheiden, dass Ihre Anwendung über die {{site.data.keyword.dev_cli_long}}-CLI ausgeführt werden soll, verwendet die Anwendung diesen Container. Die `Dockerfile` für diesen Container ist durch den Parameter [`dockerfile-run`](/docs/cli/idt?topic=cloud-cli-idt-cli#run) definiert.

## Wie implementiere ich vorhandenen Code?

Informationen zum Bereitstellen einer vorhandenen Codebasis finden Sie in [Bereitstellungs- und Cloudaktivierungsassets generieren](/docs/apps?topic=creating-apps-create-deploy-app-cli#byoc-cli).

