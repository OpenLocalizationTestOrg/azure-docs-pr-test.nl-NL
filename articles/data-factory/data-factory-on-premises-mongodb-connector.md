---
title: aaaMove gegevens van MongoDB gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe de gegevens toomove van MongoDB-database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Verplaatsen van gegevens van MongoDB met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises MongoDB-database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit een on-premises MongoDB gegevens store tooany ondersteund sink gegevensopslag kopiëren. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een data MongoDB tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooan MongoDB-gegevensarchief. 

## <a name="prerequisites"></a>Vereisten
Voor hello Azure Data Factory-service toobe kunnen tooconnect tooyour lokale MongoDB-database, moet u de volgende onderdelen Hallo installeren:

- Ondersteunde MongoDB-versies zijn: 2.4, 2.6, 3.0 en 3.2.
- Data Management Gateway op dezelfde machine Hallo die hosts Hallo-database of op een afzonderlijke computer tooavoid concurrentie voor resources met Hallo-database. Data Management Gateway is een software die is verbonden lokale gegevensbronnen toocloud services op een manier veilig en beheerd. Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway. Zie [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een data pipeline toomove gegevens.

    Wanneer u Hallo-gateway installeert, installeert deze automatisch een tooMongoDB tooconnect van Microsoft MongoDB ODBC-stuurprogramma die wordt gebruikt.

    > [!NOTE]
    > U moet toouse Hallo gateway tooconnect tooMongoDB, zelfs als deze wordt gehost in Azure IaaS VM's. Als u tooconnect tooan exemplaar van MongoDB gehost in de cloud probeert, kunt u ook Hallo gatewayexemplaar installeren in Hallo IaaS VM.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises MongoDB-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises MongoDB-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikte toodefine Data Factory-entiteiten specifieke tooMongoDB bron:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel bevat de beschrijving voor JSON-elementen die specifiek te**OnPremisesMongoDB** gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesMongoDb** |Ja |
| server |IP-adres of de hostnaam de naam van Hallo MongoDB-server. |Ja |
| poort |Toolisten TCP-poort die Hallo MongoDB-server gebruikt voor clientverbindingen. |Optionele standaardwaarde: 27017 |
| authenticationType |Basic of anonieme. |Ja |
| gebruikersnaam |Gebruiker account tooaccess MongoDB. |Ja (als u basisverificatie wordt gebruikt). |
| wachtwoord |Wachtwoord voor gebruiker Hallo. |Ja (als u basisverificatie wordt gebruikt). |
| authSource |Naam van Hallo MongoDB-database dat u wilt dat toouse toocheck uw referenties voor verificatie. |Optioneel (als basisverificatie wordt gebruikt). Standaard: maakt gebruik van Hallo-beheerdersaccount en Hallo database die is opgegeven met de eigenschap databaseName. |
| DatabaseName |Naam van Hallo MongoDB-database die u tooaccess wilt. |Ja |
| gatewayName |Naam van het Hallo-gateway die toegang heeft tot Hallo-gegevensarchief. |Ja |
| encryptedCredential |Referentie versleuteld door de gateway. |Optioneel |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **MongoDbCollection** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| CollectionName |Naam van de verzameling Hallo in MongoDB-database. |Ja |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Wanneer Hallo-bron is van het type **MongoDbSource** Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-92 queryreeks. Bijvoorbeeld: Selecteer * from MijnTabel. |Nee (als **collectionName** van **gegevensset** is opgegeven) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van MongoDB tooAzure Blob
In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Er wordt weergegeven hoe toocopy gegevens uit een lokale MongoDB tooan Azure Blob Storage. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesMongoDb](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [MongoDbCollection](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [MongoDbSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert gegevens van de resultaten van een query in de MongoDB-database tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway volgens de instructies in Hallo Hallo [Data Management Gateway](data-factory-data-management-gateway.md) artikel.

**MongoDB gekoppelde service:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

**Gekoppelde Azure Storage-service:**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**MongoDB-invoergegevensset:** instellen 'extern': 'true' informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**De kopieeractiviteit in een pijplijn met MongoDB-bron en sink van Blob:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo hierboven invoer- en uitvoergegevenssets en geplande toorun elk uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**MongoDbSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Schema door Data Factory
Azure Data Factory-service afleidt schema uit een verzameling MongoDB met behulp van Hallo nieuwste 100 documenten in Hallo-verzameling. Als deze 100 documenten niet volledig schema bevatten, kunnen sommige kolommen tijdens de kopieerbewerking Hallo worden genegeerd.

## <a name="type-mapping-for-mongodb"></a>Toewijzing van het type voor MongoDB
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens tooMongoDB Hallo na worden toewijzingen van MongoDB typen too.NET typen gebruikt.

| MongoDB-type | .NET framework-type |
| --- | --- |
| Binaire |Byte] |
| Booleaanse waarde |Booleaanse waarde |
| Date |Datum/tijd |
| NumberDouble |dubbele |
| NumberInt |Int32 |
| NumberLong |Int64 |
| Object-id |Tekenreeks |
| Tekenreeks |Tekenreeks |
| UUID |GUID |
| Object |Renormalized plat in kolommen met '_' als geneste scheidingsteken |

> [!NOTE]
> toolearn over ondersteuning voor arrays met virtuele tabellen te verwijzen[ondersteuning voor complexe typen virtuele tabellen met](#support-for-complex-types-using-virtual-tables) hieronder.

Op dit moment Hallo na MongoDB-gegevenstypen worden niet ondersteund: DBPointer, JavaScript, Max per minuut sleutel, reguliere expressie, symbool, Timestamp, Undefined

## <a name="support-for-complex-types-using-virtual-tables"></a>Ondersteuning voor complexe typen met behulp van de virtuele tabellen
Azure Data Factory maakt gebruik van een ingebouwde ODBC-stuurprogramma tooconnect tooand gegevens kopiëren van de MongoDB-database. Voor complexe gegevenstypen zoals matrices of objecten met verschillende typen op Hallo documenten normaliseert Hallo stuurprogramma gegevens opnieuw in de bijbehorende virtuele tabellen. In het bijzonder als een tabel bevat een dergelijke kolommen, genereert Hallo stuurprogramma Hallo virtuele tabellen te volgen:

* Een **basistabel**, die bevat dezelfde gegevens als de echte tabel, met uitzondering van kolommen van het complexe type Hallo HALLO hallo. de basistabel Hallo gebruikt Hallo dezelfde naam als Hallo echte tabel die wordt vertegenwoordigd.
* Een **virtuele tabel** voor elke kolom complex type zijn dat wordt uitgebreid Hallo geneste gegevens. Hallo virtuele tabellen zijn benoemde met Hallo-naam van de echte tabel hello, een scheidingsteken '_' en het Hallo-naam van het Hallo-matrix of object.

Virtuele tabellen verwijzen toohello-gegevens in de echte tabel hello, waardoor Hallo stuurprogramma tooaccess Hallo gedenormaliseerd gegevens. Zie de sectie Voorbeeld onder meer informatie. Hallo-inhoud van het MongoDB-matrices kunt u door het uitvoeren van query's en het toevoegen aan virtuele tabellen Hallo openen.

U kunt Hallo [Wizard kopiëren](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively weergeven lijst met tabellen in de MongoDB-database met inbegrip van de virtuele tabellen Hallo Hallo en een voorbeeld van gegevens binnen Hallo. U kunt ook maakt u een query in de Wizard kopiëren Hallo en toosee Hallo resultaat valideren.

### <a name="example"></a>Voorbeeld
'ExampleTable' hieronder is bijvoorbeeld een MongoDB-tabel met één kolom met een matrix van objecten in elke cel – facturen en één kolom met een matrix van scalaire typen – classificaties.

| _id | Naam van de klant | Facturen | Serviceniveau | De classificaties |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id: '123' item: 'toaster', de prijs: '456' korting: "0,2"}, {invoice_id: '124' item: 'ingesteld', prijs: '1235' korting: "0,2"}] |Zilver |[5,6] |
| 2222 |XYZ |[{invoice_id: item '135': 'koelkast', prijs: '12543' korting: "0,0"}] |Goud |[1,2] |

Hallo stuurprogramma genereert meerdere virtuele tabellen toorepresent deze één tabel. de eerste virtuele tabel Hallo is Hallo basistabel met de naam 'ExampleTable', hieronder weergegeven. Hallo basistabel bevat alle Hallo gegevens van de oorspronkelijke tabel hello, maar Hallo gegevens van Hallo matrices is weggelaten en in virtuele tabellen Hallo is uitgevouwen.

| _id | Naam van de klant | Serviceniveau |
| --- | --- | --- |
| 1111 |ABC |Zilver |
| 2222 |XYZ |Goud |

Hallo volgende tabellen bevatten Hallo virtuele tabellen die oorspronkelijke matrices in voorbeeld Hallo Hallo vertegenwoordigen. Deze tabellen bevatten de volgende Hallo:

* Verwijzing naar een back-toohello originele primaire-sleutelkolom bijbehorende toohello rij van de oorspronkelijke matrix hello (via Hallo _id kolom)
* Een indicatie van de positie van gegevens binnen de oorspronkelijke matrix Hallo HALLO hallo
* Hallo-gegevens voor elk element in een matrix van Hallo uitgevouwen

Tabel 'ExampleTable_Invoices':

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | Korting |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |toaster |456 |0.2 |
| 1111 |1 |124 |ingesteld |1235 |0.2 |
| 2222 |0 |135 |koelkast |12543 |0.0 |

Tabel 'ExampleTable_Ratings':

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.

## <a name="next-steps"></a>Volgende stappen
Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies voor het maken van een pijplijn gegevens die worden verplaatst gegevens uit een on-premises gegevens tooan Azure data store opslaan.
