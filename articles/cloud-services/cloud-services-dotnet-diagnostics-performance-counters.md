---
title: aaaUse prestatiemeters in Azure Diagnostics | Microsoft Docs
description: Gebruik prestatiemeters in Azure-cloud-services of virtuele machine toofind knelpunten en prestaties te optimaliseren.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="997ec-103">Maken en gebruiken van prestatie-items in een Azure-toepassing</span><span class="sxs-lookup"><span data-stu-id="997ec-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="997ec-104">Dit artikel wordt beschreven Hallo voordelen van en hoe tooput van de prestatiemeteritems in uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="997ec-105">U kunt ze toocollect gegevens gebruiken, knelpunten vinden en afstemmen van de prestaties van systeem en de toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="997ec-106">Prestatie-items beschikbaar voor Windows Server, IIS en ASP.NET kunnen ook worden verzameld en gebruikt toodetermine Hallo status van uw Azure-web-functies, werkrollen en virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="997ec-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="997ec-107">U kunt ook maken en gebruiken van aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="997ec-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="997ec-108">U kunt gegevens van prestatiemeteritems controleren</span><span class="sxs-lookup"><span data-stu-id="997ec-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="997ec-109">Rechtstreeks op de toepassingshost Hallo met Hallo Prestatiemeter hulpprogramma toegankelijk via Extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="997ec-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="997ec-110">Met het gebruik van System Center Operations Manager hello Azure Management Pack</span><span class="sxs-lookup"><span data-stu-id="997ec-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="997ec-111">Diagnostische gegevens overgedragen met andere controleprogramma's die toegang hebben tot Hallo tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="997ec-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="997ec-112">Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="997ec-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="997ec-113">Voor meer informatie over het bewaken van de prestaties van uw toepassing in Hallo Hallo [Azure-portal](http://portal.azure.com/), Zie [hoe tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="997ec-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="997ec-114">Voor meer gedetailleerde informatie over het maken van een logboekregistratie en tracering strategie en met behulp van diagnostische gegevens en andere technieken tootroubleshoot problemen en optimaliseren van de Azure-toepassingen, Zie [aanbevolen procedures voor het ontwikkelen van Azure oplossen Toepassingen](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="997ec-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="997ec-115">Schakel de bewaking van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="997ec-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="997ec-116">Prestatiemeteritems zijn standaard niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="997ec-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="997ec-117">Uw toepassing of het starten van de taak moet Hallo standaard diagnostics agent tooinclude Hallo specifieke prestatiemeteritems configuration gewenste toomonitor voor elk rolexemplaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="997ec-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="997ec-118">Prestatie-items voor Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="997ec-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="997ec-119">Azure biedt een subset van de beschikbare Hallo prestatiemeteritems voor Windows Server, IIS en ASP.NET-stack Hallo.</span><span class="sxs-lookup"><span data-stu-id="997ec-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="997ec-120">Hallo volgende tabel bevat enkele van de prestatiemeteritems Hallo met name van belang voor Azure-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="997ec-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="997ec-121">Prestatiemeteritem-categorie: Object (exemplaar)</span><span class="sxs-lookup"><span data-stu-id="997ec-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="997ec-122">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="997ec-122">Counter Name</span></span> | <span data-ttu-id="997ec-123">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="997ec-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="997ec-124">.NET CLR-uitzonderingen (*globale*)</span><span class="sxs-lookup"><span data-stu-id="997ec-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="997ec-125"># Uitzonderingen veroorzaakt per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="997ec-126">Uitzondering-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="997ec-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="997ec-127">.NET CLR-geheugen (*globale*)</span><span class="sxs-lookup"><span data-stu-id="997ec-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="997ec-128">% Tijd in %</span><span class="sxs-lookup"><span data-stu-id="997ec-128">% Time in GC</span></span> |<span data-ttu-id="997ec-129">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="997ec-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="997ec-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-130">ASP.NET</span></span> |<span data-ttu-id="997ec-131">Toepassing opnieuw wordt gestart</span><span class="sxs-lookup"><span data-stu-id="997ec-131">Application Restarts</span></span> |<span data-ttu-id="997ec-132">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-133">ASP.NET</span></span> |<span data-ttu-id="997ec-134">Uitvoertijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="997ec-134">Request Execution Time</span></span> |<span data-ttu-id="997ec-135">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-136">ASP.NET</span></span> |<span data-ttu-id="997ec-137">Verbroken aanvragen</span><span class="sxs-lookup"><span data-stu-id="997ec-137">Requests Disconnected</span></span> |<span data-ttu-id="997ec-138">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-139">ASP.NET</span></span> |<span data-ttu-id="997ec-140">Opnieuw gestarte werkprocessen</span><span class="sxs-lookup"><span data-stu-id="997ec-140">Worker Process Restarts</span></span> |<span data-ttu-id="997ec-141">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-142">ASP.NET-toepassingen (**totale**)</span><span class="sxs-lookup"><span data-stu-id="997ec-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="997ec-143">Totaal aantal aanvragen</span><span class="sxs-lookup"><span data-stu-id="997ec-143">Requests Total</span></span> |<span data-ttu-id="997ec-144">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-145">ASP.NET-toepassingen (**totale**)</span><span class="sxs-lookup"><span data-stu-id="997ec-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="997ec-146">Aanvragen per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-146">Requests/Sec</span></span> |<span data-ttu-id="997ec-147">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="997ec-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="997ec-149">Uitvoertijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="997ec-149">Request Execution Time</span></span> |<span data-ttu-id="997ec-150">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="997ec-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="997ec-152">Wachttijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="997ec-152">Request Wait Time</span></span> |<span data-ttu-id="997ec-153">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="997ec-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="997ec-155">Huidige aanvragen</span><span class="sxs-lookup"><span data-stu-id="997ec-155">Requests Current</span></span> |<span data-ttu-id="997ec-156">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="997ec-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="997ec-158">Aanvragen in wachtrij</span><span class="sxs-lookup"><span data-stu-id="997ec-158">Requests Queued</span></span> |<span data-ttu-id="997ec-159">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="997ec-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="997ec-161">Aanvragen dat is geweigerd</span><span class="sxs-lookup"><span data-stu-id="997ec-161">Requests Rejected</span></span> |<span data-ttu-id="997ec-162">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-163">Geheugen</span><span class="sxs-lookup"><span data-stu-id="997ec-163">Memory</span></span> |<span data-ttu-id="997ec-164">Beschikbare megabytes (MB)</span><span class="sxs-lookup"><span data-stu-id="997ec-164">Available MBytes</span></span> |<span data-ttu-id="997ec-165">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="997ec-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="997ec-166">Geheugen</span><span class="sxs-lookup"><span data-stu-id="997ec-166">Memory</span></span> |<span data-ttu-id="997ec-167">Toegewezen Bytes</span><span class="sxs-lookup"><span data-stu-id="997ec-167">Committed Bytes</span></span> |<span data-ttu-id="997ec-168">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="997ec-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="997ec-169">Processor(_Totaal)</span><span class="sxs-lookup"><span data-stu-id="997ec-169">Processor(_Total)</span></span> |<span data-ttu-id="997ec-170">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="997ec-170">% Processor Time</span></span> |<span data-ttu-id="997ec-171">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="997ec-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="997ec-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="997ec-172">TCPv4</span></span> |<span data-ttu-id="997ec-173">Verbindingsfouten</span><span class="sxs-lookup"><span data-stu-id="997ec-173">Connection Failures</span></span> |<span data-ttu-id="997ec-174">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-174">TCP Object</span></span> |
| <span data-ttu-id="997ec-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="997ec-175">TCPv4</span></span> |<span data-ttu-id="997ec-176">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="997ec-176">Connections Established</span></span> |<span data-ttu-id="997ec-177">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-177">TCP Object</span></span> |
| <span data-ttu-id="997ec-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="997ec-178">TCPv4</span></span> |<span data-ttu-id="997ec-179">Verbindingen opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="997ec-179">Connections Reset</span></span> |<span data-ttu-id="997ec-180">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-180">TCP Object</span></span> |
| <span data-ttu-id="997ec-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="997ec-181">TCPv4</span></span> |<span data-ttu-id="997ec-182">Segmenten verzonden per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-182">Segments Sent/sec</span></span> |<span data-ttu-id="997ec-183">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-183">TCP Object</span></span> |
| <span data-ttu-id="997ec-184">Netwerk Interface(*)</span><span class="sxs-lookup"><span data-stu-id="997ec-184">Network Interface(*)</span></span> |<span data-ttu-id="997ec-185">Ontvangen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-185">Bytes Received/sec</span></span> |<span data-ttu-id="997ec-186">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-186">Network Interface Object</span></span> |
| <span data-ttu-id="997ec-187">Netwerk Interface(*)</span><span class="sxs-lookup"><span data-stu-id="997ec-187">Network Interface(*)</span></span> |<span data-ttu-id="997ec-188">Verzonden bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-188">Bytes Sent/sec</span></span> |<span data-ttu-id="997ec-189">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-189">Network Interface Object</span></span> |
| <span data-ttu-id="997ec-190">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="997ec-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="997ec-191">Ontvangen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-191">Bytes Received/sec</span></span> |<span data-ttu-id="997ec-192">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-192">Network Interface Object</span></span> |
| <span data-ttu-id="997ec-193">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="997ec-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="997ec-194">Verzonden bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-194">Bytes Sent/sec</span></span> |<span data-ttu-id="997ec-195">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-195">Network Interface Object</span></span> |
| <span data-ttu-id="997ec-196">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="997ec-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="997ec-197">Totaal aantal bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="997ec-197">Bytes Total/sec</span></span> |<span data-ttu-id="997ec-198">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="997ec-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="997ec-199">Maken en aangepaste prestaties tellers tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="997ec-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="997ec-200">Azure support toocreate heeft en aangepaste prestatiemeteritems voor webrollen en werkrollen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="997ec-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="997ec-201">Hallo tellers mogelijk gebruikte tootrack en monitor toepassingsspecifieke gedrag.</span><span class="sxs-lookup"><span data-stu-id="997ec-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="997ec-202">U kunt maken en aangepaste categorieën voor prestatiemeteritems en specificaties verwijderen uit een starten van de taak, Webrol of werkrol met verhoogde machtigingen.</span><span class="sxs-lookup"><span data-stu-id="997ec-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="997ec-203">Code die gewijzigd toocustom prestatiemeteritems wordt moet wel verhoogde machtigingen toorun.</span><span class="sxs-lookup"><span data-stu-id="997ec-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="997ec-204">Als Hallo code in een Webrol of werkrol is, Hallo rol Hallo-tag moet bevatten <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef van de bestandsserver voor Hallo rol tooinitialize goed.</span><span class="sxs-lookup"><span data-stu-id="997ec-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="997ec-205">U kunt aangepaste prestaties teller tooAzure opslag van gegevens met de Hallo diagnostics agent verzenden.</span><span class="sxs-lookup"><span data-stu-id="997ec-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="997ec-206">Hallo standaard gegevens van prestatiemeteritems wordt gegenereerd door hello die Azure verwerkt.</span><span class="sxs-lookup"><span data-stu-id="997ec-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="997ec-207">Aangepaste gegevens van prestatiemeteritems moeten worden gemaakt door de functie- of worker-rol webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="997ec-208">Zie [prestaties itemtypen](https://msdn.microsoft.com/library/z573042h.aspx) voor informatie over het Hallo typen gegevens die kunnen worden opgeslagen in de aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="997ec-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="997ec-209">Zie [PerformanceCounters voorbeeld](http://code.msdn.microsoft.com/azure/) voor een voorbeeld maakt en stelt u aangepaste prestatiemeteritem-gegevens in een Webrol.</span><span class="sxs-lookup"><span data-stu-id="997ec-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="997ec-210">Gegevens van prestatiemeteritems opslaan en weergeven</span><span class="sxs-lookup"><span data-stu-id="997ec-210">Store and view performance counter data</span></span>
<span data-ttu-id="997ec-211">Azure in de cache opgeslagen gegevens met andere diagnostische gegevens van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="997ec-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="997ec-212">Deze gegevens is beschikbaar voor externe controle terwijl Hallo rolinstantie wordt uitgevoerd met toegang tot extern bureaublad tooview's zoals Prestatiemeter.</span><span class="sxs-lookup"><span data-stu-id="997ec-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="997ec-213">toopersist hello buiten rolinstantie hello, Hallo diagnostics agent moet gegevensoverdracht Hallo tooAzure gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="997ec-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="997ec-214">Hallo maximale grootte van Hallo in de cache opgeslagen gegevens van prestatiemeteritems kan worden geconfigureerd in Hallo diagnostics agent, of wordt mogelijk toobe deel uitmaken van een gedeelde limiet is geconfigureerd voor alle Hallo diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="997ec-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="997ec-215">Zie voor meer informatie over het instellen van de buffergrootte Hallo [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) en [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="997ec-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="997ec-216">Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor een overzicht van het Hallo-agent tootransfer gegevens tooa opslagaccount voor diagnostische gegevens in te stellen.</span><span class="sxs-lookup"><span data-stu-id="997ec-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="997ec-217">Elke geconfigureerde exemplaar van prestatiemeteritem wordt vastgelegd bij een opgegeven samplefrequentie en Hallo door actieve gegevens worden overgedragen toohello storage-account door een geplande aanvraag of een aanvraag voor op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="997ec-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="997ec-218">Automatische transfers kunnen zo vaak als één keer per minuut worden gepland.</span><span class="sxs-lookup"><span data-stu-id="997ec-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="997ec-219">Prestatiemeteritemgegevens overgedragen door Hallo diagnostics agent wordt opgeslagen in een tabel WADPerformanceCountersTable, in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="997ec-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="997ec-220">Deze tabel kan worden geopend en methoden die standaard Azure storage-API worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="997ec-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="997ec-221">Zie [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) voor een voorbeeld van het uitvoeren van query's en gegevens van prestatiemeteritems uit Hallo WADPerformanceCountersTable tabel weergeven.</span><span class="sxs-lookup"><span data-stu-id="997ec-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="997ec-222">Afhankelijk van Hallo diagnostics agent overdracht frequentie en wachtrij latentie, hello meest recente prestatiemeteritemgegevens in Hallo storage-account mogelijk enkele minuten verouderd.</span><span class="sxs-lookup"><span data-stu-id="997ec-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="997ec-223">Prestatiemeteritems configuratiebestand diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="997ec-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="997ec-224">Gebruik hello te volgen procedure tooenable-prestatiemeters in uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="997ec-225">Vereisten</span><span class="sxs-lookup"><span data-stu-id="997ec-225">Prerequisites</span></span>
<span data-ttu-id="997ec-226">Deze sectie wordt ervan uitgegaan dat u hebt geïmporteerd Hallo diagnostische monitor in uw toepassing en Hallo diagnostics configuration file tooyour Visual Studio-oplossing (diagnostics.wadcfg en lagere niveaus in de SDK 2.4 of diagnostics.wadcfgx in SDK 2.5 en hoger) toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="997ec-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="997ec-227">Zie stap 1 en 2 in [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md)) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="997ec-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="997ec-228">Stap 1: Verzamelen en opslaan van gegevens van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="997ec-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="997ec-229">Nadat u hebt toegevoegd Hallo diagnostics bestand tooyour Visual Studio-oplossing, kunt u Hallo verzameling en de opslag van gegevens van prestatiemeteritems configureren in een Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="997ec-230">Dit wordt gedaan door prestaties tellers toohello diagnostics bestand toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="997ec-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="997ec-231">Diagnostics-gegevens, prestatiemeteritems, eerst worden verzameld op Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="997ec-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="997ec-232">Hallo gegevens vervolgens persistente toohello WADPerformanceCountersTable tabel in hello Azure Table-service, zodat u ook nodig toospecify Hallo storage-account in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="997ec-233">Als u uw toepassing lokaal in Hallo Compute-Emulator testen bent, kunt u diagnostische gegevens ook lokaal opslaan in Hallo-Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="997ec-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="997ec-234">Voordat u de diagnostics-gegevens opslaat, moet u eerst toohello gaan [Azure-portal](http://portal.azure.com/) en een klassieke opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="997ec-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="997ec-235">Een aanbevolen procedure is toolocate uw opslagaccount in dezelfde geografische locatie als uw Azure-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="997ec-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="997ec-236">Door houden hello Azure toepassings- en storage-account zijn in Hallo dezelfde geografische locatie, u betaalt externe bandbreedtekosten voorkomen en de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="997ec-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="997ec-237">Prestaties tellers toohello diagnostics bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="997ec-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="997ec-238">Er zijn veel prestatiemeteritems die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="997ec-238">There are many counters you can use.</span></span> <span data-ttu-id="997ec-239">Hallo volgende voorbeeld ziet u enkele prestatiemeteritems die worden aanbevolen voor web- en bewaking van worker-rol.</span><span class="sxs-lookup"><span data-stu-id="997ec-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="997ec-240">Open Hallo diagnostics-bestand (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en Hallo toohello DiagnosticMonitorConfiguration element volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="997ec-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="997ec-241">Hallo bufferQuotaInMB kenmerk Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo verzameling gegevenstype (Azure Logboeken, IIS-logboeken, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="997ec-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="997ec-242">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="997ec-242">hello default is 0.</span></span> <span data-ttu-id="997ec-243">Wanneer Hallo quotum is bereikt, wordt de oudste gegevens Hallo verwijderd naarmate er nieuwe gegevens worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="997ec-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="997ec-244">Hallo som van alle Hallo bufferQuotaInMB eigenschappen moet groter dan Hallo-waarde van Hallo OverallQuotaInMB kenmerk.</span><span class="sxs-lookup"><span data-stu-id="997ec-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="997ec-245">Zie voor meer informatie over om te bepalen hoeveel opslagruimte zijn vereist voor Hallo verzamelen van diagnostische gegevens, af van de Setup-sectie van Hallo [Best Practices probleemoplossing voor Azure-toepassingen ontwikkelen](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="997ec-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="997ec-246">Hallo scheduledTransferPeriod kenmerk hello-interval tussen de geplande overdrachten van gegevens bevat, afgerond naar toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="997ec-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="997ec-247">In de Hallo volgen voorbeelden, wordt deze ingesteld tooPT30M (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="997ec-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="997ec-248">Instelling Hallo overdracht periode tooa kleine waarde, zoals 1 minuut, zal negatieve invloed hebben op de prestaties van de toepassing in productie, maar is handig als u wilt zien van diagnostische gegevens snel te werken als u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="997ec-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="997ec-249">Hallo geplande overdracht periode moet klein genoeg tooensure diagnostische gegevens zijn niet op Hallo-exemplaar, maar groot genoeg is dat het heeft geen invloed op prestaties van uw toepassing hello overschreven.</span><span class="sxs-lookup"><span data-stu-id="997ec-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="997ec-250">Hallo counterSpecifier kenmerk geeft Hallo prestaties teller toocollect.</span><span class="sxs-lookup"><span data-stu-id="997ec-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="997ec-251">Hallo sampleRate kenmerk geeft Hallo snelheid waarmee het prestatiemeteritem Hallo moet actieve, in dit geval 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="997ec-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="997ec-252">Nadat u hebt toegevoegd Hallo prestatiemeteritems die u toocollect wilt, sla uw wijzigingen toohello diagnostics-bestand.</span><span class="sxs-lookup"><span data-stu-id="997ec-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="997ec-253">Vervolgens moet u toospecify Hallo storage-account dat Hallo diagnostics-gegevens worden opgeslagen in.</span><span class="sxs-lookup"><span data-stu-id="997ec-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="997ec-254">Hallo storage-account opgeven</span><span class="sxs-lookup"><span data-stu-id="997ec-254">Specify hello storage account</span></span>
<span data-ttu-id="997ec-255">toopersist uw diagnostische informatie tooyour Azure Storage-account, moet u een verbindingsreeks in uw serviceconfiguratiebestand (ServiceConfiguration.cscfg).</span><span class="sxs-lookup"><span data-stu-id="997ec-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="997ec-256">Voor de Azure SDK 2.5, kan Hallo Storage-Account in Hallo diagnostics.wadcfgx bestand worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="997ec-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="997ec-257">Deze instructies zijn alleen van toepassing tooAzure SDK 2.4 en lager.</span><span class="sxs-lookup"><span data-stu-id="997ec-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="997ec-258">Voor de Azure SDK 2.5, kan Hallo Storage-Account in Hallo diagnostics.wadcfgx bestand worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="997ec-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="997ec-259">tooset hello verbindingsreeksen:</span><span class="sxs-lookup"><span data-stu-id="997ec-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="997ec-260">Open Hallo ServiceConfiguration.Cloud.cscfg bestand met uw favoriete teksteditor en de set Hallo-verbindingsreeks voor de opslag.</span><span class="sxs-lookup"><span data-stu-id="997ec-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="997ec-261">Hallo *AccountName* en *AccountKey* waarden zijn gevonden in hello Azure-portal op Hallo storage account dashboard onder toegangstoetsen.</span><span class="sxs-lookup"><span data-stu-id="997ec-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="997ec-262">Hallo ServiceConfiguration.Cloud.cscfg bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="997ec-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="997ec-263">Hallo ServiceConfiguration.Local.cscfg bestand openen en controleren of UseDevelopmentStorage tootrue is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="997ec-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="997ec-264">Nu dat de verbindingsreeksen Hallo zijn ingesteld, wordt uw toepassing opslagaccount voor diagnostische gegevens tooyour bewaard wanneer uw toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="997ec-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="997ec-265">Opslaan op het project bouwen en implementeren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="997ec-266">Stap 2: (Optioneel) Maak aangepaste prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="997ec-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="997ec-267">Bovendien toohello vooraf gedefinieerde prestatie-items, kunt u uw eigen aangepaste prestatiemeteritems toomonitor web- of worker rollen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="997ec-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="997ec-268">Aangepaste prestatiemeteritems kunnen gebruikte tootrack en monitor toepassingsspecifieke gedrag en kan worden gemaakt of verwijderd in een opstarttaak Webrol of een werkrol met verhoogde machtigingen.</span><span class="sxs-lookup"><span data-stu-id="997ec-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="997ec-269">Hello Azure diagnostics agent vernieuwt Hallo prestaties teller configuratie uit Hallo .wadcfg bestand een minuut na het starten.</span><span class="sxs-lookup"><span data-stu-id="997ec-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="997ec-270">Als u aangepaste prestatiemeteritems in Hallo OnStart-methode maken en uw opstarttaken langer dan een minuut tooexecute duurt, uw aangepaste prestatiemeteritems wordt niet gemaakt wanneer hello Azure Diagnostics agent tooload probeert ze.</span><span class="sxs-lookup"><span data-stu-id="997ec-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="997ec-271">In dit scenario ziet u dat Azure Diagnostics correct worden alle diagnostische gegevens, behalve van uw aangepaste prestatiemeteritems vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="997ec-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="997ec-272">tooresolve dit probleem Hallo prestatie-items maken in een opstarttaak of verplaatsen werken sommige van uw opstarttaak toohello OnStart-methode na het maken van Hallo prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="997ec-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="997ec-273">Volgende stappen toocreate een eenvoudige aangepaste Prestatiemeter '\MyCustomCounterCategory\MyButton1Counter' hello uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="997ec-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="997ec-274">Open Hallo servicedefinitiebestand (CSDEF) voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="997ec-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="997ec-275">Hallo Runtime element toohello WebRole of WorkerRole element tooallow uitvoeren met verhoogde bevoegdheden toevoegen:</span><span class="sxs-lookup"><span data-stu-id="997ec-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="997ec-276">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="997ec-276">Save hello file.</span></span>
4. <span data-ttu-id="997ec-277">Open Hallo diagnostics-bestand (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en Hallo na toohello DiagnosticMonitorConfiguration toevoegen</span><span class="sxs-lookup"><span data-stu-id="997ec-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="997ec-278">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="997ec-278">Save hello file.</span></span>
6. <span data-ttu-id="997ec-279">Hallo aangepaste Prestatiemeteritem-categorie in Hallo OnStart-methode van uw rol maken voordat base wordt aangeroepen. OnStart.</span><span class="sxs-lookup"><span data-stu-id="997ec-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="997ec-280">Hallo maakt volgende C#-voorbeeld u een aangepaste categorie als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="997ec-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="997ec-281">Hallo-tellers in uw toepassing bijwerken.</span><span class="sxs-lookup"><span data-stu-id="997ec-281">Update hello counters within your application.</span></span> <span data-ttu-id="997ec-282">Hallo voorbeeld van de volgende updates van een aangepaste prestatiemeteritem op Button1_Click gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="997ec-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="997ec-283">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="997ec-283">Save hello file.</span></span>  

<span data-ttu-id="997ec-284">Aangepaste prestatiemeteritemgegevens worden nu door hello Azure diagnostics monitor verzameld.</span><span class="sxs-lookup"><span data-stu-id="997ec-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="997ec-285">Stap 3: De gegevens van prestatiemeteritems opvragen</span><span class="sxs-lookup"><span data-stu-id="997ec-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="997ec-286">Als uw toepassing wordt geïmplementeerd en uitgevoerd, Hallo diagnostische monitor gaat verder met het verzamelen van prestatiemeteritems en persistent maken die tooAzure gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="997ec-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="997ec-287">U hulpprogramma's zoals Server Explorer gebruiken in Visual Studio [Azure Opslagverkenner](http://azurestorageexplorer.codeplex.com/), of [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) door Cerebrata tooview Hallo prestatiemeteritems van de gegevens in Hallo WADPerformanceCountersTable tabel.</span><span class="sxs-lookup"><span data-stu-id="997ec-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="997ec-288">U kunt ook programmatisch query service gebruikmaakt van Hallo tabel [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), of [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="997ec-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="997ec-289">Hallo volgende C#-voorbeeld ziet u een eenvoudige query op Hallo WADPerformanceCountersTable tabel en Hallo diagnostische gegevens tooa CSV-bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="997ec-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="997ec-290">Wanneer Hallo-prestatiemeteritems tooa CSV-bestand opgeslagen zijn, kunt u Hallo mogelijkheden in Microsoft Excel of andere hulpprogramma toovisualize Hallo gegevens grafieken.</span><span class="sxs-lookup"><span data-stu-id="997ec-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="997ec-291">Niet zeker tooadd een verwijzing tooMicrosoft.WindowsAzure.Storage.dll, die is opgenomen in hello Azure SDK voor .NET oktober 2012 en hoger.</span><span class="sxs-lookup"><span data-stu-id="997ec-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="997ec-292">Hallo-assembly is geïnstalleerde toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version num\ref\-directory.</span><span class="sxs-lookup"><span data-stu-id="997ec-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="997ec-293">Entiteiten worden toegewezen tooC #-objecten met behulp van een aangepaste klasse die is afgeleid van **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="997ec-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="997ec-294">Hallo volgende code definieert een entiteitsklasse die staat voor een prestatiemeteritem op Hallo **WADPerformanceCountersTable** tabel.</span><span class="sxs-lookup"><span data-stu-id="997ec-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="997ec-295">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="997ec-295">Next Steps</span></span>
[<span data-ttu-id="997ec-296">Aanvullende artikelen op Azure Diagnostics weergeven</span><span class="sxs-lookup"><span data-stu-id="997ec-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
