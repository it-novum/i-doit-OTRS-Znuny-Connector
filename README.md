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

### 2.2.3 CMDB Klassen für den Sync

- In der Anlage haben wir zwei Beispiel für den Aufbau von OTRS CMDB Klassen.

### 2.3 User für die Synchronisation

- Für den sync von i-doit nach OTRS wird noch ein User auf der OTRS Seite benötigt. Dieser User braucht die kompletten Rechte für die Gruppe „itsm-configitem“ Der User sollte aus Sicherheitsgründen nicht der "root" Benutzer sein, ist aber grundsätzlich möglich. Des weiteren ist es sinnvoll, allen anderen Usern in OTRS auf die CMDB nur Lese-Rechte zu vergeben, da i-doit als führendes System genutzt wird und die Werte nicht in OTRS gepflegt werden sollen.

### 2.4 i-doit Installation & Konfiguration

- Der i-doit / OTRS Connector wird wie jedes andere Modul über das Admin Center installiert.
- Nach der Installation müssen noch die entsprechenden Rechte für das otrssync Modul gesetzt werden, damit man Zugriff auf den Connector im i-doit Frontend bekommt. Ist dies geschehen, steht der Connector unter dem Menüpunkt „Extras“ zur Verfügung
- Nach der Installation in i-doit steht der Connector unter dem Menüpunkt "Extras" zur Verfügung.

#### 2.4.1 Startseite 

- Die Startseite gibt einen Überblick über die getroffenen Einstellungen für die Synchronisation und die Verbindung zum Webservice von OTRS. Außerdem kann man sehen wann die letzte erfolgreiche Synchronisation mit OTRS stattgefunden hat und ob die Möglichkeit besteht Emails zu versenden. Bei der Email Konfiguration wird zum einen überprüft , ob ein Email Server in i-doit konfiguriert ist und zum Anderen ob im Connector Email Adressen für die Benachrichtigung eintragen wurden.
