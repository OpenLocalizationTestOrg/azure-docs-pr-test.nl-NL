---
title: aaaLoad uit Azure blob tooAzure datawarehouse | Microsoft Docs
description: Meer informatie over hoe toouse PolyBase tooload gegevens van Azure blob-opslag in SQL Data Warehouse. Enkele tabellen uit openbare gegevens laden in Hallo Contoso Retail Data Warehouse-schema.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Gegevens uit Azure blob-opslag laden in SQL Data Warehouse (PolyBase)
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

PolyBase en T-SQL-opdrachten tooload gegevens gebruiken uit Azure blob-opslag in Azure SQL Data Warehouse. 

tookeep eenvoudig, deze zelfstudie wordt geladen twee tabellen vanuit een openbare Azure Storage-Blob in Hallo Contoso Retail Data Warehouse-schema. tooload hello volledige gegevensset, Hallo-voorbeeld uitvoeren [Load Hallo volledige Contoso Retail Data Warehouse] [ Load hello full Contoso Retail Data Warehouse] uit Hallo-opslagplaats voor Microsoft SQL Server-voorbeelden.

In deze zelfstudie wordt u:

1. Tooload PolyBase uit Azure blob-opslag configureren
2. Openbare gegevens laden in de database
3. Optimalisaties uitvoeren nadat de Hallo load is voltooid.

## <a name="before-you-begin"></a>Voordat u begint
toorun in deze zelfstudie, moet u een Azure-account die al een SQL Data Warehouse-database. Als u dit nog geen hebt, raadpleegt u [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Hallo-gegevensbron configureren
PolyBase gebruikt T-SQL externe objecten toodefine Hallo locatie en kenmerken van Hallo externe gegevens. Hallo externe objectdefinities worden opgeslagen in SQL Data Warehouse. Hallo-gegevens zelf is die extern zijn opgeslagen.

### <a name="11-create-a-credential"></a>1.1. Een referentie maken
**Deze stap overslaan** als u Hallo Contoso openbare gegevens laadt. U hoeft geen beveiligde toegang toohello openbare gegevens omdat die al toegankelijk tooanyone.

**Deze stap niet overslaan** als u deze zelfstudie als een sjabloon voor het laden van uw eigen gegevens. tooaccess gegevens via een referentie gebruik Hallo na script toocreate database-scoped referentie en vervolgens worden gebruikt bij het Hallo-locatie van de gegevensbron Hallo definiëren.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

Toostep 2 overslaan.

### <a name="12-create-hello-external-data-source"></a>1.2. De externe gegevensbron Hallo maken
Gebruik deze [externe gegevensbron maken] [ CREATE EXTERNAL DATA SOURCE] opdracht toostore Hallo locatie van het Hallo-gegevens en Hallo type gegevens. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Als u op uw openbare azure blob storage-containers toomake kiest, houd er rekening mee dat als de gegevenseigenaar Hallo voor gegevens kosten voor uitgaande brengt wanneer gegevens Hallo Datacenter verlaat. 
> 
> 

## <a name="2-configure-data-format"></a>2. Indeling van gegevens configureren
Hallo-gegevens worden opgeslagen in tekstbestanden in Azure blob-opslag en elk veld wordt gescheiden met een scheidingsteken. Voer deze [EXTERNAL FILE FORMAT maken] [ CREATE EXTERNAL FILE FORMAT] opdracht toospecify Hallo indeling van Hallo-gegevens in Hallo tekstbestanden. Hallo Contoso gegevens is niet-gecomprimeerde en pipe gescheiden.

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a>3. Hallo externe tabellen maken
Nu u Hallo bron- en gegevensindeling hebt opgegeven, bent u klaar toocreate Hallo externe tabellen. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Maak een schema voor Hallo-gegevens.
toocreate een plaats toostore Hallo Contoso-gegevens in de database, een schema maken.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Hallo externe tabellen maken.
Voer dit script toocreate hello DimProduct en FactOnlineSales externe tabellen. Alle we hier doen is kolomnamen en gegevenstypen definiëren, en deze binding toohello locatie en de indeling van hello Azure blob-opslag-bestanden. Hallo-definitie wordt opgeslagen in SQL Data Warehouse en Hallo gegevens nog steeds in hello Azure Storage-Blob.

Hallo **locatie** parameter Hallo map onder de hoofdmap Hallo in hello Azure Storage-Blob is. Elke tabel is in een andere map.

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a>4. Hallo gegevens laden
Er zijn verschillende manieren tooaccess externe gegevens.  U kunt query over gegevens rechtstreeks vanaf de externe tabel hello, Hallo gegevens laden in nieuwe databasetabellen of externe gegevens tooexisting databasetabellen toevoegen.  

### <a name="41-create-a-new-schema"></a>4.1. Een nieuw schema maken
CTAS maakt een nieuwe tabel die gegevens bevat.  Maak eerst een schema voor Hallo contoso gegevens.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Hallo gegevens laden in de nieuwe tabellen
tooload gegevens uit Azure blob-opslag en opslaan in een tabel in de database, gebruikt u Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie. Bij het laden van met CTAS maakt gebruik van Hallo sterk getypeerd externe tabellen die u hebt alleen created.tooload Hallo gegevens in nieuwe tabellen, gebruikt u een [CTAS] [ CTAS] instructie per tabel. 
 
CTAS wordt een nieuwe tabel gemaakt en gevuld met Hallo resultaten van een select-instructie. CTAS definieert Hallo nieuwe tabel toohave Hallo dezelfde kolommen en gegevenstypen hebben als Hallo resultaten van Hallo-instructie SELECT. Als u alle Hallo kolommen uit een externe tabel selecteert, worden nieuwe tabel Hallo een replica van Hallo kolommen en gegevenstypen in Hallo externe tabel.

In dit voorbeeld maken we zowel Hallo dimensie en Hallo feitentabel als hash-gedistribueerde tabellen. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 Hallo load voortgang bijhouden
U kunt de voortgang Hallo uw belast met dynamische beheerweergaven (DMV's) op te volgen. 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a>5. Compressie columnstore optimaliseren
Standaard worden in SQL Data Warehouse Hallo tabel opgeslagen als een geclusterde columnstore-index. Nadat een belasting is voltooid, zijn aantal rijen met Hallo gegevens niet gecomprimeerd in Hallo columnstore.  Er is een aantal redenen waarom dit kan gebeuren. toolearn meer, Zie [columnstore-indexen beheren][manage columnstore indexes].

queryprestaties toooptimize en de compressie columnstore na een load opnieuw worden opgebouwd Hallo tabel tooforce hello columnstore-index toocompress alle Hallo rijen. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Zie voor meer informatie over het onderhouden van de columnstore-indexen Hallo [columnstore-indexen beheren] [ manage columnstore indexes] artikel.

## <a name="6-optimize-statistics"></a>6. Statistieken optimaliseren
Het is beste toocreate-statistieken voor één kolom onmiddellijk na een belasting. Er zijn enkele mogelijkheden voor statistieken. Bijvoorbeeld, als u één kolom statistieken voor elke kolom maken duurt het mogelijk een lange tijd toorebuild alle Hallo statistieken. Als u weet dat bepaalde kolommen niet toobe in query predicaten gaat, kunt u statistieken maken voor deze kolommen overslaan.

Als u toocreate statistieken voor één kolom voor elke kolom van elke tabel besluit, kunt u Hallo opgeslagen procedure-codevoorbeeld `prc_sqldw_create_stats` in Hallo [statistieken] [ statistics] artikel.

Hallo volgende voorbeeld is een goed uitgangspunt voor het maken van statistieken. Statistieken voor één kolom wordt gemaakt op elke kolom in de dimensietabel Hallo en op elke gekoppelde kolom in Hallo feitentabellen. U kunt één of meerdere kolommen statistieken tooother feit tabelkolommen altijd later op toevoegen.

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a>Bereiken ontgrendeld!
Openbare gegevens is in Azure SQL Data Warehouse geladen. Taak geweldig!

U kunt nu starten Hallo tabellen met behulp van query's zoals Hallo volgende opvragen:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Volgende stappen
Contoso Retail Data Warehouse-gegevens voor tooload Hallo volledige, Hallo script in gebruiken voor meer tips voor het ontwikkeling, raadpleegt u [overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
