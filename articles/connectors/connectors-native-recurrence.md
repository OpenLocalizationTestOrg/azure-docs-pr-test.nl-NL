---
title: aaaAdd hello terugkeerpatroon trigger in logic apps | Microsoft Docs
description: Overzicht van Hallo terugkeerpatroon geactiveerd, en hoe toouse deze met een logische Azure-app.
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="85eae-103">Aan de slag met Hallo terugkeerpatroon trigger</span><span class="sxs-lookup"><span data-stu-id="85eae-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="85eae-104">Hallo terugkeerpatroon door trigger te gebruiken, kunt u krachtige werkstromen in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="85eae-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="85eae-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="85eae-105">For example, you can:</span></span>

* <span data-ttu-id="85eae-106">Een werkstroom toorun opgeslagen SQL-procedure elke dag plannen.</span><span class="sxs-lookup"><span data-stu-id="85eae-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="85eae-107">Een samenvatting weer van alle tweets binnen de afgelopen week over een bepaalde hashtag Hallo e.</span><span class="sxs-lookup"><span data-stu-id="85eae-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="85eae-108">tooget de slag met Hallo terugkeerpatroon trigger in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="85eae-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="85eae-109">Gebruik een trigger terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="85eae-109">Use a recurrence trigger</span></span>
<span data-ttu-id="85eae-110">Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="85eae-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="85eae-111">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85eae-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="85eae-112">Hier volgt een van de voorbeeldreeks hoe tooset van een terugkeerpatroon in een logische app activeren:</span><span class="sxs-lookup"><span data-stu-id="85eae-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="85eae-113">Hallo toevoegen **terugkeerpatroon** trigger als Hallo eerste stap in een logische app.</span><span class="sxs-lookup"><span data-stu-id="85eae-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="85eae-114">Hallo parameters invullen voor Hallo terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="85eae-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="85eae-115">Hallo logische app nu een uitgevoerd na elke tijdsinterval gestart.</span><span class="sxs-lookup"><span data-stu-id="85eae-115">hello logic app now starts a run after each interval of time.</span></span>

![HTTP-trigger](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="85eae-117">Details van de trigger</span><span class="sxs-lookup"><span data-stu-id="85eae-117">Trigger details</span></span>
<span data-ttu-id="85eae-118">Hallo terugkeerpatroon trigger heeft Hallo volgende eigenschappen die u kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="85eae-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="85eae-119">Er wordt een logische app geactiveerd na een opgegeven tijdsinterval.</span><span class="sxs-lookup"><span data-stu-id="85eae-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="85eae-120">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="85eae-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="85eae-121">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="85eae-121">Display name</span></span> | <span data-ttu-id="85eae-122">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="85eae-122">Property name</span></span> | <span data-ttu-id="85eae-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85eae-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85eae-124">Frequentie *</span><span class="sxs-lookup"><span data-stu-id="85eae-124">Frequency*</span></span> |<span data-ttu-id="85eae-125">frequency</span><span class="sxs-lookup"><span data-stu-id="85eae-125">frequency</span></span> |<span data-ttu-id="85eae-126">Hallo tijdseenheid: `Second`, `Minute`, `Hour`, `Day`, of `Year`.</span><span class="sxs-lookup"><span data-stu-id="85eae-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="85eae-127">Interval *</span><span class="sxs-lookup"><span data-stu-id="85eae-127">Interval*</span></span> |<span data-ttu-id="85eae-128">interval</span><span class="sxs-lookup"><span data-stu-id="85eae-128">interval</span></span> |<span data-ttu-id="85eae-129">Hallo tijdsinterval Hallo opgegeven frequentie voor Hallo terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="85eae-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="85eae-130">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="85eae-130">Time Zone</span></span> |<span data-ttu-id="85eae-131">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="85eae-131">timeZone</span></span> |<span data-ttu-id="85eae-132">Als een begintijd zonder een UTC-offset is opgegeven, is deze tijdzone wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="85eae-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="85eae-133">Begintijd</span><span class="sxs-lookup"><span data-stu-id="85eae-133">Start time</span></span> |<span data-ttu-id="85eae-134">startTime</span><span class="sxs-lookup"><span data-stu-id="85eae-134">startTime</span></span> |<span data-ttu-id="85eae-135">Hallo begintijd in [ISO 8601-notatie](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="85eae-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="85eae-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85eae-136">Next steps</span></span>
<span data-ttu-id="85eae-137">Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="85eae-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="85eae-138">U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="85eae-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

