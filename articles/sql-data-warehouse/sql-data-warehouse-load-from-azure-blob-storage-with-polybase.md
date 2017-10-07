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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="fbc21-104">Gegevens uit Azure blob-opslag laden in SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="fbc21-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc21-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="fbc21-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="fbc21-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="fbc21-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="fbc21-107">PolyBase en T-SQL-opdrachten tooload gegevens gebruiken uit Azure blob-opslag in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbc21-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="fbc21-108">tookeep eenvoudig, deze zelfstudie wordt geladen twee tabellen vanuit een openbare Azure Storage-Blob in Hallo Contoso Retail Data Warehouse-schema.</span><span class="sxs-lookup"><span data-stu-id="fbc21-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="fbc21-109">tooload hello volledige gegevensset, Hallo-voorbeeld uitvoeren [Load Hallo volledige Contoso Retail Data Warehouse] [ Load hello full Contoso Retail Data Warehouse] uit Hallo-opslagplaats voor Microsoft SQL Server-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="fbc21-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="fbc21-110">In deze zelfstudie wordt u:</span><span class="sxs-lookup"><span data-stu-id="fbc21-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="fbc21-111">Tooload PolyBase uit Azure blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="fbc21-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="fbc21-112">Openbare gegevens laden in de database</span><span class="sxs-lookup"><span data-stu-id="fbc21-112">Load public data into your database</span></span>
3. <span data-ttu-id="fbc21-113">Optimalisaties uitvoeren nadat de Hallo load is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fbc21-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fbc21-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fbc21-114">Before you begin</span></span>
<span data-ttu-id="fbc21-115">toorun in deze zelfstudie, moet u een Azure-account die al een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="fbc21-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="fbc21-116">Als u dit nog geen hebt, raadpleegt u [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fbc21-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="fbc21-117">1. Hallo-gegevensbron configureren</span><span class="sxs-lookup"><span data-stu-id="fbc21-117">1. Configure hello data source</span></span>
<span data-ttu-id="fbc21-118">PolyBase gebruikt T-SQL externe objecten toodefine Hallo locatie en kenmerken van Hallo externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="fbc21-119">Hallo externe objectdefinities worden opgeslagen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbc21-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="fbc21-120">Hallo-gegevens zelf is die extern zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="fbc21-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="fbc21-121">1.1.</span></span> <span data-ttu-id="fbc21-122">Een referentie maken</span><span class="sxs-lookup"><span data-stu-id="fbc21-122">Create a credential</span></span>
<span data-ttu-id="fbc21-123">**Deze stap overslaan** als u Hallo Contoso openbare gegevens laadt.</span><span class="sxs-lookup"><span data-stu-id="fbc21-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="fbc21-124">U hoeft geen beveiligde toegang toohello openbare gegevens omdat die al toegankelijk tooanyone.</span><span class="sxs-lookup"><span data-stu-id="fbc21-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="fbc21-125">**Deze stap niet overslaan** als u deze zelfstudie als een sjabloon voor het laden van uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="fbc21-126">tooaccess gegevens via een referentie gebruik Hallo na script toocreate database-scoped referentie en vervolgens worden gebruikt bij het Hallo-locatie van de gegevensbron Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="fbc21-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

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

<span data-ttu-id="fbc21-127">Toostep 2 overslaan.</span><span class="sxs-lookup"><span data-stu-id="fbc21-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="fbc21-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="fbc21-128">1.2.</span></span> <span data-ttu-id="fbc21-129">De externe gegevensbron Hallo maken</span><span class="sxs-lookup"><span data-stu-id="fbc21-129">Create hello external data source</span></span>
<span data-ttu-id="fbc21-130">Gebruik deze [externe gegevensbron maken] [ CREATE EXTERNAL DATA SOURCE] opdracht toostore Hallo locatie van het Hallo-gegevens en Hallo type gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="fbc21-131">Als u op uw openbare azure blob storage-containers toomake kiest, houd er rekening mee dat als de gegevenseigenaar Hallo voor gegevens kosten voor uitgaande brengt wanneer gegevens Hallo Datacenter verlaat.</span><span class="sxs-lookup"><span data-stu-id="fbc21-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="fbc21-132">2. Indeling van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="fbc21-132">2. Configure data format</span></span>
<span data-ttu-id="fbc21-133">Hallo-gegevens worden opgeslagen in tekstbestanden in Azure blob-opslag en elk veld wordt gescheiden met een scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="fbc21-134">Voer deze [EXTERNAL FILE FORMAT maken] [ CREATE EXTERNAL FILE FORMAT] opdracht toospecify Hallo indeling van Hallo-gegevens in Hallo tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="fbc21-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="fbc21-135">Hallo Contoso gegevens is niet-gecomprimeerde en pipe gescheiden.</span><span class="sxs-lookup"><span data-stu-id="fbc21-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="fbc21-136">3. Hallo externe tabellen maken</span><span class="sxs-lookup"><span data-stu-id="fbc21-136">3. Create hello external tables</span></span>
<span data-ttu-id="fbc21-137">Nu u Hallo bron- en gegevensindeling hebt opgegeven, bent u klaar toocreate Hallo externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="fbc21-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="fbc21-138">3.1.</span></span> <span data-ttu-id="fbc21-139">Maak een schema voor Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-139">Create a schema for hello data.</span></span>
<span data-ttu-id="fbc21-140">toocreate een plaats toostore Hallo Contoso-gegevens in de database, een schema maken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="fbc21-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="fbc21-141">3.2.</span></span> <span data-ttu-id="fbc21-142">Hallo externe tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-142">Create hello external tables.</span></span>
<span data-ttu-id="fbc21-143">Voer dit script toocreate hello DimProduct en FactOnlineSales externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="fbc21-144">Alle we hier doen is kolomnamen en gegevenstypen definiëren, en deze binding toohello locatie en de indeling van hello Azure blob-opslag-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fbc21-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="fbc21-145">Hallo-definitie wordt opgeslagen in SQL Data Warehouse en Hallo gegevens nog steeds in hello Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="fbc21-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="fbc21-146">Hallo **locatie** parameter Hallo map onder de hoofdmap Hallo in hello Azure Storage-Blob is.</span><span class="sxs-lookup"><span data-stu-id="fbc21-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="fbc21-147">Elke tabel is in een andere map.</span><span class="sxs-lookup"><span data-stu-id="fbc21-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-hello-data"></a><span data-ttu-id="fbc21-148">4. Hallo gegevens laden</span><span class="sxs-lookup"><span data-stu-id="fbc21-148">4. Load hello data</span></span>
<span data-ttu-id="fbc21-149">Er zijn verschillende manieren tooaccess externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="fbc21-150">U kunt query over gegevens rechtstreeks vanaf de externe tabel hello, Hallo gegevens laden in nieuwe databasetabellen of externe gegevens tooexisting databasetabellen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="fbc21-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="fbc21-151">4.1.</span></span> <span data-ttu-id="fbc21-152">Een nieuw schema maken</span><span class="sxs-lookup"><span data-stu-id="fbc21-152">Create a new schema</span></span>
<span data-ttu-id="fbc21-153">CTAS maakt een nieuwe tabel die gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="fbc21-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="fbc21-154">Maak eerst een schema voor Hallo contoso gegevens.</span><span class="sxs-lookup"><span data-stu-id="fbc21-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="fbc21-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="fbc21-155">4.2.</span></span> <span data-ttu-id="fbc21-156">Hallo gegevens laden in de nieuwe tabellen</span><span class="sxs-lookup"><span data-stu-id="fbc21-156">Load hello data into new tables</span></span>
<span data-ttu-id="fbc21-157">tooload gegevens uit Azure blob-opslag en opslaan in een tabel in de database, gebruikt u Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie.</span><span class="sxs-lookup"><span data-stu-id="fbc21-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="fbc21-158">Bij het laden van met CTAS maakt gebruik van Hallo sterk getypeerd externe tabellen die u hebt alleen created.tooload Hallo gegevens in nieuwe tabellen, gebruikt u een [CTAS] [ CTAS] instructie per tabel.</span><span class="sxs-lookup"><span data-stu-id="fbc21-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="fbc21-159">CTAS wordt een nieuwe tabel gemaakt en gevuld met Hallo resultaten van een select-instructie.</span><span class="sxs-lookup"><span data-stu-id="fbc21-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="fbc21-160">CTAS definieert Hallo nieuwe tabel toohave Hallo dezelfde kolommen en gegevenstypen hebben als Hallo resultaten van Hallo-instructie SELECT.</span><span class="sxs-lookup"><span data-stu-id="fbc21-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="fbc21-161">Als u alle Hallo kolommen uit een externe tabel selecteert, worden nieuwe tabel Hallo een replica van Hallo kolommen en gegevenstypen in Hallo externe tabel.</span><span class="sxs-lookup"><span data-stu-id="fbc21-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="fbc21-162">In dit voorbeeld maken we zowel Hallo dimensie en Hallo feitentabel als hash-gedistribueerde tabellen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="fbc21-163">4.3 Hallo load voortgang bijhouden</span><span class="sxs-lookup"><span data-stu-id="fbc21-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="fbc21-164">U kunt de voortgang Hallo uw belast met dynamische beheerweergaven (DMV's) op te volgen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="fbc21-165">5. Compressie columnstore optimaliseren</span><span class="sxs-lookup"><span data-stu-id="fbc21-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="fbc21-166">Standaard worden in SQL Data Warehouse Hallo tabel opgeslagen als een geclusterde columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="fbc21-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="fbc21-167">Nadat een belasting is voltooid, zijn aantal rijen met Hallo gegevens niet gecomprimeerd in Hallo columnstore.</span><span class="sxs-lookup"><span data-stu-id="fbc21-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="fbc21-168">Er is een aantal redenen waarom dit kan gebeuren.</span><span class="sxs-lookup"><span data-stu-id="fbc21-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="fbc21-169">toolearn meer, Zie [columnstore-indexen beheren][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="fbc21-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="fbc21-170">queryprestaties toooptimize en de compressie columnstore na een load opnieuw worden opgebouwd Hallo tabel tooforce hello columnstore-index toocompress alle Hallo rijen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="fbc21-171">Zie voor meer informatie over het onderhouden van de columnstore-indexen Hallo [columnstore-indexen beheren] [ manage columnstore indexes] artikel.</span><span class="sxs-lookup"><span data-stu-id="fbc21-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="fbc21-172">6. Statistieken optimaliseren</span><span class="sxs-lookup"><span data-stu-id="fbc21-172">6. Optimize statistics</span></span>
<span data-ttu-id="fbc21-173">Het is beste toocreate-statistieken voor één kolom onmiddellijk na een belasting.</span><span class="sxs-lookup"><span data-stu-id="fbc21-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="fbc21-174">Er zijn enkele mogelijkheden voor statistieken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-174">There are some choices for statistics.</span></span> <span data-ttu-id="fbc21-175">Bijvoorbeeld, als u één kolom statistieken voor elke kolom maken duurt het mogelijk een lange tijd toorebuild alle Hallo statistieken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="fbc21-176">Als u weet dat bepaalde kolommen niet toobe in query predicaten gaat, kunt u statistieken maken voor deze kolommen overslaan.</span><span class="sxs-lookup"><span data-stu-id="fbc21-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="fbc21-177">Als u toocreate statistieken voor één kolom voor elke kolom van elke tabel besluit, kunt u Hallo opgeslagen procedure-codevoorbeeld `prc_sqldw_create_stats` in Hallo [statistieken] [ statistics] artikel.</span><span class="sxs-lookup"><span data-stu-id="fbc21-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="fbc21-178">Hallo volgende voorbeeld is een goed uitgangspunt voor het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="fbc21-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="fbc21-179">Statistieken voor één kolom wordt gemaakt op elke kolom in de dimensietabel Hallo en op elke gekoppelde kolom in Hallo feitentabellen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="fbc21-180">U kunt één of meerdere kolommen statistieken tooother feit tabelkolommen altijd later op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="fbc21-181">Bereiken ontgrendeld!</span><span class="sxs-lookup"><span data-stu-id="fbc21-181">Achievement unlocked!</span></span>
<span data-ttu-id="fbc21-182">Openbare gegevens is in Azure SQL Data Warehouse geladen.</span><span class="sxs-lookup"><span data-stu-id="fbc21-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="fbc21-183">Taak geweldig!</span><span class="sxs-lookup"><span data-stu-id="fbc21-183">Great job!</span></span>

<span data-ttu-id="fbc21-184">U kunt nu starten Hallo tabellen met behulp van query's zoals Hallo volgende opvragen:</span><span class="sxs-lookup"><span data-stu-id="fbc21-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="fbc21-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbc21-185">Next steps</span></span>
<span data-ttu-id="fbc21-186">Contoso Retail Data Warehouse-gegevens voor tooload Hallo volledige, Hallo script in gebruiken voor meer tips voor het ontwikkeling, raadpleegt u [overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="fbc21-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
