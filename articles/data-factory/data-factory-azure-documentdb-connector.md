---
title: aaaMove gegevens van/naar Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe gegevens worden verplaatst naar/van Azure DB die Cosmos-verzameling met behulp van Azure Data Factory
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Verplaatsen van gegevens tooand van Azure Cosmos DB met Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit Azure Cosmos-DB (DocumentDB-API). Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft. 

U kunt gegevens kopiëren van een ondersteunde bron gegevens tooAzure Cosmos DB opslaan of opslaan van gegevens van Azure DB die Cosmos tooany ondersteund sink. Zie voor een lijst van gegevensarchieven als bronnen of PUT wordt ondersteund door kopieeractiviteit Hallo Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. 

> [!IMPORTANT]
> DocumentDB-API wordt alleen ondersteund door Azure DB Cosmos-connector.

gegevens als toocopy-is naar/van de JSON-bestanden of een andere verzameling van de Cosmos-DB, Zie [voor importeren/exporteren JSON-documenten](#importexport-json-documents).

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit Azure Cosmos DB verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar Cosmos DB zijn, [JSON voorbeelden](#json-examples) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooCosmos DB zijn: 

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure Cosmos DB gekoppelde service.

| **Eigenschap** | **Beschrijving** | **Vereist** |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **DocumentDb** |Ja |
| connectionString |Geef informatie nodig tooconnect tooAzure Cosmos-DB-database. |Ja |

Voorbeeld:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Raadpleeg voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van toohello [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset Hallo van het type **DocumentDbCollection** Hallo volgende eigenschappen heeft.

| **Eigenschap** | **Beschrijving** | **Vereist** |
| --- | --- | --- |
| CollectionName |Naam van Hallo documentverzameling Cosmos DB. |Ja |

Voorbeeld:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Schema door Data Factory
Voor gegevens zonder schema winkels zoals Azure Cosmos DB afleidt Hallo Data Factory-service Hallo schema in een van de volgende manieren Hallo:  

1. Als u Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service zich houdt aan deze structuur als Hallo schema. Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.
2. Als u niet Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service Hallo schema afleidt met behulp van de eerste rij Hallo in Hallo-gegevens. In dit geval als de eerste rij Hallo bevat geen volledige schema hello, sommige kolommen worden ontbreekt in Hallo resultaat van de kopieerbewerking.

Voor gegevensbronnen zonder schema, Hallo aanbevolen procedure is daarom toospecify Hallo structuur van gegevens met behulp van Hallo **structuur** eigenschap.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Raadpleeg voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten toohello [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

> [!NOTE]
> Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.

Eigenschappen beschikbaar zijn in Hallo typeProperties sectie Hallo-activiteit op Hallo anderzijds met elk activiteitstype en variëren in geval van een kopieeractiviteit afhankelijk van Hallo soorten gegevensbronnen en Put.

In geval van een kopieeractiviteit wanneer de bron van het type **DocumentDbCollectionSource** Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| **Eigenschap** | **Beschrijving** | **Toegestane waarden** | **Vereist** |
| --- | --- | --- | --- |
| query |Geef gegevens op Hallo query tooread. |Queryreeks wordt ondersteund door Azure Cosmos DB. <br/><br/>Voorbeeld:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Nee <br/><br/>Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Speciaal teken tooindicate dat document Hallo is genest |Willekeurig teken. <br/><br/>Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan. Azure Data Factory kunt toodenote gebruikershiërarchie via nestingSeparator die "." in hello bovenstaande voorbeelden. Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie. |Nee |

**DocumentDbCollectionSink** ondersteunt Hallo volgende eigenschappen:

| **Eigenschap** | **Beschrijving** | **Toegestane waarden** | **Vereist** |
| --- | --- | --- | --- |
| nestingSeparator |Er is een speciaal teken in Hallo bron kolom naam tooindicate dat document genest nodig. <br/><br/>Zoals hierboven: `Name.First` in Hallo-uitvoer produceert tabel Hallo JSON-structuur in Hallo Cosmos DB document te volgen:<br/><br/>"Name": {<br/>    ' First ': 'John'<br/>}, |Teken gebruikte tooseparate aantal geneste niveaus.<br/><br/>Standaardwaarde is `.` (punt). |Teken gebruikte tooseparate aantal geneste niveaus. <br/><br/>Standaardwaarde is `.` (punt). |
| writeBatchSize |Aantal parallelle aanvragen tooAzure Cosmos DB service toocreate documenten.<br/><br/>Bij het kopiëren van gegevens van Cosmos-database met behulp van deze eigenschap kunt u de prestaties van Hallo verfijnen. U kunt een betere prestaties verwachten wanneer u writeBatchSize verhogen omdat meer parallelle aanvragen tooCosmos DB worden verzonden. Maar u moet tooavoid beperking die kunnen genereert fout het Hallo-bericht: 'Vragen snelheid is groot'.<br/><br/>Beperking wordt bepaald door een aantal factoren, onder andere de grootte van documenten, aantal termen in documenten, indexeren beleid van de doelverzameling, enzovoort. Voor het kopiëren van, kunt u een betere verzameling (bijvoorbeeld S3) toohave Hallo meeste doorvoer beschikbaar (2500 aanvragen eenheden/seconde). |Geheel getal |Nee (standaard: 5) |
| writeBatchTimeout |Wachttijd voor Hallo bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |

## <a name="importexport-json-documents"></a>Import/Export JSON-documenten
Met deze Cosmos-DB-connector kunt u eenvoudig

* JSON-documenten importeren uit diverse bronnen in Cosmos-DB, met inbegrip van Azure Blob Azure Data Lake, on-premises bestandssysteem of andere winkels op basis van bestanden die door Azure Data Factory worden ondersteund.
* JSON-documenten uit Cosmos DB gewijzigd exporteren in verschillende winkels op basis van bestanden.
* Gegevens migreren tussen twee Cosmos DB verzamelingen op als-is.

tooachieve dergelijke schema-networkdirect kopiëren 
* Als u de wizard kopiëren, moet u Hallo **' exporteren als-tooJSON bestanden of Cosmos DB verzameling '** optie.
* Wanneer met behulp van JSON bewerkt, geen Hallo "structuur" sectie opgeven in Cosmos DB gegevensset (s) noch de eigenschap 'nestingSeparator' op Cosmos DB bron/sink in de kopieerbewerking. tooimport van / exportbestanden tooJSON, notatietype in Hallo bestand store gegevensset opgeven als 'JsonFormat', 'filePattern' config en overslaan Hallo rest indelingsinstellingen, Zie [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format) sectie voor meer informatie.

## <a name="json-examples"></a>JSON-voorbeelden
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand van Azure DB die Cosmos en Azure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Voorbeeld: Gegevens kopiëren van Azure DB die Cosmos tooAzure Blob
Hallo voorbeeld hieronder wordt:

1. Een gekoppelde service van het type [DocumentDb](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [DocumentDbCollectionSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert de gegevens in Azure Cosmos DB tooAzure Blob. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure Cosmos DB gekoppelde service:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob-opslag gekoppelde service:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Invoergegevensset van Azure Document database:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een verzameling met de naam **persoon** in een Azure DB die Cosmos-database.

Instelling 'extern': 'true' en externalData geven beleidsgegevens hello Azure Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Azure Blob-uitvoergegevensset:**

Gegevens zijn gekopieerde tooa nieuwe blob elk uur met Hallo pad voor Hallo blob opgetreden bij het Hallo specifieke datetime weergeven met een granulatie uur.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Voorbeeld JSON-document in Hallo persoon verzameling in een Cosmos-DB-database:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van een SQL zoals syntaxis via hiërarchische JSON-documenten.

Voorbeeld: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

Hallo volgende pijplijn kopieert gegevens van Hallo persoon verzameling in hello Azure Cosmos DB database tooan Azure-blob. Als onderdeel van Hallo kopie activiteit Hallo zijn invoer- en uitvoergegevenssets opgegeven.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure Cosmos-DB 
Hallo voorbeeld hieronder wordt:

1. Een gekoppelde service van het type [DocumentDb](#azure-documentdb-linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

Hallo voorbeeld kopieert gegevens van Azure blob-tooAzure Cosmos DB. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure Blob-opslag gekoppelde service:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure Cosmos DB gekoppelde service:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob invoergegevensset:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Azure Cosmos DB uitvoergegevensset:**

Hallo voorbeeld kopieert tooa verzamelen van gegevens met de naam 'Persoon'.

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Hallo volgende pijplijn kopieert gegevens van Azure Blob-toohello persoon verzameling in hello Cosmos DB. Als onderdeel van Hallo kopie activiteit Hallo zijn invoer- en uitvoergegevenssets opgegeven.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Als de Voorbeeldinvoer blob Hallo als

```
1,John,,Doe
```
Vervolgens zal Hallo uitvoer JSON in Cosmos-database zijn:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan. Azure Data Factory kunt toodenote gebruikershiërarchie via **nestingSeparator**, namelijk '. ' in dit voorbeeld. Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie.

## <a name="appendix"></a>Bijlage
1. **Vraag:** Kopieeractiviteit update voor de ondersteuning van bestaande records Hallo?

    **Antwoord:** Nee.
2. **Vraag:** records hoe een nieuwe poging van een kopie tooAzure Cosmos DB behandelen al is gekopieerd?

    **Antwoord:** als records een veld 'ID hebben' en Hallo kopieerbewerking een record met Hallo tooinsert probeert dezelfde ID, de kopieerbewerking Hallo een fout genereert.  
3. **Vraag:** biedt ondersteuning voor Data Factory [bereik of de gegevens op basis van het hash-partitionering](../documentdb/documentdb-partition-data.md)?

    **Antwoord:** Nee.
4. **Vraag:** kan ik meer dan één Azure Cosmos DB verzameling voor een tabel opgeven?

    **Antwoord:** Nee. Slechts één verzameling kan op dit moment worden opgegeven.

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
