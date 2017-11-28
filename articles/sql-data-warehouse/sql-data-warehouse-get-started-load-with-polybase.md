---
title: aaaPolyBase in SQL Data Warehouse-zelfstudie | Microsoft Docs
description: Meer informatie over wat PolyBase is en hoe toouse voor datawarehousescenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="56387-103">Gegevens laden met PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="56387-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56387-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="56387-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="56387-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="56387-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="56387-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="56387-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="56387-107">BCP</span><span class="sxs-lookup"><span data-stu-id="56387-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="56387-108">Deze zelfstudie laat zien hoe tooload gegevens in SQL Data Warehouse met AzCopy en PolyBase.</span><span class="sxs-lookup"><span data-stu-id="56387-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="56387-109">Aan het einde kunt u:</span><span class="sxs-lookup"><span data-stu-id="56387-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="56387-110">AzCopy toocopy gegevens tooAzure blob storage gebruiken</span><span class="sxs-lookup"><span data-stu-id="56387-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="56387-111">Maken van databaseobjecten toodefine Hallo gegevens</span><span class="sxs-lookup"><span data-stu-id="56387-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="56387-112">Uitvoeren van een T-SQL-query tooload Hallo gegevens</span><span class="sxs-lookup"><span data-stu-id="56387-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="56387-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="56387-113">Prerequisites</span></span>
<span data-ttu-id="56387-114">toostep voor deze zelfstudie, moet u</span><span class="sxs-lookup"><span data-stu-id="56387-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="56387-115">Een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="56387-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="56387-116">Een Azure-opslagaccount van het type standaard lokaal redundante opslag (Standard Locally Redundant Storage (Standard-LRS)), standaard geografisch redundante opslag (Standard Geo-Redundant Storage (Standard-GRS)) of standaard geografisch redundante opslag met leestoegang (Standard Read-Access Geo-Redundant Storage (Standard-RAGRS)).</span><span class="sxs-lookup"><span data-stu-id="56387-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="56387-117">AzCopy-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="56387-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="56387-118">Download en installeer Hallo [meest recente versie van AzCopy] [ latest version of AzCopy] die is geïnstalleerd met Hallo hulpprogramma's voor Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="56387-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Hulpprogramma's van Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="56387-120">Stap 1: Voorbeeld gegevens tooAzure blob-opslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="56387-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="56387-121">Volgorde tooload gegevens moeten we tooput voorbeeldgegevens in een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="56387-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="56387-122">In deze stap vult u een Azure Storage Blob met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="56387-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="56387-123">Later, we gebruiken PolyBase tooload deze voorbeeldgegevens in uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="56387-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="56387-124">A.</span><span class="sxs-lookup"><span data-stu-id="56387-124">A.</span></span> <span data-ttu-id="56387-125">Een voorbeeldtekstbestand voorbereiden</span><span class="sxs-lookup"><span data-stu-id="56387-125">Prepare a sample text file</span></span>
<span data-ttu-id="56387-126">een voorbeeldtekstbestand tooprepare:</span><span class="sxs-lookup"><span data-stu-id="56387-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="56387-127">Open Kladblok en kopieer Hallo regels met gegevens in een nieuw bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="56387-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="56387-128">Sla dit tooyour lokale tijdelijke map op als % temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="56387-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="56387-129">B.</span><span class="sxs-lookup"><span data-stu-id="56387-129">B.</span></span> <span data-ttu-id="56387-130">Het eindpunt van de blob-service zoeken</span><span class="sxs-lookup"><span data-stu-id="56387-130">Find your blob service endpoint</span></span>
<span data-ttu-id="56387-131">toofind uw blobeindpunt-service:</span><span class="sxs-lookup"><span data-stu-id="56387-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="56387-132">Selecteer in Azure Portal Hallo **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="56387-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="56387-133">Klik op Hallo gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="56387-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="56387-134">Klik in de blade Opslagaccount Hallo op Blobs.</span><span class="sxs-lookup"><span data-stu-id="56387-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Klik op Blobs.](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="56387-136">Sla de URL van het eindpunt van de blob-service op voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="56387-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Eindpunt van blob-service](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="56387-138">C.</span><span class="sxs-lookup"><span data-stu-id="56387-138">C.</span></span> <span data-ttu-id="56387-139">Uw Azure-opslagsleutel zoeken</span><span class="sxs-lookup"><span data-stu-id="56387-139">Find your Azure storage key</span></span>
<span data-ttu-id="56387-140">toofind uw Azure-opslagsleutel:</span><span class="sxs-lookup"><span data-stu-id="56387-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="56387-141">Selecteer in Azure Portal Hallo, **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="56387-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="56387-142">Klik op de gewenste toouse Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="56387-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="56387-143">Selecteer **Alle instellingen** > **Toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="56387-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="56387-144">Klik op Hallo kopie vak toocopy een van uw toegang tot sleutels toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="56387-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Azure-opslagsleutel kopiëren](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="56387-146">D.</span><span class="sxs-lookup"><span data-stu-id="56387-146">D.</span></span> <span data-ttu-id="56387-147">Hallo voorbeeld bestand tooAzure blob-opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="56387-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="56387-148">toocopy de tooAzure blob-opslag van gegevens:</span><span class="sxs-lookup"><span data-stu-id="56387-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="56387-149">Open een opdrachtprompt en wijzig de mappen toohello AzCopy-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="56387-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="56387-150">Deze opdracht wijzigt toohello standaardinstallatiemap op een 64-bits Windows-client.</span><span class="sxs-lookup"><span data-stu-id="56387-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="56387-151">Hallo opdrachtbestand tooupload Hallo volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="56387-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="56387-152">Geef de URL van het eindpunt van de blob-service op voor <blob service endpoint URL> en de Azure-toegangssleutel voor <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="56387-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="56387-153">Zie ook [aan de slag met het AzCopy-opdrachtregelprogramma Hallo][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="56387-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="56387-154">E.</span><span class="sxs-lookup"><span data-stu-id="56387-154">E.</span></span> <span data-ttu-id="56387-155">De Blob Storage-container verkennen</span><span class="sxs-lookup"><span data-stu-id="56387-155">Explore your blob storage container</span></span>
<span data-ttu-id="56387-156">geüploade tooblob opslag toosee Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="56387-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="56387-157">Ga terug blade tooyour Blob-service.</span><span class="sxs-lookup"><span data-stu-id="56387-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="56387-158">Dubbelklik onder Containers op **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="56387-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="56387-159">tooexplore hello pad tooyour gegevens, klikt u op Hallo map **datedimension** en ziet u het geüploade bestand **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="56387-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="56387-160">tooview eigenschappen, klikt u op **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="56387-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="56387-161">Houd er rekening mee dat in Hallo blade blobeigenschappen kunt u downloaden of Hallo bestand verwijderen.</span><span class="sxs-lookup"><span data-stu-id="56387-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Azure Storage-blob weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="56387-163">Stap 2: Een externe tabel voor Hallo voorbeeldgegevens maken</span><span class="sxs-lookup"><span data-stu-id="56387-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="56387-164">In deze sectie maken we een externe tabel waarin de voorbeeldgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="56387-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="56387-165">PolyBase gebruikt externe tabellen tooaccess gegevens in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="56387-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="56387-166">Aangezien het Hallo-gegevens worden niet opgeslagen in SQL Data Warehouse, verwerkt PolyBase externe verificatiegegevens toohello met behulp van een database-scoped referentie.</span><span class="sxs-lookup"><span data-stu-id="56387-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="56387-167">Hallo-voorbeeld in deze stap maakt gebruik van deze Transact-SQL-instructies toocreate een externe tabel.</span><span class="sxs-lookup"><span data-stu-id="56387-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="56387-168">[Maken van Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt Hallo geheim van de database-scoped referentie.</span><span class="sxs-lookup"><span data-stu-id="56387-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="56387-169">[Create Database Scoped Credential (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify verificatie-informatie voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="56387-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="56387-170">[Create External Data Source (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify Hallo locatie van uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="56387-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="56387-171">[Create External File Format (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify Hallo indeling van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="56387-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="56387-172">[Create External Table (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify Hallo tabeldefinitie en locatie van gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="56387-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="56387-173">Voer deze query uit voor uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="56387-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="56387-174">Een externe tabel DimDate2External met de naam in Hallo dbo-schema dat toohello voorbeeldgegevens in DimDate2.txt in hello Azure blob-opslag wijst wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="56387-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="56387-175">In SQL Server-Objectverkenner in Visual Studio ziet u Hallo externe bestandsindeling, externe gegevensbron en Hallo DimDate2External tabel.</span><span class="sxs-lookup"><span data-stu-id="56387-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Externe tabel weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="56387-177">Stap 3: gegevens laden in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="56387-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="56387-178">Zodra Hallo externe tabel is gemaakt, kunt u Hallo gegevens in een nieuwe tabel laden of in een bestaande tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="56387-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="56387-179">tooload hello gegevens in een nieuwe tabel, Voer Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie.</span><span class="sxs-lookup"><span data-stu-id="56387-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="56387-180">Hallo nieuwe tabel hebben met de naam in de query Hallo Hallo-kolommen.</span><span class="sxs-lookup"><span data-stu-id="56387-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="56387-181">de gegevenstypen Hallo van Hallo kolommen komt overeen met de Hallo-gegevenstypen in de definitie van de externe tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="56387-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="56387-182">tooload hello gegevens in een bestaande tabel, gebruikt u Hallo [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instructie.</span><span class="sxs-lookup"><span data-stu-id="56387-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="56387-183">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="56387-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="56387-184">SQL Data Warehouse bevat geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="56387-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="56387-185">Daarom tooachieve hoge queryprestaties, het is belangrijk toocreate statistieken op elke kolom in elke tabel na Hallo eerst laden.</span><span class="sxs-lookup"><span data-stu-id="56387-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="56387-186">Het is ook belangrijk tooupdate statistieken na Hallo gegevens substantieel zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="56387-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="56387-187">In dit voorbeeld maakt statistieken voor één kolom op Hallo nieuwe tabel dimdate2.</span><span class="sxs-lookup"><span data-stu-id="56387-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="56387-188">toolearn meer, Zie [statistieken][Statistics].</span><span class="sxs-lookup"><span data-stu-id="56387-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="56387-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56387-189">Next steps</span></span>
<span data-ttu-id="56387-190">Zie Hallo [PolyBase-handleiding] [ PolyBase guide] voor meer informatie over het ontwikkelen van een oplossing die gebruikmaakt van PolyBase.</span><span class="sxs-lookup"><span data-stu-id="56387-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
