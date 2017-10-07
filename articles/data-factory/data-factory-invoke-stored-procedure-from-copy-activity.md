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
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Aanroepen van opgeslagen procedure uit kopieeractiviteit in Azure Data Factory
Bij het kopiëren van gegevens in [SQL Server](data-factory-sqlserver-connector.md) of [Azure SQL Database](data-factory-azure-sql-connector.md), kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure. U kunt toouse Hallo opgeslagen procedure tooperform is verdere verwerking (samenvoegen kolommen, opzoeken van waarden, invoegen in meerdere tabellen, enz.) is vereist voordat u gegevens in de doeltabel toohello invoegt. Deze functie wordt gebruikgemaakt van [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx). 

Hallo volgende voorbeeld ziet u hoe tooinvoke een opgeslagen procedure in een SQL Server-database van een Data Factory-pijplijn (kopieeractiviteit):  

## <a name="output-dataset-json"></a>Uitvoergegevensset JSON
Stel in Hallo uitvoergegevensset JSON Hallo **type** naar: **SqlServerTable**. Stel deze in te**AzureSqlTable** toouse met een Azure SQL database. waarde voor Hallo **tableName** eigenschap moet overeenkomen met de naam van de eerste parameter van Hallo opgeslagen procedure Hallo.  

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

## <a name="sqlsink-section-in-copy-activity-json"></a>De sectie SqlSink in kopieeractiviteit JSON
Hallo definiëren **SqlSink** sectie in Hallo kopie activiteits-JSON als volgt. een opgeslagen procedure bij het invoegen van gegevens in Hallo sink/het doel-database, tooinvoke waarden opgeven voor zowel **SqlWriterStoredProcedureName** en **SqlWriterTableType** eigenschappen. Zie voor beschrijvingen van deze eigenschappen [SqlSink-sectie in Hallo SQL Server-connector artikel](data-factory-sqlserver-connector.md#sqlsink).

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

## <a name="stored-procedure-definition"></a>Definitie van de opgeslagen procedure 
In de database definiëren Hallo opgeslagen procedure met dezelfde naam als Hallo **SqlWriterStoredProcedureName**. Hallo opgeslagen procedure invoergegevens van brongegevensarchief Hallo verwerkt en voegt de gegevens in een tabel in de doeldatabase Hallo. Hallo-naam van de eerste parameter Hallo van opgeslagen procedure moet overeenkomen met de Hallo tableName gedefinieerd in de gegevensset Hallo JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>De typedefinitie van de tabel
In de database definiëren Hallo tabeltype met dezelfde naam als Hallo **SqlWriterTableType**. Hallo-schema van Hallo tabeltype moet overeenkomen met de Hallo-schema van de invoergegevensset Hallo.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Volgende stappen
Controleer Hallo connector artikelen die voor JSON-voorbeelden worden voltooid na: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
