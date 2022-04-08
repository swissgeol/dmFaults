# dmFaults
Datenmodell Störungen - Modèle de données failles - Modello di dati faglia - Data model faults 

### Beschreibung Modell Faults_V1.ili
   
Das Modell Störungen beschreibt geologische Verwerfungen und Brüche. Es setzt sich aus einem Modell ***Faults_V1.ili*** und einem Katalog mit den Attributlistenwerten ***FaultsCatalogues_V1.ili*** zusammen. Eine Graphik des uml-Schemas bildet die Verhältnisse bildlich ab ***Faults_V1.uml***.

Die benötigten Objektgeometrien `Line` und `Surface` werden in der Domain definiert, `Point` wird als Geometrie des Modells ***GeometryCHLV95_V1*** importiert. Das Topic Faults definiert jedes Objekt mit einer Objekt-ID, welche technisch als UUID erstellt wird. Das Modell ***Faults_V1*** besteht aus zwei beschreibenden Klassen `Fault` und `FaultObject`, sowie drei Geometrieklassen `Point`, `Line`, `Surface`. 

`Fault` setzt die einzelnen FaultObjects in eine hierarchische Beziehung. Es existieren in aufsteigender Reihenfolge Störung, Teilstörungssystem und Grossstörungssystem. Die Assoziation `FaultObject_Fault` beschreibt die Beziehung zwischen den Störungsobjekten und den Störungen, also der tiefsten Hierarchiestufe. Die Assoziation `ChildFault_ParentFault` erlaubt es, die verschiedenen Hierarchiestufen einer Störzone in Verbindung zu bringen.  

`FaultObject` beschreibt ein einzelnes Störungsobjekt. Eine Störung kann dadurch mehrere Störungsobjekte zugeordnet bekommen, welche sich durch ihre verschiedenen Erfassungsmethoden unterscheiden. Eine einzelne Störung kann so mehrere Messungen umfassen wie bspw. eine Kartierung und eine Bohrmessung gleichzeitig. Zum Objekt werden der Typ der Störung, die Bewegungsrichtungen, Grenzbeziehungen zu Decken- oder Schuppengrenzen, Erfassungsdetails, Extensionsparameter, Orientierungsparameter, lineare Strukturen, Versatzverhältnisse, Beziehungen zu erfassten Erdbeben, tektonische Reaktivierungsprozesse und die Personalien der Bearbeitenden erfasst.  

### Anleitung zur Erstellung der Datenbank und QGIS Projekt:

Hinweis zum Validitäts-Check: ili-Files werden direkt im Model Baker auf Syntax und Fehler kontrolliert, muss also nicht zwingend mit *ili2c* kontrolliert werden. Die Daten werden via Modelbaker als Models eingelesen. XML-Katalogdaten können ebenfalls im Wizard eingelesen werden. 

#### Vorgehen zum Erstellen des Katalogs: 
- QGIS Projekt eröffnen und *Faults_V1.ili* und *FaultsCatalogues_V1.ili* laden. 
	- Als Datenbank ein Geopackage auf Namen *FaultsCatalogues_V1.gpkg* eröffnen
	- Baskets zum Baseset werden automatisch erstellt. Falls dies nicht der Fall wäre, könnten via "Dataset Manager" weitere Baskets erstellt werden. Baskets helfen, die Daten geordnet zu halten. Es ist ratsam, immer mit Baskets zu arbeiten. 
- Anschliessend Projekt als *FaultsCatalogues.qgs* File speichern 
- im Editor das QGIS-Projekt öffnen und per Suchfunktion readOnly="1" zu readOnly="0" ändern (zwingend für Items und Multilingual Text Tables) 
- zurück im QGIS-Projekt Attributwerte (in Basket *FaultsCatalogues_V1.Catalogues*) erfassen 
	- unter "Database" --> Model Baker --> Model Baker Data Validator immer wieder auf Constraints und Eingabefehler prüfen. 
	- .xml der Attributwerte exportieren und kontrollieren 

#### Vorgehen zum Erstellen des QGIS-Projektes zur Datenerfassung: 
- QGIS Projekt eröffnen und *Faults_V1.ili* und *FaultsCatalogues_V1.ili* laden. 
	- Als Datenbank ein Geopackage auf Namen *Faults_V1.gpkg* eröffnen
	- überprüfen: werden Baskets automatisch erstellt? 
	- als .qgs speichern 
- Wertekatalog hereinladen: 
	- .xml Katalog im Editor öffnen; BID von Katalog im Projekt *Faults_V1.qgs* (TID No3) kopieren und in xml abändern, damit derselbe Katalog-Basket bei Import gebraucht wird. 
	- speichern 
	- per Wizard .xml Datei hereinladen
	- gesamtes Projekt speichern 
- Interface anpassen: 
	- Fault Objects auf rote Farbe abändern 
	- Landeskarten (farbig) hinzufügen unter Layer --> Add Layer --> Add WMS/WMTS layer 
	- Constraints überprüfen : Mandatory Values aus .ili werden nicht so übertragen ins Form: müssen unter Layer setting (Doppelklick auf Layer) --> Attributformular --> Constraints zu "Nicht NULL" abgeändert werden. 
	- in FaultObjects (allen Geometrien) Werte jeweils als "NULL-Werte erlauben" (damit keine automatischen Antworten generiert werden)
- Testen: 
	- Faults und FaultObjects erfassen und mit Data Validator testen --> Erfassung der Objekte immer in Basket Faults 
- Export der Daten mit Import / Export Wizard, dritte Option. Basket Catalogues und Basket Faults gleichzeitig anwählen. Die Katalogdaten können aus der Datei gelöscht werden. 

  
  
---


   
### Description Model Faults_V1.ili

The model Faults describes geological faults and fractures. It consists of a model ***Faults_V1.ili*** and a catalogue with the attribute list values ***FaultsCatalogues_V1.ili***. A graphic of the uml scheme illustrates the relationships ***Faults_V1.uml***.

The required object geometries `Line` and `Surface` are defined in the domain, `Point` is imported as geometry of the model ***GeometryCHLV95_V1***. The topic Faults defines each object with an object ID, which is technically created as a UUID. The model ***Faults_V1*** consists of two descriptive classes `Fault` and `FaultObject`, as well as three geometry classes `Point`, `Line`, `Surface`. 

`Fault` places the individual FaultObjects in a hierarchical relationship. Fault, subfault system and major fault system exist in ascending order. The association `FaultObject_Fault` describes the relationship between the fault objects and the faults, i.e. the lowest hierarchical level. The association `ChildFault_ParentFault` allows to relate the different hierarchy levels of a fault zone.  

`FaultObject` describes a single fault object. A fault can thus have several fault objects assigned to it, which are distinguished by their different acquisition methods. A single fault can comprise several measurements, such as a mapping and a borehole measurement at the same time. For the object, the type of fault, the directions of movement, limit relations to slab or scale boundaries, acquisition details, extension parameters, orientation parameters, linear structures, offset relations, relations to recorded earthquakes, tectonic reactivation processes and the data of the person working on the fault can be recorded. 

		
### Instructions for the creation of the database and QGIS project:

Note on the validity check: .ili files are checked for syntax and errors directly in Model Baker, so it is not mandatory to check them with ili2c. The data are read in via Modelbaker as models. XML catalogue data can also be read in the wizard. 

#### Procedure for creating the catalogue: 
- Open QGIS project and load *Faults_V1.ili* and *FaultsCatalogues_V1.ili*. 
	- Open a geopackage named *FaultsCatalogues_V1.gpkg* as database.
	- Baskets for the baseset are created automatically. If this will not be the case, further baskets could be created via "Dataset Manager". Baskets help to keep the data organised. It is advisable to always work with baskets. 
- Then save the project as FaultsCatalogues.qgs file. 
- Open the QGIS project in the editor and change readOnly="1" to readOnly="0" using the search function (mandatory for items and multilingual text tables). 
- Back in the reopened QGIS project, enter attribute values (in basket FaultsCatalogues_V1.Catalogues). 
	- under "Database" --> Model Baker --> Model Baker Data Validator check again and again for constraint and input errors. 
	- Export and check the .xml of the attribute values. 

Procedure for creating the QGIS project for data acquisition: 
- Open QGIS project and load Faults_V1.ili and FaultsCatalogues_V1.ili. 
	- Open a geopackage named Faults_V1.gpkg as database.
	- check: are baskets created automatically? 
	- save as .qgs 
- Load value catalogue: 
	- Open .xml catalogue in editor; copy BID from catalogue in Faults_V1.qgs project (TID No3) and change to xml so that the same catalogue basket is used on import. 
	
#### Procedure for creating the QGIS project for data acquisition: 
- Open QGIS project and load *Faults_V1.ili* and *FaultsCatalogues_V1.ili*. 
	- Open a geopackage named *Faults_V1.gpkg* as database.
	- check: are baskets created automatically? 
	- save as .qgs 
- Load value catalogue: 
	- Open .xml catalogue in editor; copy BID from catalogue in *Faults_V1.qgs* project (TID No3) and change to xml so that the same catalogue basket is used on import. 
	- Save 
	- Load .xml file via wizard
	- Save the whole project 
- Adapt interface: 
	- Change fault objects to red colour 
	- Add Landeskarten (farbig) under Layer --> Add Layer --> Add WMS/WMTS layer 
	- Check constraints : Mandatory values from .ili are not transferred to the form: must be changed to "Not NULL" under Layer setting (double click on layer) --> Attribute form --> Constraints. 
	- in FaultObjects (all geometries) values each as "Allow NULL values" (so that no automatic responses are generated)
- Test: 
	- Capture Faults and FaultObjects and test with Data Validator --> Capture objects always in Basket Faults. 
- Export the data with Import / Export Wizard, third option. Select Basket Catalogues and Basket Faults at the same time. The catalogue data can be deleted from the file. 
