# i-doit / OTRS / Znuny - Connector

## 1. Allgemeine Informationen 

- Der von it-novum entwickelte Connector ermöglicht Config Items von i-doit nach OTRS zu synchronisieren. Dabei besteht die Möglichkeit genau festzulegen welche Objekttypen, Kategorien und Attribute von i-doit nach OTRS übertragen werden und auf welche Objekttypen und Attribute sie dort abgebildet werden sollen.
- Darüber hinaus ist der Connector mandantenfähig. Es ist möglich mehrere unabhängige i-doit Instanzen an ein zentrales OTRS anzubinden. Hierfür müssen jeweils ein Webservice je i-doit Instanz eingerichtet werden und entsprechend im jeweiligen Connector konfiguriert werden. Pro Instanz können so auch unterschiedliche Benutzer konfiguriert werden.

## 2. Installation und Konfiguration

### 2.1 OTRS Installation & Konfiguration

- In OTRS müssen die frei verfügbaren ITSM Pakete installiert sein. Standardmäßig stehen dann bereits 5 Klassen bereit (Computer, Network….). Diese Klassen können je nach Anforderungen ergänzt oder modifiziert werden. Nur Klassen die per Copy & Paste in die Konfiguration des Connectors (siehe Import) eingefügt werden, werden entsprechend synchronisiert. Somit können in der CMDB von OTRS auch Klassen gepflegt werden, die nicht über i-doit verwaltet oder aktualisiert werden.
- In OTRS müssen zwei Dinge durchgeführt werden:

	- der Webservice muss mit den entsprechenden Methoden für CreateCI, UpdateCI und SearchCI angelegt werden
	- die Klassenstrukturen müssen aus OTRS nach i-doit kopiert und bei Änderungen im Connector oder OTRS immer manuell synchron gehalten werden.

- WICHTIG Namen und die Operationen müssen exakt so im Connector in i-doit unter den Einstellungen eingetragen sein.

### 2.2 Webservices

#### 2.2.1 Importieren des Webservices

- Im Lieferumfang der Schnittstelle sollte eine Datei (IdoitSync.yml)beinhaltet sein. Diese kann über den Adminbereich -> Webservices importiert werden. Damit der Webservice ohne Probleme funktioniert, muss zuvor das ITSM Paket installiert sein.

#### 2.2.2 Alternativ - Manuelles anlegen des Webservices

- Im nachfolgenden Bild kann man sehen wie ein Webservice in OTRS aussehen muss.

![This is an image](/images/OTRS_Webservice_Uebersicht.png)

- Die einzelnen Operationen sollten wie folgt aussehen. Weitere Einstellungen müssen nicht vorgenommen werden.

![This is an image](/images/OTRS_Webservice_Operation.png)

- Darüber hinaus müssen noch folgende Einstellungen in den Netzwerk Transport Einstellungen für "HTTP::REST" getroffen werden. Dafür klickt man auf den Button "Configure" neben dem Eintrag "Network Transport HTTP::REST" und füllt die Felder wie in der nachfolgenden Abbildung aus.

![This is an image](/images/Rest_transport_config_de.png)

#### 2.2.3 CMDB Klassen für den Sync

- In der Anlage haben wir zwei Beispiel für den Aufbau von OTRS CMDB Klassen.

### 2.3 User für die Synchronisation

- Für den sync von i-doit nach OTRS wird noch ein User auf der OTRS Seite benötigt. Dieser User braucht die kompletten Rechte für die Gruppe „itsm-configitem“ Der User sollte aus Sicherheitsgründen nicht der "root" Benutzer sein, ist aber grundsätzlich möglich. Des weiteren ist es sinnvoll, allen anderen Usern in OTRS auf die CMDB nur Lese-Rechte zu vergeben, da i-doit als führendes System genutzt wird und die Werte nicht in OTRS gepflegt werden sollen.

### 2.4 i-doit Installation & Konfiguration

- Der i-doit / OTRS Connector wird wie jedes andere Modul über das Admin Center installiert.

```otrssync-1.9.2.zip```

- Nach der Installation müssen noch die entsprechenden Rechte für das otrssync Modul gesetzt werden, damit man Zugriff auf den Connector im i-doit Frontend bekommt. Ist dies geschehen, steht der Connector unter dem Menüpunkt „Extras“ zur Verfügung

![This is an image](/images/Rechtevergabe.png)

- Nach der Installation in i-doit steht der Connector unter dem Menüpunkt "Extras" zur Verfügung.

#### 2.4.1 Startseite 

- Die Startseite gibt einen Überblick über die getroffenen Einstellungen für die Synchronisation und die Verbindung zum Webservice von OTRS. Außerdem kann man sehen wann die letzte erfolgreiche Synchronisation mit OTRS stattgefunden hat und ob die Möglichkeit besteht Emails zu versenden. Bei der Email Konfiguration wird zum einen überprüft , ob ein Email Server in i-doit konfiguriert ist und zum Anderen ob im Connector Email Adressen für die Benachrichtigung eintragen wurden.

![This is an image](/images/Startseite.png)

#### 2.4.2 Einstellungen

- Als erstes sollte die Einstellungsseite geöffnet und der **Lizenzschlüssel aktiviert** werden, 

![This is an image](/images/Aktivierung.png)

- Danach sollten die entsprechenden Einträge für die Verbindung zu OTRS, die Synchronisation, die Änderungshistorie und die Benachrichtigungen gesetzt werden.
- Unter dem Punkt **Verbindung** werden die Angaben zum Webservice von OTRS getroffen. Hier werden die URL zum OTRS-System, der Name des Webservices (der in OTRS angelegt wurde in unserem Webservice zum Import ist dies **IdoitSync**), die Aktionen für das Suchen, Aktualisieren und Anlegen von CI's (werden die Aktionen leer gelassen, wird automatisch der it-novum default SearchCI, CreateCI und UpdateCI genommen), der Benutzername und das Passwort eingetragen. Anschließend kann man über den Button "Verbindung überprüfen" testen, ob die Verbindung zum OTRS-System ordnungsgemäß funktioniert.
- Unter dem Punkt **Automatische Synchronisation** werden die zeitlichen Intervalle für die Synchronisation festgelegt. Zuerst muss man einen Haken setzen und danach das gewünschte Intervall auswählen. Es stehen die Möglichkeiten alle 10 Minuten, alle 15 Minuten, alle 30 Minuten, jede Stunde und jeden Tag zur Auswahl.
- Der Punkt **Changelog** bietet die Möglichkeit zu entscheiden wie lange man die Änderungshistorie aufheben möchte. Hier hat man die Wahl zwischen für einen Tag, für eine Woche, für einen Monat, für ein Jahr oder für immer.
- Unter dem Punkt **Email Benachrichtigungen** kann man E-Mail Adressen hinterlegen, die eine Benachrichtigung erhalten wenn ein Fehler auftritt. Es können mehrere E-Mail Adressen getrennt durch ein Semikolon hinterlegt werden.
- Abschließend alle Einstellungen speichern. Um zu überprüfen, ob die E-Mail Konfiguration funktioniert, kann man über den Button <Testmail senden> eine E-Mail an die eingetragenen E-Mail Adressen senden.
- Außerdem kann man über den Button <Kompatibilitätscheck> überprüfen, ob alle Tabellen, Spalten und Konstanten, die vom Konnektor verwendet werden, in i-doit noch vorhanden sind.

![This is an image](/images/manuelle_einstellungen.png)

- Unter dem Abschnitt "Alle Einstellungen sichern" kann man vor dem Update auf eine neuere Version oder aus anderen Gründen ein Backup aller Einstellungen erstellen. Die Backups sind über das Auswahlfeld auswählbar und können nach Auswahl wieder hergestellt oder gelöscht werden. Die Backupdateien werden auf dem Server im Datei Upload Ordner (z.B. /var/www/html/i-doit/upload/files/) abgelegt.

![This is an image](/images/manual_backup.png)


#### 2.4.3 Import OTRS Klassen

- Über den Menüpunkt "Import" kopiert man die angelegten Klassenstrukturen, im YAML Format, mit den dazugehörigen Attributen aus OTRS in den Connector. Defaultmässig werden hier die Standard Strukturen aus OTRS mitgeliefert. Werden die Klassendefinitionen in OTRS geändert oder neu angelegt, können diese per Copy & Paste hier eingefügt werden.
- Der Klassenname steht, nach dem Speichern der Struktur, im Schritt 1 für das Mapping der Objekttypen zur Verfügung. Nach dem Speichern einer Struktur werden auf der rechten Seite die verfügbaren Attribute angezeigt. Diese Attribute stehen im Schritt 3 für das Mapping der Attribute bereit.
- Beispiele für Computer und Monitore sind als Textdokument vorhanden. (computer.yaml und monitor.yaml)

![This is an image](/images/manual_import.png)

- Unter dem Punkt "Deployment States OTRS" muss man festlegen, welche Kombination aus CMDB Status und Einsatzzweck einen OTRS Deployment Status ergeben.
- Mit der Wahl des Eintrags "Alle / Rest" kann ein Wildcard gesetzt werden. Ein Beispiel: die Kombination Einsatzzweck "Produktion" und CMDB Status "Alle / Rest" führt dazu, dass alle Objekte mit dem Einsatzzweck "Produktion", die nicht mit einem CMDB Status verknüpft wurden, den Deployment Status "Production" erhalten. Der Einsatzzweck CMDB Status Kombination der Objekte, so wie sie in der Liste aufgeführt ist bedeutet für die Reihenfolge des Matchings in diesem Beispiel das zuerst die Kombination "Test" und "In Betrieb" gemapped wird, danach "Qualitätssicherung" und "Alle / Rest" und so weiter. Die niedrigste Priorität hat immer die Kombination "Alle / Rest" und "Alle / Rest".
- Allgemein kann man sagen, dass als erstes ein ausgefüllter Einsatzzweck und CMDB Status ausgewertet wird, danach die Kombination aus ausgefülltem Einsatzzweck und "Alle / Rest" für den CMDB Status,anschließend die Kombination "Alle / Rest" für Einsatzzweck und ausgefüllter CMDB Status und zum Schluss die Kombination "Alle / Rest" für Einsatzzweck und CMDB Status.

![This is an image](/images/manual_depl_states.png)

- Unter dem Abschnitt "Black list Deployment States" kann man eine Kombination von Einsatzzweck und CMBD Status auswählen, die dann bei der Synchronisation ignoriert werden sollen. Das bedeutet, wenn ein Objekt den Status Einsatzzweck "Test" hat wird es nicht synchronisiert, da als zweiter Parameter "Alle/Rest" ausgewählt wurde. Hat man ein Deployment State Mapping erstellt und fügt diese Kombination auch in die Blacklist ein, werden Objekte mit dieser Kombination nicht synchronisiert.

![This is an image](/images/manual_blacklist.png)

- Im Abschnitt "Map Archived / Deleted to Deployment State" kann man festlegen auf welchen Status CI's in OTRS gesetzt werden sollen, die in idoit auf archiviert oder gelöscht gesetzt wurden. Wählt der Anwender hier nichts aus, werden alle CI's, die Gelöscht oder Archiviert wurden in OTRS auf den Status "Inactive" gesetzt.

![This is an image](/images/manual_map_archieved_deleted.png)

#### 2.4.4 Mapping Schritt 1: Objekttypen

- Ab Schritt 1 erfolgt die Zuordnung beginnend mit den Objekttypen. Dabei werden auf der linken Seite alle in i-doit verfügbaren Objekttypen angezeigt. Auf der rechten Seite kann man aus der Drop-Down-Box die zur Verfügung stehen OTRS Klassen auswählen.
- Dabei legt man als erstes fest welche Objekttypen auf welche Klassen abgebildet werden sollen. Dabei müssen nicht alle i-doit Objekttypen, den OTRS Klassen zuordnet werden, sondern man kann auch "No Sync" auswählen, um Objekttypen von der Synchronisation auszuschließen.
- Da die Auswahl für i-doit Objekte sehr lang und unübersichtlich sein kann, lässt sich durch Eingabe des i-doit Objektnamens die Anzeige filtern.
- Ist man fertig mit der Zuordnung klickt man am Seitenende auf den Button "Weiter zu Schritt 2", um das Mapping zu speichern.

![This is an image](/images/manual_step_1.png)

#### 2.4.5 Mapping Schritt 2: Kategorien

- In Schritt 2 wählt man die Kategorien, die für die Synchronisation verwendet werden. Durch eine Vorauswahl der Kategorien schränkt man auch gleich die Auswahl der zur Verfügung stehenden Attribute ein.
- Im Default werden die Kategorien Allgemein, Kontaktzuweisung, Modell, Hostadresse, Standort, Servicezuweisung und Betriebssystem zur Auswahl angeboten. Alternativ lassen sich über den Button <Show All / Alles anzeigen> alle zur Verfügung stehenden Kategorien anzeigen und die Auswahl erweitern oder komplett ändern.15
- Ist man mit der Auswahl der Kategorien fertig, klickt man entweder auf den Button <Weiter zu Schritt 3> um zu speichern oder auf den Button <Zurück zu Schritt 1>, um die Auswahl zu verwerfen.

![This is an image](/images/manual_step_2.png)

#### 2.4.6 Mapping Schritt 3: Attribute

- Schritt 3 dient dazu die Attribute aus i-doit den Attributen aus OTRS zuzuordnen. Dabei werden pro Objekttyp nur die darin verfügbaren Kategorien angezeigt. Die Zuordnung muss für jeden ausgewählten Objekttyp durchgeführt werden. Dazu klickt man auf das jeweilige Objekt und es öffnet sich eine Box mit den verfügbaren Attributen. Man muss nicht alle Attribute aus i-doit zuordnen, sondern kann auch "No Sync" auswählen um nur die gewünschten Attribute aus i-doit nach OTRS zu übertragen.
- **HINWEIS:** Vermisst man bei der Zuordnung Attribute auf der i-doit Seite, liegt dies daran, dass der Algorithmus im Hintergrund die Attribute nicht vollständig auflösen konnte. Abhilfe schafft hier die manuelle Erweiterung der entsprechenden Tabelle.
- Ist die Zuordnung abgeschlossen klickt man auf <Speichern> oder auf den Button <Zurück zu Schritt 2> um die Zuordnung zu verwerfen.
- Nach dem Speichern kann man über den Button <Quick Sync> das erstellte Mapping anwenden und die Objekte aus i-doit nach OTRS synchronisieren. Ist das Objekt in OTRS bereits vorhanden wird es aktualisiert. Nimmt man in der Zuordnung keine Änderungen vor, kann man jederzeit die Synchronisation über diesen Button von Hand anstoßen.
- Bevor die Synchronisation ausgeführt wird, prüft die Schnittstelle für jedes zu synchronisierende Objekt, ob seit der letzten Synchronisation etwas verändert wurde und ob eine Synchronisation überhaupt notwendig ist. Es werden somit nur Objekte synchronisiert, die tatsächlich verändert wurden. Dies hält die zu übertragende Datenmenge so gering wie möglich
- **HINWEIS:** Wird ein Objekt in i-doit gelöscht oder archiviert, wird es in OTRS auf "inactive" gesetzt, da in OTRS das Löschen von Objekten nicht möglich ist.

![This is an image](/images/manual_step_3_1.png)
![This is an image](/images/manual_step_3_2.png)

#### 2.4.7 Änderungshistorie
- Die Änderungshistorie beinhaltet alle Änderungen mit Datum, Zeitpunkt und Benutzer, die im Connector durchgeführt wurden. Es besteht die Möglichkeit genau den Zeitraum einzugrenzen für den man die Änderungen am Mapping sehen möchte. Generell wird hier jede Änderung protokolliert und ist bis zum Tag der ersten Verwendung nachvollziehbar.
- Hat man allerdings die automatische Bereinigung der Änderungshistorie in den Einstellungen aktiviert sind die Änderungen immer nur solange nachvollziehbar wie die Änderungshistorie aufgehoben werden soll. Wählt man z.B. in den Einstellungen "eine Woche" aus, werden alle Einträge in der Änderungshistorie gelöscht, die älter sind als eine Woche. Diese Bereinigung wird jeden Nacht um 0:00 Uhr durchgeführt. Wurde dagegen der Wert "für immer" ausgewählt, findet keine Bereinigung statt.

![This is an image](/images/changelog.png)

### 2.5 Prüfen des Syncs auf OTRS Seite

- In OTRS sieht man nach der Synchronisation von i-doit im Overview alle übertragenen Objekte. Nachfolgend kann man sehen wie dies für die übertragenen Computer in OTRS aussehen würde. Unter "Last Changed" kann man auch genau erkennen wann die Objekte zuletzt synchronisiert wurden.

![This is an image](/images/OTRS_Overview.png)

- In der Detailansicht kann man alle Werte zu einem Objekt sehen, die von i-doit übertragen wurden. Anhand der Versionsnummer kann man sehen wie oft die Werte geändert wurden. Außerdem ist erkennbar welcher Benutzer das Objekt angelegt hat. Hier steht der Benutzer, welcher in i-doit für die Verbindung mit dem Webservice benutzt wird.

![This is an image](/images/OTRS_Computer_View.png)

- In der History kann man genau nachvollziehen welche Änderungen wann und durch wenn durchgeführt wurden. Das bedeutet jede Änderung, die durch eine Synchronisation ausgelöst wurde, wird hier genau protokolliert.

![This is an image](/images/OTRS_History.png)

## 3 Anlagen

### 3.1 OTRS Computer Klassendefinition 

```otrs_computer.yaml```

### 3.1 OTRS Monitor Klassendefinition 

```otrs_monitor.yaml```

