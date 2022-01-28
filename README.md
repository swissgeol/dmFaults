# DMFaults
Data model fault

Anleitung zur Erstellung der db und dem QGIS Projekt: 

ili-Files werden direkt im Model Baker auf Syntax und Fehler kontrolliert, muss also nicht zwingen mit ili2c kontrolliert werden. Die Daten werden via Modelbaker als Models eingelesen. XML-Katalog Daten können ebenfalls im Wizard eingelesen werden. 

Vorgehen zum Erstellen des Katalogs: 
- QGIS Projekt eröffnen und Faults_V1.ili und FaultsCatalogues_V1.ili laden. 
	- Als Datenbank ein Geopackage auf Namen FaultsCatalogues_V1.gpkg eröffnen
	- Baskets zum Baseset werden automatisch erstellt. Falls dies nicht der Fall wäre, könnten immer noch via "Dataset Manager" weitere Baskets erstellt werden. Baskets helfen, die Daten geordnet zu halten. Es ist es ratsam, immer mit Baskets zu arbeiten. 
- Anschliessend Projekt als FaultsCatalogues.qgs File speichern 
- im Editor das QGIS-Projekt öffnen und per Suchfunktion readOnly="1" zu readOnly="0" ändern (zwingend für Items und Multilingual Text Tables) 
- zurück im QGIS-Projekt Attributwerte (in Basket FaultsCatalogues_V1.Catalogues) erfassen 
	- unter "Database" --> Model Baker --> Model Baker Data Validator immer wieder auf Contraint und Eingabefehler prüfen. 
	- .xml der Attributwerte exportieren und kontrollieren 

Vorgehen zum Erstellen des QGIS-Projektes zur Datenerfassung: 
- QGIS Projekt eröffnen und Faults_V1.ili und FaultsCatalogues_V1.ili laden. 
	- Als Datenbank ein Geopackage auf Namen Faults_V1.gpkg eröffnen
	- überprüfen: werden Baskets erstellt? 
	- als .qgs speichern 
- Wertekatalog hereinladen: 
	- .xml Katalog im Editor öffnen; BID von Katalog im Projekt Faults_V1.qgs (TID No3) kopieren und in xml abändern, damit selber Katalog-Basket bei Import gebraucht wird. 
	- speichern 
	- per Wizard .xml Datei hereinladen
	- gesamtes Projekt speichern 
- Interface anpassen: 
	- Fault Objects auf rote Farbe abändern 
	- Landeskarten (farbig) hinzufügen unter Layer --> Add Layer --> Add WMS/WMTS layer 
	- Constraints überprüfen : Mandatory Values aus .ili werden nicht so übertragen ins Form: müssen unter Layer setting (Doppelklick auf Layer) --> Attributformular --> Contraints zu "Nicht NULL" abgeändert werden. 
	- in FaultObjects (allen Geometrien) Werte jeweils als "NULL-Werte erlauben" (damit keine automatischen Antworten generiert werden)
- Testen: 
	- Faults und FaultObjects erfassen und mit Data Validator testen --> Erfassung der Objekte immer in Basket Faults 
- Export der Daten mit Import / Export Wizard, dritte Option. Baskets Catalogues und Basket Faults gleichzeitig anwählen. 
