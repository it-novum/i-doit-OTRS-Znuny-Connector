# i-doit / OTRS / Znuny - Connector

1. Allgemeine Informationen

Der von it-novum entwickelte Connector ermöglicht Config Items von i-doit nach OTRS zu synchronisieren. Dabei besteht die Möglichkeit genau festzulegen welche Objekttypen, Kategorien und Attribute von i-doit nach OTRS übertragen werden und auf welche Objekttypen und Attribute sie dort abgebildet werden sollen.

Nach der Installation in i-doit steht der Connector unter dem Menüpunkt "Extras" zur Verfügung. Webservice zip aus Download Bereich importieren

Bevor man mit dem Mapping beginnen kann, muss man allerdings die wichtigsten Einstellungen vornehmen und die Objektstrukturen aus OTRS importieren. Alle Änderungen werden in einer Änderungshistorie festgehalten und können gezielt ausgewertet werden. Außerdem bietet der Connector eine Startseite auf der eine Übersicht über den aktuellen Status der Einstellungen etc. angezeigt wird.

Darüber hinaus ist der Connector mandantenfähig.Es ist möglich mehrere unabhängige i-doit Instanzen an ein zentrales OTRS anzubinden. Hierfür müssen jeweils ein Webservice je i-doit Instanz eingerichtet werden und entsprechend im jeweiligen Connector konfiguriert werden. Pro Instanz können so auch unterschiedliche Benutzer konfiguriert werden.