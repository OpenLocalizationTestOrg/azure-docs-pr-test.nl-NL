---
title: 'Zelfstudie: PolyBase in SQL Data Warehouse | Microsoft Docs'
description: Informatie over PolyBase en het gebruik van PolyBase voor datawarehousescenario's.
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
ms.openlocfilehash: 1a26fe127448f794bbad11043aa3c8770bc2ac8c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="848d8-103">Gegevens laden met PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="848d8-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="848d8-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="848d8-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="848d8-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="848d8-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="848d8-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="848d8-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="848d8-107">BCP</span><span class="sxs-lookup"><span data-stu-id="848d8-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="848d8-108">In deze zelfstudie ziet u hoe u met AzCopy en PolyBase gegevens laadt in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="848d8-108">This tutorial shows how to load data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="848d8-109">Aan het einde kunt u:</span><span class="sxs-lookup"><span data-stu-id="848d8-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="848d8-110">AzCopy gebruikt om gegevens te kopiëren naar Azure Blob-opslag;</span><span class="sxs-lookup"><span data-stu-id="848d8-110">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="848d8-111">databaseobjecten maakt om de gegevens te definiëren;</span><span class="sxs-lookup"><span data-stu-id="848d8-111">Create database objects to define the data</span></span>
* <span data-ttu-id="848d8-112">een TSQL-query uitvoert om de gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="848d8-112">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="848d8-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="848d8-113">Prerequisites</span></span>
<span data-ttu-id="848d8-114">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="848d8-114">To step through this tutorial, you need</span></span>

* <span data-ttu-id="848d8-115">Een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="848d8-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="848d8-116">Een Azure-opslagaccount van het type standaard lokaal redundante opslag (Standard Locally Redundant Storage (Standard-LRS)), standaard geografisch redundante opslag (Standard Geo-Redundant Storage (Standard-GRS)) of standaard geografisch redundante opslag met leestoegang (Standard Read-Access Geo-Redundant Storage (Standard-RAGRS)).</span><span class="sxs-lookup"><span data-stu-id="848d8-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="848d8-117">AzCopy-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="848d8-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="848d8-118">Download en installeer de [meest recente versie van AzCopy][latest version of AzCopy], dat wordt geïnstalleerd met de hulpprogramma's van Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="848d8-118">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Hulpprogramma's van Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="848d8-120">Stap 1: voorbeeldgegevens toevoegen aan Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="848d8-120">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="848d8-121">Als u gegevens wilt laden, moet u voorbeeldgegevens in een Azure Blob Storage plaatsen.</span><span class="sxs-lookup"><span data-stu-id="848d8-121">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="848d8-122">In deze stap vult u een Azure Storage Blob met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="848d8-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="848d8-123">Later gaat u PolyBase gebruiken om deze voorbeeldgegevens in de SQL Data Warehouse-database te laden.</span><span class="sxs-lookup"><span data-stu-id="848d8-123">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="848d8-124">A.</span><span class="sxs-lookup"><span data-stu-id="848d8-124">A.</span></span> <span data-ttu-id="848d8-125">Een voorbeeldtekstbestand voorbereiden</span><span class="sxs-lookup"><span data-stu-id="848d8-125">Prepare a sample text file</span></span>
<span data-ttu-id="848d8-126">Bereid als volgt een voorbeeldtekstbestand voor:</span><span class="sxs-lookup"><span data-stu-id="848d8-126">To prepare a sample text file:</span></span>

1. <span data-ttu-id="848d8-127">Open Kladblok en kopieer de volgende regels met gegevens naar een nieuw bestand.</span><span class="sxs-lookup"><span data-stu-id="848d8-127">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="848d8-128">Sla dit in uw lokale tijdelijke map op als %temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="848d8-128">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="848d8-129">B.</span><span class="sxs-lookup"><span data-stu-id="848d8-129">B.</span></span> <span data-ttu-id="848d8-130">Het eindpunt van de blob-service zoeken</span><span class="sxs-lookup"><span data-stu-id="848d8-130">Find your blob service endpoint</span></span>
<span data-ttu-id="848d8-131">Zoek als volgt het eindpunt van de blob-service:</span><span class="sxs-lookup"><span data-stu-id="848d8-131">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="848d8-132">Selecteer in de Azure-portal **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="848d8-132">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="848d8-133">Klik op het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="848d8-133">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="848d8-134">Klik op de blade Opslagaccount op Blobs.</span><span class="sxs-lookup"><span data-stu-id="848d8-134">In the Storage account blade, click Blobs</span></span>
   
    ![Klik op Blobs.](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="848d8-136">Sla de URL van het eindpunt van de blob-service op voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="848d8-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Eindpunt van blob-service](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="848d8-138">C.</span><span class="sxs-lookup"><span data-stu-id="848d8-138">C.</span></span> <span data-ttu-id="848d8-139">Uw Azure-opslagsleutel zoeken</span><span class="sxs-lookup"><span data-stu-id="848d8-139">Find your Azure storage key</span></span>
<span data-ttu-id="848d8-140">Zoek als volgt uw Azure-opslagsleutel:</span><span class="sxs-lookup"><span data-stu-id="848d8-140">To find your Azure storage key:</span></span>

1. <span data-ttu-id="848d8-141">Selecteer in de Azure-portal **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="848d8-141">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="848d8-142">Klik op het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="848d8-142">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="848d8-143">Selecteer **Alle instellingen** > **Toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="848d8-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="848d8-144">Klik op Kopiëren om een van de toegangssleutels naar het Klembord te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="848d8-144">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![Azure-opslagsleutel kopiëren](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="848d8-146">D.</span><span class="sxs-lookup"><span data-stu-id="848d8-146">D.</span></span> <span data-ttu-id="848d8-147">Het voorbeeldbestand kopiëren naar Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="848d8-147">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="848d8-148">Ga als volgt te werk om uw gegevens te kopiëren naar Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="848d8-148">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="848d8-149">Open een opdrachtprompt en wijzig de mappen in de installatiemap van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="848d8-149">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="848d8-150">Met deze opdracht schakelt u naar de standaardinstallatiemap op een 64-bits Windows-client.</span><span class="sxs-lookup"><span data-stu-id="848d8-150">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="848d8-151">Voer de volgende opdracht uit om het bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="848d8-151">Run the following command to upload the file.</span></span> <span data-ttu-id="848d8-152">Geef de URL van het eindpunt van de blob-service op voor <blob service endpoint URL> en de Azure-toegangssleutel voor <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="848d8-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="848d8-153">Zie ook [Aan de slag met het AzCopy-opdrachtregelprogramma][Getting Started with the AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="848d8-153">See also [Getting Started with the AzCopy Command-Line Utility][Getting Started with the AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="848d8-154">E.</span><span class="sxs-lookup"><span data-stu-id="848d8-154">E.</span></span> <span data-ttu-id="848d8-155">De Blob Storage-container verkennen</span><span class="sxs-lookup"><span data-stu-id="848d8-155">Explore your blob storage container</span></span>
<span data-ttu-id="848d8-156">Controleer als volgt het bestand dat naar Blob Storage is geüpload:</span><span class="sxs-lookup"><span data-stu-id="848d8-156">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="848d8-157">Ga terug naar de blade Blob-service.</span><span class="sxs-lookup"><span data-stu-id="848d8-157">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="848d8-158">Dubbelklik onder Containers op **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="848d8-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="848d8-159">Als u het pad naar uw gegevens wilt verkennen, klikt u op de map **datedimension**. Nu ziet u het geüploade bestand **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="848d8-159">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="848d8-160">Klik op **DimDate2.txt** als u eigenschappen wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="848d8-160">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="848d8-161">Op de blade Blobeigenschappen kunt u het bestand downloaden of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="848d8-161">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![Azure Storage-blob weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="848d8-163">Stap 2: een externe tabel voor de voorbeeldgegevens maken</span><span class="sxs-lookup"><span data-stu-id="848d8-163">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="848d8-164">In deze sectie maakt u een externe tabel waarin de voorbeeldgegevens worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="848d8-164">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="848d8-165">PolyBase gebruikt externe tabellen voor de toegang tot gegevens in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="848d8-165">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="848d8-166">Omdat de gegevens niet zijn opgeslagen in SQL Data Warehouse, wordt verificatie van de externe gegevens door PolyBase uitgevoerd met behulp van een database-scoped referentie.</span><span class="sxs-lookup"><span data-stu-id="848d8-166">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="848d8-167">In het voorbeeld in deze stap worden de volgende Transact-SQL-instructies gebruikt om een externe tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="848d8-167">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="848d8-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] om het geheim van de referenties van de databaseconfiguratie te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="848d8-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="848d8-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] om verificatiegegevens voor het Azure-opslagaccount op te geven.</span><span class="sxs-lookup"><span data-stu-id="848d8-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="848d8-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] om de locatie van de Azure-blobopslag op te geven.</span><span class="sxs-lookup"><span data-stu-id="848d8-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="848d8-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] om de indeling van de gegevens op te geven.</span><span class="sxs-lookup"><span data-stu-id="848d8-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="848d8-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] om de tabeldefinitie en locatie van de gegevens op te geven.</span><span class="sxs-lookup"><span data-stu-id="848d8-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="848d8-173">Voer deze query uit voor uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="848d8-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="848d8-174">Hiermee wordt een externe tabel DimDate2External gemaakt in het DBO-schema dat wijst naar de voorbeeldgegevens in DimDate2.txt in de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="848d8-174">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="848d8-175">In SQL Server-objectverkenner in Visual Studio ziet u de externe bestandsindeling, externe gegevensbron en de tabel DimDate2External.</span><span class="sxs-lookup"><span data-stu-id="848d8-175">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![Externe tabel weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="848d8-177">Stap 3: gegevens laden in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="848d8-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="848d8-178">Nadat de externe tabel is gemaakt, kunt u de gegevens in een nieuwe tabel laden of in een bestaande tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="848d8-178">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="848d8-179">Als u de gegevens in een nieuwe tabel wilt laden, voert u de instructie [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] uit.</span><span class="sxs-lookup"><span data-stu-id="848d8-179">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="848d8-180">De kolommen in de nieuwe tabel hebben in de query een naam gekregen.</span><span class="sxs-lookup"><span data-stu-id="848d8-180">The new table will have the columns named in the query.</span></span> <span data-ttu-id="848d8-181">De gegevenstypen van de kolommen komen overeen met de gegevenstypen in de definitie van de externe tabel.</span><span class="sxs-lookup"><span data-stu-id="848d8-181">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="848d8-182">Als u de gegevens in een bestaande tabel wilt laden, gebruikt u de instructie [INSERT…SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="848d8-182">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="848d8-183">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="848d8-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="848d8-184">SQL Data Warehouse bevat geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="848d8-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="848d8-185">Voor hoge queryprestaties is het dan ook belangrijk dat u voor elke kolom in elke tabel statistieken maakt nadat de tabel de eerste keer is geladen.</span><span class="sxs-lookup"><span data-stu-id="848d8-185">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="848d8-186">Het is ook belangrijk dat de statistieken worden bijgewerkt wanneer gegevens substantieel zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="848d8-186">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="848d8-187">In dit voorbeeld maakt u statistieken voor één kolom voor de nieuwe tabel DimDate2.</span><span class="sxs-lookup"><span data-stu-id="848d8-187">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="848d8-188">Zie [Statistieken][Statistics] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="848d8-188">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="848d8-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="848d8-189">Next steps</span></span>
<span data-ttu-id="848d8-190">Raadpleeg de [PolyBase-handleiding][PolyBase guide] voor meer informatie over het ontwikkelen van een oplossing die gebruikmaakt van PolyBase.</span><span class="sxs-lookup"><span data-stu-id="848d8-190">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with the AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
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
