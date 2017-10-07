---
title: aaaMapping gegevensset kolommen in Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toomap kolommen toodestination kolommen bron.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Dataset kolommen toodestination gegevensset bronkolommen toewijzen
Kolomtoewijzing kan worden gebruikt toospecify hoe Hallo 'structuur' van de bron tabel kaart toocolumns kolommen in de structuur' Hallo' van tabel sink opgegeven. Hallo **columnMapping** eigenschap is beschikbaar in Hallo **typeProperties** sectie Hallo kopieeractiviteit.

Kolomtoewijzing ondersteunt Hallo volgen scenario's:

* Alle kolommen in de structuur van de gegevensset Hallo gegevensbron zijn toegewezen tooall kolommen in de gegevenssetstructuur Hallo-sink.
* Een subset kolommen in de bron-gegevenssetstructuur Hallo Hallo is toegewezen tooall kolommen in de gegevenssetstructuur Hallo-sink.

Hallo volgen foutcondities die ertoe leiden dat een uitzondering:

* Minder kolommen of meer kolommen Hallo 'structuur' van tabel sink dan opgegeven in het Hallo-toewijzing.
* Dubbele toewijzing.
* Resultaat van de SQL-query heeft niet de naam van een kolom die is opgegeven in het Hallo-toewijzing.

> [!NOTE]
> Hallo volgende voorbeelden zijn voor Azure SQL en Azure Blob maar zijn van toepassing tooany gegevensarchief die ondersteuning biedt voor rechthoekige gegevenssets. Dataset en definities van de gekoppelde service in de voorbeelden toopoint toodata in de desbetreffende gegevensbron Hallo aanpassen.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Voorbeeld 1: kolom toewijzing van een Azure SQL tooAzure blob
In dit voorbeeld heeft een structuur van de invoertabel Hallo en of deze tooa SQL-tabel in een Azure SQL database verwijst.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

In dit voorbeeld Hallo uitvoertabel een structuur is en of deze tooa blob in Azure blob storage verwijst.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
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
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Hallo volgende JSON definieert een kopieeractiviteit in een pijplijn. Hallo-kolommen van bron toegewezen toocolumns in sink (**columnMappings**) met behulp van Hallo **conversieprogramma** eigenschap.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Stroom van de toewijzing van kolom:**

![Kolom toewijzing stroom](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Voorbeeld 2: toewijzingskolommen met SQL-query uit een Azure SQL tooAzure blob
In dit voorbeeld is een SQL-query gebruikte tooextract gegevens van Azure SQL in plaats van het Hallo-tabelnaam en kolomnamen, Hallo te geven in de sectie 'structuur'. 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
In dit geval zijn de queryresultaten Hallo eerste toegewezen toocolumns opgegeven in 'structuur' van de bron. Kolommen van bron 'structuur' hello worden vervolgens toegewezen toocolumns in sink 'structuur' met regels die zijn opgegeven in de columnMappings.  Stel dat Hallo query retourneert 5 kolommen, twee of meer kolommen dan die zijn opgegeven in Hallo 'structuur' van de bron.

**Kolom toewijzing stroom**

![Kolom toewijzing stroom-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Volgende stappen
Zie Hallo artikel voor een zelfstudie over het gebruik van de Kopieeractiviteit: 

- [Gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
