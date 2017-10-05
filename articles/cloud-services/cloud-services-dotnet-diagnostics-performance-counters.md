---
title: Prestatiemeteritems gebruiken in Azure Diagnostics | Microsoft Docs
description: Prestatiemeteritems van Azure-cloudservices of virtuele machine gebruiken om te zoeken van knelpunten en afstemmen van de prestaties.
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
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="606f3-103">Maken en gebruiken van prestatie-items in een Azure-toepassing</span><span class="sxs-lookup"><span data-stu-id="606f3-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="606f3-104">In dit artikel beschrijft de voordelen van en hoe prestatiemeteritems in uw Azure-toepassing te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="606f3-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="606f3-105">U kunt deze gebruiken voor het verzamelen van gegevens, knelpunten vinden en systeem- en -prestaties afstemmen.</span><span class="sxs-lookup"><span data-stu-id="606f3-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="606f3-106">Prestatie-items beschikbaar voor Windows Server, IIS en ASP.NET kunnen ook worden verzameld en gebruikt om te bepalen van de status van uw Azure-web-functies, werkrollen en virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="606f3-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="606f3-107">U kunt ook maken en gebruiken van aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="606f3-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="606f3-108">U kunt gegevens van prestatiemeteritems controleren</span><span class="sxs-lookup"><span data-stu-id="606f3-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="606f3-109">Rechtstreeks op de toepassingshost met het hulpprogramma Prestatiemeter is toegankelijk via Extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="606f3-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="606f3-110">Met System Center Operations Manager via de Azure Management Pack</span><span class="sxs-lookup"><span data-stu-id="606f3-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="606f3-111">Met andere controleprogramma's die toegang hebben tot de diagnostische gegevens overgebracht naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="606f3-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="606f3-112">Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="606f3-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="606f3-113">Voor meer informatie over het controleren van de prestaties van uw toepassing in de [Azure-portal](http://portal.azure.com/), Zie [hoe Monitor Cloudservices](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="606f3-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="606f3-114">Zie voor meer gedetailleerde informatie over het maken van een logboekregistratie en tracering strategie en met diagnostische gegevens en andere technieken voor het oplossen van problemen en Azure-toepassingen te optimaliseren, [Best Practices probleemoplossing voor Azure-toepassingen ontwikkelen](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="606f3-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="606f3-115">Schakel de bewaking van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="606f3-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="606f3-116">Prestatiemeteritems zijn standaard niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="606f3-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="606f3-117">Uw toepassing of een taak starten van de moet de standaardconfiguratie voor het agent van diagnostische gegevens om op te nemen van de specifieke prestatiemeteritems die u wilt controleren voor elk rolexemplaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="606f3-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="606f3-118">Prestatie-items voor Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="606f3-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="606f3-119">Azure biedt een subset van de beschikbare prestatiemeteritems voor Windows Server, IIS en de ASP.NET-stack.</span><span class="sxs-lookup"><span data-stu-id="606f3-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="606f3-120">De volgende tabel bevat enkele van de prestatiemeteritems met name van belang voor Azure-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="606f3-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="606f3-121">Prestatiemeteritem-categorie: Object (exemplaar)</span><span class="sxs-lookup"><span data-stu-id="606f3-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="606f3-122">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="606f3-122">Counter Name</span></span> | <span data-ttu-id="606f3-123">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="606f3-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="606f3-124">.NET CLR-uitzonderingen (*globale*)</span><span class="sxs-lookup"><span data-stu-id="606f3-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="606f3-125"># Uitzonderingen veroorzaakt per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="606f3-126">Uitzondering-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="606f3-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="606f3-127">.NET CLR-geheugen (*globale*)</span><span class="sxs-lookup"><span data-stu-id="606f3-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="606f3-128">% Tijd in %</span><span class="sxs-lookup"><span data-stu-id="606f3-128">% Time in GC</span></span> |<span data-ttu-id="606f3-129">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="606f3-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="606f3-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-130">ASP.NET</span></span> |<span data-ttu-id="606f3-131">Toepassing opnieuw wordt gestart</span><span class="sxs-lookup"><span data-stu-id="606f3-131">Application Restarts</span></span> |<span data-ttu-id="606f3-132">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-133">ASP.NET</span></span> |<span data-ttu-id="606f3-134">Uitvoertijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="606f3-134">Request Execution Time</span></span> |<span data-ttu-id="606f3-135">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-136">ASP.NET</span></span> |<span data-ttu-id="606f3-137">Verbroken aanvragen</span><span class="sxs-lookup"><span data-stu-id="606f3-137">Requests Disconnected</span></span> |<span data-ttu-id="606f3-138">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-139">ASP.NET</span></span> |<span data-ttu-id="606f3-140">Opnieuw gestarte werkprocessen</span><span class="sxs-lookup"><span data-stu-id="606f3-140">Worker Process Restarts</span></span> |<span data-ttu-id="606f3-141">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-142">ASP.NET-toepassingen (**totale**)</span><span class="sxs-lookup"><span data-stu-id="606f3-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="606f3-143">Totaal aantal aanvragen</span><span class="sxs-lookup"><span data-stu-id="606f3-143">Requests Total</span></span> |<span data-ttu-id="606f3-144">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-145">ASP.NET-toepassingen (**totale**)</span><span class="sxs-lookup"><span data-stu-id="606f3-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="606f3-146">Aanvragen per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-146">Requests/Sec</span></span> |<span data-ttu-id="606f3-147">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="606f3-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="606f3-149">Uitvoertijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="606f3-149">Request Execution Time</span></span> |<span data-ttu-id="606f3-150">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="606f3-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="606f3-152">Wachttijd van aanvraag</span><span class="sxs-lookup"><span data-stu-id="606f3-152">Request Wait Time</span></span> |<span data-ttu-id="606f3-153">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="606f3-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="606f3-155">Huidige aanvragen</span><span class="sxs-lookup"><span data-stu-id="606f3-155">Requests Current</span></span> |<span data-ttu-id="606f3-156">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="606f3-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="606f3-158">Aanvragen in wachtrij</span><span class="sxs-lookup"><span data-stu-id="606f3-158">Requests Queued</span></span> |<span data-ttu-id="606f3-159">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="606f3-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="606f3-161">Aanvragen dat is geweigerd</span><span class="sxs-lookup"><span data-stu-id="606f3-161">Requests Rejected</span></span> |<span data-ttu-id="606f3-162">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-163">Geheugen</span><span class="sxs-lookup"><span data-stu-id="606f3-163">Memory</span></span> |<span data-ttu-id="606f3-164">Beschikbare megabytes (MB)</span><span class="sxs-lookup"><span data-stu-id="606f3-164">Available MBytes</span></span> |<span data-ttu-id="606f3-165">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="606f3-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="606f3-166">Geheugen</span><span class="sxs-lookup"><span data-stu-id="606f3-166">Memory</span></span> |<span data-ttu-id="606f3-167">Toegewezen Bytes</span><span class="sxs-lookup"><span data-stu-id="606f3-167">Committed Bytes</span></span> |<span data-ttu-id="606f3-168">Prestatiemeteritems voor geheugen</span><span class="sxs-lookup"><span data-stu-id="606f3-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="606f3-169">Processor(_Totaal)</span><span class="sxs-lookup"><span data-stu-id="606f3-169">Processor(_Total)</span></span> |<span data-ttu-id="606f3-170">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="606f3-170">% Processor Time</span></span> |<span data-ttu-id="606f3-171">Prestatiemeteritems voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606f3-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="606f3-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="606f3-172">TCPv4</span></span> |<span data-ttu-id="606f3-173">Verbindingsfouten</span><span class="sxs-lookup"><span data-stu-id="606f3-173">Connection Failures</span></span> |<span data-ttu-id="606f3-174">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-174">TCP Object</span></span> |
| <span data-ttu-id="606f3-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="606f3-175">TCPv4</span></span> |<span data-ttu-id="606f3-176">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="606f3-176">Connections Established</span></span> |<span data-ttu-id="606f3-177">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-177">TCP Object</span></span> |
| <span data-ttu-id="606f3-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="606f3-178">TCPv4</span></span> |<span data-ttu-id="606f3-179">Verbindingen opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="606f3-179">Connections Reset</span></span> |<span data-ttu-id="606f3-180">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-180">TCP Object</span></span> |
| <span data-ttu-id="606f3-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="606f3-181">TCPv4</span></span> |<span data-ttu-id="606f3-182">Segmenten verzonden per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-182">Segments Sent/sec</span></span> |<span data-ttu-id="606f3-183">TCP-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-183">TCP Object</span></span> |
| <span data-ttu-id="606f3-184">Netwerk Interface(*)</span><span class="sxs-lookup"><span data-stu-id="606f3-184">Network Interface(*)</span></span> |<span data-ttu-id="606f3-185">Ontvangen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-185">Bytes Received/sec</span></span> |<span data-ttu-id="606f3-186">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-186">Network Interface Object</span></span> |
| <span data-ttu-id="606f3-187">Netwerk Interface(*)</span><span class="sxs-lookup"><span data-stu-id="606f3-187">Network Interface(*)</span></span> |<span data-ttu-id="606f3-188">Verzonden bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-188">Bytes Sent/sec</span></span> |<span data-ttu-id="606f3-189">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-189">Network Interface Object</span></span> |
| <span data-ttu-id="606f3-190">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="606f3-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="606f3-191">Ontvangen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-191">Bytes Received/sec</span></span> |<span data-ttu-id="606f3-192">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-192">Network Interface Object</span></span> |
| <span data-ttu-id="606f3-193">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="606f3-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="606f3-194">Verzonden bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-194">Bytes Sent/sec</span></span> |<span data-ttu-id="606f3-195">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-195">Network Interface Object</span></span> |
| <span data-ttu-id="606f3-196">Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="606f3-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="606f3-197">Totaal aantal bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="606f3-197">Bytes Total/sec</span></span> |<span data-ttu-id="606f3-198">Netwerkinterface-Object</span><span class="sxs-lookup"><span data-stu-id="606f3-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="606f3-199">Maken en aangepaste prestatiemeteritems toevoegen aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="606f3-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="606f3-200">Azure heeft ondersteuning voor het maken en wijzigen van de aangepaste prestatiemeteritems voor webrollen en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="606f3-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="606f3-201">De items kunnen worden gebruikt om te volgen en controleren van toepassingsspecifieke gedrag.</span><span class="sxs-lookup"><span data-stu-id="606f3-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="606f3-202">U kunt maken en aangepaste categorieën voor prestatiemeteritems en specificaties verwijderen uit een starten van de taak, Webrol of werkrol met verhoogde machtigingen.</span><span class="sxs-lookup"><span data-stu-id="606f3-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="606f3-203">Code die wijzigingen in aangepaste prestatiemeteritems aanbrengt moet wel verhoogde machtigingen om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="606f3-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="606f3-204">Als de code in een Webrol of worker-rol, moet de rol van de tag bevatten <Runtime executionContext="elevated" /> in het bestand ServiceDefinition.csdef voor de functie naar behoren worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="606f3-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="606f3-205">U kunt aangepaste prestatiemeteritemgegevens verzenden naar Azure-opslag met behulp van de diagnostics-agent.</span><span class="sxs-lookup"><span data-stu-id="606f3-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="606f3-206">De standaard gegevens van prestatiemeteritems wordt gegenereerd door de processen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="606f3-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="606f3-207">Aangepaste gegevens van prestatiemeteritems moeten worden gemaakt door de functie- of worker-rol webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="606f3-208">Zie [prestaties itemtypen](https://msdn.microsoft.com/library/z573042h.aspx) voor informatie over de verschillende typen gegevens die kunnen worden opgeslagen in de aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="606f3-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="606f3-209">Zie [PerformanceCounters voorbeeld](http://code.msdn.microsoft.com/azure/) voor een voorbeeld maakt en stelt u aangepaste prestatiemeteritem-gegevens in een Webrol.</span><span class="sxs-lookup"><span data-stu-id="606f3-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="606f3-210">Gegevens van prestatiemeteritems opslaan en weergeven</span><span class="sxs-lookup"><span data-stu-id="606f3-210">Store and view performance counter data</span></span>
<span data-ttu-id="606f3-211">Azure in de cache opgeslagen gegevens met andere diagnostische gegevens van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="606f3-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="606f3-212">Deze gegevens is beschikbaar voor externe controle terwijl de rolinstantie wordt uitgevoerd met behulp van externe bureaublad toegang om hulpprogramma's zoals Prestatiemeter weer te geven.</span><span class="sxs-lookup"><span data-stu-id="606f3-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="606f3-213">Om te blijven behouden de gegevens die buiten de rolinstantie, moet de agent diagnostische gegevens van de gegevens overdragen naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="606f3-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="606f3-214">De maximale grootte van de in cache opgeslagen gegevens van prestatiemeteritems kan worden geconfigureerd in de diagnostics-agent of mogelijk worden geconfigureerd als onderdeel van een gedeelde limiet voor de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="606f3-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="606f3-215">Zie voor meer informatie over het instellen van de buffergrootte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) en [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="606f3-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="606f3-216">Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor een overzicht van het instellen van de agent diagnostische gegevens overdraagt naar een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="606f3-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="606f3-217">Elke geconfigureerde exemplaar van prestatiemeteritem op een opgegeven samplefrequentie wordt vastgelegd en de steekproefgegevens wordt overgedragen aan het opslagaccount door een geplande aanvraag of een aanvraag voor op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="606f3-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="606f3-218">Automatische transfers kunnen zo vaak als één keer per minuut worden gepland.</span><span class="sxs-lookup"><span data-stu-id="606f3-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="606f3-219">Gegevens van prestatiemeteritems overgedragen door de agent diagnostische gegevens wordt opgeslagen in een tabel WADPerformanceCountersTable, in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="606f3-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="606f3-220">Deze tabel kan worden geopend en methoden die standaard Azure storage-API worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="606f3-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="606f3-221">Zie [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) voor een voorbeeld van het uitvoeren van query's en om gegevens van prestatiemeteritems uit de tabel WADPerformanceCountersTable weer te geven.</span><span class="sxs-lookup"><span data-stu-id="606f3-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="606f3-222">De meest recente prestatiemeteritemgegevens in het opslagaccount mogelijk enkele minuten verouderd, afhankelijk van de diagnostische gegevens agent overdracht frequentie en de latentie van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="606f3-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="606f3-223">Prestatiemeteritems configuratiebestand diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="606f3-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="606f3-224">Gebruik de volgende procedure om in te schakelen prestatiemeters in uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="606f3-225">Vereisten</span><span class="sxs-lookup"><span data-stu-id="606f3-225">Prerequisites</span></span>
<span data-ttu-id="606f3-226">Deze sectie wordt ervan uitgegaan dat u hebt de diagnostische monitor geïmporteerd in uw toepassing en het configuratiebestand van de diagnostische gegevens toegevoegd aan uw Visual Studio-oplossing (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger).</span><span class="sxs-lookup"><span data-stu-id="606f3-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="606f3-227">Zie stap 1 en 2 in [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md)) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="606f3-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="606f3-228">Stap 1: Verzamelen en opslaan van gegevens van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="606f3-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="606f3-229">Nadat u het bestand diagnostische gegevens aan uw Visual Studio-oplossing hebt toegevoegd, kunt u de verzameling en de opslag van gegevens van prestatiemeteritems configureren in een Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="606f3-230">Dit wordt gedaan door prestatiemeteritems toe te voegen aan het bestand diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="606f3-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="606f3-231">Diagnostics-gegevens, prestatiemeteritems, eerst worden verzameld op het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="606f3-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="606f3-232">De gegevens wordt vervolgens permanent in de tabel WADPerformanceCountersTable in de service Azure Table daarom moet u ook de storage-account in uw toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="606f3-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="606f3-233">Als u uw toepassing lokaal in de Emulator berekenen testen bent, kunt u diagnostische gegevens ook lokaal opslaan in de Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="606f3-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="606f3-234">Voordat u de diagnostics-gegevens opslaat, moet u eerst gaan naar de [Azure-portal](http://portal.azure.com/) en een klassieke opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="606f3-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="606f3-235">Er is een best practice vinden van uw opslagaccount in de dezelfde geografische locatie als uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="606f3-236">Door houdt die de Azure-toepassing en het opslagaccount zich in dezelfde geografische locatie, te voorkomen dat externe bandbreedtekosten te betalen en de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="606f3-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="606f3-237">Prestatie-items toevoegen aan het bestand diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="606f3-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="606f3-238">Er zijn veel prestatiemeteritems die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="606f3-238">There are many counters you can use.</span></span> <span data-ttu-id="606f3-239">Het volgende voorbeeld ziet enkele prestatiemeteritems die worden aanbevolen voor web- en bewaking van worker-rol.</span><span class="sxs-lookup"><span data-stu-id="606f3-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="606f3-240">Open het bestand diagnostics (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en voeg het volgende toe aan het element DiagnosticMonitorConfiguration:</span><span class="sxs-lookup"><span data-stu-id="606f3-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="606f3-241">Het kenmerk bufferQuotaInMB geeft de maximale hoeveelheid opslagruimte op het bestand systeem die beschikbaar is voor het gegevenstype voor verzameling (Azure Logboeken, IIS-logboeken, enz.).</span><span class="sxs-lookup"><span data-stu-id="606f3-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="606f3-242">De standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="606f3-242">The default is 0.</span></span> <span data-ttu-id="606f3-243">Wanneer het quotum is bereikt, wordt de oudste gegevens verwijderd als er nieuwe gegevens worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="606f3-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="606f3-244">De som van alle eigenschappen van de bufferQuotaInMB moet groter dan de waarde van het kenmerk OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="606f3-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="606f3-245">Voor meer gedetailleerde informatie om te bepalen hoeveel opslagruimte zijn vereist voor het verzamelen van diagnostische gegevens, Zie de sectie Setup af [Best Practices probleemoplossing voor Azure-toepassingen ontwikkelen](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="606f3-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="606f3-246">Het kenmerk scheduledTransferPeriod het interval tussen de geplande overdrachten van gegevens geeft, afgerond op het dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="606f3-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="606f3-247">In de volgende voorbeelden is deze ingesteld op PT30M (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="606f3-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="606f3-248">Wanneer de overdracht periode instelt op een kleine waarde, zoals 1 minuut, de prestaties van uw toepassing in productie nadelig beïnvloedt, maar kan handig zijn voor zien diagnostische gegevens snel te werken als u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="606f3-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="606f3-249">De geplande overdracht periode moet klein genoeg zijn om ervoor te zorgen dat de diagnostische gegevens niet van het exemplaar, maar groot genoeg is dat de prestaties van uw toepassing niet van invloed is overschreven.</span><span class="sxs-lookup"><span data-stu-id="606f3-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="606f3-250">Het kenmerk counterSpecifier Hiermee geeft u het prestatiemeteritem verzamelen.</span><span class="sxs-lookup"><span data-stu-id="606f3-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="606f3-251">Het kenmerk sampleRate geeft de snelheid waarmee het prestatiemeteritem moet actieve, in dit geval 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="606f3-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="606f3-252">Nadat u de prestatiemeteritems die u wilt verzamelen hebt toegevoegd, sla de wijzigingen naar het bestand diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="606f3-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="606f3-253">Vervolgens moet u het opslagaccount dat de diagnostics-gegevens gehandhaafd voor opgeven.</span><span class="sxs-lookup"><span data-stu-id="606f3-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="606f3-254">De storage-account opgeven</span><span class="sxs-lookup"><span data-stu-id="606f3-254">Specify the storage account</span></span>
<span data-ttu-id="606f3-255">Om te blijven behouden de diagnostische gegevens naar uw Azure Storage-account, moet u een verbindingsreeks in uw serviceconfiguratiebestand (ServiceConfiguration.cscfg).</span><span class="sxs-lookup"><span data-stu-id="606f3-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="606f3-256">Voor de Azure SDK 2.5, kan het Storage-Account worden opgegeven in het bestand diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="606f3-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="606f3-257">Deze instructies zijn alleen van toepassing op Azure SDK 2.4 en hieronder.</span><span class="sxs-lookup"><span data-stu-id="606f3-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="606f3-258">Voor de Azure SDK 2.5, kan het Storage-Account worden opgegeven in het bestand diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="606f3-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="606f3-259">De verbindingsreeksen instellen:</span><span class="sxs-lookup"><span data-stu-id="606f3-259">To set the connection strings:</span></span>

1. <span data-ttu-id="606f3-260">Open het ServiceConfiguration.Cloud.cscfg-bestand met behulp van uw favoriete teksteditor en stel de verbindingsreeks voor de opslag.</span><span class="sxs-lookup"><span data-stu-id="606f3-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="606f3-261">De *AccountName* en *AccountKey* waarden in de Azure-portal in het dashboard van de storage-account onder toegangstoetsen zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="606f3-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="606f3-262">Sla het bestand ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="606f3-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="606f3-263">Open het bestand ServiceConfiguration.Local.cscfg en controleren of UseDevelopmentStorage is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="606f3-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="606f3-264">Nu dat de verbindingsreeksen zijn ingesteld, wordt uw toepassing diagnostics-gegevens naar uw opslagaccount bewaard wanneer uw toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="606f3-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="606f3-265">Opslaan op het project bouwen en implementeren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="606f3-266">Stap 2: (Optioneel) Maak aangepaste prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="606f3-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="606f3-267">Naast de vooraf gedefinieerde prestatiemeteritems kunt u uw eigen aangepaste prestatiemeteritems voor het bewaken van web-of werkrollen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="606f3-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="606f3-268">Aangepaste prestatiemeteritems kunnen worden gebruikt voor het bijhouden en toepassingsspecifieke gedrag in de gaten en kan worden gemaakt of verwijderd in een opstarttaak Webrol of een werkrol met verhoogde machtigingen.</span><span class="sxs-lookup"><span data-stu-id="606f3-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="606f3-269">De prestaties teller configuratie uit het bestand .wadcfg een minuut na het starten van vernieuwen de Azure diagnostics-agent</span><span class="sxs-lookup"><span data-stu-id="606f3-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="606f3-270">Als u aangepaste prestatiemeteritems in de OnStart-methode maakt en uw opstarttaken duurt langer dan een minuut om uit te voeren, worden uw aangepaste prestatiemeteritems niet hebt gemaakt wanneer de agent Azure Diagnostics probeert te laden.</span><span class="sxs-lookup"><span data-stu-id="606f3-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="606f3-271">In dit scenario ziet u dat Azure Diagnostics correct worden alle diagnostische gegevens, behalve van uw aangepaste prestatiemeteritems vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="606f3-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="606f3-272">U lost dit probleem door de prestatiemeteritems maken in een taak starten of verplaats de werken sommige van uw taak starten van de OnStart-methode na het maken van de prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="606f3-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="606f3-273">Voer de volgende stappen voor het maken van een eenvoudige aangepaste Prestatiemeter '\MyCustomCounterCategory\MyButton1Counter':</span><span class="sxs-lookup"><span data-stu-id="606f3-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="606f3-274">Open het servicedefinitiebestand (CSDEF) voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="606f3-275">Voeg de Runtime-element op de WebRole of WorkerRole element dat moet worden uitgevoerd met verhoogde bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="606f3-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="606f3-276">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="606f3-276">Save the file.</span></span>
4. <span data-ttu-id="606f3-277">Open het bestand van de diagnostische gegevens (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en voeg het volgende toe aan de DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="606f3-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="606f3-278">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="606f3-278">Save the file.</span></span>
6. <span data-ttu-id="606f3-279">Maak de aangepaste Prestatiemeteritem-categorie in de OnStart-methode van uw rol voordat base wordt aangeroepen. OnStart.</span><span class="sxs-lookup"><span data-stu-id="606f3-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="606f3-280">De volgende C#-voorbeeld maakt een aangepaste categorie als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="606f3-280">The following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="606f3-281">Bijwerken van de items in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="606f3-281">Update the counters within your application.</span></span> <span data-ttu-id="606f3-282">Het volgende voorbeeld updates van een aangepaste prestatiemeteritem op Button1_Click gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="606f3-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="606f3-283">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="606f3-283">Save the file.</span></span>  

<span data-ttu-id="606f3-284">Aangepaste prestatiemeteritemgegevens worden nu verzameld door de monitor Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="606f3-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="606f3-285">Stap 3: De gegevens van prestatiemeteritems opvragen</span><span class="sxs-lookup"><span data-stu-id="606f3-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="606f3-286">Als uw toepassing wordt geïmplementeerd en uitgevoerd, de monitor Diagnostics gaat verder met het verzamelen van prestatiemeteritems en het behouden blijven van die gegevens naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="606f3-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="606f3-287">U hulpprogramma's zoals Server Explorer gebruiken in Visual Studio [Azure Opslagverkenner](http://azurestorageexplorer.codeplex.com/), of [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) door Cerebrata om weer te geven de prestatiemeteritems van de gegevens in de tabel WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="606f3-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="606f3-288">U kunt ook programmatisch query voor de tabel-service via [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), of [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="606f3-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="606f3-289">De volgende C#-voorbeeld ziet u een eenvoudige query op de tabel WADPerformanceCountersTable en slaat de diagnostics-gegevens op een CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="606f3-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="606f3-290">Zodra de prestatiemeteritems zijn opgeslagen op een CSV-bestand, kunt u de grafische mogelijkheden in Microsoft Excel of een ander hulpprogramma gebruiken om de gegevens te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="606f3-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="606f3-291">Zorg ervoor dat een verwijzing naar Microsoft.WindowsAzure.Storage.dll, toevoegen die wordt opgenomen in de Azure SDK voor .NET oktober 2012 en hoger.</span><span class="sxs-lookup"><span data-stu-id="606f3-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="606f3-292">De assembly is naar de map % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="606f3-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
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

<span data-ttu-id="606f3-293">Entiteiten worden toegewezen aan C#-objecten met behulp van een aangepaste klasse die is afgeleid van **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="606f3-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="606f3-294">De volgende code definieert een entiteitsklasse die staat voor een prestatiemeteritem in de **WADPerformanceCountersTable** tabel.</span><span class="sxs-lookup"><span data-stu-id="606f3-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="606f3-295">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="606f3-295">Next Steps</span></span>
[<span data-ttu-id="606f3-296">Aanvullende artikelen op Azure Diagnostics weergeven</span><span class="sxs-lookup"><span data-stu-id="606f3-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
