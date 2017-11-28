---
title: aaaAzure SQL Data Warehouse Veelgestelde vragen | Microsoft Docs
description: In dit artikel worden uit de veelgestelde vragen over Azure SQL Data Warehouse van klanten en ontwikkelaars
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="bfba8-103">SQL Data Warehouse Veelgestelde vragen over</span><span class="sxs-lookup"><span data-stu-id="bfba8-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="bfba8-104">Algemeen</span><span class="sxs-lookup"><span data-stu-id="bfba8-104">General</span></span>

<span data-ttu-id="bfba8-105">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-105">Q.</span></span> <span data-ttu-id="bfba8-106">Wat biedt SQL DW voor beveiliging van gegevens?</span><span class="sxs-lookup"><span data-stu-id="bfba8-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="bfba8-107">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-107">A.</span></span> <span data-ttu-id="bfba8-108">SQL DW biedt verschillende oplossingen voor het beveiligen van gegevens, zoals TDE en controle.</span><span class="sxs-lookup"><span data-stu-id="bfba8-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="bfba8-109">Zie voor meer informatie [beveiliging].</span><span class="sxs-lookup"><span data-stu-id="bfba8-109">For more information, see [Security].</span></span>

<span data-ttu-id="bfba8-110">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-110">Q.</span></span> <span data-ttu-id="bfba8-111">Waar vind ik controleren welke standaarden wettelijke of zakelijke is SQL DW naleven?</span><span class="sxs-lookup"><span data-stu-id="bfba8-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="bfba8-112">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-112">A.</span></span> <span data-ttu-id="bfba8-113">Ga naar Hallo [Microsoft Compliance] pagina voor verschillende producten voor naleving door product zoals SOC en ISO.</span><span class="sxs-lookup"><span data-stu-id="bfba8-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="bfba8-114">Eerst kiezen door naleving titel vervolgens Azure uitbreiden in Hallo in bereik Microsoft cloud services-sectie aan de rechterkant Hallo van Hallo pagina toosee welke services Azure-services zijn die compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="bfba8-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="bfba8-115">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-115">Q.</span></span> <span data-ttu-id="bfba8-116">Kan ik verbinden met Power BI?</span><span class="sxs-lookup"><span data-stu-id="bfba8-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="bfba8-117">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-117">A.</span></span> <span data-ttu-id="bfba8-118">Ja.</span><span class="sxs-lookup"><span data-stu-id="bfba8-118">Yes!</span></span> <span data-ttu-id="bfba8-119">Hoewel Power BI ondersteunt de directe query met SQL DW, het niet bedoeld voor een groot aantal gebruikers of realtime-gegevens.</span><span class="sxs-lookup"><span data-stu-id="bfba8-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="bfba8-120">Voor gebruik in productieomgevingen van Power BI, wordt u aangeraden PowerBI naast Azure Analysis Services of Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="bfba8-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="bfba8-121">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-121">Q.</span></span> <span data-ttu-id="bfba8-122">Wat zijn de capaciteitslimiet van SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="bfba8-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="bfba8-123">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-123">A.</span></span> <span data-ttu-id="bfba8-124">Zie onze huidige [Capaciteitslimieten] pagina.</span><span class="sxs-lookup"><span data-stu-id="bfba8-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="bfba8-125">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-125">Q.</span></span> <span data-ttu-id="bfba8-126">Waarom wordt mijn schaal/onderbreken/hervatten duurt te lang waardoor?</span><span class="sxs-lookup"><span data-stu-id="bfba8-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="bfba8-127">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-127">A.</span></span> <span data-ttu-id="bfba8-128">Een verscheidenheid aan factoren kan invloed hebben op Hallo tijd voor de compute-beheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bfba8-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="bfba8-129">Als u een algemeen case voor transactionele terugdraaien langlopende bewerkingen is.</span><span class="sxs-lookup"><span data-stu-id="bfba8-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="bfba8-130">Wanneer een bewerking voor schaal of onderbreken is gestart, worden alle binnenkomende sessies geblokkeerd en query's zijn geleegd.</span><span class="sxs-lookup"><span data-stu-id="bfba8-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="bfba8-131">In volgorde tooleave Hallo systeem stabiele status worden transacties teruggedraaid terug voordat een bewerking kan beginnen.</span><span class="sxs-lookup"><span data-stu-id="bfba8-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="bfba8-132">Hallo groter Hallo-nummer en grotere Hallo logboekgrootte van transacties, Hallo langer Hallo-bewerking is vastgelopen Hallo tooa stabiele systeemstatus terugzetten.</span><span class="sxs-lookup"><span data-stu-id="bfba8-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="bfba8-133">Gebruikersondersteuning</span><span class="sxs-lookup"><span data-stu-id="bfba8-133">User support</span></span>

<span data-ttu-id="bfba8-134">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-134">Q.</span></span> <span data-ttu-id="bfba8-135">Ik heb een aanvraag functie waar kan ik verzenden?</span><span class="sxs-lookup"><span data-stu-id="bfba8-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="bfba8-136">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-136">A.</span></span> <span data-ttu-id="bfba8-137">Als u een aanvraag van de functie, dient u deze op onze [UserVoice] pagina</span><span class="sxs-lookup"><span data-stu-id="bfba8-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="bfba8-138">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-138">Q.</span></span> <span data-ttu-id="bfba8-139">Hoe kan ik doen x?</span><span class="sxs-lookup"><span data-stu-id="bfba8-139">How can I do x?</span></span>

<span data-ttu-id="bfba8-140">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-140">A.</span></span> <span data-ttu-id="bfba8-141">Voor hulp bij het ontwikkelen met SQL Data Warehouse, kunt u vragen stellen op onze [Stack Overflow] pagina.</span><span class="sxs-lookup"><span data-stu-id="bfba8-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="bfba8-142">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-142">Q.</span></span> <span data-ttu-id="bfba8-143">Hoe verzend ik een ondersteuningsticket</span><span class="sxs-lookup"><span data-stu-id="bfba8-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="bfba8-144">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-144">A.</span></span> <span data-ttu-id="bfba8-145">[Ondersteuningstickets] kunnen worden ingediend via Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bfba8-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="bfba8-146">Ondersteuning voor SQL-taal of onderdeel</span><span class="sxs-lookup"><span data-stu-id="bfba8-146">SQL language/feature support</span></span> 

<span data-ttu-id="bfba8-147">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-147">Q.</span></span> <span data-ttu-id="bfba8-148">Welke gegevenstypen biedt ondersteuning voor SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="bfba8-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="bfba8-149">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-149">A.</span></span> <span data-ttu-id="bfba8-150">SQL Data Warehouse Zie [gegevenstypen].</span><span class="sxs-lookup"><span data-stu-id="bfba8-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="bfba8-151">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-151">Q.</span></span> <span data-ttu-id="bfba8-152">Welke tabelfuncties ondersteund?</span><span class="sxs-lookup"><span data-stu-id="bfba8-152">What table features do you support?</span></span>

<span data-ttu-id="bfba8-153">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-153">A.</span></span> <span data-ttu-id="bfba8-154">Terwijl de SQL Data Warehouse ondersteunt vele functies, sommige worden niet ondersteund en worden beschreven in [niet-ondersteunde functies van de tabel].</span><span class="sxs-lookup"><span data-stu-id="bfba8-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="bfba8-155">Tools en beheer</span><span class="sxs-lookup"><span data-stu-id="bfba8-155">Tooling and administration</span></span>

<span data-ttu-id="bfba8-156">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-156">Q.</span></span> <span data-ttu-id="bfba8-157">U bieden ondersteuning voor Database-projecten in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfba8-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="bfba8-158">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-158">A.</span></span> <span data-ttu-id="bfba8-159">We ondersteunen momenteel geen Database-projecten in Visual Studio voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfba8-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="bfba8-160">Als u wilt toocast een stem tooget u deze opties functie, gaat u naar onze User Voice [Database-projecten functie aanvraag].</span><span class="sxs-lookup"><span data-stu-id="bfba8-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="bfba8-161">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-161">Q.</span></span> <span data-ttu-id="bfba8-162">Ondersteunt SQL Data Warehouse REST-API's?</span><span class="sxs-lookup"><span data-stu-id="bfba8-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="bfba8-163">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-163">A.</span></span> <span data-ttu-id="bfba8-164">Ja.</span><span class="sxs-lookup"><span data-stu-id="bfba8-164">Yes.</span></span> <span data-ttu-id="bfba8-165">De meeste REST-functionaliteit die kan worden gebruikt met SQL Database is ook beschikbaar met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfba8-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="bfba8-166">U vindt informatie in de documentatie voor REST API of [MSDN].</span><span class="sxs-lookup"><span data-stu-id="bfba8-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="bfba8-167">Bezig met laden</span><span class="sxs-lookup"><span data-stu-id="bfba8-167">Loading</span></span>

<span data-ttu-id="bfba8-168">Q.</span><span class="sxs-lookup"><span data-stu-id="bfba8-168">Q.</span></span> <span data-ttu-id="bfba8-169">Welke clientstuurprogramma's ondersteund?</span><span class="sxs-lookup"><span data-stu-id="bfba8-169">What client drivers do you support?</span></span>

<span data-ttu-id="bfba8-170">A.</span><span class="sxs-lookup"><span data-stu-id="bfba8-170">A.</span></span> <span data-ttu-id="bfba8-171">Ondersteuning voor stuurprogramma's voor DW vindt u op Hallo [verbindingsreeksen] pagina</span><span class="sxs-lookup"><span data-stu-id="bfba8-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="bfba8-172">V: wat bestandsindelingen worden ondersteund door PolyBase met SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="bfba8-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="bfba8-173">A: Orc, RC parketvloeren en platte tekst met scheidingstekens</span><span class="sxs-lookup"><span data-stu-id="bfba8-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="bfba8-174">V: wat kan ik toofrom SQL DW met PolyBase verbinding maken?</span><span class="sxs-lookup"><span data-stu-id="bfba8-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="bfba8-175">A: [Azure Data Lake Store] en [Azure Storage-Blobs]</span><span class="sxs-lookup"><span data-stu-id="bfba8-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="bfba8-176">V: is berekening naar beneden duwen mogelijk wanneer u verbinding maakt tooAzure Storage-Blobs of ADLS?</span><span class="sxs-lookup"><span data-stu-id="bfba8-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="bfba8-177">A: SQL DW PolyBase communiceert Nee, alleen Hallo opslagonderdelen.</span><span class="sxs-lookup"><span data-stu-id="bfba8-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="bfba8-178">V: kan ik tooHDI verbinden?</span><span class="sxs-lookup"><span data-stu-id="bfba8-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="bfba8-179">A: HDI kunt ADLS of WASB gebruiken als Hallo HDFS-laag.</span><span class="sxs-lookup"><span data-stu-id="bfba8-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="bfba8-180">Als u als uw HDFS-laag hebt, kunt u die gegevens laden in SQL DW.</span><span class="sxs-lookup"><span data-stu-id="bfba8-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="bfba8-181">U kunt echter naar beneden duwen berekening toohello HDI-exemplaar niet genereren.</span><span class="sxs-lookup"><span data-stu-id="bfba8-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bfba8-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfba8-182">Next steps</span></span>
<span data-ttu-id="bfba8-183">Zie voor meer informatie over SQL Data Warehouse als geheel onze [overzicht] pagina.</span><span class="sxs-lookup"><span data-stu-id="bfba8-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[verbindingsreeksen]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Ondersteuningstickets]: ./sql-data-warehouse-get-started-create-support-ticket.md
[beveiliging]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[Capaciteitslimieten]: ./sql-data-warehouse-service-capacity-limits.md
[gegevenstypen]: ./sql-data-warehouse-tables-data-types.md
[niet-ondersteunde functies van de tabel]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage-Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Database-projecten functie aanvraag]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[overzicht]: ./sql-data-warehouse-overview-faq.md