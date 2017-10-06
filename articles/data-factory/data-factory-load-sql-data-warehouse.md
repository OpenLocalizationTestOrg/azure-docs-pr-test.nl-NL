---
title: aaaLoad terabytes aan gegevens in SQL Data Warehouse | Microsoft Docs
description: Laat zien hoe 1 TB aan gegevens kunnen worden geladen in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="edc31-103">Laden van 1 TB in Azure SQL Data Warehouse onder 15 minuten met Data Factory</span><span class="sxs-lookup"><span data-stu-id="edc31-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="edc31-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is een cloud-gebaseerde, uitbreidbare database geschikt is voor het verwerken van grote hoeveelheden relationele en niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="edc31-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="edc31-105">Gebaseerd op de uitgebreide parallelle verwerkingsarchitectuur (MPP) en is SQL Data Warehouse geoptimaliseerd voor enterprise datawarehouse-werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="edc31-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="edc31-106">Biedt cloud elasticiteit met Hallo flexibiliteit tooscale opslag en onafhankelijk van elkaar te berekenen.</span><span class="sxs-lookup"><span data-stu-id="edc31-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="edc31-107">Aan de slag met Azure SQL Data Warehouse is nu eenvoudiger dan ooit met **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="edc31-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="edc31-108">Azure Data Factory is een volledig beheerde cloud-gebaseerde integration-gegevensservice gebruikt toopopulate een SQL Data Warehouse met Hallo gegevens uit uw bestaande systeem en bespaart u kostbare tijd worden kan bij het evalueren van SQL Data Warehouse en het bouwen van uw analyses oplossingen.</span><span class="sxs-lookup"><span data-stu-id="edc31-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="edc31-109">Hier volgen de belangrijkste voordelen van het laden van gegevens in Azure SQL Data Warehouse met behulp van Azure Data Factory Hallo:</span><span class="sxs-lookup"><span data-stu-id="edc31-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="edc31-110">**Eenvoudig tooset up**: 5 stap intuïtieve wizard geen scripts nodig.</span><span class="sxs-lookup"><span data-stu-id="edc31-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="edc31-111">**Uitgebreide ondersteuning voor gegevensopslag**: ingebouwde ondersteuning voor een groot aantal on-premises en cloud-gebaseerde gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="edc31-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="edc31-112">**Beveiligd en compatibel**: gegevens worden overgedragen via HTTPS of ExpressRoute en global service aanwezigheid zorgt ervoor dat uw gegevens Hallo geografische grens nooit verlaten</span><span class="sxs-lookup"><span data-stu-id="edc31-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="edc31-113">**Ongeëvenaarde prestaties door middel van PolyBase** – met behulp van Polybase is Hallo meest efficiënte manier toomove gegevens in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edc31-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="edc31-114">Hallo fasering van blob-functie kunt u snelheden hoge belasting van alle typen gegevensarchieven naast Azure Blob storage, die Polybase ondersteunt standaard Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="edc31-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="edc31-115">Dit artikel ziet u hoe toouse Data Factory-Wizard kopiëren tooload 1 TB gegevens uit Azure Blob Storage in Azure SQL Data Warehouse in onder 15 minuten op meer dan 1,2 GBps doorvoer.</span><span class="sxs-lookup"><span data-stu-id="edc31-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="edc31-116">In dit artikel bevat stapsgewijze instructies voor het verplaatsen van gegevens in Azure SQL Data Warehouse met behulp van Hallo Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="edc31-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="edc31-117">Raadpleeg voor algemene informatie over de mogelijkheden van Data Factory bij het verplaatsen van gegevens naar/van Azure SQL Data Warehouse [tooand gegevens verplaatsen van Azure SQL Data Warehouse met behulp van Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="edc31-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="edc31-118">U kunt ook samenstellen pijplijnen met Azure portal, Visual Studio, PowerShell, enzovoort. Zie [zelfstudie: gegevens kopiëren van Azure Blob-tooAzure SQL-Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor een snel overzicht met stapsgewijze instructies voor het gebruik van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="edc31-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="edc31-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edc31-119">Prerequisites</span></span>
* <span data-ttu-id="edc31-120">Azure Blob Storage: dit experiment maakt gebruik van Azure Blob-opslag (GRS) voor het opslaan van TPC-H testen gegevensset.</span><span class="sxs-lookup"><span data-stu-id="edc31-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="edc31-121">Als u een Azure storage-account niet hebt, ontdek [hoe toocreate een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="edc31-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="edc31-122">[TPC-H](http://www.tpc.org/tpch/) gegevens: we gaan toouse TPC-H zoals Hallo testen gegevensset.</span><span class="sxs-lookup"><span data-stu-id="edc31-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="edc31-123">toodo, moet u toouse `dbgen` uit de werkset TPC-H, waarmee u Hallo gegevensset genereren.</span><span class="sxs-lookup"><span data-stu-id="edc31-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="edc31-124">U kunt ofwel de broncode voor downloaden `dbgen` van [TPC hulpprogramma's](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) gecompileerd en uzelf of download Hallo gecompileerd binair van [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="edc31-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="edc31-125">Voer dbgen.exe door de volgende Hallo toogenerate 1 TB plat bestand voor de opdrachten `lineitem` tabel verspreiding in 10 bestanden:</span><span class="sxs-lookup"><span data-stu-id="edc31-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="edc31-126">…</span><span class="sxs-lookup"><span data-stu-id="edc31-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="edc31-127">Nu gegenereerd kopie Hallo bestanden tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="edc31-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="edc31-128">Raadpleeg te[tooand gegevens verplaatsen van een on-premises bestandssysteem met behulp van Azure Data Factory](data-factory-onprem-file-system-connector.md) voor het toodo die met ADF-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="edc31-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="edc31-129">Azure SQL datawarehouse: dit experiment laadt gegevens in Azure SQL Data Warehouse is gemaakt met 6000 dwu 's</span><span class="sxs-lookup"><span data-stu-id="edc31-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="edc31-130">Raadpleeg te[maken van een Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) voor gedetailleerde instructies over hoe toocreate een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="edc31-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="edc31-131">tooget hello best mogelijke load prestaties in SQL Data Warehouse met Polybase kiest maximum aantal Data Warehouse Units (dwu's) zijn toegestaan in Hallo prestaties instelling, die 6000 dwu's.</span><span class="sxs-lookup"><span data-stu-id="edc31-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="edc31-132">Bij het laden van een Azure Blob, Hallo gegevens laden van de prestaties kunnen worden rechtstreeks evenredig toohello aantal dwu's die u op Hallo SQL Data Warehouse configureert:</span><span class="sxs-lookup"><span data-stu-id="edc31-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="edc31-133">Laden van 1 TB in 1.000 duurt DWU SQL Data Warehouse 87 minuten (~ 200 MBps doorvoer) bij het laden van 1 TB in 2.000 DWU SQL Data Warehouse vergt 46 minuten (~ 380 MBps doorvoer) bij het laden van 1 TB in 6000 DWU SQL Data Warehouse duurt 14 minuten (~1.2 GBps doorvoer)</span><span class="sxs-lookup"><span data-stu-id="edc31-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="edc31-134">een SQL Data Warehouse met 6000 Dwu toocreate Hallo prestaties schuifregelaar alle Hallo manier toohello naar rechts verplaatsen:</span><span class="sxs-lookup"><span data-stu-id="edc31-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Schuifregelaar voor prestaties](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="edc31-136">Voor een bestaande database die niet is geconfigureerd met 6000 dwu's, kunt u het schalen met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="edc31-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="edc31-137">Navigeer toohello database in Azure-portal en er is een **Scale** knop in Hallo **overzicht** deelvenster wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="edc31-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Knop schaal](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="edc31-139">Klik op Hallo **Scale** knop tooopen Hallo volgende deelvenster Hallo schuifregelaar toohello maximumwaarde verplaatsen en klikt u op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="edc31-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Dialoogvenster schaal](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="edc31-141">Dit experiment gegevens laadt in met behulp van Azure SQL Data Warehouse `xlargerc` bronklasse.</span><span class="sxs-lookup"><span data-stu-id="edc31-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="edc31-142">tooachieve best mogelijke doorvoer, exemplaar moet toobe uitgevoerd met behulp van een SQL Data Warehouse-gebruiker die behoren te`xlargerc` bronklasse.</span><span class="sxs-lookup"><span data-stu-id="edc31-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="edc31-143">Meer informatie over hoe toodo die door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="edc31-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="edc31-144">Doelschema tabel maken in Azure SQL Data Warehouse-database door Hallo DDL-instructie te volgen:</span><span class="sxs-lookup"><span data-stu-id="edc31-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="edc31-145">Met de vereiste stappen Hallo voltooid, zijn er nu klaar tooconfigure hello kopieeractiviteit Hallo Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="edc31-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="edc31-146">De wizard Kopiëren starten</span><span class="sxs-lookup"><span data-stu-id="edc31-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="edc31-147">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edc31-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="edc31-148">Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="edc31-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="edc31-149">In Hallo **nieuwe gegevensfactory** blade:</span><span class="sxs-lookup"><span data-stu-id="edc31-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="edc31-150">Voer **LoadIntoSQLDWDataFactory** voor Hallo **naam**.</span><span class="sxs-lookup"><span data-stu-id="edc31-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="edc31-151">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="edc31-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="edc31-152">Als u de foutmelding Hallo: **Data factory-naam 'LoadIntoSQLDWDataFactory' is niet beschikbaar**, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameLoadIntoSQLDWDataFactory) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="edc31-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="edc31-153">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="edc31-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="edc31-154">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="edc31-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="edc31-155">Voor de resourcegroep Doe Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edc31-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="edc31-156">Selecteer **gebruik bestaande** tooselect een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="edc31-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="edc31-157">Selecteer **nieuw** tooenter een naam voor een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="edc31-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="edc31-158">Selecteer een **locatie** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="edc31-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="edc31-159">Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="edc31-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="edc31-160">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="edc31-160">Click **Create**.</span></span>
4. <span data-ttu-id="edc31-161">Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="edc31-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Startpagina van de gegevensfactory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="edc31-163">Klik op Hallo Data Factory-startpagina op Hallo **gegevens kopiëren** tegel toolaunch **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="edc31-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="edc31-164">Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instellen (of) laat dit ingeschakeld en maakt een uitzondering voor **login.microsoftonline.com**en probeer het opnieuw starten van Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="edc31-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="edc31-165">Stap 1: Planning laden van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="edc31-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="edc31-166">de eerste stap Hallo is tooconfigure Hallo gegevens laden van de planning.</span><span class="sxs-lookup"><span data-stu-id="edc31-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="edc31-167">In Hallo **eigenschappen** pagina:</span><span class="sxs-lookup"><span data-stu-id="edc31-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="edc31-168">Voer **CopyFromBlobToAzureSqlDataWarehouse** voor **taaknaam**</span><span class="sxs-lookup"><span data-stu-id="edc31-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="edc31-169">Selecteer **eenmaal nu uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="edc31-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="edc31-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-170">Click **Next**.</span></span>  

    ![Wizard voor kopiëren - pagina eigenschappen](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="edc31-172">Stap 2: Een bron configureren</span><span class="sxs-lookup"><span data-stu-id="edc31-172">Step 2: Configure source</span></span>
<span data-ttu-id="edc31-173">Deze sectie ziet u stappen tooconfigure Hallo bron Hallo: Azure Blob die 1 TB TPC Hallo-H regelitem bestanden.</span><span class="sxs-lookup"><span data-stu-id="edc31-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="edc31-174">Selecteer Hallo **Azure Blob Storage** Hallo gegevens opslaan en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Wizard voor kopiëren - pagina van de bron selecteren](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="edc31-176">Vul Hallo-verbindingsgegevens voor hello Azure Blob storage-account in en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Wizard - informatie van de gegevensbronverbinding kopiëren](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="edc31-178">Kies Hallo **map** met Hallo TPC-H regel bestanden item en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Wizard kopiëren - invoermap selecteren](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="edc31-180">Wanneer u op klikt **volgende**, Hallo bestandsindelingsinstellingen worden automatisch gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="edc31-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="edc31-181">Controleer toomake ervoor dat kolomscheidingsteken is ' | 'in plaats van Hallo standaard komma','.</span><span class="sxs-lookup"><span data-stu-id="edc31-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="edc31-182">Klik op **volgende** nadat u Hallo gegevens hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="edc31-182">Click **Next** after you have previewed hello data.</span></span>

    ![Wizard voor kopiëren - bestandsindelingsinstellingen](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="edc31-184">Stap 3: Doel configureren</span><span class="sxs-lookup"><span data-stu-id="edc31-184">Step 3: Configure destination</span></span>
<span data-ttu-id="edc31-185">Deze sectie leest u hoe tooconfigure bestemming Hallo: `lineitem` tabel in hello Azure SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="edc31-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="edc31-186">Kies **Azure SQL Data Warehouse** als bestemming Hallo opslaan en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Wizard voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="edc31-188">Vul in het Hallo-verbindingsgegevens voor Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edc31-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="edc31-189">Zorg ervoor dat u opgeeft Hallo-gebruiker die lid is van de rol Hallo `xlargerc` (Zie Hallo **vereisten** gedeelte voor meer informatie), en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Wizard - verbindingsgegevens bestemming kopiëren](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="edc31-191">Kies de doeltabel Hallo en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-191">Choose hello destination table and click **Next**.</span></span>

    ![Wizard - tabel toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="edc31-193">In de pagina Schema-toewijzing, laat u 'Toepassen kolomtoewijzing' optie uitgeschakeld en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="edc31-194">Stap 4: Prestatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="edc31-194">Step 4: Performance settings</span></span>

<span data-ttu-id="edc31-195">**Toestaan van polybase** is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="edc31-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="edc31-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="edc31-196">Click **Next**.</span></span>

![Wizard - schema toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="edc31-198">Stap 5: Implementeren en controleren van de load-resultaten</span><span class="sxs-lookup"><span data-stu-id="edc31-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="edc31-199">Klik op **voltooien** knop toodeploy.</span><span class="sxs-lookup"><span data-stu-id="edc31-199">Click **Finish** button toodeploy.</span></span>

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="edc31-201">Nadat het Hallo-implementatie is voltooid, klikt u op `Click here toomonitor copy pipeline` toomonitor Hallo kopiëren uitvoeren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="edc31-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="edc31-202">Selecteer Hallo kopieerpijplijn u hebt gemaakt in Hallo **Activiteitsvensters** lijst.</span><span class="sxs-lookup"><span data-stu-id="edc31-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="edc31-204">Vindt u details uitvoering in Hallo Hallo-kopie **activiteit venster Explorer** in Hallo rechterpaneel inclusief Hallo gegevensvolume van bron gelezen en geschreven naar bestemming, duur en de gemiddelde doorvoer Hallo voor Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="edc31-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="edc31-205">Zoals u van Hallo schermopname te volgen zien kunt, 1 TB kopiëren uit Azure Blob Storage in SQL Data Warehouse duurde 14 minuten, effectief 1,22 GBps doorvoer kan bereiken.</span><span class="sxs-lookup"><span data-stu-id="edc31-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Wizard - geslaagd dialoogvenster kopiëren](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="edc31-207">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="edc31-207">Best practices</span></span>
<span data-ttu-id="edc31-208">Hier volgen enkele aanbevolen procedures voor het uitvoeren van uw Azure SQL Data Warehouse-database:</span><span class="sxs-lookup"><span data-stu-id="edc31-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="edc31-209">Gebruik een grotere bronklasse bij het laden in een GECLUSTERDE COLUMNSTORE-INDEX.</span><span class="sxs-lookup"><span data-stu-id="edc31-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="edc31-210">Voor efficiënter joins, kunt u overwegen hash distributie door een kolom selecteren in plaats van standaard round robin distributie.</span><span class="sxs-lookup"><span data-stu-id="edc31-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="edc31-211">Voor snellere load snelheden, kunt u overwegen heap voor tijdelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="edc31-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="edc31-212">Statistieken maken als u klaar bent met het laden van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edc31-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="edc31-213">Zie [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="edc31-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edc31-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edc31-214">Next steps</span></span>
* <span data-ttu-id="edc31-215">[Data Factory-Wizard kopiëren](data-factory-copy-wizard.md) -in dit artikel bevat informatie over Hallo Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="edc31-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="edc31-216">[Prestaties van de activiteit en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md) -in dit artikel bevat Hallo verwijzing prestatiemetingen en prestatieafstemming handleiding.</span><span class="sxs-lookup"><span data-stu-id="edc31-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
