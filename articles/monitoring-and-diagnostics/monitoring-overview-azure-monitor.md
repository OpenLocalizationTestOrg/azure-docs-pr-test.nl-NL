---
title: aaaAzure Systeemmonitor-overzicht | Microsoft Docs
description: Monitor voor Azure verzamelt statistieken voor gebruik in waarschuwingen, webhooks, automatisch schalen en automatisering. Artikel ook de naam van andere Microsoft-controle-opties.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="2c6bb-104">Overzicht van Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="2c6bb-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="2c6bb-105">Dit artikel bevat een overzicht van hello Azure Monitor-service in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-105">This article provides an overview of hello Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="2c6bb-106">Wordt besproken wat Azure Monitor biedt en aanwijzers tooadditional informatie bevat over het toouse Azure bewaken.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-106">It discusses what Azure Monitor does and provides pointers tooadditional information on how toouse Azure Monitor.</span></span>  <span data-ttu-id="2c6bb-107">Als u liever een video-inleiding, Zie de volgende stappen koppelingen op Hallo onder aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-107">If you prefer a video introduction, see Next steps links at hello bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="2c6bb-108">Uw toepassing of het systeem waarom te bewaken</span><span class="sxs-lookup"><span data-stu-id="2c6bb-108">Why monitor your application or system</span></span>
<span data-ttu-id="2c6bb-109">Cloud-toepassingen zijn complexe met veel bewegende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="2c6bb-110">Monitoring biedt gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-110">Monitoring provides data tooensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="2c6bb-111">Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-111">It also helps you toostave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="2c6bb-112">Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-112">In addition, you can use monitoring data toogain deep insights about your application.</span></span> <span data-ttu-id="2c6bb-113">Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-113">That knowledge can help you tooimprove application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="2c6bb-114">Monitor voor Azure en Microsoft's andere bewaking producten</span><span class="sxs-lookup"><span data-stu-id="2c6bb-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="2c6bb-115">Azure biedt een basisniveau infrastructuur metrische gegevens en logboeken voor de meeste services in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="2c6bb-116">Azure-services die nog plaats niet hun gegevens naar Azure-Monitor wordt deze geplaatst er in Hallo toekomstige.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-116">Azure services that do not yet put their data into Azure Monitor will put it there in hello future.</span></span>

<span data-ttu-id="2c6bb-117">Microsoft geleverd aanvullende producten en services die extra bewakingsmogelijkheden bieden voor ontwikkelaars, DevOps of IT-Ops waarvoor ook on-premises installaties.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="2c6bb-118">Zie voor een overzicht van en kennis van hoe deze verschillende producten en services samenwerken [bewaken in Microsoft Azure](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c6bb-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="2c6bb-119">Bronnen - Compute bewaking</span><span class="sxs-lookup"><span data-stu-id="2c6bb-119">Monitoring Sources - Compute</span></span>

![Model voor controle en diagnostische gegevens voor niet-rekenresources](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="2c6bb-121">Hallo Compute services bevatten</span><span class="sxs-lookup"><span data-stu-id="2c6bb-121">hello Compute services include</span></span> 
- <span data-ttu-id="2c6bb-122">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="2c6bb-122">Cloud Services</span></span> 
- <span data-ttu-id="2c6bb-123">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2c6bb-123">Virtual Machines</span></span> 
- <span data-ttu-id="2c6bb-124">Virtuele-machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="2c6bb-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="2c6bb-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2c6bb-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="2c6bb-126">Toepassing - Logboeken met diagnostische gegevens, logboeken en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="2c6bb-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="2c6bb-127">Toepassingen kunnen worden uitgevoerd in Hallo Gastbesturingssysteem in Hallo compute-model.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-127">Applications can run on top of hello Guest OS in hello compute model.</span></span> <span data-ttu-id="2c6bb-128">Ze verzenden hun eigen set logboeken en metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="2c6bb-129">Monitor voor Azure is afhankelijk van hello Azure diagnostics-extensie (Windows of Linux) toocollect meeste logboeken en niveau metrische gegevens voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-129">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) toocollect most application level metrics and logs.</span></span> <span data-ttu-id="2c6bb-130">Hallo-typen zijn</span><span class="sxs-lookup"><span data-stu-id="2c6bb-130">hello types include</span></span>

* <span data-ttu-id="2c6bb-131">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="2c6bb-131">Performance counters</span></span>
* <span data-ttu-id="2c6bb-132">Toepassingslogboeken</span><span class="sxs-lookup"><span data-stu-id="2c6bb-132">Application Logs</span></span>
* <span data-ttu-id="2c6bb-133">Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="2c6bb-133">Windows Event Logs</span></span>
* <span data-ttu-id="2c6bb-134">De gebeurtenisbron .NET</span><span class="sxs-lookup"><span data-stu-id="2c6bb-134">.NET Event Source</span></span>
* <span data-ttu-id="2c6bb-135">IIS-logboeken</span><span class="sxs-lookup"><span data-stu-id="2c6bb-135">IIS Logs</span></span>
* <span data-ttu-id="2c6bb-136">ETW op basis van het manifest</span><span class="sxs-lookup"><span data-stu-id="2c6bb-136">Manifest based ETW</span></span>
* <span data-ttu-id="2c6bb-137">Crashdumps</span><span class="sxs-lookup"><span data-stu-id="2c6bb-137">Crash Dumps</span></span>
* <span data-ttu-id="2c6bb-138">Klant-foutenlogboeken</span><span class="sxs-lookup"><span data-stu-id="2c6bb-138">Customer Error Logs</span></span>

<span data-ttu-id="2c6bb-139">Zonder Hallo-extensie voor diagnostische gegevens zijn slechts enkele metrische gegevens zoals CPU-gebruik beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-139">Without hello diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="2c6bb-140">Host en de Gast-VM metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="2c6bb-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="2c6bb-141">Hallo hebben eerder vermelde rekenresources en een toegewezen host VM gastbesturingssysteem ze met communiceren.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-141">hello previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="2c6bb-142">Hallo host, VM en gastbesturingssysteem zijn Hallo equivalent van basis-VM en Gast-VM in Hallo Hyper-V-hypervisor model.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-142">hello host VM and guest OS are hello equivalent of root VM and guest VM in hello Hyper-V hypervisor model.</span></span> <span data-ttu-id="2c6bb-143">U kunt metrische gegevens verzamelen op beide.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-143">You can collect metrics on both.</span></span> <span data-ttu-id="2c6bb-144">U kunt ook diagnostische logboeken verzamelen op Hallo gastbesturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-144">You can also collect diagnostics logs on hello guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="2c6bb-145">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="2c6bb-145">Activity Log</span></span>
<span data-ttu-id="2c6bb-146">U kunt Hallo activiteitenlogboek (eerder operationele of controlelogboeken genoemd) voor meer informatie zoeken over uw resource volgens hello Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-146">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> <span data-ttu-id="2c6bb-147">Hallo-logboek bevat informatie zoals de tijden waarop resources worden gemaakt of vernietigd.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-147">hello log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="2c6bb-148">Zie voor meer informatie [overzicht activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2c6bb-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="2c6bb-149">Bronnen - alle andere bewaking</span><span class="sxs-lookup"><span data-stu-id="2c6bb-149">Monitoring Sources - everything else</span></span>

![Model voor controle en diagnostische gegevens voor de compute-bronnen](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="2c6bb-151">Resource - diagnostische logboeken en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="2c6bb-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="2c6bb-152">Verzamelbaar metrische gegevens en diagnostische logboeken variëren, afhankelijk van het brontype Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-152">Collectable metrics and diagnostics logs vary based on hello resource type.</span></span> <span data-ttu-id="2c6bb-153">Web-Apps biedt bijvoorbeeld statistieken op Hallo schijf-i/o en CPU procent.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-153">For example, Web Apps provides statistics on hello Disk IO and Percent CPU.</span></span> <span data-ttu-id="2c6bb-154">Deze metrische gegevens bestaan voor een Service Bus-wachtrij die in plaats daarvan metrische gegevens zoals de grootte en het bericht doorvoer wachtrij biedt niet.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="2c6bb-155">Een lijst met verzamelbaar metrische gegevens voor elke resource is beschikbaar op [ondersteund metrische gegevens](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2c6bb-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="2c6bb-156">Host en de Gast-VM metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="2c6bb-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="2c6bb-157">Er is niet noodzakelijkerwijs een 1:1-toewijzing tussen de bron en een bepaalde Host of Gast-VM zodat metrische gegevens niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="2c6bb-158">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="2c6bb-158">Activity Log</span></span>
<span data-ttu-id="2c6bb-159">Hallo activiteitenlogboek is hetzelfde als voor de rekenresources Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-159">hello activity log is hello same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="2c6bb-160">Gebruikt voor het bewaken van gegevens</span><span class="sxs-lookup"><span data-stu-id="2c6bb-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="2c6bb-161">Nadat u uw gegevens verzamelt, kunt u doen met het volgende in de Azure-Monitor Hallo</span><span class="sxs-lookup"><span data-stu-id="2c6bb-161">Once you collect your data, you can do hello following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="2c6bb-162">Route</span><span class="sxs-lookup"><span data-stu-id="2c6bb-162">Route</span></span>
<span data-ttu-id="2c6bb-163">U kunt bewaking gegevens tooother locaties in realtime streamen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-163">You can stream monitoring data tooother locations in real time.</span></span>

<span data-ttu-id="2c6bb-164">Voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="2c6bb-164">Examples include:</span></span>

- <span data-ttu-id="2c6bb-165">TooApplication Insights verzenden zodat u de bijbehorende uitgebreidere visualisatie en analyse hulpprogramma's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-165">Send tooApplication Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="2c6bb-166">Stuur tooEvent Hubs zodat u hulpprogramma's toothird derden kunt versturen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-166">Send tooEvent Hubs so you can route toothird-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="2c6bb-167">Store en archiveren</span><span class="sxs-lookup"><span data-stu-id="2c6bb-167">Store and Archive</span></span>
<span data-ttu-id="2c6bb-168">Sommige bewakingsgegevens is al opgeslagen en beschikbaar zijn in de Azure-Monitor voor een bepaalde tijdsduur.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="2c6bb-169">Metrische gegevens worden opgeslagen voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="2c6bb-170">Logboekvermeldingen activiteit worden gedurende 90 dagen opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="2c6bb-171">Diagnostische logboeken worden niet op alle opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="2c6bb-172">Als u toostore gegevens langer dan Hallo perioden die wilt hierboven worden genoemd, kunt u een Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-172">If you want toostore data longer than hello time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="2c6bb-173">Het bewaken van gegevens wordt opgeslagen in uw storage-account op basis van een bewaarbeleid instellen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="2c6bb-174">U hebt toopay voor Hallo ruimte Hallo gegevens in Azure-opslag in beslag.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-174">You do have toopay for hello space hello data takes up in Azure storage.</span></span> 

<span data-ttu-id="2c6bb-175">Enkele manieren toouse deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="2c6bb-175">A few ways toouse this data:</span></span>

- <span data-ttu-id="2c6bb-176">U kunt andere hulpprogramma's binnen of buiten Azure worden gelezen en verwerkt hebben eenmaal geschreven.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="2c6bb-177">U downloadt Hallo-gegevens voor een lokale archief lokaal of uw bewaarbeleid in Hallo tookeep cloudgegevens voor langere tijd wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-177">You download hello data locally for a local archive or change your retention policy in hello cloud tookeep data for extended periods of time.</span></span>  
- <span data-ttu-id="2c6bb-178">U laten Hallo gegevens in Azure-opslag voor onbepaalde tijd voor archief doeleinden.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-178">You leave hello data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="2c6bb-179">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2c6bb-179">Query</span></span>
<span data-ttu-id="2c6bb-180">U kunt hello Azure Monitor REST API, platformoverschrijdende opdrachtregelinterface (CLI)-opdrachten, PowerShell-cmdlets gebruiken of Hallo .NET SDK tooaccess Hallo gegevens in Hallo systeem- of Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="2c6bb-180">You can use hello Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or hello .NET SDK tooaccess hello data in hello system or Azure storage</span></span>

<span data-ttu-id="2c6bb-181">Voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="2c6bb-181">Examples include:</span></span>

* <span data-ttu-id="2c6bb-182">Ophalen van gegevens voor een aangepaste bewaking toepassing die u hebt geschreven</span><span class="sxs-lookup"><span data-stu-id="2c6bb-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="2c6bb-183">Aangepaste query's maken en verzenden van die toepassing gegevens tooa van derden.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-183">Creating custom queries and sending that data tooa third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="2c6bb-184">Visualiseren</span><span class="sxs-lookup"><span data-stu-id="2c6bb-184">Visualize</span></span>
<span data-ttu-id="2c6bb-185">De controlegegevens in de afbeeldingen en grafieken visualiseren, kunt u trends sneller dan het opzoeken via Hallo gegevens zelf te vinden.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through hello data itself.</span></span>  

<span data-ttu-id="2c6bb-186">Een aantal visualisatie methoden zijn:</span><span class="sxs-lookup"><span data-stu-id="2c6bb-186">A few visualization methods include:</span></span>

* <span data-ttu-id="2c6bb-187">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2c6bb-187">Use hello Azure portal</span></span>
* <span data-ttu-id="2c6bb-188">Route gegevens tooAzure Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c6bb-188">Route data tooAzure Application Insights</span></span>
* <span data-ttu-id="2c6bb-189">Route gegevens tooMicrosoft Power BI</span><span class="sxs-lookup"><span data-stu-id="2c6bb-189">Route data tooMicrosoft PowerBI</span></span>
* <span data-ttu-id="2c6bb-190">Route Hallo gegevens tooa van derden visualisatie hulpprogramma met ofwel live te streamen of doordat de Hallo hulpprogramma lezen vanuit een archief in Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="2c6bb-190">Route hello data tooa third-party visualization tool using either live streaming or by having hello tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="2c6bb-191">Automatiseren</span><span class="sxs-lookup"><span data-stu-id="2c6bb-191">Automate</span></span>
<span data-ttu-id="2c6bb-192">U kunt gegevens tootrigger bewakingswaarschuwingen gebruiken of zelfs hele processen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-192">You can use monitoring data tootrigger alerts or even whole processes.</span></span> <span data-ttu-id="2c6bb-193">Voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="2c6bb-193">Examples include:</span></span>

* <span data-ttu-id="2c6bb-194">Gebruik gegevens tooautoscale compute-exemplaren omhoog of omlaag op basis van het laden van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-194">Use data tooautoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="2c6bb-195">Verzend een e-mailberichten wanneer een metriek een vooraf ingestelde drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="2c6bb-196">Een actie van een web-URL (webhook) tooexecute aanroepen in een systeem buiten Azure</span><span class="sxs-lookup"><span data-stu-id="2c6bb-196">Call a web URL (webhook) tooexecute an action in a system outside of Azure</span></span>
* <span data-ttu-id="2c6bb-197">Een runbook in Azure automation tooperform een verscheidenheid aan taken starten</span><span class="sxs-lookup"><span data-stu-id="2c6bb-197">Start a runbook in Azure automation tooperform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="2c6bb-198">Methoden van de toegang tot Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="2c6bb-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="2c6bb-199">In het algemeen kunt u gegevens bijhouden, Routering en ophalen via een van de volgende methoden Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-199">In general, you can manipulate data tracking, routing, and retrieval using one of hello following methods.</span></span> <span data-ttu-id="2c6bb-200">Niet alle methoden zijn beschikbaar voor alle acties of gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="2c6bb-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2c6bb-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="2c6bb-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c6bb-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="2c6bb-203">Platformoverschrijdende opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="2c6bb-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="2c6bb-204">REST API</span><span class="sxs-lookup"><span data-stu-id="2c6bb-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="2c6bb-205">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="2c6bb-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="2c6bb-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c6bb-206">Next steps</span></span>
<span data-ttu-id="2c6bb-207">Meer informatie over</span><span class="sxs-lookup"><span data-stu-id="2c6bb-207">Learn more about</span></span>
- <span data-ttu-id="2c6bb-208">Een video-overzicht van alleen Azure-Monitor is beschikbaar op</span><span class="sxs-lookup"><span data-stu-id="2c6bb-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="2c6bb-209">[Aan de slag met Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="2c6bb-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="2c6bb-210">Een extra video uitleg over een scenario waarin u Azure-Monitor kunt is beschikbaar op [verkennen Microsoft Azure-bewaking en diagnostische gegevens](https://channel9.msdn.com/events/Ignite/2016/BRK2234) en [Azure Monitor in een video Ignite 2016](https://myignite.microsoft.com/videos/4977)</span><span class="sxs-lookup"><span data-stu-id="2c6bb-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="2c6bb-211">Uitvoeren via hello Azure Monitor interface in [aan de slag met Azure-Monitor](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2c6bb-211">Run through hello Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="2c6bb-212">Hallo instellen [Azure Diagnostics Extensions](../azure-diagnostics.md) als u toodiagnose problemen in uw Cloud-Service, de virtuele Machine probeert virtuele machine instellen of Service Fabric-toepassing schalen.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-212">Set up hello [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting toodiagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="2c6bb-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) als u toodiagnostic problemen in uw App Service-Web-app probeert.</span><span class="sxs-lookup"><span data-stu-id="2c6bb-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying toodiagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="2c6bb-214">[Het oplossen van Azure Storage](../storage/common/storage-e2e-troubleshooting.md) bij gebruik van Storage-Blobs, tabellen of wachtrijen</span><span class="sxs-lookup"><span data-stu-id="2c6bb-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="2c6bb-215">[Meld u Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) en Hallo [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="2c6bb-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and hello [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
