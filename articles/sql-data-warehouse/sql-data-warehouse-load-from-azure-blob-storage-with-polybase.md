---
title: Laden van Azure blob met Azure datawarehouse | Microsoft Docs
description: Informatie over hoe u gegevens uit Azure blob-opslag laden in SQL Data Warehouse met PolyBase. Enkele tabellen uit openbare gegevens laden in het datawarehouse van Contoso Retail-schema.
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="13f3f-104">Gegevens uit Azure blob-opslag laden in SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="13f3f-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13f3f-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="13f3f-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="13f3f-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="13f3f-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="13f3f-107">PolyBase en T-SQL-opdrachten gebruiken voor gegevens uit Azure blob-opslag laden in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="13f3f-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="13f3f-108">Deze zelfstudie wordt in het schema Contoso Retail Data Warehouse het gemak houden de twee tabellen van een openbare Azure Storage-Blob geladen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="13f3f-109">Het voorbeeld uitvoert voor het laden van de volledige gegevensset, [volledige Contoso Retail Data Warehouse laden] [ Load the full Contoso Retail Data Warehouse] uit de opslagplaats voor Microsoft SQL Server-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="13f3f-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="13f3f-110">In deze zelfstudie wordt u:</span><span class="sxs-lookup"><span data-stu-id="13f3f-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="13f3f-111">PolyBase laden uit Azure blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="13f3f-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="13f3f-112">Openbare gegevens laden in de database</span><span class="sxs-lookup"><span data-stu-id="13f3f-112">Load public data into your database</span></span>
3. <span data-ttu-id="13f3f-113">Optimalisaties uitvoeren nadat de belasting is voltooid.</span><span class="sxs-lookup"><span data-stu-id="13f3f-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="13f3f-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="13f3f-114">Before you begin</span></span>
<span data-ttu-id="13f3f-115">Als u wilt uitvoeren in deze zelfstudie, moet u een Azure-account die al een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="13f3f-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="13f3f-116">Als u dit nog geen hebt, raadpleegt u [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="13f3f-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="13f3f-117">1. Configureer de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="13f3f-117">1. Configure the data source</span></span>
<span data-ttu-id="13f3f-118">PolyBase gebruikt externe T-SQL-objecten voor het definiëren van de locatie en de kenmerken van de externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="13f3f-119">De externe objectdefinities worden opgeslagen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="13f3f-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="13f3f-120">De gegevens zelf is die extern zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="13f3f-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="13f3f-121">1.1.</span></span> <span data-ttu-id="13f3f-122">Een referentie maken</span><span class="sxs-lookup"><span data-stu-id="13f3f-122">Create a credential</span></span>
<span data-ttu-id="13f3f-123">**Deze stap overslaan** als u de openbare Contoso-gegevens worden geladen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="13f3f-124">U hoeft niet op veilige toegang tot openbare gegevens omdat die al toegankelijk voor iedereen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="13f3f-125">**Deze stap niet overslaan** als u deze zelfstudie als een sjabloon voor het laden van uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="13f3f-126">Toegang tot gegevens via een referentie op die het volgende script gebruiken voor het maken van een database-scoped referentie en vervolgens worden gebruikt bij het definiëren van de locatie van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="13f3f-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="13f3f-127">Verder met stap 2.</span><span class="sxs-lookup"><span data-stu-id="13f3f-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="13f3f-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="13f3f-128">1.2.</span></span> <span data-ttu-id="13f3f-129">De externe gegevensbron maken</span><span class="sxs-lookup"><span data-stu-id="13f3f-129">Create the external data source</span></span>
<span data-ttu-id="13f3f-130">Gebruik deze [externe gegevensbron maken] [ CREATE EXTERNAL DATA SOURCE] opdracht voor het opslaan van de locatie van de gegevens en het type gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="13f3f-131">Als u uw azure blob storage-containers om openbaar te maken kiest, houd er rekening mee dat als eigenaar van de gegevens u gefactureerd voor gegevens kosten voor uitgaande wanneer gegevens het datacenter verlaat.</span><span class="sxs-lookup"><span data-stu-id="13f3f-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="13f3f-132">2. Indeling van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="13f3f-132">2. Configure data format</span></span>
<span data-ttu-id="13f3f-133">De gegevens worden opgeslagen in tekstbestanden in Azure blob-opslag en elk veld wordt gescheiden met een scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="13f3f-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="13f3f-134">Voer deze [EXTERNAL FILE FORMAT maken] [ CREATE EXTERNAL FILE FORMAT] opdracht voor het opgeven van de indeling van de gegevens in de tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="13f3f-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="13f3f-135">De Contoso-gegevens niet-gecomprimeerde en pipe gescheiden.</span><span class="sxs-lookup"><span data-stu-id="13f3f-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="13f3f-136">3. De externe tabellen maken</span><span class="sxs-lookup"><span data-stu-id="13f3f-136">3. Create the external tables</span></span>
<span data-ttu-id="13f3f-137">Nu dat u hebt opgegeven dat de bron- en gegevensindeling, bent u klaar voor het maken van de externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="13f3f-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="13f3f-138">3.1.</span></span> <span data-ttu-id="13f3f-139">Maak een schema voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-139">Create a schema for the data.</span></span>
<span data-ttu-id="13f3f-140">Maak een schema voor het maken van een plaats voor het opslaan van de Contoso-gegevens in uw database.</span><span class="sxs-lookup"><span data-stu-id="13f3f-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="13f3f-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="13f3f-141">3.2.</span></span> <span data-ttu-id="13f3f-142">Maak de externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-142">Create the external tables.</span></span>
<span data-ttu-id="13f3f-143">Voer dit script voor het maken van de DimProduct en FactOnlineSales externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="13f3f-144">Alle we hier doen is kolomnamen en gegevenstypen definiëren, en ze te binden aan de locatie en de indeling van de Azure blob-opslag-bestanden.</span><span class="sxs-lookup"><span data-stu-id="13f3f-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="13f3f-145">De definitie is opgeslagen in SQL Data Warehouse en de gegevens nog in de Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="13f3f-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="13f3f-146">De **locatie** parameter is de map onder de hoofdmap in de Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="13f3f-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="13f3f-147">Elke tabel is in een andere map.</span><span class="sxs-lookup"><span data-stu-id="13f3f-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="13f3f-148">4. De gegevens laden</span><span class="sxs-lookup"><span data-stu-id="13f3f-148">4. Load the data</span></span>
<span data-ttu-id="13f3f-149">Er is een verschillende manieren om toegang te krijgen tot externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-149">There's different ways to access external data.</span></span>  <span data-ttu-id="13f3f-150">U kunt een query over gegevens rechtstreeks vanuit de externe tabel, de gegevens in de nieuwe databasetabellen laden of externe gegevens toevoegen aan bestaande databasetabellen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="13f3f-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="13f3f-151">4.1.</span></span> <span data-ttu-id="13f3f-152">Een nieuw schema maken</span><span class="sxs-lookup"><span data-stu-id="13f3f-152">Create a new schema</span></span>
<span data-ttu-id="13f3f-153">CTAS maakt een nieuwe tabel die gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="13f3f-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="13f3f-154">Maak eerst een schema voor de contoso-gegevens.</span><span class="sxs-lookup"><span data-stu-id="13f3f-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="13f3f-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="13f3f-155">4.2.</span></span> <span data-ttu-id="13f3f-156">De gegevens in de nieuwe tabellen laden</span><span class="sxs-lookup"><span data-stu-id="13f3f-156">Load the data into new tables</span></span>
<span data-ttu-id="13f3f-157">Gebruiken om gegevens uit Azure blob-opslag laden en opslaan in een tabel in de database, de [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie.</span><span class="sxs-lookup"><span data-stu-id="13f3f-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="13f3f-158">Laden met CTAS maakt gebruik van de sterk getypeerde externe tabellen die u zojuist hebt gemaakt. Als u wilt de gegevens in de nieuwe tabellen laden, gebruikt u een [CTAS] [ CTAS] instructie per tabel.</span><span class="sxs-lookup"><span data-stu-id="13f3f-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="13f3f-159">CTAS wordt een nieuwe tabel gemaakt en gevuld met de resultaten van een select-instructie.</span><span class="sxs-lookup"><span data-stu-id="13f3f-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="13f3f-160">CTAS wordt gedefinieerd in de nieuwe tabel dezelfde kolommen en gegevenstypen hebben als de resultaten van de select-instructie.</span><span class="sxs-lookup"><span data-stu-id="13f3f-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="13f3f-161">Als u alle kolommen uit een externe tabel selecteert, worden de nieuwe tabel een replica van de kolommen en gegevenstypen in de externe tabel.</span><span class="sxs-lookup"><span data-stu-id="13f3f-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="13f3f-162">We maken als u de dimensie en de feitentabel als hash-gedistribueerde tabellen in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="13f3f-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="13f3f-163">4.3 de load-voortgang bijhouden</span><span class="sxs-lookup"><span data-stu-id="13f3f-163">4.3 Track the load progress</span></span>
<span data-ttu-id="13f3f-164">U kunt de voortgang van uw belasting met dynamische beheerweergaven (DMV's) te volgen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="13f3f-165">5. Compressie columnstore optimaliseren</span><span class="sxs-lookup"><span data-stu-id="13f3f-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="13f3f-166">Standaard worden in de tabel in SQL Data Warehouse opgeslagen als een geclusterde columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="13f3f-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="13f3f-167">Nadat een belasting is voltooid, kunnen sommige van de rijen met gegevens niet in de columnstore worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="13f3f-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="13f3f-168">Er is een aantal redenen waarom dit kan gebeuren.</span><span class="sxs-lookup"><span data-stu-id="13f3f-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="13f3f-169">Zie voor meer informatie, [columnstore-indexen beheren][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="13f3f-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="13f3f-170">Voor het optimaliseren van de prestaties van query's en de compressie columnstore na een werklast in de tabel om af te dwingen de columnstore-index moeten worden gecomprimeerd alle rijen opnieuw worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="13f3f-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="13f3f-171">Zie voor meer informatie over het onderhouden van de columnstore-indexen, de [columnstore-indexen beheren] [ manage columnstore indexes] artikel.</span><span class="sxs-lookup"><span data-stu-id="13f3f-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="13f3f-172">6. Statistieken optimaliseren</span><span class="sxs-lookup"><span data-stu-id="13f3f-172">6. Optimize statistics</span></span>
<span data-ttu-id="13f3f-173">Het is raadzaam om te maken van statistieken voor één kolom onmiddellijk na een belasting.</span><span class="sxs-lookup"><span data-stu-id="13f3f-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="13f3f-174">Er zijn enkele mogelijkheden voor statistieken.</span><span class="sxs-lookup"><span data-stu-id="13f3f-174">There are some choices for statistics.</span></span> <span data-ttu-id="13f3f-175">Bijvoorbeeld als u statistieken voor één kolom in elke kolom maakt het mogelijk lang duren voor het opnieuw samenstellen van de statistieken.</span><span class="sxs-lookup"><span data-stu-id="13f3f-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="13f3f-176">Als u weet dat bepaalde kolommen niet gaan worden als in query predicaten, kunt u statistieken maken voor deze kolommen overslaan.</span><span class="sxs-lookup"><span data-stu-id="13f3f-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="13f3f-177">Als u besluit te maken van statistieken voor één kolom voor elke kolom van elke tabel, kunt u de voorbeeldcode van de opgeslagen procedure `prc_sqldw_create_stats` in de [statistieken] [ statistics] artikel.</span><span class="sxs-lookup"><span data-stu-id="13f3f-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="13f3f-178">Het volgende voorbeeld is een goed uitgangspunt voor het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="13f3f-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="13f3f-179">Statistieken voor één kolom wordt gemaakt op elke kolom in de dimensietabel en op elke gekoppelde kolom in de feitentabellen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="13f3f-180">U kunt altijd statistieken met één of meerdere kolommen naar andere kolommen van de tabel feit later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="13f3f-181">Bereiken ontgrendeld!</span><span class="sxs-lookup"><span data-stu-id="13f3f-181">Achievement unlocked!</span></span>
<span data-ttu-id="13f3f-182">Openbare gegevens is in Azure SQL Data Warehouse geladen.</span><span class="sxs-lookup"><span data-stu-id="13f3f-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="13f3f-183">Taak geweldig!</span><span class="sxs-lookup"><span data-stu-id="13f3f-183">Great job!</span></span>

<span data-ttu-id="13f3f-184">U kunt nu starten opvragen van de tabellen met behulp van query's als volgt:</span><span class="sxs-lookup"><span data-stu-id="13f3f-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="13f3f-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="13f3f-185">Next steps</span></span>
<span data-ttu-id="13f3f-186">De volledige Contoso Retail-datawarehouse om gegevens te laden, gebruikt u het script in voor meer tips voor ontwikkeling, Zie [overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="13f3f-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
