---
title: Toewijzing van gegevensset kolommen in Azure Data Factory | Microsoft Docs
description: Informatie over het toewijzen van kolommen in de gegevensbron aan kolommen van de bestemming.
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="11a01-103">Bronkolommen gegevensset toewijzen aan bestemming gegevensset kolommen</span><span class="sxs-lookup"><span data-stu-id="11a01-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="11a01-104">Kolomtoewijzing kan worden gebruikt om op te geven hoe kolommen opgegeven in de 'structuur"van tabeltoewijzing van bron naar kolommen opgegeven in de 'structuur' van tabel sink.</span><span class="sxs-lookup"><span data-stu-id="11a01-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="11a01-105">De **columnMapping** eigenschap is beschikbaar in de **typeProperties** sectie van de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="11a01-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="11a01-106">Kolomtoewijzing ondersteunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="11a01-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="11a01-107">Alle kolommen in de structuur van de gegevensset bron worden toegewezen aan alle kolommen in de structuur van de gegevensset sink.</span><span class="sxs-lookup"><span data-stu-id="11a01-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="11a01-108">Een subset van de kolommen in de structuur van de gegevensbron dataset wordt toegewezen aan alle kolommen in de structuur van de gegevensset sink.</span><span class="sxs-lookup"><span data-stu-id="11a01-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="11a01-109">Hier volgen de fouten die ertoe leiden dat een uitzondering:</span><span class="sxs-lookup"><span data-stu-id="11a01-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="11a01-110">Minder kolommen of meer kolommen in de 'structuur' van tabel sink dan opgegeven in de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="11a01-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="11a01-111">Dubbele toewijzing.</span><span class="sxs-lookup"><span data-stu-id="11a01-111">Duplicate mapping.</span></span>
* <span data-ttu-id="11a01-112">Resultaat van de SQL-query heeft niet de naam van een kolom die is opgegeven in de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="11a01-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="11a01-113">De volgende voorbeelden zijn voor Azure SQL en Azure Blob, maar zijn van toepassing op een gegevensopslag die ondersteuning biedt voor rechthoekige gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="11a01-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="11a01-114">Dataset en definities van de gekoppelde service in de voorbeelden om te verwijzen naar gegevens in de relevante gegevens aanpassen.</span><span class="sxs-lookup"><span data-stu-id="11a01-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="11a01-115">Voorbeeld 1 – toewijzingskolommen van Azure SQL naar Azure blob</span><span class="sxs-lookup"><span data-stu-id="11a01-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="11a01-116">In dit voorbeeld heeft een structuur van de invoertabel en deze verwijst naar een SQL-tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="11a01-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="11a01-117">In dit voorbeeld wordt de uitvoertabel heeft een structuur en deze verwijst naar een blob in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="11a01-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="11a01-118">De volgende JSON definieert een kopieeractiviteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="11a01-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="11a01-119">De kolommen van bron toegewezen aan kolommen in sink (**columnMappings**) met behulp van de **conversieprogramma** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="11a01-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="11a01-120">**Stroom van de toewijzing van kolom:**</span><span class="sxs-lookup"><span data-stu-id="11a01-120">**Column mapping flow:**</span></span>

![Kolom toewijzing stroom](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="11a01-122">Voorbeeld 2: toewijzingskolommen met SQL-query uit Azure SQL naar Azure blob</span><span class="sxs-lookup"><span data-stu-id="11a01-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="11a01-123">In dit voorbeeld wordt een SQL-query om gegevens te extraheren uit de SQL Azure in plaats van de tabelnaam en de kolomnamen van de te geven in de sectie 'structuur' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11a01-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="11a01-124">De queryresultaten worden in dit geval eerst toegewezen aan kolommen die is opgegeven in 'structuur' van de bron.</span><span class="sxs-lookup"><span data-stu-id="11a01-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="11a01-125">De kolommen van bron 'structuur' worden vervolgens toegewezen aan kolommen in sink 'structuur' met regels die zijn opgegeven in de columnMappings.</span><span class="sxs-lookup"><span data-stu-id="11a01-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="11a01-126">Stel dat de query retourneert 5 kolommen, twee of meer kolommen dan die zijn opgegeven in de 'structuur' van de bron.</span><span class="sxs-lookup"><span data-stu-id="11a01-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="11a01-127">**Kolom toewijzing stroom**</span><span class="sxs-lookup"><span data-stu-id="11a01-127">**Column mapping flow**</span></span>

![Kolom toewijzing stroom-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="11a01-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11a01-129">Next steps</span></span>
<span data-ttu-id="11a01-130">Zie het artikel voor een zelfstudie over het gebruik van de Kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="11a01-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="11a01-131">Gegevens kopiëren van Blob-opslag naar SQL-Database</span><span class="sxs-lookup"><span data-stu-id="11a01-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
