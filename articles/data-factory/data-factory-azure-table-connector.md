---
title: aaaMove gegevens van/naar Azure Table | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van/naar Azure Table Storage met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Verplaatsen van gegevens tooand van Azure-tabel met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit Azure Table Storage. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft. 

U kunt gegevens kopiëren van een ondersteunde bron gegevens opslaan tooAzure Table Storage of Azure Table Storage tooany ondersteund sink gegevens opslaan. Zie voor een lijst van gegevensarchieven als bronnen of PUT wordt ondersteund door kopieeractiviteit Hallo Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. 

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure-tabelopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure-tabelopslag zijn [JSON voorbeelden](#json-examples) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Table Storage zijn: 

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Er zijn twee typen van de gekoppelde services kunt u een Azure blob storage tooan Azure data factory toolink. Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service. Hallo gekoppelde Azure Storage-service biedt Hallo data factory met globale toegang toohello Azure Storage. Terwijl hello Azure Storage SAS (Shared Access Signature) gekoppelde biedt service Hallo gegevensfactory met de toegang beperkt/tijdsgebonden toohello Azure Storage. Er zijn geen andere verschillen tussen deze twee gekoppelde services. Kies Hallo gekoppelde service die bij uw behoeften past. Hallo vindt volgende secties u meer informatie over deze twee gekoppelde services.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureTable** Hallo volgende eigenschappen heeft.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in hello Azure Table-Database-instantie waarnaar de gekoppelde service verwijst. |Ja. Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming. Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming. |

### <a name="schema-by-data-factory"></a>Schema door Data Factory
Voor gegevens zonder schema winkels zoals Azure Table afleidt Hallo Data Factory-service Hallo schema in een van de volgende manieren Hallo:

1. Als u Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service zich houdt aan deze structuur als Hallo schema. Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.
2. Als u geen Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Data Factory Hallo schema afleidt met behulp van de eerste rij Hallo in Hallo-gegevens. Als de eerste rij Hallo bevat geen volledige schema hello, worden sommige kolommen in dit geval gemist in Hallo resultaat van de kopieerbewerking.

Voor gegevensbronnen zonder schema, Hallo aanbevolen procedure is daarom toospecify Hallo structuur van gegevens met behulp van Hallo **structuur** eigenschap.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.

Eigenschappen beschikbaar zijn in Hallo typeProperties sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

**AzureTableSource** ondersteunt de volgende eigenschappen in de sectie typeProperties Hallo:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| azureTableSourceQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |Azure-tabel queryreeks. Zie de voorbeelden in de volgende sectie Hallo. |Nee. Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming. Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming. |
| azureTableSourceIgnoreTableNotFound |Geef aan of slikken Hallo uitzondering van de tabel niet bestaat. |DE WAARDE TRUE<br/>DE WAARDE FALSE |Nee |

### <a name="azuretablesourcequery-examples"></a>Voorbeelden van azureTableSourceQuery
Als Azure Table-kolom van het tekenreekstype:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Als Azure Table-kolom van het type datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** ondersteunt de volgende eigenschappen in de sectie typeProperties Hallo:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Standaardwaarde voor de partitiesleutel die kan worden gebruikt door Hallo sink. |Een string-waarde. |Nee |
| azureTablePartitionKeyName |Naam van het Hallo-kolom waarvan de waarden worden gebruikt als partitiesleutels opgeven. Als niet wordt opgegeven, wordt AzureTableDefaultPartitionKeyValue gebruikt als partitiesleutel Hallo. |De naam van een kolom. |Nee |
| azureTableRowKeyName |Naam van het Hallo-kolom waarvan de kolomwaarden worden gebruikt als de rijsleutel opgeven. Als niet wordt opgegeven, gebruikt u een GUID voor elke rij. |De naam van een kolom. |Nee |
| azureTableInsertType |Hallo modus tooinsert gegevens in Azure-tabel.<br/><br/>Deze eigenschap bepaalt of bestaande rijen in de uitvoertabel Hallo met partitie-als rijsleutels die overeenkomt met de waarden vervangen of samenvoegen van hebben. <br/><br/>toolearn over hoe deze instellingen (merge en vervangen) werken, Zie [invoegen of Merge entiteit](https://msdn.microsoft.com/library/azure/hh452241.aspx) en [invoegen of vervangen entiteit](https://msdn.microsoft.com/library/azure/hh452242.aspx) onderwerpen. <br/><br> Deze instelling is van toepassing op Hallo rijniveau niet Hallo-tabelniveau, en geen van beide optie worden de rijen in de uitvoertabel Hallo die niet bestaan in de invoer Hallo verwijderd. |samenvoegen (standaard)<br/>vervangen |Nee |
| writeBatchSize |Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| writeBatchTimeout |Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt. |TimeSpan<br/><br/>Voorbeeld: "00: 20:00 ' (20 minuten) |Nee (standaard toostorage client standaardtime-out waarde 90 sec) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Een kolom tooa bestemming bronkolom met Hallo conversieprogramma JSON eigenschap voordat u de doelkolom Hallo kunt zoals Hallo azureTablePartitionKeyName worden toegewezen.

In de Hallo voorbeeld te volgen, bronkolom DivisionID is toegewezen toohello doelkolom: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Hallo DivisionID is opgegeven als partitiesleutel Hallo.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>JSON-voorbeelden
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand van Azure Table Storage en Azure Blob-Database. Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen tooany van Hallo ondersteund Put. Zie voor meer informatie Hallo sectie 'ondersteunde gegevensarchieven en indelingen' in [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Voorbeeld: Gegevens kopiëren van Azure Table tooAzure Blob
Hallo volgende ziet:

1. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel).
2. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).
3. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [AzureTableSource](#activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert de gegevens die behoren toohello standaardpartitie in een blob van Azure Table tooa elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Gekoppelde Azure storage-service:**

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
Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**. Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven. Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.  

**Azure Table invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in Azure-tabel.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**De kopieeractiviteit in een pijplijn met AzureTableSource en BlobSink:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**AzureTableSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven met **AzureTableSourceQuery** eigenschap selecteert Hallo gegevens uit Hallo standaardpartitie elke toocopy uur.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure tabel
Hallo volgende ziet:

1. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel)
2. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).
4. Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureTableSink](#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens van een Azure blob-tooan Azure-tabel per uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Gekoppelde Azure storage (voor Azure Table & Blob)-service:**

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

Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**. Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven. Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.

**Azure Blob invoergegevensset:**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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

**Azure-tabel uitvoergegevensset:**

Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in de Azure-tabel. Maken van een Azure-tabel met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**De kopieeractiviteit in een pijplijn met BlobSource en AzureTableSink:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a>Toewijzing van het type voor Azure-tabel
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen.

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens te & van Azure Table Hallo na [toewijzingen die zijn gedefinieerd door de service Azure Table](https://msdn.microsoft.com/library/azure/dd179338.aspx) worden gebruikt vanuit Azure tabel OData typen too.NET type en vice versa.

| OData-gegevenstype | .NET-type | Details |
| --- | --- | --- |
| Edm.Binary |Byte] |Een matrix met bytes up too64 KB. |
| Edm.Boolean |BOOL |Een Booleaanse waarde. |
| Edm.DateTime |Datum/tijd |Een 64-bits waarde wordt uitgedrukt als Coordinated Universal Time (UTC). Hallo ondersteund DateTime bereik van 12:00 middernacht, 1 januari 1601 A.D. begint (C.E.) UTC. Hallo bereik eindigt op 31 December 9999. |
| Edm.Double |dubbele |Een 64-bits drijvende-kommawaarde. |
| Edm.Guid |GUID |Een globally unique identifier van 128-bits. |
| Edm.Int32 |Int32 |Een 32-bits geheel getal. |
| Edm.Int64 |Int64 |Een 64-bits geheel getal. |
| Edm.String |Tekenreeks |Een waarde UTF-16-codering. Tekenreekswaarden mogelijk up too64 KB. |

### <a name="type-conversion-sample"></a>Type conversie voorbeeld
Hallo volgende voorbeeld is voor het kopiëren van gegevens uit een Azure Blob-tooAzure tabel met typeconversies.

Stel Hallo Blob-gegevenssets is CSV-indeling en drie kolommen bevat. Een van deze is een datetime-kolom met een aangepaste datum / tijdindeling met behulp van Franse afkortingen voor dag van week Hallo.

Bron van de Blob-gegevensset Hallo als volgt samen met de definities voor Hallo kolommen definiëren.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Toewijzing van het type Hallo van Azure Table OData type too.NET type gezien, zou u Hallo tabel definiëren in Azure Table Hello schema te volgen.

**Azure tabelschema:**

| Kolomnaam | Type |
| --- | --- |
| gebruikers-id |Edm.Int64 |
| naam |Edm.String |
| lastlogindate |Edm.DateTime |

Definieer vervolgens als volgt hello Azure Table-gegevensset. U hoeft niet toospecify "structuur" sectie met informatie over Hallo omdat Hallo-informatie is al opgegeven in Hallo onderliggende gegevensarchief.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

In dit geval Data Factory automatisch gegevenstypeconversies inclusief Hallo Datetime-veld met de Hallo aangepaste datum/tijd-indeling met behulp van 'fr-fr' hello cultuur, bij het verplaatsen van gegevens uit Blob tooAzure tabel.

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize, Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md).
