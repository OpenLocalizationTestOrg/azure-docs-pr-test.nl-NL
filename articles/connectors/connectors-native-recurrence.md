---
title: De trigger terugkeerpatroon in logic apps toevoegen | Microsoft Docs
description: Overzicht van de trigger terugkeerpatroon en het gebruik ervan met een Azure logic app.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="623ad-103">Aan de slag met de trigger terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="623ad-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="623ad-104">U kunt met behulp van de trigger terugkeerpatroon krachtige werkstromen maken in de cloud.</span><span class="sxs-lookup"><span data-stu-id="623ad-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="623ad-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="623ad-105">For example, you can:</span></span>

* <span data-ttu-id="623ad-106">Een werkstroom wilt uitvoeren van een opgeslagen SQL-procedure elke dag plannen.</span><span class="sxs-lookup"><span data-stu-id="623ad-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="623ad-107">Een samenvatting weer van alle tweets e gedurende de afgelopen week over een bepaalde hashtag.</span><span class="sxs-lookup"><span data-stu-id="623ad-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="623ad-108">Om te beginnen met de trigger terugkeerpatroon in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="623ad-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="623ad-109">Gebruik een trigger terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="623ad-109">Use a recurrence trigger</span></span>
<span data-ttu-id="623ad-110">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="623ad-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="623ad-111">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="623ad-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="623ad-112">Hier volgt een voorbeeld van de volgorde van het instellen van een trigger terugkeerpatroon in een logische app:</span><span class="sxs-lookup"><span data-stu-id="623ad-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="623ad-113">Voeg de **terugkeerpatroon** trigger als de eerste stap in een logische app.</span><span class="sxs-lookup"><span data-stu-id="623ad-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="623ad-114">Vul in de parameters voor het terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="623ad-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="623ad-115">De logische app nu een uitgevoerd na elke tijdsinterval gestart.</span><span class="sxs-lookup"><span data-stu-id="623ad-115">The logic app now starts a run after each interval of time.</span></span>

![HTTP-trigger](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="623ad-117">Details van de trigger</span><span class="sxs-lookup"><span data-stu-id="623ad-117">Trigger details</span></span>
<span data-ttu-id="623ad-118">De trigger terugkeerpatroon heeft de volgende eigenschappen die u kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="623ad-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="623ad-119">Er wordt een logische app geactiveerd na een opgegeven tijdsinterval.</span><span class="sxs-lookup"><span data-stu-id="623ad-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="623ad-120">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="623ad-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="623ad-121">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="623ad-121">Display name</span></span> | <span data-ttu-id="623ad-122">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="623ad-122">Property name</span></span> | <span data-ttu-id="623ad-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="623ad-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="623ad-124">Frequentie *</span><span class="sxs-lookup"><span data-stu-id="623ad-124">Frequency*</span></span> |<span data-ttu-id="623ad-125">Frequentie</span><span class="sxs-lookup"><span data-stu-id="623ad-125">frequency</span></span> |<span data-ttu-id="623ad-126">De tijdseenheid: `Second`, `Minute`, `Hour`, `Day`, of `Year`.</span><span class="sxs-lookup"><span data-stu-id="623ad-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="623ad-127">Interval *</span><span class="sxs-lookup"><span data-stu-id="623ad-127">Interval*</span></span> |<span data-ttu-id="623ad-128">Interval</span><span class="sxs-lookup"><span data-stu-id="623ad-128">interval</span></span> |<span data-ttu-id="623ad-129">Het interval van de opgegeven frequentie voor het terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="623ad-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="623ad-130">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="623ad-130">Time Zone</span></span> |<span data-ttu-id="623ad-131">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="623ad-131">timeZone</span></span> |<span data-ttu-id="623ad-132">Als een begintijd zonder een UTC-offset is opgegeven, is deze tijdzone wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="623ad-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="623ad-133">Begintijd</span><span class="sxs-lookup"><span data-stu-id="623ad-133">Start time</span></span> |<span data-ttu-id="623ad-134">startTime</span><span class="sxs-lookup"><span data-stu-id="623ad-134">startTime</span></span> |<span data-ttu-id="623ad-135">De begintijd in [ISO 8601-notatie](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="623ad-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="623ad-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="623ad-136">Next steps</span></span>
<span data-ttu-id="623ad-137">Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="623ad-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="623ad-138">U kunt de beschikbare connectors in logische apps door te kijken verkennen onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="623ad-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

