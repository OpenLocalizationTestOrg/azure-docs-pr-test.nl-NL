## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Structuurdefinitie voor de rechthoekige gegevenssets opgeven
Hallo structuur sectie in Hallo gegevenssets JSON is een **optionele** sectie voor rechthoekige tabellen (met rijen en kolommen) en bevat een verzameling van kolommen voor Hallo tabel. Hallo structuur sectie gebruikt u voor beide met type-informatie voor typeconversies of kolomtoewijzingen doen. Hallo volgende secties worden deze functies in detail beschreven. 

Elke kolom bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van het Hallo-kolom. |Ja |
| type |Het gegevenstype van kolom Hallo. Zie type conversies hieronder voor meer details met betrekking tot wanneer moet u informatie opgeven |Nee |
| Cultuur |.NET gebaseerde cultuur toobe gebruikt bij het type is opgegeven en .NET-type Datetime of Datetimeoffset. Standaardwaarde is "en-us '. |Nee |
| Indeling |Indeling van tekenreeks toobe gebruikt bij het type is opgegeven en .NET-type Datetime of Datetimeoffset. |Nee |

Hallo toont volgende voorbeeld Hallo structuur sectie JSON voor een tabel met drie kolommen userid, naam en lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Gebruik Hallo volgen richtlijnen voor wanneer tooinclude "structuur" informatie en welke tooinclude in Hallo **structuur** sectie.

* **Voor gestructureerde gegevensbronnen** die schema en het type informatie samen met de Hallo gegevens zelf (bronnen, zoals Azure-tabel van SQL Server, Oracle, enzovoort), moet u Hallo 'structuur,' sectie alleen als u de kolomtoewijzing komen van specifieke wilt opslaan bronkolommen toospecific kolommen in sink en hun namen zijn Hallo niet dezelfde (Zie de details in de kolom toewijzing hieronder). 
  
    Zoals eerder vermeld, is in de sectie 'structuur' Hallo-informatie optioneel. Voor gestructureerde bronnen al type-informatie beschikbaar is als onderdeel van de definitie van de gegevensset in het gegevensarchief hello, dus u mag geen bevatten informatie over wanneer u Hallo "structuur" sectie opneemt.
* **Voor schema op lezen gegevensbronnen (specifiek Azure-blobopslag)** kunt u toostore gegevens zonder schema of het type informatie met Hallo gegevens opslaan. Voor deze soorten gegevensbronnen moet u 'structuur' opnemen in Hallo 2 gevallen te volgen:
  * Wilt u de kolomtoewijzing toodo.
  * Wanneer Hallo gegevensset een bron in een kopieeractiviteit is, kunt u informatie in 'structuur' en gegevensfactory deze type-informatie wordt gebruikt voor conversie toonative typen voor Hallo sink. Zie [tooand gegevens verplaatsen van een Azure-Blob](../articles/data-factory/data-factory-azure-blob-connector.md) artikel voor meer informatie.

### <a name="supported-net-based-types"></a>Ondersteund. Op basis van NET typen
Typewaarden voor type-informatie in 'structuur' opgeeft voor het schema op lezen gegevensbronnen als Azure-blob op basis van Data factory ondersteunt Hallo CLS compatibele .NET te volgen.

* Int16
* Int32 
* Int64
* Één
* dubbele
* Decimale
* Byte]
* BOOL
* Tekenreeks 
* GUID
* Datum/tijd
* DateTimeOffset
* Periode 

Voor Datetime & Datetimeoffset kunt u eventueel ook 'Cultuur' & 'indeling' string toofacilitate parseren van de aangepaste datum/tijd-tekenreeks opgeven. Zie voorbeeld voor typeconversie hieronder.

