---
title: de aanvraag en -antwoord acties aaaUse | Microsoft Docs
description: Overzicht van het Hallo-aanvraag en antwoord-trigger en action in een Azure logic app
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="705c4-103">Aan de slag met Hallo-aanvraag en antwoord-onderdelen</span><span class="sxs-lookup"><span data-stu-id="705c4-103">Get started with hello request and response components</span></span>
<span data-ttu-id="705c4-104">Hallo Components aanvraag en -antwoord in een logische app, kunt u in realtime tooevents reageren.</span><span class="sxs-lookup"><span data-stu-id="705c4-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="705c4-105">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="705c4-105">For example, you can:</span></span>

* <span data-ttu-id="705c4-106">Reageren op tooan HTTP-aanvraag met gegevens uit een on-premises database via een logische app.</span><span class="sxs-lookup"><span data-stu-id="705c4-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="705c4-107">Een logische app vanaf een externe webhook-gebeurtenis geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="705c4-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="705c4-108">Een logische app met de actie aanvraag en -antwoord uit in een andere logische app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="705c4-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="705c4-109">tooget gestart met Hallo-aanvraag en antwoord-acties in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="705c4-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="705c4-110">Hallo HTTP-aanvraag trigger gebruiken</span><span class="sxs-lookup"><span data-stu-id="705c4-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="705c4-111">Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="705c4-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="705c4-112">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="705c4-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="705c4-113">Hier volgt een van de voorbeeldreeks hoe tooset van een HTTP van Hallo Logic App-ontwerper aanvragen.</span><span class="sxs-lookup"><span data-stu-id="705c4-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="705c4-114">Hallo-trigger toevoegen **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="705c4-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="705c4-115">U kunt desgewenst een JSON-schema (met behulp van een hulpprogramma zoals [JSONSchema.net](http://jsonschema.net)) voor Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="705c4-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="705c4-116">Hierdoor kunnen Hallo designer toogenerate tokens voor eigenschappen in Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="705c4-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="705c4-117">Nog een actie toevoegen zodat u Hallo logische app kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="705c4-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="705c4-118">Na het opslaan van Hallo logische app, kunt u Hallo HTTP-aanvraag-URL ophalen van Hallo aanvraag kaart.</span><span class="sxs-lookup"><span data-stu-id="705c4-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="705c4-119">Een HTTP POST (kunt u een hulpprogramma zoals [Postman](https://www.getpostman.com/)) toohello URL triggers Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="705c4-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="705c4-120">Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord toohello aanroeper onmiddellijk geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="705c4-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="705c4-121">U kunt Hallo antwoord actie toocustomize een antwoord.</span><span class="sxs-lookup"><span data-stu-id="705c4-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Antwoord trigger](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="705c4-123">Hallo HTTP-antwoord actie gebruiken</span><span class="sxs-lookup"><span data-stu-id="705c4-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="705c4-124">Hallo HTTP-antwoord actie is alleen geldig wanneer u deze gebruikt in een werkstroom die wordt geactiveerd door een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="705c4-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="705c4-125">Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord toohello aanroeper onmiddellijk geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="705c4-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="705c4-126">U kunt een antwoord-actie bij elke stap in de werkstroom Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="705c4-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="705c4-127">Hallo logische app alleen houdt Hallo inkomende aanvraag open voor één minuut op een reactie.</span><span class="sxs-lookup"><span data-stu-id="705c4-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="705c4-128">Na een minuut, als er geen antwoord is verzonden vanuit workflow hello (en een actie antwoord in de definitie van de Hallo bestaat) een `504 GATEWAY TIMEOUT` toohello aanroeper wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="705c4-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="705c4-129">Hier ziet u hoe tooadd een actie van de HTTP-antwoord:</span><span class="sxs-lookup"><span data-stu-id="705c4-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="705c4-130">Selecteer Hallo **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="705c4-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="705c4-131">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="705c4-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="705c4-132">Typ in het zoekvak Hallo actie, **antwoord** toolist Hallo antwoord in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="705c4-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Selecteer Hallo antwoord actie](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="705c4-134">In de parameters die vereist voor de HTTP-antwoordbericht Hallo zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="705c4-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Volledige Hallo antwoord actie](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="705c4-136">Klik op Hallo linkerbovenhoek van Hallo werkbalk toosave en uw logische app worden beide opslaan en publiceren (activeren).</span><span class="sxs-lookup"><span data-stu-id="705c4-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="705c4-137">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="705c4-137">Request trigger</span></span>
<span data-ttu-id="705c4-138">Hier vindt u details Hallo Hallo-trigger die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="705c4-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="705c4-139">Er is een trigger één aanvraag.</span><span class="sxs-lookup"><span data-stu-id="705c4-139">There is a single request trigger.</span></span>

| <span data-ttu-id="705c4-140">Trigger</span><span class="sxs-lookup"><span data-stu-id="705c4-140">Trigger</span></span> | <span data-ttu-id="705c4-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="705c4-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="705c4-142">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="705c4-142">Request</span></span> |<span data-ttu-id="705c4-143">Deze gebeurtenis treedt op wanneer er een HTTP-aanvraag wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="705c4-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="705c4-144">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="705c4-144">Response action</span></span>
<span data-ttu-id="705c4-145">Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="705c4-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="705c4-146">Er is een enkele antwoordthread-actie kan alleen worden gebruikt wanneer u gaat vergezeld van een aanvraag-trigger.</span><span class="sxs-lookup"><span data-stu-id="705c4-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="705c4-147">Actie</span><span class="sxs-lookup"><span data-stu-id="705c4-147">Action</span></span> | <span data-ttu-id="705c4-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="705c4-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="705c4-149">Antwoord</span><span class="sxs-lookup"><span data-stu-id="705c4-149">Response</span></span> |<span data-ttu-id="705c4-150">Retourneert dat een antwoord toohello gecorreleerde HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="705c4-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="705c4-151">Details van de trigger en action</span><span class="sxs-lookup"><span data-stu-id="705c4-151">Trigger and action details</span></span>
<span data-ttu-id="705c4-152">Hallo volgende tabellen beschrijven Hallo invoervelden voor Hallo trigger en action en bijbehorende uitvoerdetails Hallo.</span><span class="sxs-lookup"><span data-stu-id="705c4-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="705c4-153">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="705c4-153">Request trigger</span></span>
<span data-ttu-id="705c4-154">Hallo Hieronder volgt een invoerveld voor de trigger Hallo van een binnenkomende HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="705c4-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="705c4-155">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="705c4-155">Display name</span></span> | <span data-ttu-id="705c4-156">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="705c4-156">Property name</span></span> | <span data-ttu-id="705c4-157">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="705c4-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="705c4-158">JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="705c4-158">JSON Schema</span></span> |<span data-ttu-id="705c4-159">Schema</span><span class="sxs-lookup"><span data-stu-id="705c4-159">schema</span></span> |<span data-ttu-id="705c4-160">Hallo JSON-schema van de aanvraagtekst Hallo HTTP</span><span class="sxs-lookup"><span data-stu-id="705c4-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="705c4-161">**Uitvoerdetails**</span><span class="sxs-lookup"><span data-stu-id="705c4-161">**Output details**</span></span>

<span data-ttu-id="705c4-162">Hallo hieronder vindt u uitvoerdetails voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="705c4-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="705c4-163">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="705c4-163">Property name</span></span> | <span data-ttu-id="705c4-164">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="705c4-164">Data type</span></span> | <span data-ttu-id="705c4-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="705c4-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="705c4-166">Headers</span><span class="sxs-lookup"><span data-stu-id="705c4-166">Headers</span></span> |<span data-ttu-id="705c4-167">object</span><span class="sxs-lookup"><span data-stu-id="705c4-167">object</span></span> |<span data-ttu-id="705c4-168">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="705c4-168">Request headers</span></span> |
| <span data-ttu-id="705c4-169">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="705c4-169">Body</span></span> |<span data-ttu-id="705c4-170">object</span><span class="sxs-lookup"><span data-stu-id="705c4-170">object</span></span> |<span data-ttu-id="705c4-171">Request-object</span><span class="sxs-lookup"><span data-stu-id="705c4-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="705c4-172">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="705c4-172">Response action</span></span>
<span data-ttu-id="705c4-173">Hallo volgen invoervelden voor Hallo HTTP-antwoord in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="705c4-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="705c4-174">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="705c4-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="705c4-175">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="705c4-175">Display name</span></span> | <span data-ttu-id="705c4-176">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="705c4-176">Property name</span></span> | <span data-ttu-id="705c4-177">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="705c4-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="705c4-178">Status Code *</span><span class="sxs-lookup"><span data-stu-id="705c4-178">Status Code*</span></span> |<span data-ttu-id="705c4-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="705c4-179">statusCode</span></span> |<span data-ttu-id="705c4-180">Hallo HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="705c4-180">hello HTTP status code</span></span> |
| <span data-ttu-id="705c4-181">Headers</span><span class="sxs-lookup"><span data-stu-id="705c4-181">Headers</span></span> |<span data-ttu-id="705c4-182">Headers</span><span class="sxs-lookup"><span data-stu-id="705c4-182">headers</span></span> |<span data-ttu-id="705c4-183">Een JSON-object van een antwoord headers tooinclude</span><span class="sxs-lookup"><span data-stu-id="705c4-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="705c4-184">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="705c4-184">Body</span></span> |<span data-ttu-id="705c4-185">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="705c4-185">body</span></span> |<span data-ttu-id="705c4-186">Hallo-antwoordtekst</span><span class="sxs-lookup"><span data-stu-id="705c4-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="705c4-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="705c4-187">Next steps</span></span>
<span data-ttu-id="705c4-188">Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="705c4-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="705c4-189">U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="705c4-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

