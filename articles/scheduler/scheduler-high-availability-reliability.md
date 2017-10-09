---
title: aaaScheduler hoge beschikbaarheid en betrouwbaarheid
description: Hoge beschikbaarheid en betrouwbaarheid
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="b14e5-103">Hoge beschikbaarheid en betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="b14e5-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="b14e5-104">Hoge beschikbaarheid met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b14e5-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="b14e5-105">Als een Azure-platform-service core Azure Scheduler is maximaal beschikbaar en functionaliteit voor zowel geografisch redundante service-implementatie en geo-landinstelling taak replicatie.</span><span class="sxs-lookup"><span data-stu-id="b14e5-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="b14e5-106">Geografisch redundante service-implementatie</span><span class="sxs-lookup"><span data-stu-id="b14e5-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="b14e5-107">Azure Scheduler is beschikbaar via de gebruikersinterface in bijna elke geografische regio die deel uitmaakt van Azure vandaag Hallo.</span><span class="sxs-lookup"><span data-stu-id="b14e5-107">Azure Scheduler is available via hello UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="b14e5-108">Hallo-lijst met regio's die beschikbaar is in Azure Scheduler is [hier vermeld](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="b14e5-108">hello list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="b14e5-109">Als een datacentrum in een gehoste regio niet beschikbaar wordt weergegeven, zijn Hallo failover-mogelijkheden van Azure Scheduler zodat Hallo service beschikbaar vanuit een ander datacenter is.</span><span class="sxs-lookup"><span data-stu-id="b14e5-109">If a data center in a hosted region is rendered unavailable, hello failover capabilities of Azure Scheduler are such that hello service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="b14e5-110">Geo-landinstelling taak replicatie</span><span class="sxs-lookup"><span data-stu-id="b14e5-110">Geo-regional job replication</span></span>
<span data-ttu-id="b14e5-111">Niet alleen Hallo is Azure Scheduler front-end beschikbaar voor de management-aanvragen, maar uw eigen baan is ook geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="b14e5-111">Not only is hello Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="b14e5-112">Wanneer er een storing in een regio, wordt Azure Scheduler failover wordt uitgevoerd en garandeert dat die Hallo-taak wordt uitgevoerd vanaf een ander datacenter Hallo gekoppelde geografische regio.</span><span class="sxs-lookup"><span data-stu-id="b14e5-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that hello job is run from another data center in hello paired geographic region.</span></span>

<span data-ttu-id="b14e5-113">Bijvoorbeeld, als u een taak hebt gemaakt in Zuid-centraal VS, repliceert Azure Scheduler automatisch deze taak in Noordelijk Centraal, VS.</span><span class="sxs-lookup"><span data-stu-id="b14e5-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="b14e5-114">Wanneer er een fout in Zuid-centraal VS, Azure Scheduler zorgt ervoor dat Hallo-taak wordt uitgevoerd vanaf Noordelijk Centraal, VS.</span><span class="sxs-lookup"><span data-stu-id="b14e5-114">When there’s a failure in South Central US, Azure Scheduler ensures that hello job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="b14e5-115">Azure Scheduler als gevolg hiervan zorgt ervoor dat uw gegevens blijft binnen dezelfde breder geografische regio in geval van een Azure storing Hallo.</span><span class="sxs-lookup"><span data-stu-id="b14e5-115">As a result, Azure Scheduler ensures that your data stays within hello same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="b14e5-116">Als gevolg hiervan moet u de taak alleen tooadd hoge beschikbaarheid dubbele – Azure Scheduler automatisch biedt mogelijkheden voor hoge beschikbaarheid voor uw taken.</span><span class="sxs-lookup"><span data-stu-id="b14e5-116">As a result, you need not duplicate your job just tooadd high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="b14e5-117">Azure Scheduler-betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="b14e5-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="b14e5-118">Azure Scheduler wordt gegarandeerd dat een eigen hoge beschikbaarheid en gaat een andere benadering taken toouser gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b14e5-118">Azure Scheduler guarantees its own high-availability and takes a different approach toouser-created jobs.</span></span> <span data-ttu-id="b14e5-119">De taak kan bijvoorbeeld een HTTP-eindpunt is niet beschikbaar aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b14e5-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="b14e5-120">Azure Scheduler niettemin probeert tooexecute uw taak voltooid, doordat u alternatieve opties toodeal met fout.</span><span class="sxs-lookup"><span data-stu-id="b14e5-120">Azure Scheduler nonetheless tries tooexecute your job successfully, by giving you alternative options toodeal with failure.</span></span> <span data-ttu-id="b14e5-121">Azure Scheduler wordt dit op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="b14e5-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="b14e5-122">Configureerbare beleid voor opnieuw proberen via "retryPolicy"</span><span class="sxs-lookup"><span data-stu-id="b14e5-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="b14e5-123">Azure Scheduler kunt u tooconfigure een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="b14e5-123">Azure Scheduler allows you tooconfigure a retry policy.</span></span> <span data-ttu-id="b14e5-124">Standaard, als een taak mislukt, probeert Scheduler Hallo taak opnieuw vier keer, met een interval van 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="b14e5-124">By default, if a job fails, Scheduler tries hello job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="b14e5-125">U kunt deze opnieuw beleid toobe agressievere (bijvoorbeeld tien keer met een interval van 30 seconden) opnieuw configureren of lossere (bijvoorbeeld twee keer per dag intervallen.)</span><span class="sxs-lookup"><span data-stu-id="b14e5-125">You may re-configure this retry policy toobe more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="b14e5-126">Als een voorbeeld van wanneer Hiermee kunt kunt u een taak die eenmaal per week wordt uitgevoerd en roept een HTTP-eindpunt maken.</span><span class="sxs-lookup"><span data-stu-id="b14e5-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="b14e5-127">Als Hallo HTTP-eindpunt is niet toegankelijk wegens een paar uur wanneer de taak wordt uitgevoerd, kunt u niet toowait één meer week voor Hallo taak toorun opnieuw omdat zelfs Hallo standaardbeleid voor opnieuw proberen mislukken.</span><span class="sxs-lookup"><span data-stu-id="b14e5-127">If hello HTTP endpoint is down for a few hours when your job runs, you may not want toowait one more week for hello job toorun again since even hello default retry policy will fail.</span></span> <span data-ttu-id="b14e5-128">In dergelijke gevallen kunt u mogelijk opnieuw configureren Hallo standaardproces voor nieuwe pogingen beleid tooretry elke drie uur (bijvoorbeeld) in plaats van elke 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="b14e5-128">In such cases, you may reconfigure hello standard retry policy tooretry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="b14e5-129">hoe tooconfigure een beleid voor opnieuw proberen te verwijzen toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span><span class="sxs-lookup"><span data-stu-id="b14e5-129">toolearn how tooconfigure a retry policy, refer too[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="b14e5-130">Alternatieve eindpunt configuratiemogelijkheden via "errorAction"</span><span class="sxs-lookup"><span data-stu-id="b14e5-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="b14e5-131">Als Hallo doel eindpunt voor uw Azure Scheduler-taak niet bereikbaar blijft, terugvalt Azure Scheduler alternatieve eindpunt voor foutafhandeling toohello nadat u het beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="b14e5-131">If hello target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back toohello alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="b14e5-132">Als een alternatieve eindpunt voor foutafhandeling is geconfigureerd, wordt het door Azure Scheduler aanroept.</span><span class="sxs-lookup"><span data-stu-id="b14e5-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="b14e5-133">Uw eigen taken zijn met een alternatieve eindpunt maximaal beschikbaar is in Hallo face van de fout.</span><span class="sxs-lookup"><span data-stu-id="b14e5-133">With an alternate endpoint, your own jobs are highly available in hello face of failure.</span></span>

<span data-ttu-id="b14e5-134">Azure Scheduler volgt bijvoorbeeld in Hallo diagram hieronder, de nieuwe poging beleid toohit een New York-webservice.</span><span class="sxs-lookup"><span data-stu-id="b14e5-134">As an example, in hello diagram below, Azure Scheduler follows its retry policy toohit a New York web service.</span></span> <span data-ttu-id="b14e5-135">Nadat Hallo mislukken pogingen, wordt gecontroleerd of er een alternatief is.</span><span class="sxs-lookup"><span data-stu-id="b14e5-135">After hello retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="b14e5-136">Vervolgens gaat het verder en wordt gestart die aanvragen indienen toohello alternatieve Hello dezelfde beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="b14e5-136">It then goes ahead and starts making requests toohello alternate with hello same retry policy.</span></span>

![][2]

<span data-ttu-id="b14e5-137">Let op Hallo van hetzelfde beleid voor opnieuw proberen is van toepassing tooboth Hallo oorspronkelijke actie en Hallo alternatieve fout.</span><span class="sxs-lookup"><span data-stu-id="b14e5-137">Note that hello same retry policy applies tooboth hello original action and hello alternate error action.</span></span> <span data-ttu-id="b14e5-138">Het ook mogelijk toohave Hallo alternatieve fout van de actie actietype afwijken van actietype Hallo belangrijkste actie.</span><span class="sxs-lookup"><span data-stu-id="b14e5-138">It’s also possible toohave hello alternate error action’s action type be different from hello main action’s action type.</span></span> <span data-ttu-id="b14e5-139">Bijvoorbeeld, terwijl de belangrijkste actie Hallo van een HTTP-eindpunt aanroepen kan, Hallo foutbewerking in plaats daarvan mogelijk een opslagwachtrij-, service bus-wachtrij- of service bus-onderwerpactie die foutregistratie biedt.</span><span class="sxs-lookup"><span data-stu-id="b14e5-139">For example, while hello main action may be invoking an HTTP endpoint, hello error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="b14e5-140">hoe een eindpunt alternate tooconfigure te verwijzen toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span><span class="sxs-lookup"><span data-stu-id="b14e5-140">toolearn how tooconfigure an alternate endpoint, refer too[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="b14e5-141">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b14e5-141">See Also</span></span>
 [<span data-ttu-id="b14e5-142">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="b14e5-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b14e5-143">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="b14e5-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b14e5-144">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b14e5-144">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="b14e5-145">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b14e5-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b14e5-146">Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b14e5-146">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="b14e5-147">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b14e5-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b14e5-148">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="b14e5-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b14e5-149">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="b14e5-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="b14e5-150">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="b14e5-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
