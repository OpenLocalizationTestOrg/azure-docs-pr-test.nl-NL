---
title: aaaPush gegevens tooSearch index met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toopush gegevens tooAzure Search-Index met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Push-gegevens tooan Azure Search-index met behulp van Azure Data Factory
Dit artikel wordt beschreven hoe toouse hello Kopieeractiviteit toopush van een ondersteunde brongegevens gegevensarchief tooAzure Search-index. Ondersteunde bron gegevensarchieven worden vermeld in de bronkolom Hallo Hallo [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin Kopieeractiviteit en combinaties van ondersteunde gegevens store een algemeen overzicht van de verplaatsing van gegevens biedt.

## <a name="enabling-connectivity"></a>Connectiviteit inschakelen
tooallow Data Factory-service verbinding tooan on-premises gegevensopslag, u Data Management Gateway installeren in uw on-premises omgeving. U kunt de gateway installeren op Hallo dezelfde machine die als host fungeert voor de brongegevens Hallo opslaan of op een afzonderlijke computer tooavoid concurrentie voor resources met Hallo gegevens opslaan.

Data Management Gateway maakt verbinding lokale gegevensbronnen toocloud services op een manier veilig en beheerd. Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over Data Management Gateway.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een bron data store tooAzure Search-index worden met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens tooAzure Search-index zijn [JSON-voorbeeld: gegevens kopiëren van lokale SQL Server tooAzure Search-index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Search-Index zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service

Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello Azure Search gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| type | Hallo type eigenschap moet worden ingesteld op: **AzureSearch**. | Ja |
| URL | De URL voor hello Azure Search-service. | Ja |
| sleutel | Administratorsleutel voor hello Azure Search-service. | Ja |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset

Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset. Hallo **typeProperties** sectie verschilt voor elk type dataset. Hallo typeProperties sectie voor een gegevensset van het type Hallo **AzureSearchIndex** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| type | de eigenschap type Hello te moet worden ingesteld**AzureSearchIndex**.| Ja |
| NaamCommunity | Naam van hello Azure Search-index. Data Factory maakt geen Hallo index. Hallo-index moet bestaan in Azure Search. | Ja |


## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoertabellen en verschillende beleidsregels zijn beschikbaar voor alle typen activiteiten. Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties sectie variëren met elk activiteitstype. Voor de Kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Voor de Kopieeractiviteit wanneer Hallo sink Hallo type **AzureSearchIndexSink**, Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Hiermee geeft u op of toomerge of vervangen, wanneer een document al in Hallo index bestaat. Zie Hallo [WriteBehavior eigenschap](#writebehavior-property).| samenvoegen (standaard)<br/>Uploaden| Nee |
| writeBatchSize | Gegevens geüpload in hello Azure Search-index wanneer Hallo buffergrootte writeBatchSize bereikt. Zie Hallo [WriteBatchSize eigenschap](#writebatchsize-property) voor meer informatie. | 1 too1 000. Standaardwaarde is 1000. | Nee |

### <a name="writebehavior-property"></a>De eigenschap WriteBehavior
AzureSearchSink upserts bij het schrijven van gegevens. Met andere woorden, bij het schrijven van een document als Hallo documentsleutel al in de Azure Search-index hello bestaat Azure Search-updates Hallo bestaand document in plaats van er een conflict uitzondering is opgetreden.

Hallo AzureSearchSink biedt Hallo na twee upsert gedrag (via AzureSearch SDK):

- **Samenvoegen**: alle Hallo-kolommen in een nieuw document Hallo worden gecombineerd met een bestaande Hallo. Voor kolommen met null-waarde in een nieuw document Hallo blijft Hallo-waarde in een bestaande Hallo behouden.
- **Uploaden**: Hallo nieuw document vervangt bestaande Hallo. Voor de kolommen is niet opgegeven in een nieuw document hello, toonull op Hallo waarde is ingesteld of er een niet-null-waarde in een bestaand document Hallo of niet is.

Hallo standaardgedrag is **samenvoegen**.

### <a name="writebatchsize-property"></a>De eigenschap WriteBatchSize
Azure Search-service ondersteunt documenten schrijven als een batch. Een batch kan 1 too1, 000 acties bevatten. Een actie verwerkt één document tooperform Hallo uploaden/merge-bewerking.

### <a name="data-type-support"></a>Ondersteuning voor gegevenstype
Hallo volgende tabel geeft aan of een Azure Search-gegevenstype of niet wordt ondersteund.

| Azure Search-gegevenstype | Ondersteund in Azure Search Sink |
| ---------------------- | ------------------------------ |
| Tekenreeks | J |
| Int32 | J |
| Int64 | J |
| dubbele | J |
| Booleaanse waarde | J |
| DataTimeOffset | J |
| Tekenreeksmatrix | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>JSON-voorbeeld: gegevens kopiëren van lokale SQL Server tooAzure Search-index

Hallo volgende ziet:

1.  Een gekoppelde service van het type [AzureSearch](#linked-service-properties).
2.  Een gekoppelde service van het type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSearchIndex](#dataset-properties).
4.  Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) en [AzureSearchIndexSink](#copy-activity-properties).

Hallo voorbeeld kopieert per uur timeseries gegevens uit een lokale SQL Server-database tooan Azure Search-index. Hallo JSON-eigenschappen die in dit voorbeeld worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway op uw on-premises machine. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**Azure Search gekoppelde service:**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**SQL Server gekoppeld-service**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**SQL Server-invoergegevensset**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens. U kunt een query over meerdere tabellen in dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor een van deze dataset Hallo tableName typeProperty Hallo.

Instelling 'extern': 'true' informeert Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Azure Search uitvoergegevensset:**

Hallo voorbeeld kopieën gegevens tooan Azure Search-index met de naam **producten**. Data Factory maakt geen Hallo index. tootest hello steekproef, maakt u een index met deze naam. Hello Azure Search-index maken met Hallo hetzelfde aantal kolommen in Hallo invoergegevensset. Nieuwe vermeldingen worden toohello Azure Search-index toegevoegd om het uur.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**De kopieeractiviteit in een pijplijn met de SQL-bron en sink van Azure Search-Index:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**AzureSearchIndexSink**. Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist. Hallo volgende JSON-fragment toont Hallo-wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld. Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Kopiëren van een cloud-bron
Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist. Hallo volgende JSON-fragment toont Hallo-wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld. Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen. Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en afstemmen  
Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) en verschillende manieren toooptimize deze.

## <a name="next-steps"></a>Volgende stappen
Zie Hallo artikelen te volgen:

* [Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.
