---
title: aaaMigrate uw gegevens tooSQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw gegevens tooAzure SQL Data Warehouse om oplossingen te ontwikkelen.
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
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="f4765-103">Uw gegevens migreren</span><span class="sxs-lookup"><span data-stu-id="f4765-103">Migrate Your Data</span></span>
<span data-ttu-id="f4765-104">Gegevens kunnen worden verplaatst van verschillende bronnen in uw SQL Data Warehouse met een aantal verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="f4765-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="f4765-105">Kopiëren van de ADF, SSIS en bcp kan alle gebruikte tooachieve dit doel.</span><span class="sxs-lookup"><span data-stu-id="f4765-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="f4765-106">Echter, als Hallo hoeveelheid gegevens toeneemt moet u bedenken Hallo migratieproces in stappen op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="f4765-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="f4765-107">Hierdoor kunnen u Hallo kans toooptimize elke stap voor prestaties en herstelmogelijkheden tooensure een smooth gegevensmigratie.</span><span class="sxs-lookup"><span data-stu-id="f4765-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="f4765-108">Dit artikel wordt eerst Hallo eenvoudige migratiescenario's van ADF kopiëren, SSIS en bcp.</span><span class="sxs-lookup"><span data-stu-id="f4765-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="f4765-109">Vervolgens uiterlijk enigszins dieper in hoe Hallo migratie kan worden geoptimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="f4765-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="f4765-110">Azure Data Factory (ADF) kopiëren</span><span class="sxs-lookup"><span data-stu-id="f4765-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="f4765-111">[Kopiëren van de ADF] [ ADF Copy] maakt deel uit van [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="f4765-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="f4765-112">U kunt ADF kopiëren tooexport tooflat gegevensbestanden die zich op de lokale opslag tooremote platte bestanden bewaard in Azure blob-opslag of rechtstreeks in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4765-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="f4765-113">Als uw gegevens in platte bestanden begint, dan u eerst tootransfer moet het storage-blob tooAzure voordat u begint een laden in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4765-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="f4765-114">Zodra het Hallo-gegevens worden overgedragen naar Azure blob-opslag kunt u toouse [ADF kopiëren] [ ADF Copy] opnieuw toopush Hallo gegevens in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4765-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="f4765-115">PolyBase biedt ook de optie voor het laden van gegevens Hallo hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="f4765-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="f4765-116">Dat betekent dat twee hulpprogramma's voor gebruik in plaats van een.</span><span class="sxs-lookup"><span data-stu-id="f4765-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="f4765-117">Als u de beste prestaties Hallo moet u PolyBase gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f4765-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="f4765-118">Als u een ervaring één hulpprogramma wilt (en Hallo gegevens niet enorme zijn) is ADF uw antwoord.</span><span class="sxs-lookup"><span data-stu-id="f4765-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="f4765-119">Via het volgende artikel voor een groot toohello HEAD [ADF voorbeelden][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="f4765-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="f4765-120">Integratieservices</span><span class="sxs-lookup"><span data-stu-id="f4765-120">Integration Services</span></span>
<span data-ttu-id="f4765-121">Integration Services (SSIS) is een krachtige en flexibele extraheren Transform and Load (ETL) hulpprogramma die ondersteuning biedt voor complexe werkstromen, gegevenstransformatie en verschillende opties voor het laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f4765-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="f4765-122">SSIS toosimply overdracht gegevens tooAzure gebruiken of als onderdeel van een bredere migratie.</span><span class="sxs-lookup"><span data-stu-id="f4765-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="f4765-123">SSIS kunt tooUTF-8 zonder Hallo bytevolgordemarkering in Hallo-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="f4765-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="f4765-124">Dit moet u eerst hello gebruiken kolom onderdeel tooconvert Hallo-tekengegevens in afgeleide tooconfigure Hallo stroom toouse Hallo 65001 UTF-8 code gegevenspagina.</span><span class="sxs-lookup"><span data-stu-id="f4765-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="f4765-125">Zodra het Hallo-kolommen zijn geconverteerd, schrijf Hallo gegevens toohello plat bestand bestemming adapter ervoor te zorgen dat 65001 ook is geselecteerd als Hallo codetabel voor Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f4765-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="f4765-126">SSIS verbindt tooSQL Data Warehouse, net zoals SQL Server-implementatie tooa verbinding wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4765-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="f4765-127">Uw verbindingen moet echter toobe met een ADO.NET-Verbindingsbeheer.</span><span class="sxs-lookup"><span data-stu-id="f4765-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="f4765-128">U moet ook behandelen tooconfigure Hallo 'Gebruik bulksgewijs invoegen indien beschikbaar' instelling toomaximize doorvoer.</span><span class="sxs-lookup"><span data-stu-id="f4765-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="f4765-129">Raadpleeg toohello [ADO.NET-doeladapter] [ ADO.NET destination adapter] artikel toolearn meer over deze eigenschap</span><span class="sxs-lookup"><span data-stu-id="f4765-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="f4765-130">Verbinding maken met tooAzure SQL Data Warehouse met behulp van OLEDB wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f4765-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="f4765-131">Bovendien is er altijd Hallo kans dat een pakket mislukt, mogelijk vanwege problemen met toothrottling of netwerk.</span><span class="sxs-lookup"><span data-stu-id="f4765-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="f4765-132">Ontwerp pakketten zodat ze kunnen worden hervat op Hallo storingspunt, zonder opnieuw uitvoeren, werkt die vóór de fout Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f4765-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="f4765-133">Raadpleeg voor meer informatie Hallo [SSIS-documentatie][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="f4765-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="f4765-134">bcp</span><span class="sxs-lookup"><span data-stu-id="f4765-134">bcp</span></span>
<span data-ttu-id="f4765-135">BCP is een opdrachtregelprogramma dat is ontworpen voor een plat bestand gegevens importeren en exporteren.</span><span class="sxs-lookup"><span data-stu-id="f4765-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="f4765-136">Sommige transformatie kan worden uitgevoerd tijdens het exporteren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f4765-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="f4765-137">eenvoudige transformaties tooperform gebruik van een query-tooselect en Hallo gegevens transformeren.</span><span class="sxs-lookup"><span data-stu-id="f4765-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="f4765-138">Eenmaal geëxporteerd, kunnen Hallo platte bestanden rechtstreeks in Hallo doel Hallo SQL Data Warehouse-database worden geladen.</span><span class="sxs-lookup"><span data-stu-id="f4765-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="f4765-139">Het is vaak een goed idee tooencapsulate Hallo transformaties gebruikt tijdens de gegevens in een weergave in het bronsysteem Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="f4765-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="f4765-140">Dit zorgt ervoor dat Hallo logica wordt bewaard en Hallo-proces herhaald wordt.</span><span class="sxs-lookup"><span data-stu-id="f4765-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="f4765-141">Voordelen van bcp zijn:</span><span class="sxs-lookup"><span data-stu-id="f4765-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="f4765-142">Eenvoud.</span><span class="sxs-lookup"><span data-stu-id="f4765-142">Simplicity.</span></span> <span data-ttu-id="f4765-143">BCP-opdrachten zijn eenvoudige toobuild en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f4765-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="f4765-144">Het laadproces is opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="f4765-144">Re-startable load process.</span></span> <span data-ttu-id="f4765-145">Eenmaal geëxporteerde Hallo load mag een onbeperkt aantal keren uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f4765-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="f4765-146">Beperkingen van bcp zijn:</span><span class="sxs-lookup"><span data-stu-id="f4765-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="f4765-147">BCP werkt met gebruikmaking platte bestanden alleen.</span><span class="sxs-lookup"><span data-stu-id="f4765-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="f4765-148">Deze functie niet samenwerkt met zoals XML- of JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="f4765-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="f4765-149">Data transformation mogelijkheden zijn beperkt toohello export alleen Faseren en eenvoudige aard</span><span class="sxs-lookup"><span data-stu-id="f4765-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="f4765-150">BCP is niet robuust van aangepast toobe bij het laden van gegevens via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4765-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="f4765-151">Netwerk instabiliteit kan ertoe leiden dat een fout bij het laden.</span><span class="sxs-lookup"><span data-stu-id="f4765-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="f4765-152">BCP is afhankelijk van Hallo schema aanwezig zijn in Hallo doel database voorafgaande toohello laden</span><span class="sxs-lookup"><span data-stu-id="f4765-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="f4765-153">Zie voor meer informatie [bcp tooload gegevens worden gebruikt in SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4765-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="f4765-154">Gegevensmigratie optimaliseren</span><span class="sxs-lookup"><span data-stu-id="f4765-154">Optimizing data migration</span></span>
<span data-ttu-id="f4765-155">Een migratieproces SQLDW kan worden effectief onderverdeeld in drie afzonderlijke stappen:</span><span class="sxs-lookup"><span data-stu-id="f4765-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="f4765-156">Het exporteren van de brongegevens</span><span class="sxs-lookup"><span data-stu-id="f4765-156">Export of source data</span></span>
2. <span data-ttu-id="f4765-157">Overdracht van gegevens tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4765-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="f4765-158">In de doeldatabase SQLDW Hallo laden</span><span class="sxs-lookup"><span data-stu-id="f4765-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="f4765-159">Elke stap kan worden afzonderlijk geoptimaliseerde toocreate een robuuste, opnieuw gestart en robuuste migratieproces die optimaliseert de prestaties bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="f4765-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="f4765-160">Optimaliseren laden van gegevens</span><span class="sxs-lookup"><span data-stu-id="f4765-160">Optimizing data load</span></span>
<span data-ttu-id="f4765-161">Kijken naar deze in omgekeerde volgorde voor even; Er is een Hallo snelste manier tooload gegevens met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4765-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="f4765-162">Optimaliseren voor een PolyBase laadproces wordt geplaatst vereisten op de vorige stappen dus is het beste toounderstand dit Hallo vooraf.</span><span class="sxs-lookup"><span data-stu-id="f4765-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="f4765-163">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="f4765-163">They are:</span></span>

1. <span data-ttu-id="f4765-164">Codering van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="f4765-164">Encoding of data files</span></span>
2. <span data-ttu-id="f4765-165">Indeling van de gegevensbestanden worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="f4765-165">Format of data files</span></span>
3. <span data-ttu-id="f4765-166">Locatie van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="f4765-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="f4765-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="f4765-167">Encoding</span></span>
<span data-ttu-id="f4765-168">PolyBase vereist gegevens bestanden toobe UTF-8- of UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="f4765-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="f4765-169">Indeling van de gegevensbestanden worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="f4765-169">Format of data files</span></span>
<span data-ttu-id="f4765-170">PolyBase vereist een vaste rijeinde van \n of nieuwe regel aangeeft.</span><span class="sxs-lookup"><span data-stu-id="f4765-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="f4765-171">Uw gegevensbestanden moeten toothis standaard voldoen.</span><span class="sxs-lookup"><span data-stu-id="f4765-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="f4765-172">Er zijn geen beperkingen op tekenreeks- of afsluitingen.</span><span class="sxs-lookup"><span data-stu-id="f4765-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="f4765-173">Hebt u toodefine voor elke kolom in Hallo-bestand als onderdeel van de externe tabel in PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4765-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="f4765-174">Zorg ervoor dat alle geëxporteerde kolommen vereist zijn en dat Hallo typen toohello vereist standaarden voldoen.</span><span class="sxs-lookup"><span data-stu-id="f4765-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="f4765-175">Raadpleeg terug toohello [migreren uw schema] artikel voor informatie over de ondersteunde gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="f4765-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="f4765-176">Locatie van gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="f4765-176">Location of data files</span></span>
<span data-ttu-id="f4765-177">SQL Data Warehouse gebruikt uitsluitend PolyBase tooload gegevens uit Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f4765-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="f4765-178">Als gevolg daarvan kan moet Hallo gegevens eerst overgedragen naar de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="f4765-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="f4765-179">Gegevensoverdracht optimaliseren</span><span class="sxs-lookup"><span data-stu-id="f4765-179">Optimizing data transfer</span></span>
<span data-ttu-id="f4765-180">Een van de traagste onderdelen van de gegevensmigratie Hallo is Hallo overdracht van Hallo gegevens tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f4765-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="f4765-181">Niet alleen kunt netwerkbandbreedte een probleem kunnen zijn, maar ook netwerk betrouwbaarheid kunt ernstig wordt verstoord uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f4765-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="f4765-182">Standaard is migreren gegevens tooAzure via internet zodat kans op fouten van overdracht plaatsvinden redelijkerwijs waarschijnlijk Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4765-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="f4765-183">Deze fouten vereisen echter gegevens toobe opnieuw verzonden geheel of gedeeltelijk.</span><span class="sxs-lookup"><span data-stu-id="f4765-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="f4765-184">Gelukkig hebt u verschillende opties tooimprove Hallo snelheid en herstelmogelijkheden van dit proces:</span><span class="sxs-lookup"><span data-stu-id="f4765-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="f4765-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="f4765-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="f4765-186">U kunt met behulp van tooconsider [ExpressRoute] [ ExpressRoute] toospeed up Hallo overdracht.</span><span class="sxs-lookup"><span data-stu-id="f4765-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="f4765-187">[ExpressRoute] [ ExpressRoute] biedt u met een particuliere verbinding tot stand gebrachte tooAzure zodat Hallo verbinding verloopt niet via Hallo openbare internet.</span><span class="sxs-lookup"><span data-stu-id="f4765-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="f4765-188">Dit is geen een verplichte stap.</span><span class="sxs-lookup"><span data-stu-id="f4765-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="f4765-189">Echter het verbeteren van doorvoer wanneer tooAzure gegevens worden gepusht uit een on-premises of CO-locatiefaciliteit.</span><span class="sxs-lookup"><span data-stu-id="f4765-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="f4765-190">voordelen van het gebruik van Hallo [ExpressRoute] [ ExpressRoute] zijn:</span><span class="sxs-lookup"><span data-stu-id="f4765-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="f4765-191">Hogere mate van betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="f4765-191">Increased reliability</span></span>
2. <span data-ttu-id="f4765-192">Snellere netwerksnelheid</span><span class="sxs-lookup"><span data-stu-id="f4765-192">Faster network speed</span></span>
3. <span data-ttu-id="f4765-193">Lagere netwerklatentie</span><span class="sxs-lookup"><span data-stu-id="f4765-193">Lower network latency</span></span>
4. <span data-ttu-id="f4765-194">hogere netwerkbeveiliging</span><span class="sxs-lookup"><span data-stu-id="f4765-194">higher network security</span></span>

<span data-ttu-id="f4765-195">[ExpressRoute] [ ExpressRoute] is handig voor een aantal scenario's; niet alleen Hallo migratie.</span><span class="sxs-lookup"><span data-stu-id="f4765-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="f4765-196">Geïnteresseerd?</span><span class="sxs-lookup"><span data-stu-id="f4765-196">Interested?</span></span> <span data-ttu-id="f4765-197">Bezoek voor meer informatie en neem prijzen Hallo [ExpressRoute-documentatie][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="f4765-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="f4765-198">Azure Import- en Export-Service</span><span class="sxs-lookup"><span data-stu-id="f4765-198">Azure Import and Export Service</span></span>
<span data-ttu-id="f4765-199">Hello is Azure importeren en exporteren Service een overdrachtsproces gegevens is ontworpen voor grote (GB ++) toomassive (TB ++) overdrachten van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4765-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="f4765-200">Dit omvat het schrijven van uw gegevens toodisks en het verzenden tooan Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="f4765-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="f4765-201">de inhoud van de schijf Hello wordt vervolgens in Azure Storage-Blobs namens jou worden geladen.</span><span class="sxs-lookup"><span data-stu-id="f4765-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="f4765-202">Een weergave op hoog niveau van Hallo importeren exportproces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f4765-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="f4765-203">Een Azure Blob Storage-container tooreceive Hallo gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="f4765-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="f4765-204">De opslag van uw gegevens toolocal exporteren</span><span class="sxs-lookup"><span data-stu-id="f4765-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="f4765-205">Hallo gegevens too3.5 inch SATA III-II harde schijven met Hallo [Azure Import/Export Tool] kopiëren</span><span class="sxs-lookup"><span data-stu-id="f4765-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="f4765-206">Maken van een Import-taak met hello Azure Import- en exporteren Service bieden Hallo journaal-bestanden die wordt geproduceerd door Hallo [Azure Import/Export Tool]</span><span class="sxs-lookup"><span data-stu-id="f4765-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="f4765-207">Hallo schijven uw aangewezen Azure-Datacenter verzenden</span><span class="sxs-lookup"><span data-stu-id="f4765-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="f4765-208">Uw gegevens zijn overgedragen tooyour Azure Blob Storage-container</span><span class="sxs-lookup"><span data-stu-id="f4765-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="f4765-209">Hallo gegevens laden in SQLDW met PolyBase</span><span class="sxs-lookup"><span data-stu-id="f4765-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="f4765-210">[AZCopy][AZCopy] hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="f4765-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="f4765-211">Hallo [AZCopy][AZCopy] hulpprogramma is een uitstekend hulpprogramma voor het ophalen van de gegevens die binnenkomen in Azure Storage-Blobs.</span><span class="sxs-lookup"><span data-stu-id="f4765-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="f4765-212">Is bedoeld voor kleine (MB ++) toovery grote (GB ++) gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="f4765-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="f4765-213">[AZCopy] ook goed robuuste doorvoer ontworpen tooprovide is opgetreden bij het overbrengen van gegevens tooAzure en daarom is een ideale keuze voor Hallo gegevensoverdracht stap.</span><span class="sxs-lookup"><span data-stu-id="f4765-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="f4765-214">Eenmaal overgebrachte kunt u Hallo-gegevens met PolyBase in SQL Data Warehouse laden.</span><span class="sxs-lookup"><span data-stu-id="f4765-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="f4765-215">U kunt ook AZCopy opnemen in uw SSIS-pakketten met behulp van een 'Proces uitvoeren'.</span><span class="sxs-lookup"><span data-stu-id="f4765-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="f4765-216">toouse AZCopy u eerst toodownload nodig hebt en deze installeren.</span><span class="sxs-lookup"><span data-stu-id="f4765-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="f4765-217">Er is een [productieversie] [ production version] en een [preview-versie] [ preview version] beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f4765-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="f4765-218">tooupload een bestand van het bestandssysteem u een opdracht zoals Hallo een hieronder moet:</span><span class="sxs-lookup"><span data-stu-id="f4765-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="f4765-219">Een samenvatting van het proces op hoog niveau kan worden:</span><span class="sxs-lookup"><span data-stu-id="f4765-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="f4765-220">Een Azure-opslag-blob-container tooreceive Hallo gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="f4765-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="f4765-221">De opslag van uw gegevens toolocal exporteren</span><span class="sxs-lookup"><span data-stu-id="f4765-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="f4765-222">Uw gegevens in Azure Blob Storage-container Hallo AZCopy</span><span class="sxs-lookup"><span data-stu-id="f4765-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="f4765-223">Hallo gegevens laden in SQL Data Warehouse met PolyBase</span><span class="sxs-lookup"><span data-stu-id="f4765-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="f4765-224">Volledige documentatie beschikbaar: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="f4765-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="f4765-225">Optimaliseren gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="f4765-225">Optimizing data export</span></span>
<span data-ttu-id="f4765-226">Bovendien kan toooptimize Hallo exporteren van het Hallo gegevens tooimprove Hallo processen meer ook zoeken door tooensuring dat Hallo export verspreid door PolyBase u toohello-vereisten voldoet.</span><span class="sxs-lookup"><span data-stu-id="f4765-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="f4765-227">Gegevenscompressie</span><span class="sxs-lookup"><span data-stu-id="f4765-227">Data compression</span></span>
<span data-ttu-id="f4765-228">Gzip gecomprimeerde gegevens kan worden gelezen door PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4765-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="f4765-229">Als u kunnen toocompress die en de gegevensbestanden toogzip vervolgens minimaliseert u Hallo en de hoeveelheid gegevens die via Hallo netwerk wordt gepusht.</span><span class="sxs-lookup"><span data-stu-id="f4765-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="f4765-230">Meerdere bestanden</span><span class="sxs-lookup"><span data-stu-id="f4765-230">Multiple files</span></span>
<span data-ttu-id="f4765-231">Niet alleen tooimprove snelheid exporteren van grote tabellen in verschillende bestanden op te splitsen helpt, maar ook met overbrengen re-startability en Hallo algehele beheerbaarheid van Hallo gegevens eenmaal in hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f4765-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="f4765-232">Een van de Hallo veel nice functies van PolyBase is Hiermee worden alle Hallo-bestanden naar de map lezen en behandelen als één tabel.</span><span class="sxs-lookup"><span data-stu-id="f4765-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="f4765-233">Daarom is het een goed idee tooisolate Hallo-bestanden voor elke tabel in de eigen map.</span><span class="sxs-lookup"><span data-stu-id="f4765-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="f4765-234">PolyBase biedt ook ondersteuning voor een functie die bekend als 'recursieve map traversal'.</span><span class="sxs-lookup"><span data-stu-id="f4765-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="f4765-235">U kunt deze functie toofurther verbeteren Hallo organisatie van de geëxporteerde gegevens tooimprove uw gegevensbeheer.</span><span class="sxs-lookup"><span data-stu-id="f4765-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="f4765-236">toolearn meer informatie over het laden van gegevens met PolyBase, Zie [tooload-gegevens met PolyBase in SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4765-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4765-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4765-237">Next steps</span></span>
<span data-ttu-id="f4765-238">Zie voor meer informatie over de migratie [migreren van uw oplossing tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4765-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="f4765-239">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="f4765-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
