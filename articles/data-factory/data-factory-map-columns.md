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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="44278-103">Dataset kolommen toodestination gegevensset bronkolommen toewijzen</span><span class="sxs-lookup"><span data-stu-id="44278-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="44278-104">Kolomtoewijzing kan worden gebruikt toospecify hoe Hallo 'structuur' van de bron tabel kaart toocolumns kolommen in de structuur' Hallo' van tabel sink opgegeven.</span><span class="sxs-lookup"><span data-stu-id="44278-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="44278-105">Hallo **columnMapping** eigenschap is beschikbaar in Hallo **typeProperties** sectie Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="44278-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="44278-106">Kolomtoewijzing ondersteunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="44278-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="44278-107">Alle kolommen in de structuur van de gegevensset Hallo gegevensbron zijn toegewezen tooall kolommen in de gegevenssetstructuur Hallo-sink.</span><span class="sxs-lookup"><span data-stu-id="44278-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="44278-108">Een subset kolommen in de bron-gegevenssetstructuur Hallo Hallo is toegewezen tooall kolommen in de gegevenssetstructuur Hallo-sink.</span><span class="sxs-lookup"><span data-stu-id="44278-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="44278-109">Hallo volgen foutcondities die ertoe leiden dat een uitzondering:</span><span class="sxs-lookup"><span data-stu-id="44278-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="44278-110">Minder kolommen of meer kolommen Hallo 'structuur' van tabel sink dan opgegeven in het Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="44278-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="44278-111">Dubbele toewijzing.</span><span class="sxs-lookup"><span data-stu-id="44278-111">Duplicate mapping.</span></span>
* <span data-ttu-id="44278-112">Resultaat van de SQL-query heeft niet de naam van een kolom die is opgegeven in het Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="44278-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="44278-113">Hallo volgende voorbeelden zijn voor Azure SQL en Azure Blob maar zijn van toepassing tooany gegevensarchief die ondersteuning biedt voor rechthoekige gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="44278-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="44278-114">Dataset en definities van de gekoppelde service in de voorbeelden toopoint toodata in de desbetreffende gegevensbron Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="44278-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="44278-115">Voorbeeld 1: kolom toewijzing van een Azure SQL tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="44278-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="44278-116">In dit voorbeeld heeft een structuur van de invoertabel Hallo en of deze tooa SQL-tabel in een Azure SQL database verwijst.</span><span class="sxs-lookup"><span data-stu-id="44278-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="44278-117">In dit voorbeeld Hallo uitvoertabel een structuur is en of deze tooa blob in Azure blob storage verwijst.</span><span class="sxs-lookup"><span data-stu-id="44278-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="44278-118">Hallo volgende JSON definieert een kopieeractiviteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="44278-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="44278-119">Hallo-kolommen van bron toegewezen toocolumns in sink (**columnMappings**) met behulp van Hallo **conversieprogramma** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="44278-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="44278-120">**Stroom van de toewijzing van kolom:**</span><span class="sxs-lookup"><span data-stu-id="44278-120">**Column mapping flow:**</span></span>

![Kolom toewijzing stroom](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="44278-122">Voorbeeld 2: toewijzingskolommen met SQL-query uit een Azure SQL tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="44278-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="44278-123">In dit voorbeeld is een SQL-query gebruikte tooextract gegevens van Azure SQL in plaats van het Hallo-tabelnaam en kolomnamen, Hallo te geven in de sectie 'structuur'.</span><span class="sxs-lookup"><span data-stu-id="44278-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="44278-124">In dit geval zijn de queryresultaten Hallo eerste toegewezen toocolumns opgegeven in 'structuur' van de bron.</span><span class="sxs-lookup"><span data-stu-id="44278-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="44278-125">Kolommen van bron 'structuur' hello worden vervolgens toegewezen toocolumns in sink 'structuur' met regels die zijn opgegeven in de columnMappings.</span><span class="sxs-lookup"><span data-stu-id="44278-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="44278-126">Stel dat Hallo query retourneert 5 kolommen, twee of meer kolommen dan die zijn opgegeven in Hallo 'structuur' van de bron.</span><span class="sxs-lookup"><span data-stu-id="44278-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="44278-127">**Kolom toewijzing stroom**</span><span class="sxs-lookup"><span data-stu-id="44278-127">**Column mapping flow**</span></span>

![Kolom toewijzing stroom-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="44278-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44278-129">Next steps</span></span>
<span data-ttu-id="44278-130">Zie Hallo artikel voor een zelfstudie over het gebruik van de Kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="44278-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="44278-131">Gegevens kopiëren van Blob Storage tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="44278-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
