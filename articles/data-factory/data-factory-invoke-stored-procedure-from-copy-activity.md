---
title: Aanroepen van opgeslagen procedure uit Azure Data Factory-Kopieeractiviteit | Microsoft Docs
description: Informatie over het aanroepen van een opgeslagen procedure in Azure SQL Database of SQL Server van een kopieeractiviteit Azure Data Factory.
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
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="836f8-103">Aanroepen van opgeslagen procedure uit kopieeractiviteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="836f8-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="836f8-104">Bij het kopiëren van gegevens in [SQL Server](data-factory-sqlserver-connector.md) of [Azure SQL Database](data-factory-azure-sql-connector.md), kunt u de **SqlSink** in een kopieeractiviteit om aan te roepen, een opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="836f8-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="836f8-105">U kunt gebruiken de opgeslagen procedure voor het uitvoeren van extra verwerking (samenvoegen kolommen, opzoeken van waarden, invoegen in meerdere tabellen, enz.) is vereist voordat u gegevens in de doeltabel.</span><span class="sxs-lookup"><span data-stu-id="836f8-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="836f8-106">Deze functie wordt gebruikgemaakt van [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="836f8-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="836f8-107">Het volgende voorbeeld ziet u hoe aan te roepen, een opgeslagen procedure in een SQL Server-database van een Data Factory-pijplijn (kopieeractiviteit):</span><span class="sxs-lookup"><span data-stu-id="836f8-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="836f8-108">Uitvoergegevensset JSON</span><span class="sxs-lookup"><span data-stu-id="836f8-108">Output dataset JSON</span></span>
<span data-ttu-id="836f8-109">In de uitvoergegevensset JSON stelt u de **type** naar: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="836f8-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="836f8-110">Stel deze in op **AzureSqlTable** voor gebruik met een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="836f8-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="836f8-111">De waarde voor **tableName** eigenschap moet overeenkomen met de naam van de eerste parameter van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="836f8-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="836f8-112">De sectie SqlSink in kopieeractiviteit JSON</span><span class="sxs-lookup"><span data-stu-id="836f8-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="836f8-113">Definieer de **SqlSink** sectie als volgt in de JSON van de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="836f8-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="836f8-114">Als u wilt een opgeslagen procedure aanroepen tijdens het invoegen van gegevens in de doel-sink-database, kunt u waarden opgeven voor zowel **SqlWriterStoredProcedureName** en **SqlWriterTableType** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="836f8-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="836f8-115">Zie voor beschrijvingen van deze eigenschappen [SqlSink-sectie in het SQL Server-connector artikel](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="836f8-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="836f8-116">Definitie van de opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="836f8-116">Stored procedure definition</span></span> 
<span data-ttu-id="836f8-117">Definieer de opgeslagen procedure met dezelfde naam als in uw database **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="836f8-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="836f8-118">De opgeslagen procedure verwerkt invoergegevens uit de gegevensopslag van de bron en voegt de gegevens in een tabel in de doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="836f8-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="836f8-119">De naam van de eerste parameter van de opgeslagen procedure moet overeenkomen met de tabelnaam die wordt gedefinieerd in de gegevensset JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="836f8-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="836f8-120">De typedefinitie van de tabel</span><span class="sxs-lookup"><span data-stu-id="836f8-120">Table type definition</span></span>
<span data-ttu-id="836f8-121">Definieer het tabeltype met dezelfde naam als in uw database **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="836f8-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="836f8-122">Het schema van het type moet overeenkomen met het schema van de invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="836f8-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="836f8-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="836f8-123">Next steps</span></span>
<span data-ttu-id="836f8-124">Bekijk de volgende connector artikelen die voor volledige JSON-voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="836f8-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="836f8-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="836f8-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="836f8-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="836f8-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
