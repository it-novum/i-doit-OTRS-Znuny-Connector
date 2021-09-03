# i-doit / OTRS / Znuny - Connector

##__1. Allgemeine Informationen__

- Der von it-novum entwickelte Connector ermöglicht Config Items von i-doit nach OTRS zu synchronisieren. Dabei besteht die Möglichkeit genau festzulegen welche Objekttypen, Kategorien und Attribute von i-doit nach OTRS übertragen werden und auf welche Objekttypen und Attribute sie dort abgebildet werden sollen.
- Darüber hinaus ist der Connector mandantenfähig. Es ist möglich mehrere unabhängige i-doit Instanzen an ein zentrales OTRS anzubinden. Hierfür müssen jeweils ein Webservice je i-doit Instanz eingerichtet werden und entsprechend im jeweiligen Connector konfiguriert werden. Pro Instanz können so auch unterschiedliche Benutzer konfiguriert werden.

##__2. Installation und Konfiguration__

###2.1 OTRS Installation & Konfiguration

- In OTRS müssen die frei verfügbaren ITSM Pakete installiert sein. Standardmäßig stehen dann bereits 5 Klassen bereit (Computer, Network….). Diese Klassen können je nach Anforderungen ergänzt oder modifiziert werden. Nur Klassen die per Copy & Paste in die Konfiguration des Connectors (siehe Import) eingefügt werden, werden entsprechend synchronisiert. Somit können in der CMDB von OTRS auch Klassen gepflegt werden, die nicht über i-doit verwaltet oder aktualisiert werden.
- In OTRS müssen zwei Dinge durchgeführt werden:

	- der Webservice muss mit den entsprechenden Methoden für CreateCI, UpdateCI und SearchCI angelegt werden
	- die Klassenstrukturen müssen aus OTRS nach i-doit kopiert und bei Änderungen im Connector oder OTRS immer manuell synchron gehalten werden.

- WICHTIG Namen und die Operationen müssen exakt so im Connector in i-doit unter den Einstellungen eingetragen sein.

###2.2 Webservices

####2.2.1 Importieren des Webservices

- Im Lieferumfang der Schnittstelle sollte eine Datei (IdoitSync.yml)beinhaltet sein. Diese kann über den Adminbereich -> Webservices importiert werden. Damit der Webservice ohne Probleme funktioniert, muss zuvor das ITSM Paket installiert sein.