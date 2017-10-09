---
title: aaaLoad gegevens in Azure SQL Data Warehouse | Microsoft Docs
description: Meer informatie over Hallo algemene scenario's om gegevens te laden in SQL Data Warehouse. Deze omvatten het gebruik van PolyBase, Azure blob-opslag, platte bestanden en back-ups van schijf. U kunt ook hulpprogramma's van derden gebruiken.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="bfb68-105">Gegevens laden in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bfb68-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bfb68-106">Een samenvatting van Hallo scenario opties en aanbevelingen voor het laden van gegevens in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="bfb68-107">Hallo lastigste onderdeel van het laden van gegevens is meestal Hallo gegevens voorbereiden voor Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="bfb68-108">Azure vereenvoudigt laden met behulp van Azure blob-opslag als algemene gegevensopslag voor een groot aantal Hallo services en met behulp van Azure Data Factory Hallo tooorchestrate communicatie en gegevens die verkeer tussen Azure-services.</span><span class="sxs-lookup"><span data-stu-id="bfb68-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="bfb68-109">Deze processen worden geïntegreerd met PolyBase-technologie die gebruikmaakt van massively parallel verwerken (MPP) tooload gegevens parallel uit Azure blob storage in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="bfb68-110">Zie voor zelfstudies die voorbeelddatabases worden geladen, [laden voorbeelddatabases][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="bfb68-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="bfb68-111">Laden van Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="bfb68-111">Load from Azure blob storage</span></span>
<span data-ttu-id="bfb68-112">Hallo snelste manier tooimport gegevens in SQL Data Warehouse zijn toouse PolyBase tooload gegevens uit Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="bfb68-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="bfb68-113">PolyBase gebruikt SQL Data Warehouse van verwerking massively parallel (MPP) ontwerp tooload gegevens parallel uit Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="bfb68-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="bfb68-114">toouse PolyBase, kunt u T-SQL-opdrachten of een Azure Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="bfb68-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="bfb68-115">1. Gebruik PolyBase en T-SQL</span><span class="sxs-lookup"><span data-stu-id="bfb68-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="bfb68-116">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-116">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-117">Uw gegevens tooAzure blob-opslag- of Azure Data Lake Store verplaatsen en sla het in tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="bfb68-118">Externe objecten in SQL Data Warehouse toodefine Hallo locatie en indeling van Hallo gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="bfb68-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="bfb68-119">Een T-SQL-opdracht tooload Hallo gegevens parallel worden uitgevoerd in een nieuwe databasetabel.</span><span class="sxs-lookup"><span data-stu-id="bfb68-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="bfb68-120">Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="bfb68-121">2. Azure Data Factory gebruiken</span><span class="sxs-lookup"><span data-stu-id="bfb68-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="bfb68-122">U kunt een Azure Data Factory-pijplijn die gebruikmaakt van PolyBase tooload gegevens uit Azure blob storage in SQL Data Warehouse maken voor een eenvoudigere manier toouse PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bfb68-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="bfb68-123">Dit is snel tooconfigure omdat u niet toodefine Hallo T-SQL-objecten hoeft.</span><span class="sxs-lookup"><span data-stu-id="bfb68-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="bfb68-124">Als u tooquery Hallo externe gegevens zonder dat u deze importeert, gebruikt u de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="bfb68-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="bfb68-125">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-125">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-126">De gegevens tooAzure blob-opslag verplaatsen en sla het in tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="bfb68-127">Azure Data Factory ondersteunt momenteel geen ADLS-connectiviteit met PolyBase).</span><span class="sxs-lookup"><span data-stu-id="bfb68-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="bfb68-128">Een Azure Data Factory pijplijn tooingest Hallo gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="bfb68-129">Hallo PolyBase-optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="bfb68-130">Plannen en uitvoeren van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="bfb68-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="bfb68-131">Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="bfb68-132">Laden van SQL Server</span><span class="sxs-lookup"><span data-stu-id="bfb68-132">Load from SQL Server</span></span>
<span data-ttu-id="bfb68-133">tooload gegevens uit SQL Server-tooSQL Data Warehouse Integration Services (SSIS), kunt u zet platte bestanden of schijven tooMicrosoft worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="bfb68-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="bfb68-134">Lees verder toosee een samenvatting van Hallo verschillende processen en koppelingen tootutorials laden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="bfb68-135">tooplan volledige gegevens migreren van SQL Server-tooSQL Data Warehouse, Zie Hallo [Migratieoverzicht][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="bfb68-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="bfb68-136">Integratieservices (SSIS) gebruiken</span><span class="sxs-lookup"><span data-stu-id="bfb68-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="bfb68-137">Als u al Integration Services (SSIS) pakketten tooload in SQL Server gebruikt, kunt u uw pakketten toouse SQL Server Hallo bron-en SQL Data Warehouse als bestemming Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="bfb68-138">Dit is snel en eenvoudig toodo en is een goede keuze als u niet toomigrate uw laden probeert toouse gegevens die al in de cloud Hallo verwerken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="bfb68-139">Hallo afweging is Hallo load zijn lager dan het gebruik van PolyBase omdat deze SSIS geen Hallo load parallel voert.</span><span class="sxs-lookup"><span data-stu-id="bfb68-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="bfb68-140">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-140">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-141">De Integration Services pakket toopoint toohello SQL Server-exemplaar voor Hallo bron en Hallo SQL Data Warehouse-database voor de bestemming Hallo herzien.</span><span class="sxs-lookup"><span data-stu-id="bfb68-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="bfb68-142">Migreer uw schema tooSQL datawarehouse, indien deze nog niet er is.</span><span class="sxs-lookup"><span data-stu-id="bfb68-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="bfb68-143">Hallo-toewijzing wijzigen in uw pakketten gebruiken alleen Hallo gegevenstypen die worden ondersteund door SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="bfb68-144">Plannen en uitvoeren van Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="bfb68-144">Schedule and run hello package.</span></span>

<span data-ttu-id="bfb68-145">Zie voor een zelfstudie [laden van gegevens uit SQL Server-tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="bfb68-146">AZCopy (aanbevolen voor < 10 TB gegevens) gebruiken</span><span class="sxs-lookup"><span data-stu-id="bfb68-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="bfb68-147">Als de gegevensgrootte van uw < 10 TB is, kunt u Hallo gegevens exporteren uit SQL Server tooflat bestanden kopiëren Hallo bestanden tooAzure blob-opslag en gebruik vervolgens PolyBase tooload Hallo gegevens in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bfb68-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="bfb68-148">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-148">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-149">Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="bfb68-150">Hallo AZCopy-opdrachtregelprogramma toocopy gegevens uit platte bestanden tooAzure blob storage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="bfb68-151">Gebruik tooload PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="bfb68-152">Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="bfb68-153">Gebruikt bcp</span><span class="sxs-lookup"><span data-stu-id="bfb68-153">Use bcp</span></span>
<span data-ttu-id="bfb68-154">Als u een kleine hoeveelheid gegevens hebt kunt u bcp tooload rechtstreeks in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="bfb68-155">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-155">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-156">Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="bfb68-157">Gebruikt bcp tooload gegevens uit platte bestanden rechtstreeks tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="bfb68-158">Zie voor een zelfstudie [laden van gegevens uit SQL Server-tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="bfb68-159">Gebruik voor importeren/exporteren (aanbevolen voor > 10 TB gegevens)</span><span class="sxs-lookup"><span data-stu-id="bfb68-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="bfb68-160">Als de gegevensomvang van uw > 10 TB is en u toomove wilt het tooAzure, het is raadzaam dat u ons schijf verzend- [voor importeren/exporteren][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="bfb68-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="bfb68-161">Samenvatting van het laadproces</span><span class="sxs-lookup"><span data-stu-id="bfb68-161">Summary of loading process</span></span>

1. <span data-ttu-id="bfb68-162">Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat bestanden op naar schijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="bfb68-163">Hallo schijven tooMicrosoft verzenden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="bfb68-164">Microsoft laadt hello gegevens in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bfb68-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="bfb68-165">Laden van HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfb68-165">Load from HDInsight</span></span>
<span data-ttu-id="bfb68-166">Laden van gegevens uit HDInsight met PolyBase biedt ondersteuning voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfb68-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="bfb68-167">Hallo-proces is hetzelfde als het laden van gegevens uit Azure Blob Storage - met PolyBase tooconnect tooHDInsight tooload gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfb68-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="bfb68-168">1. Gebruik PolyBase en T-SQL</span><span class="sxs-lookup"><span data-stu-id="bfb68-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="bfb68-169">Overzicht van het laadproces:</span><span class="sxs-lookup"><span data-stu-id="bfb68-169">Summary of loading process:</span></span>

1. <span data-ttu-id="bfb68-170">Uw tooHDInsight gegevens verplaatsen en op te slaan in tekstbestanden, ORC of parketvloeren-indeling.</span><span class="sxs-lookup"><span data-stu-id="bfb68-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="bfb68-171">Externe objecten in SQL Data Warehouse toodefine Hallo locatie en indeling van Hallo gegevens configureren.</span><span class="sxs-lookup"><span data-stu-id="bfb68-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="bfb68-172">Een T-SQL-opdracht tooload Hallo gegevens parallel worden uitgevoerd in een nieuwe databasetabel.</span><span class="sxs-lookup"><span data-stu-id="bfb68-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="bfb68-173">Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="bfb68-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="bfb68-174">Aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="bfb68-174">Recommendations</span></span>
<span data-ttu-id="bfb68-175">Veel van onze partners hebben bij het laden van oplossingen.</span><span class="sxs-lookup"><span data-stu-id="bfb68-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="bfb68-176">toofind meer, een overzicht van onze [oplossingspartners][solution partners].</span><span class="sxs-lookup"><span data-stu-id="bfb68-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="bfb68-177">Als uw gegevens afkomstig is van een niet-relationele bron en u wilt dat deze in SQL Data Warehouse u tooload moet tootransform in rijen en kolommen voordat u het laden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="bfb68-178">Hallo getransformeerd gegevens hoeft niet toobe opgeslagen in een database, deze kan worden opgeslagen in tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="bfb68-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="bfb68-179">Statistieken maken voor zojuist geladen gegevens.</span><span class="sxs-lookup"><span data-stu-id="bfb68-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="bfb68-180">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="bfb68-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="bfb68-181">In de volgorde tooget Hallo optimale prestaties van uw query's is het belangrijk toocreate statistieken voor alle kolommen van alle tabellen na Hallo eerst laden of belangrijke wijzigingen plaatsvinden in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="bfb68-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="bfb68-182">Zie voor meer informatie [statistieken][Statistics].</span><span class="sxs-lookup"><span data-stu-id="bfb68-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfb68-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfb68-183">Next steps</span></span>
<span data-ttu-id="bfb68-184">Zie voor meer tips voor het ontwikkeling Hallo [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="bfb68-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
