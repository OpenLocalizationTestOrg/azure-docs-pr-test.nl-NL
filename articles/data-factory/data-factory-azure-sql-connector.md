---
title: aaaCopy gegevens van/naar Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van/naar Azure SQL Database met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Tooand gegevens kopiëren van Azure SQL Database met Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens tooand van Azure SQL Database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.  

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **van Azure SQL Database** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure SQL-Database**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Ondersteund verificatietype
Azure SQL Database-connector biedt ondersteuning voor basisverificatie.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure SQL Database verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL database kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure SQL database tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure SQL-Database, [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 
3. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo. En u een andere dataset toospecify Hallo SQL-tabel maken in hello Azure SQL-database waarin Hallo-gegevens die zijn gekopieerd uit Hallo blob-opslag. Zie voor eigenschappen van gegevensset die specifieke tooAzure Data Lake Store, [eigenschappen van gegevensset](#dataset-properties) sectie.
4. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u van Azure SQL Database tooAzure Blob Storage kopiëren wilt, gebruikt u SqlSource en BlobSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure SQL-Database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure SQL Database zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-sql-database) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure SQL-Database zijn: 

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Een Azure SQL gekoppelde service wordt een Azure SQL database tooyour data factory. Hallo volgende tabel bevat de beschrijving voor JSON-elementen specifieke tooAzure SQL gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureSqlDatabase** |Ja |
| connectionString |Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig. Alleen basisverificatie wordt ondersteund. |Ja |

> [!IMPORTANT]
> Configureer [Azure SQL Database-Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Hallo databaseserver te[Azure Services tooaccess Hallo server toestaan](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Bovendien configureren als u gegevens tooAzure SQL-Database kopieert van de externe Azure met inbegrip van on-premises gegevensbronnen met data factory-gateway, de juiste IP-adresbereik voor Hallo-machine dat gegevens tooAzure SQL-Database verzendt.

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
een gegevensset toorepresent toospecify invoer- of -gegevens in een Azure SQL database, stelt u Hallo type-eigenschap van Hallo gegevensset: **AzureSqlTable**. Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Azure SQL gekoppelde service.  

Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureSqlTable** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in hello Azure SQL Database-exemplaar waarnaar de gekoppelde service verwijst. |Ja |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

> [!NOTE]
> Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.

Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Als u gegevens uit een Azure SQL-database verplaatst, u Hallo brontype instellen in de kopieerbewerking Hallo te**SqlSource**. Als u gegevens tooan Azure SQL-database verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**SqlSink**. Deze sectie bevat een lijst met eigenschappen die worden ondersteund door SqlSource en SqlSink.

### <a name="sqlsource"></a>SqlSource
In de kopieerbewerking wanneer Hallo bron van het type **SqlSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Voorbeeld: `select * from MyTable`. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen hello Azure SQL Database tooget Hallo brongegevens. U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, Hallo kolommen die zijn gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query zijn (`select column1, column2 from mytable`) toorun tegen hello Azure SQL Database. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

> [!NOTE]
> Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON. Er zijn geen controles uitgevoerd voor deze tabel al.
>
>

### <a name="sqlsource-example"></a>Voorbeeld van SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**Hallo opgeslagen proceduredefinitie:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy). |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef de naam van een kolom voor de Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy). |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |
| sqlWriterStoredProcedureName |Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |
| sqlWriterTableType |Geef een tabel type naam toobe in Hallo opgeslagen procedure gebruikt. Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype. Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen. |Een typenaam van de tabel. |Nee |

#### <a name="sqlsink-example"></a>Voorbeeld van SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand uit SQL-Database
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand van Azure SQL Database en Azure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Voorbeeld: Gegevens kopiëren van Azure SQL Database tooAzure Blob
Hallo definieert dezelfde Hallo Data Factory-entiteiten te volgen:

1. Een gekoppelde service van het type [AzureSqlDatabase](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [SqlSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit een tabel in Azure SQL database tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.  

**Azure SQL Database, gekoppelde service:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Zie Hallo [Azure SQL gekoppelde Service](#linked-service) sectie voor Hallo lijst van eigenschappen die worden ondersteund door deze gekoppelde service.

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
Zie Hallo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artikel voor Hallo lijst met eigenschappen die ondersteund worden door deze gekoppelde service.


**Azure SQL invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.

Instelling 'extern': 'true' informeert hello Azure Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

Zie Hallo [type-eigenschappen van Azure SQL gegevensset](#dataset) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.  

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
Zie Hallo [type-eigenschappen van Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.  

**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van Blob:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
In voorbeeld Hallo **sqlReaderQuery** voor Hallo SqlSource is opgegeven. Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget Azure SQL Database-Hallo brongegevens. U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn Hallo kolommen gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query toorun tegen hello Azure SQL Database. Bijvoorbeeld: `select column1, column2 from mytable`. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

Zie Hallo [Sql-bron](#sqlsource) sectie en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSource en BlobSink.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure SQL-Database
Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:  

1. Een gekoppelde service van het type [AzureSqlDatabase](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlSink](#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit Azure blob tooa tabel in Azure SQL database om het uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL gekoppelde service:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Zie Hallo [Azure SQL gekoppelde Service](#linked-service) sectie voor Hallo lijst van eigenschappen die worden ondersteund door deze gekoppelde service.

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
Zie Hallo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artikel voor Hallo lijst met eigenschappen die ondersteund worden door deze gekoppelde service.


**Azure Blob invoergegevensset:**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Zie Hallo [type-eigenschappen van Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.

**Azure SQL Database uitvoergegevensset:**

Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in Azure SQL. Hallo-tabel maken in Azure SQL met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
Zie Hallo [type-eigenschappen van Azure SQL gegevensset](#dataset) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.

**Een kopieeractiviteit in een pijplijn met Blob-bron en sink SQL:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
Zie Hallo [Sql Sink](#sqlsink) sectie en [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSink en BlobSource.

## <a name="identity-columns-in-hello-target-database"></a>Id-kolommen in de doeldatabase Hallo
Deze sectie toont een voorbeeld van het kopiëren van gegevens uit een brontabel zonder een doeltabel identiteit kolom tooa met een identiteitskolom.

**Brontabel:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Doeltabel:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
U ziet dat doeltabel Hallo heeft een identiteitskolom.

**Bron gegevensset JSON-definitie**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Doel-dataset JSON-definitie**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Merk op dat als de bron en doel-tabel verschillende schema's zijn (doel heeft een extra kolom met de identiteit). In dit scenario moet u toospecify **structuur** eigenschap in Hallo doel gegevenssetdefinitie, waaronder Hallo identiteitskolom niet.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Aanroepen van opgeslagen procedure uit SQL-sink
Zie voor een voorbeeld van een opgeslagen procedure van SQL-sink in een kopieeractiviteit van een pijplijn wordt aangeroepen, [opgeslagen procedure voor SQL-sink aanroepen in de kopieerbewerking](data-factory-invoke-stored-procedure-from-copy-activity.md) artikel. 

## <a name="type-mapping-for-azure-sql-database"></a>Toewijzing van het type voor Azure SQL Database
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens tooand van Azure SQL Database, worden hello volgende toewijzingen gebruikt vanuit SQL type too.NET type en vice versa. Hallo-toewijzing is hetzelfde als SQL Server gegevenstypetoewijzing voor ADO.NET Hallo.

| SQL Server Database Engine-type | .NET framework-type |
| --- | --- |
| bigint |Int64 |
| Binaire |Byte] |
| bits |Booleaanse waarde |
| CHAR |Tekenreeks, Char] |
| Datum |Datum/tijd |
| Datum/tijd |Datum/tijd |
| datetime2 |Datum/tijd |
| DateTimeOffset |DateTimeOffset |
| Decimale |Decimale |
| FILESTREAM-kenmerk (varbinary(max)) |Byte] |
| Float |dubbele |
| Afbeelding |Byte] |
| int |Int32 |
| Money |Decimale |
| nchar |Tekenreeks, Char] |
| ntext |Tekenreeks, Char] |
| numerieke |Decimale |
| nvarchar |Tekenreeks, Char] |
| echte |Één |
| ROWVERSION |Byte] |
| smalldatetime |Datum/tijd |
| smallint |Int16 |
| smallmoney |Decimale |
| sql_variant |Object * |
| Tekst |Tekenreeks, Char] |
| tijd |TimeSpan |
| tijdstempel |Byte] |
| tinyint |Byte |
| uniqueidentifier |GUID |
| varbinary |Byte] |
| varchar |Tekenreeks, Char] |
| xml |XML |

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Herhaalbare kopiëren
Bij het kopiëren van gegevens tooSQL Server-Database, voegt Hallo kopieeractiviteit gegevenstabel toohello sink standaard. een UPSERT tooperform in plaats daarvan Zie [herhaalbare schrijven tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artikel. 

Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
