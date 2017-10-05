---
title: Meer informatie over het beperken van in BizTalk Services | Microsoft Docs
description: Meer informatie over bandbreedtebeperking drempelwaarden en de resulterende gedrag van de runtime voor BizTalk Services. Bandbreedtebeperking is gebaseerd op het gebruik van geheugen en het aantal berichten. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="90bd2-105">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="90bd2-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="90bd2-106">Azure BizTalk Services implementeert service bandbreedtebeperking op basis van twee voorwaarden: geheugengebruik en het aantal gelijktijdige berichten verwerken.</span><span class="sxs-lookup"><span data-stu-id="90bd2-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="90bd2-107">Dit onderwerp geeft een lijst van de bandbreedteregeling drempelwaarden en beschrijft het runtimegedrag wanneer er een voorwaarde bandbreedteregeling optreedt.</span><span class="sxs-lookup"><span data-stu-id="90bd2-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="90bd2-108">Beperking van de drempelwaarden</span><span class="sxs-lookup"><span data-stu-id="90bd2-108">Throttling Thresholds</span></span>
<span data-ttu-id="90bd2-109">De volgende tabel bevat de drempelwaarden en bandbreedteregeling bron:</span><span class="sxs-lookup"><span data-stu-id="90bd2-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="90bd2-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="90bd2-110">Description</span></span> | <span data-ttu-id="90bd2-111">Lage drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="90bd2-111">Low Threshold</span></span> | <span data-ttu-id="90bd2-112">Hoge drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="90bd2-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90bd2-113">Geheugen</span><span class="sxs-lookup"><span data-stu-id="90bd2-113">Memory</span></span> |<span data-ttu-id="90bd2-114">% van totale systeem geheugen beschikbaar/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="90bd2-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="90bd2-115">Totaal aantal beschikbare PageFileBytes is ongeveer 2 keer de hoeveelheid RAM van het systeem.</span><span class="sxs-lookup"><span data-stu-id="90bd2-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="90bd2-116">60%</span><span class="sxs-lookup"><span data-stu-id="90bd2-116">60%</span></span> |<span data-ttu-id="90bd2-117">70%</span><span class="sxs-lookup"><span data-stu-id="90bd2-117">70%</span></span> |
| <span data-ttu-id="90bd2-118">Berichtverwerking</span><span class="sxs-lookup"><span data-stu-id="90bd2-118">Message Processing</span></span> |<span data-ttu-id="90bd2-119">Aantal berichten tegelijkertijd verwerken</span><span class="sxs-lookup"><span data-stu-id="90bd2-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="90bd2-120">40 * aantal kernen</span><span class="sxs-lookup"><span data-stu-id="90bd2-120">40 * number of cores</span></span> |<span data-ttu-id="90bd2-121">100 * aantal kernen</span><span class="sxs-lookup"><span data-stu-id="90bd2-121">100 * number of cores</span></span> |

<span data-ttu-id="90bd2-122">Wanneer een hoge drempelwaarde is bereikt, begint de Azure BizTalk Services om te beperken.</span><span class="sxs-lookup"><span data-stu-id="90bd2-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="90bd2-123">Beperking stopt wanneer de lage drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="90bd2-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="90bd2-124">Bijvoorbeeld, is uw service met behulp van 65% systeemgeheugen.</span><span class="sxs-lookup"><span data-stu-id="90bd2-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="90bd2-125">In dit geval heeft de service niet beperken.</span><span class="sxs-lookup"><span data-stu-id="90bd2-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="90bd2-126">Uw service wordt gestart met behulp van het systeemgeheugen 70%.</span><span class="sxs-lookup"><span data-stu-id="90bd2-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="90bd2-127">In dit geval kan de service beperkt en blijft totdat de service geheugen (lage drempelwaarde) 60 gebruikt % beperken.</span><span class="sxs-lookup"><span data-stu-id="90bd2-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="90bd2-128">Azure BizTalk Services houdt de status van de bandbreedteregeling (normale status versus beperkte status) en de duur van de bandbreedteregeling.</span><span class="sxs-lookup"><span data-stu-id="90bd2-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="90bd2-129">Runtime-gedrag</span><span class="sxs-lookup"><span data-stu-id="90bd2-129">Runtime Behavior</span></span>
<span data-ttu-id="90bd2-130">Wanneer u Azure BizTalk Services in een bandbreedteregeling staat, gebeurt het volgende:</span><span class="sxs-lookup"><span data-stu-id="90bd2-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="90bd2-131">Beperking is per rolexemplaar.</span><span class="sxs-lookup"><span data-stu-id="90bd2-131">Throttling is per role instance.</span></span> <span data-ttu-id="90bd2-132">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="90bd2-132">For example:</span></span><br/>
  <span data-ttu-id="90bd2-133">RoleInstanceA is beperking.</span><span class="sxs-lookup"><span data-stu-id="90bd2-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="90bd2-134">RoleInstanceB is geen beperking.</span><span class="sxs-lookup"><span data-stu-id="90bd2-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="90bd2-135">In deze situatie verwerkt berichten in RoleInstanceB zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="90bd2-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="90bd2-136">Berichten in RoleInstanceA worden verwijderd en mislukt met de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="90bd2-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="90bd2-137">
  **Server is bezet. Probeer het opnieuw.**</span><span class="sxs-lookup"><span data-stu-id="90bd2-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="90bd2-138">Een pull-bronnen geen pollen of downloaden van een bericht.</span><span class="sxs-lookup"><span data-stu-id="90bd2-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="90bd2-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="90bd2-139">For example:</span></span><br/>
  <span data-ttu-id="90bd2-140">Een pijplijn haalt berichten uit een externe FTP-bron.</span><span class="sxs-lookup"><span data-stu-id="90bd2-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="90bd2-141">De rolinstantie tijdens het doorzoeken van de pull opgehaald in een status bandbreedteregeling.</span><span class="sxs-lookup"><span data-stu-id="90bd2-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="90bd2-142">In dit geval is stopt de pijplijn aanvullende berichten downloaden totdat de rolinstantie niet meer beperking.</span><span class="sxs-lookup"><span data-stu-id="90bd2-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="90bd2-143">Een antwoord wordt verzonden naar de client, zodat de client opnieuw van het bericht indienen kunt.</span><span class="sxs-lookup"><span data-stu-id="90bd2-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="90bd2-144">U moet wachten totdat de beperking opgelost is.</span><span class="sxs-lookup"><span data-stu-id="90bd2-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="90bd2-145">In het bijzonder moet u wachten tot de lage drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="90bd2-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="90bd2-146">Belangrijke opmerkingen</span><span class="sxs-lookup"><span data-stu-id="90bd2-146">Important notes</span></span>
* <span data-ttu-id="90bd2-147">Beperking kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="90bd2-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="90bd2-148">Drempelwaarden beperking kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="90bd2-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="90bd2-149">Beperking, is de hele systeem geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="90bd2-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="90bd2-150">De Azure SQL Database-Server heeft ook ingebouwde beperking.</span><span class="sxs-lookup"><span data-stu-id="90bd2-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="90bd2-151">Aanvullende onderwerpen voor Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="90bd2-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="90bd2-152">De Azure BizTalk Services SDK installeren</span><span class="sxs-lookup"><span data-stu-id="90bd2-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="90bd2-153">Zelfstudies: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="90bd2-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="90bd2-154">De Azure BizTalk Services SDK gaan gebruiken</span><span class="sxs-lookup"><span data-stu-id="90bd2-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="90bd2-155">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="90bd2-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="90bd2-156">Zie ook</span><span class="sxs-lookup"><span data-stu-id="90bd2-156">See Also</span></span>
* [<span data-ttu-id="90bd2-157">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="90bd2-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="90bd2-158">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="90bd2-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="90bd2-159">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="90bd2-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="90bd2-160">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="90bd2-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="90bd2-161">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="90bd2-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="90bd2-162">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="90bd2-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

