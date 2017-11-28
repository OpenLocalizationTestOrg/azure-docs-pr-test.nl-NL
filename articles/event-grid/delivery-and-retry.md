---
title: Azure Event raster levering en probeer het opnieuw
description: Beschrijft hoe Azure gebeurtenis raster gebeurtenissen biedt en de manier waarop niet-bezorgde berichten worden verwerkt.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: e0f8afdfd84ea3c0c061459c27da285f6ae8957e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="4fc31-103">Gebeurtenis raster berichtbezorging en probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="4fc31-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="4fc31-104">Dit artikel wordt beschreven hoe Azure gebeurtenis raster omgaat met gebeurtenissen bij levering is niet bevestigd.</span><span class="sxs-lookup"><span data-stu-id="4fc31-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="4fc31-105">Gebeurtenis raster bevat duurzame levering.</span><span class="sxs-lookup"><span data-stu-id="4fc31-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="4fc31-106">Elk bericht ten minste eenmaal voor elk abonnement levert.</span><span class="sxs-lookup"><span data-stu-id="4fc31-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="4fc31-107">Gebeurtenissen worden verzonden naar de geregistreerde webhook van elk abonnement onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="4fc31-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="4fc31-108">Als een webhook Bevestig de ontvangst van een gebeurtenis niet binnen 60 seconden na de eerste poging voor levering, opnieuw gebeurtenis raster levering van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4fc31-108">If a webhook does not acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="4fc31-109">Bericht bezorgingsstatus</span><span class="sxs-lookup"><span data-stu-id="4fc31-109">Message delivery status</span></span>

<span data-ttu-id="4fc31-110">Gebeurtenis raster maakt gebruik van HTTP-antwoordcodes ontvangst te bevestigen van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="4fc31-110">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="4fc31-111">Geslaagd-codes</span><span class="sxs-lookup"><span data-stu-id="4fc31-111">Success codes</span></span>

<span data-ttu-id="4fc31-112">De volgende codes voor HTTP-antwoord geven aan dat een gebeurtenis met succes is bezorgd bij uw webhook.</span><span class="sxs-lookup"><span data-stu-id="4fc31-112">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="4fc31-113">Gebeurtenis raster beschouwt levering voltooid.</span><span class="sxs-lookup"><span data-stu-id="4fc31-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="4fc31-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="4fc31-114">200 OK</span></span>
- <span data-ttu-id="4fc31-115">202 geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="4fc31-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="4fc31-116">Fout-codes</span><span class="sxs-lookup"><span data-stu-id="4fc31-116">Failure codes</span></span>

<span data-ttu-id="4fc31-117">De volgende codes voor HTTP-antwoord geven aan dat een gebeurtenis bezorging is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4fc31-117">The following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="4fc31-118">Gebeurtenis raster opnieuw geprobeerd om de gebeurtenis te verzenden.</span><span class="sxs-lookup"><span data-stu-id="4fc31-118">Event Grid tries again to send the event.</span></span> 

- <span data-ttu-id="4fc31-119">400 onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="4fc31-119">400 Bad Request</span></span>
- <span data-ttu-id="4fc31-120">401-niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="4fc31-120">401 Unauthorized</span></span>
- <span data-ttu-id="4fc31-121">404 – Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="4fc31-121">404 Not Found</span></span>
- <span data-ttu-id="4fc31-122">Time-out voor 408 aanvragen</span><span class="sxs-lookup"><span data-stu-id="4fc31-122">408 Request timeout</span></span>
- <span data-ttu-id="4fc31-123">414 URI te lang</span><span class="sxs-lookup"><span data-stu-id="4fc31-123">414 URI Too Long</span></span>
- <span data-ttu-id="4fc31-124">Interne serverfout 500</span><span class="sxs-lookup"><span data-stu-id="4fc31-124">500 Internal Server Error</span></span>
- <span data-ttu-id="4fc31-125">503 Service niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="4fc31-125">503 Service Unavailable</span></span>
- <span data-ttu-id="4fc31-126">504 gateway Timeout</span><span class="sxs-lookup"><span data-stu-id="4fc31-126">504 Gateway Timeout</span></span>

<span data-ttu-id="4fc31-127">Andere antwoordcode of een gebrek aan een antwoord geeft een fout.</span><span class="sxs-lookup"><span data-stu-id="4fc31-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="4fc31-128">Gebeurtenis raster pogingen levering.</span><span class="sxs-lookup"><span data-stu-id="4fc31-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="4fc31-129">Intervallen voor nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="4fc31-129">Retry intervals</span></span>

<span data-ttu-id="4fc31-130">Een beleid voor opnieuw proberen van exponentieel uitstel gebruikt voor gebeurtenis raster voor de levering van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4fc31-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="4fc31-131">Als uw webhook niet reageert of een foutcode retourneert, opnieuw gebeurtenis raster levering op het volgende schema:</span><span class="sxs-lookup"><span data-stu-id="4fc31-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="4fc31-132">10 seconden</span><span class="sxs-lookup"><span data-stu-id="4fc31-132">10 seconds</span></span>
2. <span data-ttu-id="4fc31-133">30 seconden</span><span class="sxs-lookup"><span data-stu-id="4fc31-133">30 seconds</span></span>
3. <span data-ttu-id="4fc31-134">1 minuut</span><span class="sxs-lookup"><span data-stu-id="4fc31-134">1 minute</span></span>
4. <span data-ttu-id="4fc31-135">5 minuten</span><span class="sxs-lookup"><span data-stu-id="4fc31-135">5 minutes</span></span>
5. <span data-ttu-id="4fc31-136">10 minuten</span><span class="sxs-lookup"><span data-stu-id="4fc31-136">10 minutes</span></span>
6. <span data-ttu-id="4fc31-137">30 minuten</span><span class="sxs-lookup"><span data-stu-id="4fc31-137">30 minutes</span></span>
7. <span data-ttu-id="4fc31-138">1 uur</span><span class="sxs-lookup"><span data-stu-id="4fc31-138">1 hour</span></span>

<span data-ttu-id="4fc31-139">Gebeurtenis raster voegt een kleine willekeurige toe aan alle intervallen voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="4fc31-139">Event Grid adds a small randomization to all retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="4fc31-140">Probeer duur</span><span class="sxs-lookup"><span data-stu-id="4fc31-140">Retry duration</span></span>

<span data-ttu-id="4fc31-141">Tijdens de preview verloopt Azure gebeurtenis raster alle gebeurtenissen die niet worden bezorgd binnen twee uur.</span><span class="sxs-lookup"><span data-stu-id="4fc31-141">During the preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="4fc31-142">Voordat u algemeen beschikbaar is, wordt deze tijd worden verhoogd tot 24 uur.</span><span class="sxs-lookup"><span data-stu-id="4fc31-142">Before General Availability, this time will be increased to 24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4fc31-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fc31-143">Next steps</span></span>

* <span data-ttu-id="4fc31-144">Zie voor een inleiding tot gebeurtenis raster, [over gebeurtenis raster](overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fc31-144">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="4fc31-145">Zie om snel aan de slag met Event raster [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="4fc31-145">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>