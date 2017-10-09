---
title: aaaAdd een vertraging in logic apps | Microsoft Docs
description: Overzicht van Hallo vertraging en vertraging-totdat acties, en hoe toouse ze aan een Azure logic app.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="72834-103">Aan de slag met Hallo vertraging en vertraging-totdat acties</span><span class="sxs-lookup"><span data-stu-id="72834-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="72834-104">Met behulp van Hallo vertraging en ' vertraging-totdat ' acties, werkstroom-scenario's kan worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="72834-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="72834-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="72834-105">For example, you can:</span></span>

* <span data-ttu-id="72834-106">Wacht totdat een weekdag toosend status bijwerken via e-mail.</span><span class="sxs-lookup"><span data-stu-id="72834-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="72834-107">Vertraging Hallo werkstroom totdat een HTTP-aanroep heeft tijd toofinish voordat wordt hervat en ophalen van het Hallo-resultaat.</span><span class="sxs-lookup"><span data-stu-id="72834-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="72834-108">tooget gestart met Hallo vertraging actie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="72834-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="72834-109">Hallo vertraging acties gebruiken</span><span class="sxs-lookup"><span data-stu-id="72834-109">Use hello delay actions</span></span>
<span data-ttu-id="72834-110">Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="72834-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="72834-111">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72834-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="72834-112">Hier volgt een van de voorbeeldreeks hoe toouse een vertraging stap in een logische app:</span><span class="sxs-lookup"><span data-stu-id="72834-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="72834-113">Klik na het toevoegen van een trigger **nieuwe stap** tooadd een actie.</span><span class="sxs-lookup"><span data-stu-id="72834-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="72834-114">Zoeken naar **vertraging** toobring Hallo vertraging acties.</span><span class="sxs-lookup"><span data-stu-id="72834-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="72834-115">In dit voorbeeld selecteren we **vertraging**.</span><span class="sxs-lookup"><span data-stu-id="72834-115">In this example, we will select **Delay**.</span></span>
   
    ![Vertraging acties](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="72834-117">Voltooi alle Hallo actie eigenschappen tooconfigure Hallo vertraging.</span><span class="sxs-lookup"><span data-stu-id="72834-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Vertraging config](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="72834-119">Klik op **opslaan** toopublish en Hallo logische app activeren.</span><span class="sxs-lookup"><span data-stu-id="72834-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="72834-120">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="72834-120">Action details</span></span>
<span data-ttu-id="72834-121">Hallo terugkeerpatroon trigger heeft Hallo volgende eigenschappen die kunnen worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="72834-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="72834-122">Vertraging actie</span><span class="sxs-lookup"><span data-stu-id="72834-122">Delay action</span></span>
<span data-ttu-id="72834-123">Deze actie vertragingen hello uitvoeren voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="72834-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="72834-124">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="72834-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="72834-125">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="72834-125">Display name</span></span> | <span data-ttu-id="72834-126">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="72834-126">Property name</span></span> | <span data-ttu-id="72834-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72834-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72834-128">Aantal *</span><span class="sxs-lookup"><span data-stu-id="72834-128">Count*</span></span> |<span data-ttu-id="72834-129">Aantal</span><span class="sxs-lookup"><span data-stu-id="72834-129">count</span></span> |<span data-ttu-id="72834-130">het aantal keer eenheden toodelay Hallo</span><span class="sxs-lookup"><span data-stu-id="72834-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="72834-131">Eenheid *</span><span class="sxs-lookup"><span data-stu-id="72834-131">Unit*</span></span> |<span data-ttu-id="72834-132">eenheid</span><span class="sxs-lookup"><span data-stu-id="72834-132">unit</span></span> |<span data-ttu-id="72834-133">Hallo tijdseenheid: `Second`, `Minute`, `Hour`, of`Day`</span><span class="sxs-lookup"><span data-stu-id="72834-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="72834-134">Vertraging-totdat de actie</span><span class="sxs-lookup"><span data-stu-id="72834-134">Delay-until action</span></span>
<span data-ttu-id="72834-135">Deze actie een vertraging Hallo uitgevoerd totdat het een opgegeven datum/tijd.</span><span class="sxs-lookup"><span data-stu-id="72834-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="72834-136">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="72834-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="72834-137">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="72834-137">Display name</span></span> | <span data-ttu-id="72834-138">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="72834-138">Property name</span></span> | <span data-ttu-id="72834-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72834-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72834-140">Jaar *</span><span class="sxs-lookup"><span data-stu-id="72834-140">Year*</span></span> |<span data-ttu-id="72834-141">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="72834-141">timestamp</span></span> |<span data-ttu-id="72834-142">Hallo jaar toodelay tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="72834-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="72834-143">Maand *</span><span class="sxs-lookup"><span data-stu-id="72834-143">Month*</span></span> |<span data-ttu-id="72834-144">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="72834-144">timestamp</span></span> |<span data-ttu-id="72834-145">Hallo maand toodelay tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="72834-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="72834-146">Dag *</span><span class="sxs-lookup"><span data-stu-id="72834-146">Day*</span></span> |<span data-ttu-id="72834-147">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="72834-147">timestamp</span></span> |<span data-ttu-id="72834-148">Hallo dag toodelay tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="72834-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="72834-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72834-149">Next steps</span></span>
<span data-ttu-id="72834-150">Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="72834-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="72834-151">U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="72834-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

