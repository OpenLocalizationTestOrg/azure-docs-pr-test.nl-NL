---
title: Uw gegevens te migreren naar SQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw gegevens naar Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="2dfa7-103">Uw gegevens migreren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-103">Migrate Your Data</span></span>
<span data-ttu-id="2dfa7-104">Gegevens kunnen worden verplaatst van verschillende bronnen in uw SQL Data Warehouse met een aantal verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="2dfa7-105">ADF kopiëren, SSIS en bcp kunnen alle worden gebruikt om dit doel te bereiken.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="2dfa7-106">Echter, als de hoeveelheid gegevens toeneemt moet u bedenken splitsen van het migratieproces in stappen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="2dfa7-107">Hierdoor kunnen u elke stap voor prestaties en herstelmogelijkheden bij een migratie smooth gegevens optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="2dfa7-108">Dit artikel wordt eerst de eenvoudige migratiescenario's van ADF kopiëren, SSIS en bcp.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="2dfa7-109">Vervolgens uiterlijk enigszins dieper in hoe de migratie kan worden geoptimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="2dfa7-110">Azure Data Factory (ADF) kopiëren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="2dfa7-111">[Kopiëren van de ADF] [ ADF Copy] maakt deel uit van [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="2dfa7-112">ADF kopiëren kunt u uw gegevens exporteren naar platte bestanden op de lokale opslag, naar externe platte bestanden die zijn ondergebracht in Azure blob-opslag of rechtstreeks in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="2dfa7-113">Als uw gegevens in platte bestanden begint en vervolgens u eerst moet overzetten naar Azure storage-blob voordat u begint een laden in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="2dfa7-114">Nadat de gegevens worden overgedragen naar Azure blob-opslag kunt u gebruiken [ADF kopiëren] [ ADF Copy] opnieuw om de gegevens in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="2dfa7-115">PolyBase biedt ook een optie voor het laden van de gegevens voor hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="2dfa7-116">Dat betekent dat twee hulpprogramma's voor gebruik in plaats van een.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="2dfa7-117">Als u de beste prestaties moet u PolyBase gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="2dfa7-118">Als u een ervaring één hulpprogramma wilt (en de gegevens niet enorme zijn) is ADF uw antwoord.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="2dfa7-119">HEAD via het volgende artikel voor een groot [ADF voorbeelden][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="2dfa7-120">Integratieservices</span><span class="sxs-lookup"><span data-stu-id="2dfa7-120">Integration Services</span></span>
<span data-ttu-id="2dfa7-121">Integration Services (SSIS) is een krachtige en flexibele extraheren Transform and Load (ETL) hulpprogramma die ondersteuning biedt voor complexe werkstromen, gegevenstransformatie en verschillende opties voor het laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="2dfa7-122">SSIS gebruiken voor gegevens over te dragen naar Azure of als onderdeel van een bredere migratie.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="2dfa7-123">SSIS kunt exporteren naar UTF-8 zonder de bytevolgordemarkering in het bestand.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="2dfa7-124">Als u wilt configureren gebruiken dit moet u eerst het onderdeel afgeleide kolom converteren van de tekengegevens in de gegevensstroom gebruiken de 65001 UTF-8-codetabel.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="2dfa7-125">Zodra de kolommen zijn geconverteerd, moet u de gegevens schrijven naar de plat bestand-doeladapter ervoor te zorgen dat 65001 ook is geselecteerd als de codetabel voor het bestand.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="2dfa7-126">SSIS maakt verbinding met SQL Data Warehouse, net zoals deze verbinding met een SQL Server-implementatie maken wilt.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="2dfa7-127">Uw verbindingen moet echter worden door een ADO.NET-Verbindingsbeheer te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="2dfa7-128">U moet ook zorgt voor het configureren van de 'Gebruik bulksgewijs invoegen indien beschikbaar' instelling doorvoer maximaliseren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="2dfa7-129">Raadpleeg de [ADO.NET-doeladapter] [ ADO.NET destination adapter] artikel voor meer informatie over deze eigenschap</span><span class="sxs-lookup"><span data-stu-id="2dfa7-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="2dfa7-130">Verbinding maken met Azure SQL Data Warehouse met behulp van OLEDB wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="2dfa7-131">Er is bovendien altijd de mogelijkheid om een pakket vanwege problemen met beperking of het netwerk mislukken.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="2dfa7-132">Ontwerp pakketten zodat ze kunnen worden hervat op het moment van mislukt, zonder opnieuw uitvoeren, werkt die vóór de fout is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="2dfa7-133">Raadpleeg voor meer informatie de [SSIS-documentatie][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="2dfa7-134">bcp</span><span class="sxs-lookup"><span data-stu-id="2dfa7-134">bcp</span></span>
<span data-ttu-id="2dfa7-135">BCP is een opdrachtregelprogramma dat is ontworpen voor een plat bestand gegevens importeren en exporteren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="2dfa7-136">Sommige transformatie kan worden uitgevoerd tijdens het exporteren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="2dfa7-137">Eenvoudige transformaties gebruik om uit te voeren een query om te selecteren en de gegevens transformeren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="2dfa7-138">Eenmaal geëxporteerd, kunnen de platte bestanden vervolgens worden geladen rechtstreeks in het doel de SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="2dfa7-139">Het is vaak een goed idee om de transformaties gebruikt tijdens het exporteren van gegevens in een weergave in het bronsysteem inkapselen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="2dfa7-140">Dit zorgt ervoor dat de logica wordt bewaard, en het proces herhaald wordt.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="2dfa7-141">Voordelen van bcp zijn:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="2dfa7-142">Eenvoud.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-142">Simplicity.</span></span> <span data-ttu-id="2dfa7-143">BCP opdrachten zijn eenvoudig te bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="2dfa7-144">Het laadproces is opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-144">Re-startable load process.</span></span> <span data-ttu-id="2dfa7-145">Eenmaal geëxporteerde de belasting kan worden uitgevoerd van een willekeurig aantal malen</span><span class="sxs-lookup"><span data-stu-id="2dfa7-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="2dfa7-146">Beperkingen van bcp zijn:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="2dfa7-147">BCP werkt met gebruikmaking platte bestanden alleen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="2dfa7-148">Deze functie niet samenwerkt met zoals XML- of JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="2dfa7-149">Data transformation mogelijkheden zijn beperkt tot alleen de export-fase en eenvoudige aard zijn</span><span class="sxs-lookup"><span data-stu-id="2dfa7-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="2dfa7-150">BCP is niet aangepast aan robuuste worden bij het laden van gegevens via het internet.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="2dfa7-151">Netwerk instabiliteit kan ertoe leiden dat een fout bij het laden.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="2dfa7-152">BCP is afhankelijk van het schema wordt aanwezig is in de doeldatabase voorafgaand aan de belasting</span><span class="sxs-lookup"><span data-stu-id="2dfa7-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="2dfa7-153">Zie voor meer informatie [gebruikt bcp om gegevens te laden in SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="2dfa7-154">Gegevensmigratie optimaliseren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-154">Optimizing data migration</span></span>
<span data-ttu-id="2dfa7-155">Een migratieproces SQLDW kan worden effectief onderverdeeld in drie afzonderlijke stappen:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="2dfa7-156">Het exporteren van de brongegevens</span><span class="sxs-lookup"><span data-stu-id="2dfa7-156">Export of source data</span></span>
2. <span data-ttu-id="2dfa7-157">Overdracht van gegevens naar Azure</span><span class="sxs-lookup"><span data-stu-id="2dfa7-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="2dfa7-158">In de doeldatabase SQLDW laden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="2dfa7-159">Elke stap kan afzonderlijk worden geoptimaliseerd voor het maken van een robuuste, opnieuw gestart en robuuste migratieproces die optimaliseert de prestaties bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="2dfa7-160">Optimaliseren laden van gegevens</span><span class="sxs-lookup"><span data-stu-id="2dfa7-160">Optimizing data load</span></span>
<span data-ttu-id="2dfa7-161">Kijken naar deze in omgekeerde volgorde voor even; Er is de snelste manier om gegevens te laden met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="2dfa7-162">Optimaliseren voor een laadproces PolyBase plaatst vereisten op de voorgaande stappen is het verstandig om te begrijpen dit vooraf.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="2dfa7-163">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-163">They are:</span></span>

1. <span data-ttu-id="2dfa7-164">Codering van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-164">Encoding of data files</span></span>
2. <span data-ttu-id="2dfa7-165">Indeling van de gegevensbestanden worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="2dfa7-165">Format of data files</span></span>
3. <span data-ttu-id="2dfa7-166">Locatie van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="2dfa7-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="2dfa7-167">Encoding</span></span>
<span data-ttu-id="2dfa7-168">PolyBase vereist-gegevensbestanden UTF-8-of UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="2dfa7-169">Indeling van de gegevensbestanden worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="2dfa7-169">Format of data files</span></span>
<span data-ttu-id="2dfa7-170">PolyBase vereist een vaste rijeinde van \n of nieuwe regel aangeeft.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="2dfa7-171">Uw gegevensbestanden moeten voldoen aan deze standaard.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="2dfa7-172">Er zijn geen beperkingen op tekenreeks- of afsluitingen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="2dfa7-173">U moet voor elke kolom in het bestand als onderdeel van de externe tabel in PolyBase definiëren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="2dfa7-174">Zorg ervoor dat alle geëxporteerde kolommen vereist zijn en dat de typen aan de vereiste normen voldoen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="2dfa7-175">Raadpleeg terug naar de [migreren uw schema] artikel voor informatie over de ondersteunde gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="2dfa7-176">Locatie van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-176">Location of data files</span></span>
<span data-ttu-id="2dfa7-177">SQL Data Warehouse gebruikmaakt van PolyBase uitsluitend laden van gegevens uit Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="2dfa7-178">Als gevolg daarvan kan zijn de gegevens eerst overgebracht naar de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="2dfa7-179">Gegevensoverdracht optimaliseren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-179">Optimizing data transfer</span></span>
<span data-ttu-id="2dfa7-180">Een van de traagste onderdelen van de gegevensmigratie is de overdracht van gegevens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="2dfa7-181">Niet alleen kunt netwerkbandbreedte een probleem kunnen zijn, maar ook netwerk betrouwbaarheid kunt ernstig wordt verstoord uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="2dfa7-182">Gegevens migreren naar Azure is standaard via internet zodat de kans op fouten van overdracht plaatsvinden redelijkerwijs waarschijnlijk zijn.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="2dfa7-183">Deze fouten vereisen echter opnieuw worden verzonden geheel of gedeeltelijk.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="2dfa7-184">Gelukkig hebt u verschillende mogelijkheden voor het verbeteren van de snelheid en herstelmogelijkheden van dit proces:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="2dfa7-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="2dfa7-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="2dfa7-186">U kunt overwegen om [ExpressRoute] [ ExpressRoute] om de overdracht te versnellen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="2dfa7-187">[ExpressRoute] [ ExpressRoute] biedt een particuliere verbinding met Azure zodat de verbinding niet via het openbare internet gaat.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="2dfa7-188">Dit is geen een verplichte stap.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="2dfa7-189">Echter, het verbeteren van doorvoer wanneer gegevens worden gepusht naar Azure uit een on-premises of CO-locatiefaciliteit.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="2dfa7-190">De voordelen van het gebruik van [ExpressRoute] [ ExpressRoute] zijn:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="2dfa7-191">Hogere mate van betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="2dfa7-191">Increased reliability</span></span>
2. <span data-ttu-id="2dfa7-192">Snellere netwerksnelheid</span><span class="sxs-lookup"><span data-stu-id="2dfa7-192">Faster network speed</span></span>
3. <span data-ttu-id="2dfa7-193">Lagere netwerklatentie</span><span class="sxs-lookup"><span data-stu-id="2dfa7-193">Lower network latency</span></span>
4. <span data-ttu-id="2dfa7-194">hogere netwerkbeveiliging</span><span class="sxs-lookup"><span data-stu-id="2dfa7-194">higher network security</span></span>

<span data-ttu-id="2dfa7-195">[ExpressRoute] [ ExpressRoute] is handig voor een aantal scenario's; niet alleen de migratie.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="2dfa7-196">Geïnteresseerd?</span><span class="sxs-lookup"><span data-stu-id="2dfa7-196">Interested?</span></span> <span data-ttu-id="2dfa7-197">Ga voor meer informatie en prijzen Ga naar de [ExpressRoute-documentatie][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="2dfa7-198">Azure Import- en Export-Service</span><span class="sxs-lookup"><span data-stu-id="2dfa7-198">Azure Import and Export Service</span></span>
<span data-ttu-id="2dfa7-199">De Azure importeren en exporteren-Service is een overdrachtsproces gegevens is ontworpen voor grote (GB ++) voor grootschalige (TB ++) de overdracht van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="2dfa7-200">Dit omvat het schrijven van uw gegevens naar de schijven en ze verzenden naar een Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="2dfa7-201">Inhoud van de schijf wordt vervolgens in Azure Storage-Blobs namens jou worden geladen.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="2dfa7-202">Een weergave op hoog niveau van het importeerproces voor het exporteren is als volgt:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="2dfa7-203">Een Azure Blob Storage-container voor het ontvangen van de gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="2dfa7-204">Uw gegevens worden geëxporteerd naar de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="2dfa7-204">Export your data to local storage</span></span>
3. <span data-ttu-id="2dfa7-205">Kopieer de gegevens naar 3.5 inch SATA III-II harde schijven met behulp van de [Azure Import/Export hulpprogramma]</span><span class="sxs-lookup"><span data-stu-id="2dfa7-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="2dfa7-206">Maken van een Import-taak met de Azure importeren en exporteren Service bieden de journaal-bestanden die wordt geproduceerd door de [Azure hulpprogramma voor importeren/exporteren]</span><span class="sxs-lookup"><span data-stu-id="2dfa7-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="2dfa7-207">Verzenden van de schijven uw aangewezen Azure-Datacenter</span><span class="sxs-lookup"><span data-stu-id="2dfa7-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="2dfa7-208">Uw gegevens worden overgedragen naar uw Azure Blob Storage-container</span><span class="sxs-lookup"><span data-stu-id="2dfa7-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="2dfa7-209">De gegevens in SQLDW met PolyBase laden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="2dfa7-210">[AZCopy][AZCopy] hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="2dfa7-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="2dfa7-211">De [AZCopy][AZCopy] hulpprogramma is een uitstekend hulpprogramma voor het ophalen van de gegevens die binnenkomen in Azure Storage-Blobs.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="2dfa7-212">Het is ontworpen voor kleine (MB ++) voor zeer grote (GB ++) gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="2dfa7-213">[AZCopy] is ontworpen voor een goede robuuste doorvoer bij de overdracht van gegevens naar Azure en daarom is een uitstekende keuze is voor de stap van de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="2dfa7-214">Eenmaal overgebrachte kunt u de gegevens met PolyBase in SQL Data Warehouse laden.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="2dfa7-215">U kunt ook AZCopy opnemen in uw SSIS-pakketten met behulp van een 'Proces uitvoeren'.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="2dfa7-216">Voor het gebruik van AZCopy moet u eerst te downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="2dfa7-217">Er is een [productieversie] [ production version] en een [preview-versie] [ preview version] beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="2dfa7-218">Als u wilt uploaden van een bestand van het bestandssysteem moet u een opdracht zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="2dfa7-219">Een samenvatting van het proces op hoog niveau kan worden:</span><span class="sxs-lookup"><span data-stu-id="2dfa7-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="2dfa7-220">Een Azure-opslag-blob-container voor het ontvangen van de gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="2dfa7-221">Uw gegevens worden geëxporteerd naar de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="2dfa7-221">Export your data to local storage</span></span>
3. <span data-ttu-id="2dfa7-222">AZCopy uw gegevens in de Azure Blob Storage-container</span><span class="sxs-lookup"><span data-stu-id="2dfa7-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="2dfa7-223">De gegevens laden in SQL Data Warehouse met PolyBase</span><span class="sxs-lookup"><span data-stu-id="2dfa7-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="2dfa7-224">Volledige documentatie beschikbaar: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="2dfa7-225">Optimaliseren gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="2dfa7-225">Optimizing data export</span></span>
<span data-ttu-id="2dfa7-226">Naast ervoor te zorgen dat de export aan de voorschriften door PolyBase voldoet kunt u ook zoeken naar de uitvoer van de gegevens voor het verbeteren van het proces verder optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="2dfa7-227">Gegevenscompressie</span><span class="sxs-lookup"><span data-stu-id="2dfa7-227">Data compression</span></span>
<span data-ttu-id="2dfa7-228">Gzip gecomprimeerde gegevens kan worden gelezen door PolyBase.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="2dfa7-229">Als u uw gegevens naar de gzip-bestanden te comprimeren wordt u de hoeveelheid gegevens die via het netwerk wordt gepusht minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="2dfa7-230">Meerdere bestanden</span><span class="sxs-lookup"><span data-stu-id="2dfa7-230">Multiple files</span></span>
<span data-ttu-id="2dfa7-231">Grote tabellen in verschillende bestanden splitsen niet alleen kan worden verbeterd export snelheid, maar ook met overdracht re-startability en de algehele beheerbaarheid van de gegevens eenmaal in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="2dfa7-232">Een van de vele nice functies van PolyBase is Hiermee worden de bestanden naar de map lezen en behandelen als een tabel.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="2dfa7-233">Daarom een goed idee om te isoleren van de bestanden voor elke tabel in de eigen map.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="2dfa7-234">PolyBase biedt ook ondersteuning voor een functie die bekend als 'recursieve map traversal'.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="2dfa7-235">U kunt deze functie gebruiken voor het verder verbeteren van de organisatie van de geëxporteerde gegevens voor het verbeteren van uw gegevens beheren.</span><span class="sxs-lookup"><span data-stu-id="2dfa7-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="2dfa7-236">Zie voor meer informatie over het laden van gegevens met PolyBase, [gebruik PolyBase gegevens laadt in SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dfa7-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2dfa7-237">Next steps</span></span>
<span data-ttu-id="2dfa7-238">Zie voor meer informatie over de migratie [migreren van uw oplossing naar SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="2dfa7-239">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="2dfa7-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
