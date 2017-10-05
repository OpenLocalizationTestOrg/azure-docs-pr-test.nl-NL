---
title: Terabytes aan gegevens laden in SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="e4666-103">Laden van 1 TB in Azure SQL Data Warehouse onder 15 minuten met Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4666-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="e4666-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is een cloud-gebaseerde, uitbreidbare database geschikt is voor het verwerken van grote hoeveelheden relationele en niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4666-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="e4666-105">Gebaseerd op de uitgebreide parallelle verwerkingsarchitectuur (MPP) en is SQL Data Warehouse geoptimaliseerd voor enterprise datawarehouse-werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="e4666-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="e4666-106">Elasticiteit cloud biedt de flexibiliteit om te schalen van opslag en onafhankelijk berekenen.</span><span class="sxs-lookup"><span data-stu-id="e4666-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="e4666-107">Aan de slag met Azure SQL Data Warehouse is nu eenvoudiger dan ooit met **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="e4666-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="e4666-108">Azure Data Factory is een volledig beheerde cloud-gebaseerde integration-gegevensservice kan worden gebruikt voor het vullen van een SQL Data Warehouse met de gegevens uit uw bestaande systeem en bespaart u kostbare tijd bij het evalueren van SQL Data Warehouse en het bouwen van uw analyses oplossingen.</span><span class="sxs-lookup"><span data-stu-id="e4666-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="e4666-109">Hier volgen de belangrijkste voordelen van het laden van gegevens in Azure SQL Data Warehouse met behulp van Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="e4666-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="e4666-110">**Eenvoudig instellen van**: 5 stap intuïtieve wizard geen scripts nodig.</span><span class="sxs-lookup"><span data-stu-id="e4666-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="e4666-111">**Uitgebreide ondersteuning voor gegevensopslag**: ingebouwde ondersteuning voor een groot aantal on-premises en cloud-gebaseerde gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="e4666-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="e4666-112">**Beveiligd en compatibel**: gegevens worden overgedragen via HTTPS of ExpressRoute en global service aanwezigheid zorgt ervoor dat uw gegevens de geografische grens nooit verlaten</span><span class="sxs-lookup"><span data-stu-id="e4666-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="e4666-113">**Ongeëvenaarde prestaties door middel van PolyBase** – met behulp van Polybase is de meest efficiënte manier om gegevens te verplaatsen naar Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e4666-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e4666-114">De fasering blob-functie kunt u hoge belasting snelheden van alle typen gegevensarchieven naast Azure Blob storage, die ondersteuning biedt voor de Polybase standaard bereiken.</span><span class="sxs-lookup"><span data-stu-id="e4666-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="e4666-115">In dit artikel leest u hoe Data Factory-Wizard kopiëren gebruiken om u te 1 TB gegevens uit Azure Blob-opslag laden in Azure SQL Data Warehouse in onder 15 minuten op meer dan 1,2 GBps doorvoer.</span><span class="sxs-lookup"><span data-stu-id="e4666-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="e4666-116">In dit artikel bevat stapsgewijze instructies voor het verplaatsen van gegevens naar Azure SQL Data Warehouse met behulp van de Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e4666-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="e4666-117">Raadpleeg voor algemene informatie over de mogelijkheden van Data Factory bij het verplaatsen van gegevens naar/van Azure SQL Data Warehouse [gegevens verplaatsen en naar Azure SQL Data Warehouse met behulp van Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e4666-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="e4666-118">U kunt ook samenstellen pijplijnen met Azure portal, Visual Studio, PowerShell, enzovoort. Zie [zelfstudie: gegevens kopiëren van Azure-Blob naar Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor een snel overzicht met stapsgewijze instructies voor het gebruik van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e4666-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="e4666-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e4666-119">Prerequisites</span></span>
* <span data-ttu-id="e4666-120">Azure Blob Storage: dit experiment maakt gebruik van Azure Blob-opslag (GRS) voor het opslaan van TPC-H testen gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e4666-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="e4666-121">Als u een Azure storage-account niet hebt, ontdek [het maken van een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e4666-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="e4666-122">[TPC-H](http://www.tpc.org/tpch/) gegevens: we gaan TPC-H gebruiken als de tests gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e4666-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="e4666-123">Hiervoor moet u gebruiken `dbgen` uit de werkset TPC-H, die u helpt bij het genereren van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e4666-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="e4666-124">Kunt u de broncode voor downloaden `dbgen` van [TPC extra](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) zelf compileren en downloaden van de gecompileerde binaire van [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="e4666-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="e4666-125">Dbgen.exe uitvoeren met de volgende opdrachten voor het genereren van 1 TB plat bestand voor `lineitem` tabel verspreiding in 10 bestanden:</span><span class="sxs-lookup"><span data-stu-id="e4666-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="e4666-126">…</span><span class="sxs-lookup"><span data-stu-id="e4666-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="e4666-127">Nu de gegenereerde bestanden kopiëren naar Azure-Blob.</span><span class="sxs-lookup"><span data-stu-id="e4666-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="e4666-128">Raadpleeg [gegevens verplaatsen naar en van een on-premises bestandssysteem met behulp van Azure Data Factory](data-factory-onprem-file-system-connector.md) voor hoe dat met ADF-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e4666-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="e4666-129">Azure SQL datawarehouse: dit experiment laadt gegevens in Azure SQL Data Warehouse is gemaakt met 6000 dwu 's</span><span class="sxs-lookup"><span data-stu-id="e4666-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="e4666-130">Raadpleeg [maken van een Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) voor gedetailleerde instructies voor het maken van een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="e4666-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="e4666-131">Als u de beste prestaties van de mogelijke laden in SQL Data Warehouse met Polybase, kiest u maximale aantal Data Warehouse Units (dwu's) zijn toegestaan in de prestatie-instelling, 6000 dwu's.</span><span class="sxs-lookup"><span data-stu-id="e4666-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e4666-132">Bij het laden van een Azure Blob, is het laden van de prestaties van gegevens rechtstreeks evenredig met het aantal dwu's die u op de SQL Data Warehouse configureert:</span><span class="sxs-lookup"><span data-stu-id="e4666-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="e4666-133">Laden van 1 TB in 1.000 duurt DWU SQL Data Warehouse 87 minuten (~ 200 MBps doorvoer) bij het laden van 1 TB in 2.000 DWU SQL Data Warehouse vergt 46 minuten (~ 380 MBps doorvoer) bij het laden van 1 TB in 6000 DWU SQL Data Warehouse duurt 14 minuten (~1.2 GBps doorvoer)</span><span class="sxs-lookup"><span data-stu-id="e4666-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="e4666-134">Als een SQL Data Warehouse maken met 6000 dwu's, de schuifregelaar prestaties helemaal naar rechts:</span><span class="sxs-lookup"><span data-stu-id="e4666-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Schuifregelaar voor prestaties](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="e4666-136">Voor een bestaande database die niet is geconfigureerd met 6000 dwu's, kunt u het schalen met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e4666-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="e4666-137">Navigeer naar de database in Azure-portal en er is een **Scale** knop in de **overzicht** deelvenster wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="e4666-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Knop schaal](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="e4666-139">Klik op de **Scale** knop opent u het volgende deelvenster en klik op de schuifregelaar aan de maximumwaarde **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e4666-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Dialoogvenster schaal](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="e4666-141">Dit experiment gegevens laadt in met behulp van Azure SQL Data Warehouse `xlargerc` bronklasse.</span><span class="sxs-lookup"><span data-stu-id="e4666-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="e4666-142">Als u wilt bereiken best mogelijke doorvoer, kopie moet worden uitgevoerd met behulp van een SQL Data Warehouse-gebruiker die horen bij `xlargerc` bronklasse.</span><span class="sxs-lookup"><span data-stu-id="e4666-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="e4666-143">Meer informatie over hoe dat door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="e4666-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="e4666-144">Tabel doelschema in Azure SQL Data Warehouse-database maken door het uitvoeren van de volgende DDL-instructie:</span><span class="sxs-lookup"><span data-stu-id="e4666-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="e4666-145">Met de vereiste stappen voltooid, zijn er nu klaar om te configureren met de kopieerbewerking met de Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e4666-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="e4666-146">De wizard Kopiëren starten</span><span class="sxs-lookup"><span data-stu-id="e4666-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="e4666-147">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e4666-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e4666-148">Klik op **+ nieuw** vanuit de linkerbovenhoek op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="e4666-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="e4666-149">In de blade **Nieuwe gegevensfactory**:</span><span class="sxs-lookup"><span data-stu-id="e4666-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="e4666-150">Voer **LoadIntoSQLDWDataFactory** voor de **naam**.</span><span class="sxs-lookup"><span data-stu-id="e4666-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="e4666-151">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="e4666-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="e4666-152">Als u de foutmelding: **Data factory-naam 'LoadIntoSQLDWDataFactory' is niet beschikbaar**, wijzig de naam van de gegevensfactory (bijvoorbeeld yournameLoadIntoSQLDWDataFactory) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e4666-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="e4666-153">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="e4666-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="e4666-154">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e4666-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="e4666-155">Voer een van de volgende stappen uit voor de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="e4666-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="e4666-156">Selecteer **Bestaande gebruiken** om een bestaande resourcegroep te selecteren.</span><span class="sxs-lookup"><span data-stu-id="e4666-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="e4666-157">Selecteer **Nieuwe maken** als u een naam voor een resourcegroep wilt typen.</span><span class="sxs-lookup"><span data-stu-id="e4666-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="e4666-158">Selecteer een **locatie** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="e4666-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="e4666-159">Selecteer het selectievakje **Vastmaken aan dashboard** onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="e4666-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="e4666-160">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4666-160">Click **Create**.</span></span>
4. <span data-ttu-id="e4666-161">Wanneer het aanmaken is voltooid, ziet u de blade **Gegevensfactory** zoals op de volgende afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e4666-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Startpagina van de gegevensfactory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="e4666-163">Op de startpagina van de gegevensfactory klikt u op de tegel **Gegevens kopiëren** om de **wizard Kopiëren** te openen.</span><span class="sxs-lookup"><span data-stu-id="e4666-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e4666-164">Als u ziet dat de webbrowser is vastgelopen bij Autoriseren... schakelt u **Cookies van derden en sitegegevens blokkeren** uit, of u laat dit ingeschakeld en u maakt een uitzondering voor **login.microsoftonline.com** en opent u de wizard opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e4666-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="e4666-165">Stap 1: Planning laden van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="e4666-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="e4666-166">De eerste stap is om de gegevens bij het laden van schema te configureren.</span><span class="sxs-lookup"><span data-stu-id="e4666-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="e4666-167">Op de pagina **Eigenschappen**:</span><span class="sxs-lookup"><span data-stu-id="e4666-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="e4666-168">Voer **CopyFromBlobToAzureSqlDataWarehouse** voor **taaknaam**</span><span class="sxs-lookup"><span data-stu-id="e4666-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="e4666-169">Selecteer **eenmaal nu uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="e4666-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="e4666-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-170">Click **Next**.</span></span>  

    ![Wizard voor kopiëren - pagina eigenschappen](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="e4666-172">Stap 2: Een bron configureren</span><span class="sxs-lookup"><span data-stu-id="e4666-172">Step 2: Configure source</span></span>
<span data-ttu-id="e4666-173">Deze sectie leest u de stappen voor het configureren van de bron: Azure Blob met de TPC 1 TB-H regelitem bestanden.</span><span class="sxs-lookup"><span data-stu-id="e4666-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="e4666-174">Selecteer de **Azure Blob Storage** de gegevens opslaan en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Wizard voor kopiëren - pagina van de bron selecteren](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="e4666-176">Vul de verbindingsgegevens voor de Azure Blob storage-account in en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Wizard - informatie van de gegevensbronverbinding kopiëren](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="e4666-178">Kies de **map** met de TPC-H item bestanden regel en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Wizard kopiëren - invoermap selecteren](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="e4666-180">Wanneer u op klikt **volgende**, de instellingen van het bestand-indeling worden automatisch gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="e4666-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="e4666-181">Controleer of het kolomscheidingsteken voor die is ' | 'in plaats van de standaard-komma','.</span><span class="sxs-lookup"><span data-stu-id="e4666-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="e4666-182">Klik op **volgende** nadat u de gegevens hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="e4666-182">Click **Next** after you have previewed the data.</span></span>

    ![Wizard voor kopiëren - bestandsindelingsinstellingen](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="e4666-184">Stap 3: Doel configureren</span><span class="sxs-lookup"><span data-stu-id="e4666-184">Step 3: Configure destination</span></span>
<span data-ttu-id="e4666-185">Deze sectie leest u over het configureren van de bestemming: `lineitem` tabel in de Azure SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="e4666-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="e4666-186">Kies **Azure SQL Data Warehouse** opslaan als het doel en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Wizard voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="e4666-188">Vul in de verbindingsgegevens voor Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e4666-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="e4666-189">Zorg ervoor dat u opgeeft dat de gebruiker die lid is van de rol `xlargerc` (Zie de **vereisten** gedeelte voor meer informatie), en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Wizard - verbindingsgegevens bestemming kopiëren](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="e4666-191">Kies de doeltabel en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-191">Choose the destination table and click **Next**.</span></span>

    ![Wizard - tabel toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="e4666-193">In de pagina Schema-toewijzing, laat u 'Toepassen kolomtoewijzing' optie uitgeschakeld en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="e4666-194">Stap 4: Prestatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="e4666-194">Step 4: Performance settings</span></span>

<span data-ttu-id="e4666-195">**Toestaan van polybase** is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e4666-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="e4666-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e4666-196">Click **Next**.</span></span>

![Wizard - schema toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="e4666-198">Stap 5: Implementeren en controleren van de load-resultaten</span><span class="sxs-lookup"><span data-stu-id="e4666-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="e4666-199">Klik op **voltooien** knop om te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e4666-199">Click **Finish** button to deploy.</span></span>

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="e4666-201">Nadat de implementatie voltooid is, klikt u op `Click here to monitor copy pipeline` voor het bewaken van de kopie voortgang uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e4666-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="e4666-202">Selecteer de kopieerpijplijn die u hebt gemaakt in de **Activiteitsvensters** lijst.</span><span class="sxs-lookup"><span data-stu-id="e4666-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="e4666-204">Vindt u de kopie die details uitvoering van de **activiteit venster Explorer** in het rechterpaneel inclusief gegevensvolume van bron gelezen en geschreven naar de bestemming, duur en de gemiddelde doorvoer voor de verwerking.</span><span class="sxs-lookup"><span data-stu-id="e4666-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="e4666-205">Zoals u in de volgende schermafdruk ziet, duurde 1 TB uit Azure Blob Storage kopiëren naar SQL Data Warehouse 14 minuten, effectief 1,22 GBps doorvoer kan bereiken!</span><span class="sxs-lookup"><span data-stu-id="e4666-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Wizard - geslaagd dialoogvenster kopiëren](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="e4666-207">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="e4666-207">Best practices</span></span>
<span data-ttu-id="e4666-208">Hier volgen enkele aanbevolen procedures voor het uitvoeren van uw Azure SQL Data Warehouse-database:</span><span class="sxs-lookup"><span data-stu-id="e4666-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="e4666-209">Gebruik een grotere bronklasse bij het laden in een GECLUSTERDE COLUMNSTORE-INDEX.</span><span class="sxs-lookup"><span data-stu-id="e4666-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="e4666-210">Voor efficiënter joins, kunt u overwegen hash distributie door een kolom selecteren in plaats van standaard round robin distributie.</span><span class="sxs-lookup"><span data-stu-id="e4666-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="e4666-211">Voor snellere load snelheden, kunt u overwegen heap voor tijdelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4666-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="e4666-212">Statistieken maken als u klaar bent met het laden van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e4666-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="e4666-213">Zie [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4666-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4666-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4666-214">Next steps</span></span>
* <span data-ttu-id="e4666-215">[Data Factory-Wizard kopiëren](data-factory-copy-wizard.md) -in dit artikel bevat informatie over de Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e4666-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="e4666-216">[Prestaties van de activiteit en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md) -in dit artikel bevat de verwijzing prestatiemetingen en prestatieafstemming handleiding.</span><span class="sxs-lookup"><span data-stu-id="e4666-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
