---
title: Aanvraag en -antwoord acties gebruiken | Microsoft Docs
description: Overzicht van de aanvraag en antwoord-trigger en action in een Azure logic app
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="6c780-103">Aan de slag met de aanvraag en antwoord-onderdelen</span><span class="sxs-lookup"><span data-stu-id="6c780-103">Get started with the request and response components</span></span>
<span data-ttu-id="6c780-104">Met de aanvraag- en -onderdelen in een logische app kunt u in realtime reageren op gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6c780-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="6c780-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6c780-105">For example, you can:</span></span>

* <span data-ttu-id="6c780-106">Reageren op een HTTP-aanvraag met gegevens van een on-premises database via een logische app.</span><span class="sxs-lookup"><span data-stu-id="6c780-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="6c780-107">Een logische app vanaf een externe webhook-gebeurtenis geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="6c780-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="6c780-108">Een logische app met de actie aanvraag en -antwoord uit in een andere logische app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="6c780-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="6c780-109">Om te beginnen met de aanvraag en antwoord-acties in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c780-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="6c780-110">Gebruik de trigger HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="6c780-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="6c780-111">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="6c780-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="6c780-112">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c780-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="6c780-113">Hier volgt een voorbeeld van de volgorde van het instellen van een HTTP-aanvraag in de ontwerpfunctie voor Logic App.</span><span class="sxs-lookup"><span data-stu-id="6c780-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="6c780-114">De trigger toevoegen **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="6c780-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="6c780-115">U kunt desgewenst een JSON-schema (met behulp van een hulpprogramma zoals [JSONSchema.net](http://jsonschema.net)) voor de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="6c780-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="6c780-116">Hierdoor kan de ontwerpfunctie voor het genereren van tokens voor eigenschappen in de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6c780-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="6c780-117">Nog een actie toevoegen zodat u de logische app kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="6c780-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="6c780-118">Na het opslaan van de logische app, kunt u de HTTP-aanvraag-URL ophalen van de aanvraag-kaart.</span><span class="sxs-lookup"><span data-stu-id="6c780-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="6c780-119">Een HTTP POST (kunt u een hulpprogramma zoals [Postman](https://www.getpostman.com/)) naar de URL activeert de logische app.</span><span class="sxs-lookup"><span data-stu-id="6c780-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="6c780-120">Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord wordt onmiddellijk geretourneerd naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="6c780-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="6c780-121">U kunt de antwoord-actie voor het aanpassen van een antwoord.</span><span class="sxs-lookup"><span data-stu-id="6c780-121">You can use the response action to customize a response.</span></span>
> 
> 

![Antwoord trigger](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="6c780-123">Gebruik de actie HTTP-antwoord</span><span class="sxs-lookup"><span data-stu-id="6c780-123">Use the HTTP Response action</span></span>
<span data-ttu-id="6c780-124">De HTTP-antwoord-actie is alleen geldig wanneer u deze gebruikt in een werkstroom die wordt geactiveerd door een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6c780-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="6c780-125">Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord wordt onmiddellijk geretourneerd naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="6c780-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="6c780-126">U kunt een antwoord actie toevoegen bij elke stap in de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="6c780-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="6c780-127">De logische app alleen houdt de binnenkomende aanvraag open voor één minuut op een reactie.</span><span class="sxs-lookup"><span data-stu-id="6c780-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="6c780-128">Na een minuut, als er geen antwoord is verzonden van de werkstroom (en een actie antwoord in de definitie bestaat), een `504 GATEWAY TIMEOUT` wordt geretourneerd naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="6c780-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="6c780-129">Dit is het toevoegen van een HTTP-antwoord-actie:</span><span class="sxs-lookup"><span data-stu-id="6c780-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="6c780-130">Selecteer de **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="6c780-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="6c780-131">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6c780-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="6c780-132">Typ in het zoekvak actie **antwoord** voor een lijst met de actie antwoord.</span><span class="sxs-lookup"><span data-stu-id="6c780-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Selecteer de actie antwoord](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="6c780-134">In de parameters die vereist voor het HTTP-antwoordbericht zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6c780-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![De reactie actie niet voltooien](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="6c780-136">Klik op de linkerbovenhoek van de werkbalk om op te slaan en uw logische app wordt opslaan en publiceren (activeren).</span><span class="sxs-lookup"><span data-stu-id="6c780-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="6c780-137">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="6c780-137">Request trigger</span></span>
<span data-ttu-id="6c780-138">Hier volgen de details voor de trigger die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="6c780-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="6c780-139">Er is een trigger één aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6c780-139">There is a single request trigger.</span></span>

| <span data-ttu-id="6c780-140">Trigger</span><span class="sxs-lookup"><span data-stu-id="6c780-140">Trigger</span></span> | <span data-ttu-id="6c780-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6c780-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c780-142">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="6c780-142">Request</span></span> |<span data-ttu-id="6c780-143">Deze gebeurtenis treedt op wanneer er een HTTP-aanvraag wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="6c780-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="6c780-144">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="6c780-144">Response action</span></span>
<span data-ttu-id="6c780-145">Hier volgen de details voor de actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="6c780-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="6c780-146">Er is een enkele antwoordthread-actie kan alleen worden gebruikt wanneer u gaat vergezeld van een aanvraag-trigger.</span><span class="sxs-lookup"><span data-stu-id="6c780-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="6c780-147">Actie</span><span class="sxs-lookup"><span data-stu-id="6c780-147">Action</span></span> | <span data-ttu-id="6c780-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6c780-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c780-149">Antwoord</span><span class="sxs-lookup"><span data-stu-id="6c780-149">Response</span></span> |<span data-ttu-id="6c780-150">Retourneert een antwoord aan de gecorreleerde HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="6c780-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="6c780-151">Details van de trigger en action</span><span class="sxs-lookup"><span data-stu-id="6c780-151">Trigger and action details</span></span>
<span data-ttu-id="6c780-152">De volgende tabellen beschrijven de invoervelden voor de trigger en action en de bijbehorende details uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6c780-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="6c780-153">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="6c780-153">Request trigger</span></span>
<span data-ttu-id="6c780-154">Hier volgt een invoerveld voor de trigger van een binnenkomende HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6c780-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="6c780-155">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="6c780-155">Display name</span></span> | <span data-ttu-id="6c780-156">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6c780-156">Property name</span></span> | <span data-ttu-id="6c780-157">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6c780-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c780-158">JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="6c780-158">JSON Schema</span></span> |<span data-ttu-id="6c780-159">Schema</span><span class="sxs-lookup"><span data-stu-id="6c780-159">schema</span></span> |<span data-ttu-id="6c780-160">De JSON-schema van het hoofdgedeelte van de HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="6c780-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="6c780-161">**Uitvoerdetails**</span><span class="sxs-lookup"><span data-stu-id="6c780-161">**Output details**</span></span>

<span data-ttu-id="6c780-162">Hier volgen de uitvoerdetails voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6c780-162">The following are output details for the request.</span></span>

| <span data-ttu-id="6c780-163">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6c780-163">Property name</span></span> | <span data-ttu-id="6c780-164">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="6c780-164">Data type</span></span> | <span data-ttu-id="6c780-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6c780-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c780-166">Headers</span><span class="sxs-lookup"><span data-stu-id="6c780-166">Headers</span></span> |<span data-ttu-id="6c780-167">object</span><span class="sxs-lookup"><span data-stu-id="6c780-167">object</span></span> |<span data-ttu-id="6c780-168">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="6c780-168">Request headers</span></span> |
| <span data-ttu-id="6c780-169">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="6c780-169">Body</span></span> |<span data-ttu-id="6c780-170">object</span><span class="sxs-lookup"><span data-stu-id="6c780-170">object</span></span> |<span data-ttu-id="6c780-171">Request-object</span><span class="sxs-lookup"><span data-stu-id="6c780-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="6c780-172">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="6c780-172">Response action</span></span>
<span data-ttu-id="6c780-173">Hier volgen de invoervelden voor de HTTP-antwoord-actie.</span><span class="sxs-lookup"><span data-stu-id="6c780-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="6c780-174">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="6c780-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="6c780-175">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="6c780-175">Display name</span></span> | <span data-ttu-id="6c780-176">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6c780-176">Property name</span></span> | <span data-ttu-id="6c780-177">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6c780-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c780-178">Status Code *</span><span class="sxs-lookup"><span data-stu-id="6c780-178">Status Code*</span></span> |<span data-ttu-id="6c780-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="6c780-179">statusCode</span></span> |<span data-ttu-id="6c780-180">De HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="6c780-180">The HTTP status code</span></span> |
| <span data-ttu-id="6c780-181">Headers</span><span class="sxs-lookup"><span data-stu-id="6c780-181">Headers</span></span> |<span data-ttu-id="6c780-182">Headers</span><span class="sxs-lookup"><span data-stu-id="6c780-182">headers</span></span> |<span data-ttu-id="6c780-183">Een JSON-object van een antwoordheaders om op te nemen</span><span class="sxs-lookup"><span data-stu-id="6c780-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="6c780-184">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="6c780-184">Body</span></span> |<span data-ttu-id="6c780-185">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="6c780-185">body</span></span> |<span data-ttu-id="6c780-186">Hoofdtekst van de reactie</span><span class="sxs-lookup"><span data-stu-id="6c780-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c780-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c780-187">Next steps</span></span>
<span data-ttu-id="6c780-188">Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c780-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="6c780-189">U kunt de beschikbare connectors in logische apps door te kijken verkennen onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6c780-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

