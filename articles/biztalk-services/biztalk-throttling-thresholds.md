---
title: aaaLearn over bandbreedtebeperking in BizTalk Services | Microsoft Docs
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="0fdfd-105">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="0fdfd-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="0fdfd-106">Azure BizTalk Services implementeert service bandbreedtebeperking op basis van twee voorwaarden: geheugen gebruiks- en Hallo aantal gelijktijdige berichten verwerken.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="0fdfd-107">In dit onderwerp bevat Hallo beperking drempelwaarden en beschrijft van Hallo runtimegedrag wanneer er een voorwaarde bandbreedteregeling optreedt.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="0fdfd-108">Beperking van de drempelwaarden</span><span class="sxs-lookup"><span data-stu-id="0fdfd-108">Throttling Thresholds</span></span>
<span data-ttu-id="0fdfd-109">Hallo volgende Tabellijsten Hallo bandbreedteregeling bron- en drempelwaarden:</span><span class="sxs-lookup"><span data-stu-id="0fdfd-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="0fdfd-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0fdfd-110">Description</span></span> | <span data-ttu-id="0fdfd-111">Lage drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="0fdfd-111">Low Threshold</span></span> | <span data-ttu-id="0fdfd-112">Hoge drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="0fdfd-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fdfd-113">Geheugen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-113">Memory</span></span> |<span data-ttu-id="0fdfd-114">% van totale systeem geheugen beschikbaar/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="0fdfd-115">Totaal aantal beschikbare PageFileBytes is ongeveer 2 maal Hallo RAM-geheugen van Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="0fdfd-116">60%</span><span class="sxs-lookup"><span data-stu-id="0fdfd-116">60%</span></span> |<span data-ttu-id="0fdfd-117">70%</span><span class="sxs-lookup"><span data-stu-id="0fdfd-117">70%</span></span> |
| <span data-ttu-id="0fdfd-118">Berichtverwerking</span><span class="sxs-lookup"><span data-stu-id="0fdfd-118">Message Processing</span></span> |<span data-ttu-id="0fdfd-119">Aantal berichten tegelijkertijd verwerken</span><span class="sxs-lookup"><span data-stu-id="0fdfd-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="0fdfd-120">40 * aantal kernen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-120">40 * number of cores</span></span> |<span data-ttu-id="0fdfd-121">100 * aantal kernen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-121">100 * number of cores</span></span> |

<span data-ttu-id="0fdfd-122">Wanneer u een hoge drempelwaarde wordt bereikt, wordt in Azure BizTalk Services toothrottle gestart.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="0fdfd-123">Beperking stopt wanneer Hallo lage drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="0fdfd-124">Bijvoorbeeld, is uw service met behulp van 65% systeemgeheugen.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="0fdfd-125">Hallo service komt niet in deze situatie vertraging.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="0fdfd-126">Uw service wordt gestart met behulp van het systeemgeheugen 70%.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="0fdfd-127">In dit geval Hallo service bandbreedte en toothrottle wordt vervolgd totdat Hallo service 60% (lage drempelwaarde) het systeemgeheugen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="0fdfd-128">Azure BizTalk Services houdt Hallo beperking status (normale status versus beperkte status) en Hallo duur beperking.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="0fdfd-129">Runtime-gedrag</span><span class="sxs-lookup"><span data-stu-id="0fdfd-129">Runtime Behavior</span></span>
<span data-ttu-id="0fdfd-130">Wanneer u Azure BizTalk Services in een bandbreedteregeling staat, wordt Hallo volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="0fdfd-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="0fdfd-131">Beperking is per rolexemplaar.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-131">Throttling is per role instance.</span></span> <span data-ttu-id="0fdfd-132">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fdfd-132">For example:</span></span><br/>
  <span data-ttu-id="0fdfd-133">RoleInstanceA is beperking.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="0fdfd-134">RoleInstanceB is geen beperking.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="0fdfd-135">In deze situatie verwerkt berichten in RoleInstanceB zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="0fdfd-136">Berichten in RoleInstanceA worden verwijderd en mislukt met de volgende fout Hallo:</span><span class="sxs-lookup"><span data-stu-id="0fdfd-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="0fdfd-137">
  **Server is bezet. Probeer het opnieuw.**</span><span class="sxs-lookup"><span data-stu-id="0fdfd-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="0fdfd-138">Een pull-bronnen geen pollen of downloaden van een bericht.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="0fdfd-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fdfd-139">For example:</span></span><br/>
  <span data-ttu-id="0fdfd-140">Een pijplijn haalt berichten uit een externe FTP-bron.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="0fdfd-141">Hallo rolinstantie doen Hallo pull opgehaald in een status bandbreedteregeling.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="0fdfd-142">In dit geval stopt Hallo pijplijn aanvullende berichten downloaden totdat de rolinstantie Hallo niet meer beperking.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="0fdfd-143">Een antwoord wordt verzonden toohello client Hallo-client kan het Hallo-bericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="0fdfd-144">U moet wachten tot het Hallo-beperking is opgelost.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="0fdfd-145">In het bijzonder moet u wachten tot Hallo lage drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="0fdfd-146">Belangrijke opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-146">Important notes</span></span>
* <span data-ttu-id="0fdfd-147">Beperking kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="0fdfd-148">Drempelwaarden beperking kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="0fdfd-149">Beperking, is de hele systeem geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="0fdfd-150">Hello Azure SQL Database-Server heeft ook ingebouwde beperking.</span><span class="sxs-lookup"><span data-stu-id="0fdfd-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="0fdfd-151">Aanvullende onderwerpen voor Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="0fdfd-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="0fdfd-152">Hello Azure BizTalk Services SDK installeren</span><span class="sxs-lookup"><span data-stu-id="0fdfd-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="0fdfd-153">Zelfstudies: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="0fdfd-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="0fdfd-154">Hoe gaan gebruiken Azure BizTalk Services SDK Hallo</span><span class="sxs-lookup"><span data-stu-id="0fdfd-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="0fdfd-155">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="0fdfd-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="0fdfd-156">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0fdfd-156">See Also</span></span>
* [<span data-ttu-id="0fdfd-157">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="0fdfd-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="0fdfd-158">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="0fdfd-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="0fdfd-159">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="0fdfd-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="0fdfd-160">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="0fdfd-161">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="0fdfd-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="0fdfd-162">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="0fdfd-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

