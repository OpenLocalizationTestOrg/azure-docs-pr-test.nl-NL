---
title: aaaLoad - Azure Data Lake Store tooSQL Data Warehouse | Microsoft Docs
description: Meer informatie over hoe toouse PolyBase externe tooload gegevens van Azure Data Lake Store tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="bbc7a-103">Gegevens uit Azure Data Lake Store laden in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bbc7a-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="bbc7a-104">Dit document biedt u alle stappen die u moet tooload uw eigen gegevens van Azure Data Lake Store (ADLS) in SQL Data Warehouse met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="bbc7a-105">Terwijl u kunnen toorun ad-hoc-query's over Hallo-gegevens die zijn opgeslagen in met behulp van de externe tabellen Hallo ADLS bent, als best practice raadzaam Hallo gegevens importeren in SQL Data Warehouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="bbc7a-106">Schatting van de tijd: 10 minuten, ervan uitgaande dat er Hallo vereisten moet toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="bbc7a-107">In deze zelfstudie leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="bbc7a-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="bbc7a-108">Externe Database objecten tooload van Azure Data Lake Store maken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="bbc7a-109">Verbinding maken met Azure Data Lake Store Directory tooan.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="bbc7a-110">Gegevens laden in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bbc7a-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bbc7a-111">Before you begin</span></span>
<span data-ttu-id="bbc7a-112">toorun deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="bbc7a-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="bbc7a-113">Azure Active Directory-toepassing toouse voor verificatie van de Service-naar-Service.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="bbc7a-114">toocreate, volg [Active directory-verificatie](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="bbc7a-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="bbc7a-115">U moet Hallo client-ID en sleutel OAuth2.0 Token Endpoint-waarde van uw Active Directory-toepassing tooconnect tooyour Azure Data Lake van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="bbc7a-116">Details voor hoe tooget deze waarden in de bovenstaande Hallo-koppeling worden.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="bbc7a-117">Opmerking voor registratie in Azure Active Directory-App Hallo toepassings-ID gebruiken als Hallo Client-ID.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="bbc7a-118">SQL Server Management Studio of SQL Server Data Tools, toodownload SSMS en verbinding maken met Zie [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="bbc7a-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="bbc7a-119">Een Azure SQL Data Warehouse toocreate één Volg: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="bbc7a-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="bbc7a-120">Een Azure Data Lake Store, met of zonder versleuteling ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="bbc7a-121">een Volg toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="bbc7a-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="bbc7a-122">Hallo-gegevensbron configureren</span><span class="sxs-lookup"><span data-stu-id="bbc7a-122">Configure hello data source</span></span>
<span data-ttu-id="bbc7a-123">PolyBase gebruikt T-SQL externe objecten toodefine Hallo locatie en kenmerken van Hallo externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="bbc7a-124">Hallo externe objecten worden opgeslagen in SQL Data Warehouse en verwijzing Hallo gegevens th is die extern zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="bbc7a-125">Een referentie maken</span><span class="sxs-lookup"><span data-stu-id="bbc7a-125">Create a credential</span></span>
<span data-ttu-id="bbc7a-126">tooaccess uw Azure Data Lake opslaan, moet u een databasehoofdsleutel tooencrypt toocreate uw geheime referentie is gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="bbc7a-127">Vervolgens maakt u een scoped databasereferentie die Hallo principal Servicereferenties ingesteld in AAD opslaat.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="bbc7a-128">Syntaxis verschilt voor mensen die u hebt gebruikt PolyBase tooconnect tooWindows Azure Storage-Blobs, houd er rekening mee dat Hallo-referentie.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="bbc7a-129">tooconnect tooAzure Data Lake Store, moet u **eerste** een Azure Active Directory-toepassing maken, maakt u een toegangssleutel en Hallo toegang toohello Azure Data Lake toepassingsbron verlenen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="bbc7a-130">Instrucitons tooperform deze stappen zijn gevonden [hier](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="bbc7a-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="bbc7a-131">De externe gegevensbron Hallo maken</span><span class="sxs-lookup"><span data-stu-id="bbc7a-131">Create hello external data source</span></span>
<span data-ttu-id="bbc7a-132">Gebruik deze [externe gegevensbron maken] [ CREATE EXTERNAL DATA SOURCE] opdracht toostore Hallo locatie van het Hallo-gegevens en Hallo type gegevens.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="bbc7a-133">U vindt Hallo ADL URI in hello Azure-portal en www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="bbc7a-134">Indeling van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="bbc7a-134">Configure data format</span></span>
<span data-ttu-id="bbc7a-135">tooimport hello gegevens uit ADLS, moet u toospecify Hallo externe bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="bbc7a-136">Deze opdracht heeft indeling-specifieke opties toodescribe uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="bbc7a-137">Hieronder volgt een voorbeeld van een veelgebruikte bestandsindeling die een pipe gescheiden tekstbestand is.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="bbc7a-138">Bekijk onze T-SQL-documentatie voor een volledige lijst met [EXTERNAL FILE FORMAT maken][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="bbc7a-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="bbc7a-139">Hallo externe tabellen maken</span><span class="sxs-lookup"><span data-stu-id="bbc7a-139">Create hello external tables</span></span>
<span data-ttu-id="bbc7a-140">Nu u Hallo bron- en gegevensindeling hebt opgegeven, bent u klaar toocreate Hallo externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="bbc7a-141">Externe tabellen zijn interactie met externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="bbc7a-142">PolyBase gebruikt recursieve directory traversal tooread alle bestanden in alle submappen van de opgegeven in de parameter locatie Hallo Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="bbc7a-143">Hallo volgende voorbeeld toont ook hoe toocreate Hallo object.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="bbc7a-144">U moet toocustomize Hallo instructie toowork met Hallo gegevens hebt u in ADLS.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="bbc7a-145">Externe tabel overwegingen</span><span class="sxs-lookup"><span data-stu-id="bbc7a-145">External Table Considerations</span></span>
<span data-ttu-id="bbc7a-146">Het maken van een externe tabel is eenvoudig, maar er zijn enkele nuances waarvoor toobe besproken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="bbc7a-147">Laden van gegevens met PolyBase is sterk getypeerd.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="bbc7a-148">Dit betekent dat elke rij Hallo gegevens wordt ingenomen Hallo tabelschemadefinitie moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="bbc7a-149">Als een bepaalde rij komt niet overeen met de schemadefinitie hello, wordt Hallo rij afgewezen op Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="bbc7a-150">Hallo REJECT_TYPE en REJECT_VALUE opties kunt u toodefine hoeveel rijen of welk percentage van Hallo gegevens moet aanwezig zijn in de laatste tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="bbc7a-151">Tijdens het laden, als Hallo afwijzen waarde is bereikt, mislukt Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="bbc7a-152">meest voorkomende oorzaak van de Hallo van geweigerde rijen is een niet-overeenkomend schema definitie.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="bbc7a-153">Als een kolom onjuist voor Hallo-schema van int opgegeven is het Hallo-gegevens in Hallo-bestand een tekenreeks is, wordt elke rij tooload mislukken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="bbc7a-154">Hallo locatie geeft Hallo bovenste map die u wilt dat tooread gegevens uit.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="bbc7a-155">Als er zou submappen onder /DimProduct/ PolyBase in dit geval alle Hallo gegevens binnen Hallo submappen importeren.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="bbc7a-156">Hallo gegevens laden</span><span class="sxs-lookup"><span data-stu-id="bbc7a-156">Load hello data</span></span>
<span data-ttu-id="bbc7a-157">tooload gegevens van Azure Data Lake Store gebruiken Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="bbc7a-158">Laden met CTAS gebruikt Hallo sterk hebt getypt, externe tabel die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="bbc7a-159">CTAS wordt een nieuwe tabel gemaakt en gevuld met Hallo resultaten van een select-instructie.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="bbc7a-160">CTAS definieert Hallo nieuwe tabel toohave Hallo dezelfde kolommen en gegevenstypen hebben als Hallo resultaten van Hallo-instructie SELECT.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="bbc7a-161">Als u alle Hallo kolommen uit een externe tabel selecteert, is Hallo nieuwe tabel een replica van Hallo kolommen en gegevenstypen in Hallo externe tabel.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="bbc7a-162">In dit voorbeeld maakt er een hash-tabel gedistribueerde DimProduct aangeroepen vanuit de externe tabel DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="bbc7a-163">Compressie columnstore optimaliseren</span><span class="sxs-lookup"><span data-stu-id="bbc7a-163">Optimize columnstore compression</span></span>
<span data-ttu-id="bbc7a-164">Standaard worden in SQL Data Warehouse Hallo tabel opgeslagen als een geclusterde columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="bbc7a-165">Nadat een belasting is voltooid, zijn aantal rijen met Hallo gegevens niet gecomprimeerd in Hallo columnstore.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="bbc7a-166">Er is een aantal redenen waarom dit kan gebeuren.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="bbc7a-167">toolearn meer, Zie [columnstore-indexen beheren][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="bbc7a-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="bbc7a-168">queryprestaties toooptimize en de compressie columnstore na een load opnieuw worden opgebouwd Hallo tabel tooforce hello columnstore-index toocompress alle Hallo rijen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="bbc7a-169">Zie voor meer informatie over het onderhouden van de columnstore-indexen Hallo [columnstore-indexen beheren] [ manage columnstore indexes] artikel.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="bbc7a-170">Statistieken optimaliseren</span><span class="sxs-lookup"><span data-stu-id="bbc7a-170">Optimize statistics</span></span>
<span data-ttu-id="bbc7a-171">Het is beste toocreate-statistieken voor één kolom onmiddellijk na een belasting.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="bbc7a-172">Er zijn enkele mogelijkheden voor statistieken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-172">There are some choices for statistics.</span></span> <span data-ttu-id="bbc7a-173">Bijvoorbeeld, als u één kolom statistieken voor elke kolom maken duurt het mogelijk een lange tijd toorebuild alle Hallo statistieken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="bbc7a-174">Als u weet dat bepaalde kolommen niet toobe in query predicaten gaat, kunt u statistieken maken voor deze kolommen overslaan.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="bbc7a-175">Als u toocreate statistieken voor één kolom voor elke kolom van elke tabel besluit, kunt u Hallo opgeslagen procedure-codevoorbeeld `prc_sqldw_create_stats` in Hallo [statistieken] [ statistics] artikel.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="bbc7a-176">Hallo volgende voorbeeld is een goed uitgangspunt voor het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="bbc7a-177">Statistieken voor één kolom wordt gemaakt op elke kolom in de dimensietabel Hallo en op elke gekoppelde kolom in Hallo feitentabellen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="bbc7a-178">U kunt één of meerdere kolommen statistieken tooother feit tabelkolommen altijd later op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="bbc7a-179">Bereiken ontgrendeld!</span><span class="sxs-lookup"><span data-stu-id="bbc7a-179">Achievement unlocked!</span></span>
<span data-ttu-id="bbc7a-180">U hebt gegevens geladen in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bbc7a-181">Taak geweldig!</span><span class="sxs-lookup"><span data-stu-id="bbc7a-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="bbc7a-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bbc7a-182">Next Steps</span></span>
<span data-ttu-id="bbc7a-183">Laden van gegevens is Hallo eerste stap toodeveloping een datawarehouse-oplossing met behulp van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bbc7a-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="bbc7a-184">Bekijk onze ontwikkeling bronnen op [tabellen](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) en [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="bbc7a-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
