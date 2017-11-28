---
title: aaaInvoke opgeslagen procedure van Azure Data Factory-Kopieeractiviteit | Microsoft Docs
description: "Meer informatie over hoe de activiteit voor het kopiëren van een opgeslagen procedure in Azure SQL Database of SQL Server uit een Azure Data Factory tooinvoke."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="6d47e-103">Aanroepen van opgeslagen procedure uit kopieeractiviteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6d47e-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="6d47e-104">Bij het kopiëren van gegevens in [SQL Server](data-factory-sqlserver-connector.md) of [Azure SQL Database](data-factory-azure-sql-connector.md), kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="6d47e-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="6d47e-105">U kunt toouse Hallo opgeslagen procedure tooperform is verdere verwerking (samenvoegen kolommen, opzoeken van waarden, invoegen in meerdere tabellen, enz.) is vereist voordat u gegevens in de doeltabel toohello invoegt.</span><span class="sxs-lookup"><span data-stu-id="6d47e-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="6d47e-106">Deze functie wordt gebruikgemaakt van [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d47e-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="6d47e-107">Hallo volgende voorbeeld ziet u hoe tooinvoke een opgeslagen procedure in een SQL Server-database van een Data Factory-pijplijn (kopieeractiviteit):</span><span class="sxs-lookup"><span data-stu-id="6d47e-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="6d47e-108">Uitvoergegevensset JSON</span><span class="sxs-lookup"><span data-stu-id="6d47e-108">Output dataset JSON</span></span>
<span data-ttu-id="6d47e-109">Stel in Hallo uitvoergegevensset JSON Hallo **type** naar: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="6d47e-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="6d47e-110">Stel deze in te**AzureSqlTable** toouse met een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6d47e-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="6d47e-111">waarde voor Hallo **tableName** eigenschap moet overeenkomen met de naam van de eerste parameter van Hallo opgeslagen procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d47e-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="6d47e-112">De sectie SqlSink in kopieeractiviteit JSON</span><span class="sxs-lookup"><span data-stu-id="6d47e-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="6d47e-113">Hallo definiëren **SqlSink** sectie in Hallo kopie activiteits-JSON als volgt.</span><span class="sxs-lookup"><span data-stu-id="6d47e-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="6d47e-114">een opgeslagen procedure bij het invoegen van gegevens in Hallo sink/het doel-database, tooinvoke waarden opgeven voor zowel **SqlWriterStoredProcedureName** en **SqlWriterTableType** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6d47e-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="6d47e-115">Zie voor beschrijvingen van deze eigenschappen [SqlSink-sectie in Hallo SQL Server-connector artikel](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="6d47e-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="6d47e-116">Definitie van de opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="6d47e-116">Stored procedure definition</span></span> 
<span data-ttu-id="6d47e-117">In de database definiëren Hallo opgeslagen procedure met dezelfde naam als Hallo **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="6d47e-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="6d47e-118">Hallo opgeslagen procedure invoergegevens van brongegevensarchief Hallo verwerkt en voegt de gegevens in een tabel in de doeldatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d47e-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="6d47e-119">Hallo-naam van de eerste parameter Hallo van opgeslagen procedure moet overeenkomen met de Hallo tableName gedefinieerd in de gegevensset Hallo JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="6d47e-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="6d47e-120">De typedefinitie van de tabel</span><span class="sxs-lookup"><span data-stu-id="6d47e-120">Table type definition</span></span>
<span data-ttu-id="6d47e-121">In de database definiëren Hallo tabeltype met dezelfde naam als Hallo **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="6d47e-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="6d47e-122">Hallo-schema van Hallo tabeltype moet overeenkomen met de Hallo-schema van de invoergegevensset Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d47e-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="6d47e-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d47e-123">Next steps</span></span>
<span data-ttu-id="6d47e-124">Controleer Hallo connector artikelen die voor JSON-voorbeelden worden voltooid na:</span><span class="sxs-lookup"><span data-stu-id="6d47e-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="6d47e-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6d47e-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="6d47e-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6d47e-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
