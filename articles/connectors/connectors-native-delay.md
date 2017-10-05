---
title: Toevoegen van een vertraging in logic apps | Microsoft Docs
description: Overzicht van de vertraging en vertraging-totdat acties en hoe u deze met een Azure logic app gebruikt.
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="5eeba-103">Aan de slag met vertraging en vertraging-totdat acties</span><span class="sxs-lookup"><span data-stu-id="5eeba-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="5eeba-104">Met behulp van de vertraging en ' vertraging-totdat ' acties, werkstroom-scenario's kan worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="5eeba-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="5eeba-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5eeba-105">For example, you can:</span></span>

* <span data-ttu-id="5eeba-106">Wachten totdat een weekdag een statusupdate verzenden via e-mail.</span><span class="sxs-lookup"><span data-stu-id="5eeba-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="5eeba-107">De werkstroom uit te stellen tot er een HTTP-aanroep is tijd om te voltooien voordat wordt hervat en het ophalen van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="5eeba-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="5eeba-108">Om te beginnen met de actie vertraging in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5eeba-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="5eeba-109">De vertraging acties gebruiken</span><span class="sxs-lookup"><span data-stu-id="5eeba-109">Use the delay actions</span></span>
<span data-ttu-id="5eeba-110">Een actie is een bewerking die wordt uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="5eeba-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="5eeba-111">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5eeba-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="5eeba-112">Hier volgt een voorbeeld van de volgorde van het gebruik van een vertraging stap in een logische app:</span><span class="sxs-lookup"><span data-stu-id="5eeba-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="5eeba-113">Klik na het toevoegen van een trigger **nieuwe stap** een actie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5eeba-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="5eeba-114">Zoeken naar **vertraging** online zetten van de acties vertraging.</span><span class="sxs-lookup"><span data-stu-id="5eeba-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="5eeba-115">In dit voorbeeld selecteren we **vertraging**.</span><span class="sxs-lookup"><span data-stu-id="5eeba-115">In this example, we will select **Delay**.</span></span>
   
    ![Vertraging acties](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="5eeba-117">Voltooi alle van de actie-eigenschappen voor het configureren van de vertraging.</span><span class="sxs-lookup"><span data-stu-id="5eeba-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Vertraging config](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="5eeba-119">Klik op **opslaan** publiceren en activeren van de logische app.</span><span class="sxs-lookup"><span data-stu-id="5eeba-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="5eeba-120">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="5eeba-120">Action details</span></span>
<span data-ttu-id="5eeba-121">De trigger terugkeerpatroon heeft de volgende eigenschappen die kunnen worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5eeba-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="5eeba-122">Vertraging actie</span><span class="sxs-lookup"><span data-stu-id="5eeba-122">Delay action</span></span>
<span data-ttu-id="5eeba-123">Deze actie een vertraging de uitvoeren voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="5eeba-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="5eeba-124">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="5eeba-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="5eeba-125">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5eeba-125">Display name</span></span> | <span data-ttu-id="5eeba-126">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="5eeba-126">Property name</span></span> | <span data-ttu-id="5eeba-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5eeba-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5eeba-128">Aantal *</span><span class="sxs-lookup"><span data-stu-id="5eeba-128">Count*</span></span> |<span data-ttu-id="5eeba-129">Aantal</span><span class="sxs-lookup"><span data-stu-id="5eeba-129">count</span></span> |<span data-ttu-id="5eeba-130">Het aantal tijdseenheden vertraging</span><span class="sxs-lookup"><span data-stu-id="5eeba-130">The number of time units to delay</span></span> |
| <span data-ttu-id="5eeba-131">Eenheid *</span><span class="sxs-lookup"><span data-stu-id="5eeba-131">Unit*</span></span> |<span data-ttu-id="5eeba-132">eenheid</span><span class="sxs-lookup"><span data-stu-id="5eeba-132">unit</span></span> |<span data-ttu-id="5eeba-133">De tijdseenheid: `Second`, `Minute`, `Hour`, of`Day`</span><span class="sxs-lookup"><span data-stu-id="5eeba-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="5eeba-134">Vertraging-totdat de actie</span><span class="sxs-lookup"><span data-stu-id="5eeba-134">Delay-until action</span></span>
<span data-ttu-id="5eeba-135">Deze actie een vertraging de uitvoeren tot een opgegeven datum/tijd.</span><span class="sxs-lookup"><span data-stu-id="5eeba-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="5eeba-136">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="5eeba-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="5eeba-137">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5eeba-137">Display name</span></span> | <span data-ttu-id="5eeba-138">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="5eeba-138">Property name</span></span> | <span data-ttu-id="5eeba-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5eeba-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5eeba-140">Jaar *</span><span class="sxs-lookup"><span data-stu-id="5eeba-140">Year*</span></span> |<span data-ttu-id="5eeba-141">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="5eeba-141">timestamp</span></span> |<span data-ttu-id="5eeba-142">Het jaar tot uitstellen tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="5eeba-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="5eeba-143">Maand *</span><span class="sxs-lookup"><span data-stu-id="5eeba-143">Month*</span></span> |<span data-ttu-id="5eeba-144">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="5eeba-144">timestamp</span></span> |<span data-ttu-id="5eeba-145">De maand tot uitstellen tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="5eeba-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="5eeba-146">Dag *</span><span class="sxs-lookup"><span data-stu-id="5eeba-146">Day*</span></span> |<span data-ttu-id="5eeba-147">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="5eeba-147">timestamp</span></span> |<span data-ttu-id="5eeba-148">De dag uitstellen tot (GMT)</span><span class="sxs-lookup"><span data-stu-id="5eeba-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="5eeba-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5eeba-149">Next steps</span></span>
<span data-ttu-id="5eeba-150">Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5eeba-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5eeba-151">U kunt de beschikbare connectors in logische apps door te kijken verkennen onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5eeba-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

