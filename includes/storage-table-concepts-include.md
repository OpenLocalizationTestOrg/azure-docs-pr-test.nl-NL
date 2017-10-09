## <a name="what-is-table-storage"></a>Wat is Table Storage
Met Azure Table Storage kunnen grote hoeveelheden gestructureerde gegevens worden opgeslagen. Hallo-service is een NoSQL-gegevensarchief die accepteert geverifieerde aanroepen binnen en buiten hello Azure-cloud. Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens. Enkele voorbeelden van veelvoorkomende toepassingen van Tabel Storage:

* Opslaan van terabytes aan gestructureerde gegevens die kunnen worden geleverd aan webschaaltoepassingen
* Opslaan van gegevenssets die geen complexe joins, refererende sleutels of opgeslagen procedures vereisen en die kunnen worden gedenormaliseerd voor snelle toegang
* Snel een query voor gegevens uitvoeren met een geclusterde index
* Toegang tot gegevens via Hallo OData-protocol en LINQ-query's met WCF Data Service .NET-bibliotheken

U kunt Table storage toostore en query grote sets gestructureerde, niet-relationele gegevens en uw tabellen opgeschaald wanneer de vraag toeneemt.

## <a name="table-storage-concepts"></a>Concepten van Table Storage
Tabelopslag bevat Hallo volgende onderdelen:

![Diagram van onderdelen van Table Storage][Table1]

* **URL-indeling:** voor tabellen in een account wordt code met de volgende adresindeling gebruikt:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  U kunt Azure-tabellen rechtstreeks met dit adres met Hallo OData-protocol kunt oplossen. Zie [OData.org][OData.org] voor meer informatie.
* **Storage-Account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Zie [Azure Storage Scalability and Performance Targets](../articles/storage/common/storage-scalability-targets.md) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.
* **Tabel**: een tabel is een verzameling entiteiten. Met tabellen wordt geen schema voor entiteiten afgedwongen, wat betekent dat één tabel entiteiten kan bevatten die verschillende sets eigenschappen hebben. Hallo aantal tabellen dat een opslagaccount kan bevatten wordt alleen beperkt door Hallo de capaciteitslimiet van opslag.
* **Entiteit**: een entiteit is een set eigenschappen, vergelijkbare tooa databaserij. Een entiteit mag up too1MB in grootte.
* **Eigenschappen**: een eigenschap is een naamwaardepaar. Elke entiteit kan too252 eigenschappen toostore gegevens bevatten. Elke entiteit heeft ook drie systeemeigenschappen waarmee een partitiesleutel, een rijsleutel en een timestamp worden opgegeven. Entiteiten met Hallo dezelfde partitiesleutel kan sneller worden opgevraagd en in atomische bewerkingen ingevoegd of bijgewerkt. De rijsleutel van een entiteit is de unieke id in een partitie.

Zie voor meer informatie over de naamgeving van tabellen en eigenschappen [Understanding Hallo Table Service Data Model](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
