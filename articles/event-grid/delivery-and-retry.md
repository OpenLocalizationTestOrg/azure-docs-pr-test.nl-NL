---
title: aaaAzure gebeurtenis raster levering en probeer het opnieuw
description: Beschrijft hoe Azure gebeurtenis raster gebeurtenissen biedt en de manier waarop niet-bezorgde berichten worden verwerkt.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="36933-103">Gebeurtenis raster berichtbezorging en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="36933-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="36933-104">Dit artikel wordt beschreven hoe Azure gebeurtenis raster omgaat met gebeurtenissen bij levering is niet bevestigd.</span><span class="sxs-lookup"><span data-stu-id="36933-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="36933-105">Gebeurtenis raster bevat duurzame levering.</span><span class="sxs-lookup"><span data-stu-id="36933-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="36933-106">Elk bericht ten minste eenmaal voor elk abonnement levert.</span><span class="sxs-lookup"><span data-stu-id="36933-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="36933-107">Gebeurtenissen worden geregistreerd toohello webhook van elk abonnement onmiddellijk worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="36933-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="36933-108">Als een webhook niet ontvangstbevestiging is van een gebeurtenis binnen 60 seconden na de eerste levering Hallo proberen, gebeurtenis raster levering van Hallo gebeurtenis opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="36933-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="36933-109">Bericht bezorgingsstatus</span><span class="sxs-lookup"><span data-stu-id="36933-109">Message delivery status</span></span>

<span data-ttu-id="36933-110">Gebeurtenis raster maakt gebruik van HTTP-antwoord codes tooacknowledge ontvangst van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="36933-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="36933-111">Geslaagd-codes</span><span class="sxs-lookup"><span data-stu-id="36933-111">Success codes</span></span>

<span data-ttu-id="36933-112">Hallo volgende HTTP-antwoordcodes erop wijzen dat een gebeurtenis is geleverd met succes tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="36933-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="36933-113">Gebeurtenis raster beschouwt levering voltooid.</span><span class="sxs-lookup"><span data-stu-id="36933-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="36933-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="36933-114">200 OK</span></span>
- <span data-ttu-id="36933-115">202 geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="36933-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="36933-116">Fout-codes</span><span class="sxs-lookup"><span data-stu-id="36933-116">Failure codes</span></span>

<span data-ttu-id="36933-117">Hallo volgende HTTP-antwoordcodes erop wijzen dat een gebeurtenis bezorging is mislukt.</span><span class="sxs-lookup"><span data-stu-id="36933-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="36933-118">Gebeurtenis raster opnieuw geprobeerd toosend Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="36933-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="36933-119">400 onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="36933-119">400 Bad Request</span></span>
- <span data-ttu-id="36933-120">401-niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="36933-120">401 Unauthorized</span></span>
- <span data-ttu-id="36933-121">404 – Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="36933-121">404 Not Found</span></span>
- <span data-ttu-id="36933-122">Time-out voor 408 aanvragen</span><span class="sxs-lookup"><span data-stu-id="36933-122">408 Request timeout</span></span>
- <span data-ttu-id="36933-123">414 URI te lang</span><span class="sxs-lookup"><span data-stu-id="36933-123">414 URI Too Long</span></span>
- <span data-ttu-id="36933-124">Interne serverfout 500</span><span class="sxs-lookup"><span data-stu-id="36933-124">500 Internal Server Error</span></span>
- <span data-ttu-id="36933-125">503 Service niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="36933-125">503 Service Unavailable</span></span>
- <span data-ttu-id="36933-126">504 gateway Timeout</span><span class="sxs-lookup"><span data-stu-id="36933-126">504 Gateway Timeout</span></span>

<span data-ttu-id="36933-127">Andere antwoordcode of een gebrek aan een antwoord geeft een fout.</span><span class="sxs-lookup"><span data-stu-id="36933-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="36933-128">Gebeurtenis raster pogingen levering.</span><span class="sxs-lookup"><span data-stu-id="36933-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="36933-129">Intervallen voor nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="36933-129">Retry intervals</span></span>

<span data-ttu-id="36933-130">Een beleid voor opnieuw proberen van exponentieel uitstel gebruikt voor gebeurtenis raster voor de levering van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="36933-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="36933-131">Als uw webhook niet reageert of een foutcode retourneert, opnieuw gebeurtenis raster levering op Hallo schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="36933-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="36933-132">10 seconden</span><span class="sxs-lookup"><span data-stu-id="36933-132">10 seconds</span></span>
2. <span data-ttu-id="36933-133">30 seconden</span><span class="sxs-lookup"><span data-stu-id="36933-133">30 seconds</span></span>
3. <span data-ttu-id="36933-134">1 minuut</span><span class="sxs-lookup"><span data-stu-id="36933-134">1 minute</span></span>
4. <span data-ttu-id="36933-135">5 minuten</span><span class="sxs-lookup"><span data-stu-id="36933-135">5 minutes</span></span>
5. <span data-ttu-id="36933-136">10 minuten</span><span class="sxs-lookup"><span data-stu-id="36933-136">10 minutes</span></span>
6. <span data-ttu-id="36933-137">30 minuten</span><span class="sxs-lookup"><span data-stu-id="36933-137">30 minutes</span></span>
7. <span data-ttu-id="36933-138">1 uur</span><span class="sxs-lookup"><span data-stu-id="36933-138">1 hour</span></span>

<span data-ttu-id="36933-139">Gebeurtenis raster voegt een kleine willekeurige tooall opnieuw intervallen.</span><span class="sxs-lookup"><span data-stu-id="36933-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="36933-140">Probeer duur</span><span class="sxs-lookup"><span data-stu-id="36933-140">Retry duration</span></span>

<span data-ttu-id="36933-141">Tijdens de preview hello verloopt Azure gebeurtenis raster alle gebeurtenissen die niet worden bezorgd binnen twee uur.</span><span class="sxs-lookup"><span data-stu-id="36933-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="36933-142">Voordat algemeen beschikbaar is worden deze tijd toegenomen too24 uur.</span><span class="sxs-lookup"><span data-stu-id="36933-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="36933-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36933-143">Next steps</span></span>

* <span data-ttu-id="36933-144">Zie voor een inleiding-tooEvent raster [over gebeurtenis raster](overview.md).</span><span class="sxs-lookup"><span data-stu-id="36933-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="36933-145">tooquickly aan de slag met Event raster, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="36933-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
