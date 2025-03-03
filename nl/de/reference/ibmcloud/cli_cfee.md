---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, cloud foundry enterprise environment, cfee, ibmcloud cfee, cfee environment, cfee instance, target user, list cfee

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# Mit dem CFEE-Service arbeiten
{: #ibmcloud_commands_cfee}

Mit {{site.data.keyword.cfee_full}} (CFEE) können Sie mehrere isolierte und auf Unternehmen abgestimmte Cloud Foundry-Plattformen bedarfsgesteuert instanziieren. Instanzen des IBM Cloud Foundry Enterprise-Service werden in Ihrem eigenen Konto in der {{site.data.keyword.cloud_notm}}-Umgebung ausgeführt. Die Umgebung wird auf isolierter Hardware (Kubernetes-Cluster) bereitgestellt. Sie haben volle Kontrolle über die Umgebung, einschließlich Zugriffssteuerung, Kapazitätsmanagement, Versionsaktualisierungen, Ressourcennutzung und Überwachung.

Verwenden Sie die folgenden Befehle, um CFEE-Umgebungen, -Organisationen, -Bereiche, -Benutzer und -Rollen zu verwalten.
{: shortdesc}

## ibmcloud cfee environments
{: #ibmcloud_cfee_environments}

CFEE-Umgebungen auflisten:
```
ibmcloud cfee environments
```
{: codeblock}

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

## ibmcloud cfee environment
{: #ibmcloud_cfee_environment}

Details zu einer CFEE-Umgebung anzeigen:
```
ibmcloud cfee environment NAME [--id]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>NAME (erforderlich)</dt>
   <dd>Der Name der Umgebung, die angezeigt werden soll.</dd>
   <dt>--id</dt>
   <dd>Nur ID anzeigen</dd>
  </dl>

<strong>Beispiele</strong>:

Details der CFEE-Umgebung `env_example` anzeigen:
```
ibmcloud cfee environment env_example
```
{: codeblock}

ID der CFEE-Umgebung `env_example` anzeigen:
```
ibmcloud cfee environment env_example --id
```
{: codeblock}

## ibmcloud cfee orgs
{: #ibmcloud_cfee_orgs}

Alle Organisationen auflisten:
```
ibmcloud cfee orgs [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Alle Organisationen auflisten:
```
ibmcloud cfee orgs
```
{: codeblock}

Alle Organisationen der CFEE-Umgebung `env_example` auflisten:
```
ibmcloud cfee orgs --env env_example
```
{: codeblock}

## ibmcloud cfee org
{: #ibmcloud_cfee_org}

Details zu einer Organisation anzeigen:
```
ibmcloud cfee org ORG [--guid] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>--guid</dt>
   <dd>Nur GUID der Organisation anzeigen, alle anderen Ausgaben für die Organisation werden unterdrückt</dd>
  </dl>

<strong>Beispiele</strong>:

Details der CFEE-Organisation `org_example` anzeigen:
```
ibmcloud cfee org org_example
```
{: codeblock}

Details der CFEE-Organisation `org_example` der CFEE-Umgebung `env_example` anzeigen:
```
ibmcloud cfee org org_example --env env_example
```
{: codeblock}

GUID der CFEE-Organisation `org_example` anzeigen:
```
ibmcloud cfee org org_example --guid
```
{: codeblock}

## ibmcloud cfee org-create
{: #ibmcloud_cfee_org_create}

Organisation erstellen:
```
ibmcloud cfee org-create ORG [-q, --quota QUOTA] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, die erstellt wird.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>-q, --quota QUOTA</dt>
   <dd>Kontingent, das der neu erstellten Organisation zugewiesen werden soll (Standardkontingent verwenden, wenn keine Angabe gemacht wird)</dd>
  </dl>

<strong>Beispiele</strong>:

CFEE-Organisation `org_example` erstellen:
```
ibmcloud cfee org-create org_example
```
{: codeblock}

CFEE-Organisation `org_example` der CFEE-Umgebung `env_example` erstellen:
```
ibmcloud cfee org-create org_example --env env_example
```
{: codeblock}

CFEE-Organisation `org_example` mit Kontingent `quote_example` erstellen:
```
ibmcloud cfee org org-create org_example --quota quota_example
```
{: codeblock}

## ibmcloud cfee org-delete
{: #ibmcloud_cfee_org_delete}

Organisation löschen:
```
ibmcloud cfee org-delete ORG [-f, --force] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, die gelöscht wird.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>-f, --force</dt>
   <dd>Löschen ohne Bestätigung erzwingen</dd>
  </dl>

<strong>Beispiele</strong>:

CFEE-Organisation `org_example` löschen:
```
ibmcloud cfee org-delete org_example
```
{: codeblock}

CFEE-Organisation `org_example` der CFEE-Umgebung `env_example` löschen:
```
ibmcloud cfee org-delete org_example --env env_example
```
{: codeblock}

CFEE-Organisation `org_example` ohne Bestätigung löschen:
```
ibmcloud cfee org org-delete org_example -f
```
{: codeblock}

## ibmcloud cfee org-users
{: #ibmcloud_cfee_org_users}

Benutzer in angegebener Organisation nach Rolle anzeigen:
```
ibmcloud cfee org-users ORG [-a, --all] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>-a, --all</dt>
   <dd>Alle Benutzer in der angegebenen Organisation auflisten</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Benutzer in CFEE-Organisation `org_example` anzeigen:
```
ibmcloud cfee org-users org_example
```
{: codeblock}

Benutzer in CFEE-Organisation `org_example` der CFEE-Umgebung `env_example` anzeigen:
```
ibmcloud cfee org-users org_example --env env_example
```
{: codeblock}

Alle Benutzer in CFEE-Organisation `org_example` auflisten:
```
ibmcloud cfee org-users org_example -a
```
{: codeblock}

## ibmcloud cfee org-role-set
{: #ibmcloud_cfee_org_role_set}

Organisationsrolle einem Benutzer zuweisen (Organisationsmanager erforderlich)
```
ibmcloud cfee org-role-set USER_EMAIL ORG ROLE [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_EMAIL (erforderlich)</dt>
   <dd>Die E-Mail-Adresse des Benutzers, der zugewiesen wird.</dd>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, der dieser Benutzer zugewiesen wird.</dd>
   <dt>ROLE (erforderlich)</dt>
   <dd>Der Name der Organisationsrolle, der dieser Benutzer zugeordnet wird. Beispiel:
   <ul>
   <li>OrgManager: Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</li>
   <li>BillingManager: Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</li>
   <li>OrgAuditor: Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte.</li>
   </ul>
   </dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Rolle `BillingManager` dem Benutzer `test@exmaple.com` in der Organisation `org_example` zuweisen:
```
ibmcloud cfee org-role-set tes@example.com org_example BillingManager
```
{: codeblock}

Rolle `BillingManager` dem Benutzer `test@exmaple.com` in der Organisation `org_example` der CFEE-Umgebung `env_example` zuweisen:
```
ibmcloud cfee org-role-set tes@example.com org_example BillingManager --env env_example
```
{: codeblock}

## ibmcloud cfee org-role-unset
{: #ibmcloud_cfee_org_role_unset}

Organisationsrolle eines Benutzers entfernen (nur Organisationsmanager oder Benutzer selbst):
```
ibmcloud cfee org-role-unset USER_EMAIL ORG ROLE [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_EMAIL (erforderlich)</dt>
   <dd>Die E-Mail-Adresse des Benutzers, der entfernt wird.</dd>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, aus der dieser Benutzer entfernt wird.</dd>
   <dt>ROLE (erforderlich)</dt>
   <dd>Der Name der Organisationsrolle, aus der dieser Benutzer entfernt wird. Beispiel:
   <ul>
   <li>OrgManager: Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</li>
   <li>BillingManager: Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</li>
   <li>OrgAuditor: Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte.</li>
   </ul>
   </dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Rolle `BillingManager` des Benutzers `test@exmaple.com` aus Organisation `org_example` entfernen:
```
ibmcloud cfee org-role-unset tes@example.com org_example BillingManager
```
{: codeblock}

Rolle `BillingManager` des Benutzers `test@exmaple.com` aus der Organisation `org_example` der CFEE-Umgebung `env_example` entfernen:
```
ibmcloud cfee org-role-unset tes@example.com org_example BillingManager --env env_example
```
{: codeblock}

## ibmcloud cfee spaces
{: #ibmcloud_cfee_spaces}

Alle Bereiche auflisten:
```
ibmcloud cfee spaces [-o,--org ORG] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>-o, --org ORG</dt>
   <dd>Organisationsname. Standardmäßig wird die aktuelle Organisation verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Alle Bereiche auflisten:
```
ibmcloud cfee spaces
```
{: codeblock}

Alle Bereiche der Organisation `org_example` und der CFEE-Umgebung `env_example` auflisten
```
ibmcloud cfee spaces -o org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space
{: #ibmcloud_cfee_space}

Informationen des angegebenen Bereichs anzeigen
```
ibmcloud cfee space SPACE [--guid] [--security-group-rules] [-o,--org ORG] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs, der angezeigt werden soll.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>--guid</dt>
   <dd>GUID eines angegebenen Bereichs abrufen und anzeigen. Alle anderen Ausgaben für den Bereich werden unterdrückt.</dd>
   <dt>-o, --org ORG</dt>
   <dd>Organisationsname. Standardmäßig wird die aktuelle Organisation verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>--security-group-rules</dt>
   <dd>Regeln für alle Sicherheitsgruppen abrufen, die dem Bereich zugeordnet sind.</dd>
  </dl>

<strong>Beispiele</strong>:

Informationen zum Bereich `space_example` anzeigen:
```
ibmcloud cfee space space_example
```
{: codeblock}

GUID zum Bereich `space_example` abrufen und anzeigen:
```
ibmcloud cfee space space_example --guid
```
{: codeblock}

Regeln für alle Sicherheitsgruppen, die dem Bereich `space_example` zugeordnet sind, anzeigen:
```
ibmcloud cfee space space_example --security-group-rules
```
{: codeblock}

Informationen zum Bereich `space_example` der Organisation `org_example` und der CFEE-Umgebung `env_example` anzeigen:
```
ibmcloud cfee space space_example -o org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space-create
{: #ibmcloud_cfee_space_create}

Einen neuen Bereich erstellen
```
ibmcloud cfee space-create SPACE [-o, --org ORG] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs, der erstellt wird.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>-o, --org ORG</dt>
   <dd>Organisationsname. Standardmäßig wird die aktuelle Organisation verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Neuen Bereich `space_example` erstellen:
```
ibmcloud cfee space-create space_example
```
{: codeblock}

Neuen Bereich `space_example` unter der Organisation `org_example` und der CFEE-Umgebung `env_example` erstellen:
```
ibmcloud cfee space-create space_example -o org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space-rename
{: #ibmcloud_cfee_space_rename}

Bereich umbenennen:
```
ibmcloud cfee space-rename OLD_NAME NEW_NAME [-o, --org ORG] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>OLD_NAME (erforderlich)</dt>
   <dd>Der bisherige Name des Bereichs, der umbenannt werden soll.</dd>
   <dt>NEW_NAME (erforderlich)</dt>
   <dd>Der neue Name für den Bereich, der umbenannt werden soll.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>-o, --org ORG</dt>
   <dd>Organisationsname. Standardmäßig wird die aktuelle Organisation verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Bereich `space_example` in `new_pace_example` umbenennen:
```
ibmcloud cfee space-rename space_example new_pace_example
```
{: codeblock}

Umbenennung des Bereichs `space_example` in `new_pace_example` unter der Organisation `org_example` und der CFEE-Umgebung `env_example` durchführen:
```
ibmcloud cfee space-rename space_example new_pace_example -o org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space-delete
{: #ibmcloud_cfee_space_delete}

Bereich löschen:
```
ibmcloud cfee space-delete SPACE [-f, --force] [-o, --org ORG] [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs, der gelöscht werden soll.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
   <dt>-f, --force</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
   <dt>-o, --org ORG</dt>
   <dd>Organisationsname. Standardmäßig wird die aktuelle Organisation verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Bereich `space_example` löschen:
```
ibmcloud cfee space-delete space_example
```
{: codeblock}

Bereich `space_example` unter der Organisation `org_example` und der CFEE-Umgebung `env_example` ohne Bestätigung löschen:
```
ibmcloud cfee space-delete space_example new_pace_example -f -o org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space-role-set
{: #ibmcloud_cfee_space_role_set}

Bereichsrolle einem Benutzer zuordnen
```
ibmcloud cfee space-role-set USER_EMAIL ORG SPACE ROLE [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_EMAIL (erforderlich)</dt>
   <dd>Die E-Mail-Adresse des Benutzers, der zugewiesen wird.</dd>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, der dieser Benutzer zugewiesen wird.</dd>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs, dem dieser Benutzer zugewiesen wird.</dd>
   <dt>ROLE (erforderlich)</dt>
   <dd>Der Name der Bereichsrolle, der dieser Benutzer zugewiesen wird. Beispiel:
   <ul>
   <li>SpaceManager: Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</li>
   <li>SpaceDeveloper: Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</li>
   <li>SpaceAuditor: Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</li>
   </ul></dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Benutzer `test@exmaple.com` der Organisation `org_example` und dem Bereich `space_example` mit der Rolle `SpaceManager` zuweisen:
```
ibmcloud cfee space-role-set tes@example.com org_example space_example SpaceManager
```
{: codeblock}

Benutzer `test@exmaple.com` der Organisation `org_example` und dem Bereich `space_example` mit der Rolle `SpaceManager` unter der Umgebung `env_example` zuweisen:
```
ibmcloud cfee space-role-set tes@example.com org_example space_example SpaceManager --env env_example
```
{: codeblock}

## ibmcloud cfee space-role-unset
{: #ibmcloud_cfee_space_role_unset}

Bereichsrolle eines Benutzers entfernen
```
ibmcloud cfee space-role-unset USER_EMAIL ORG SPACE ROLE [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_EMAIL (erforderlich)</dt>
   <dd>Die E-Mail-Adresse des Benutzers, der entfernt wird.</dd>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation, aus der dieser Benutzer entfernt wird.</dd>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs, aus dem dieser Benutzer entfernt wird.</dd>
   <dt>ROLE (erforderlich)</dt>
   <dd>Der Name der Bereichsrolle, aus der dieser Benutzer entfernt wird. Beispiel:
   <ul>
   <li>SpaceManager: Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</li>
   <li>SpaceDeveloper: Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</li>
   <li>SpaceAuditor: Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</li>
   </ul></dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Benutzer `test@exmaple.com` aus der Organisation `org_example` und dem Bereich `space_example` mit der Rolle `SpaceManager` entfernen:
```
ibmcloud cfee space-role-unset tes@example.com org_example space_example SpaceManager
```
{: codeblock}

Benutzer `test@exmaple.com` aus der Organisation `org_example` und dem Bereich `space_example` mit der Rolle `SpaceManager` unter der Umgebung `env_example` entfernen:
```
ibmcloud cfee space-role-unset tes@example.com org_example space_example SpaceManager --env env_example
```
{: codeblock}

## ibmcloud cfee space-roles
{: #ibmcloud_cfee_space_roles}

Alle Bereichsrollen des aktuellen Benutzers unter einer bestimmten Organisation abrufen

```
ibmcloud cfee space-roles ORG [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Alle Bereichsrollen des aktuellen Benutzers unter der Organisation `org_example` abrufen:
```
ibmcloud cfee space-roles org_example
```
{: codeblock}

Alle Bereichsrollen des aktuellen Benutzers unter der Organisation `org_example` und der Umgebung `env_example` abrufen:
```
ibmcloud cfee space-roles org_example --env env_example
```
{: codeblock}

## ibmcloud cfee space-users
{: #ibmcloud_cfee_space_users}

Benutzer im angegebenen Bereich nach Rolle anzeigen
```
ibmcloud cfee space-users ORG SPACE [--env ENV]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>ORG (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>SPACE (erforderlich)</dt>
   <dd>Der Name des Bereichs.</dd>
   <dt>--env ENV</dt>
   <dd>Der Name der CFEE-Umgebung. Standardmäßig wird die aktuelle CFEE-Umgebung verwendet, wenn keine Angabe gemacht wurde.</dd>
  </dl>

<strong>Beispiele</strong>:

Alle Benutzer im Bereich `space_example` und der Organisation `org_example` anzeigen:
```
ibmcloud cfee space-users org_example space_example
```
{: codeblock}

Alle Benutzer im Bereich `space_example` und der Organisation `org_example` und der Umgebung `env_example` anzeigen:
```
ibmcloud cfee space-users org_example space_example --env env_example
```
{: codeblock}

## ibmcloud cfee create
{: #ibmcloud_cfee_create}

Anforderung zum Erstellen einer neuen Instanz von Cloud Foundry Enterprise Environment erstellen:
```
ibmcloud cfee create NAME LOCATION [--cells CELLS] [--isolation ISOLATION] [--private-vlan ID, --public-vlan ID] [--plan ID]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>NAME (erforderlich)</dt>
   <dd>Der Name der Instanz.</dd>
   <dt>LOCATION (erforderlich)</dt>
   <dd>Die Position, an der die Instanz erstellt werden soll.</dd>
   <dt>--cells CELLS</dt>
   <dd>Geben Sie die Anzahl der Zellen für dieses CFEE an. Der Standardwert ist 2 und der Mindestwert ist 1. In einer CFEE mit einer Zelle kann es keine hohe Verfügbarkeit geben.</dd>
   <dt>--isolation ISOLATION</dt>
   <dd>Geben Sie die Isolation des IBM Kubernetes-Clusters an. Optionen sind "dediziert" und "freigegeben". Der Standardwert ist "freigegeben". Für einen "dedizierten" Cluster werden mehr Gebühren berechnet.</dd>
   <dt>--private-vlan ID</dt>
   <dd>Geben Sie die ID des privaten VLAN an. Standardmäßig finden wir eine verfügbare Gruppe von VLANS oder wir erstellen ein Paar für Sie.</dd>
   <dt>--public-vlan ID</dt>
   <dd>Geben Sie die ID des öffentlichen VLAN an. Standardmäßig finden wir eine verfügbare Gruppe von VLANS oder wir erstellen ein Paar für Sie.</dd>
   <dt>--plan ID</dt>
   <dd>Geben Sie die ID des Plans an. Standardmäßig erfolgt die Bereitstellung im Standardplan.</dd>
  </dl>

<strong>Beispiele</strong>:

Erstellen Sie eine Instanz mit dem Namen `test-cfee` in `dal10`:

```
ibmcloud cfee create test-cfee dal10
```

Erstellen Sie eine `dedizierte` Instanz mit `4` Zellen mit dem Namen `test-cfee` in `dal10`:

```
ibmcloud cfee create test-cfee dal10 --cells 4 --isolation dedicated
```

## ibmcloud cfee create-locations
{: #ibmcloud_cfee_create_locations}

Erstellen Sie eine Anforderung zum Abrufen einer Liste verfügbarer Rechenzentren für die Zielregionen.
```
ibmcloud cfee create-locations
```
{: codeblock}

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:


## ibmcloud cfee create-permission-get
{: #ibmcloud_cfee_create_permission_get}

Überprüfen Sie, ob ein Benutzer über alle Berechtigungen verfügt, die zum Erstellen einer CFEE-Instanz erforderlich sind. Der Befehl überprüft die folgenden Zugriffsrichtlinien für den Zielbenutzer: Editor für die CFEE-Services, die Administratorrolle für den Kubernetes-Service, die Rolle des Editors für die Plattform und die Rolle des Servicezugriffsmanagers für den Cloud Object Storage-Service und die Entwicklerrolle für den aktuellen Bereich in der aktuellen Organisation für die Bereitstellung von Compose for PostgreSQL.

```
ibmcloud cfee create-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output FORMAT]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers.</dd>
   <dt>--access-group GROUP_NAME</dt>
   <dd>Der Name der Zugriffsgruppe, in der die Berechtigungen überprüft werden sollen. Die Standardzugriffsgruppe ist "cfee-provision-access-group".</dd>
   <dt>--output FORMAT</dt>
   <dd>Geben Sie das Ausgabeformat für Berechtigungen an. Momentan wird nur JSON unterstützt.</dd>
  </dl>
  
<strong>Beispiele</strong>:

Überprüfen Sie die CFEE-Erstellungsberechtigungen für den Benutzer `name@example.com`:

```
ibmcloud cfee create-permission-get name@example.com
```

Überprüfen Sie die CFEE-Erstellungsberechtigungen für den Benutzer `name@example.com` und in der Zugriffsgruppe `test-access-group`:

```
ibmcloud cfee create-permission-get name@example.com -ag test-access-group
```

## ibmcloud cfee create-permission-set
{: #ibmcloud_cfee_create_permission_set}

Erteilen Sie dem Benutzer alle Berechtigungen, die zum Erstellen einer CFEE-Instanz erforderlich sind. Mit dem Befehl werden die folgenden Zugriffsrichtlinien für den Zielbenutzer erstellt: Editorrolle für den CFEE-Service, Administratorrolle für den Kubernetes-Service, die Rolle des Editors für die Plattform und die Rolle des Servicezugriffsmanagers für den Cloud Object Storage-Service und Entwicklerrolle für den aktuellen Bereich in der aktuellen Organisation für die Bereitstellung von Compose for PostgreSQL.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers.</dd>
   <dt>--access-group GROUP_NAME</dt>
   <dd>Der Name der Zugriffsgruppe, in der Berechtigungen erteilt werden sollen. Die Standardzugriffsgruppe ist "cfee-provision-access-group".</dd>
  </dl>
  
<strong>Beispiele</strong>:

Erteilen Sie dem Benutzer `name@example.com` CFEE-Erstellungsberechtigungen über die Standardzugriffsgruppe:
```
ibmcloud cfee create-permission-set name@example.com
```
{: codeblock}

Erteilen Sie dem Benutzer `name@example.com` CFEE-Erstellungsberechtigungen über die Zugriffsgruppe `test-access-group`:
```
ibmcloud cfee create-permission-set name@example.com -ag test-access-group
```
{: codeblock}

## ibmcloud cfee create-status
{: #ibmcloud_cfee_create_status}

Überprüfen Sie den Bereitstellungsstatus einer CFEE-Instanz:
```
ibmcloud cfee create-status NAME or ID [--poll] [--output FORMAT]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>NAME oder ID (erforderlich)</dt>
   <dd>Der Name oder die ID der CFEE-Instanz.</dd>
   <dt>--poll</dt>
   <dd>Geben Sie an, ob dieser Aufruf wiederholt werden soll, damit die Abfrage so lange erfolgt, bis ein stabiler Zustand erreicht ist.</dd>
   <dt>--output FORMAT</dt>
   <dd>Geben Sie das Ausgabeformat an. Momentan wird nur JSON unterstützt.</dd>
  </dl>
