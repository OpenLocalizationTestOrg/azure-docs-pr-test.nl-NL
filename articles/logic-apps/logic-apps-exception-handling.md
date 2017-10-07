---
title: aaaError & uitzonderingsverwerking - Azure Logic Apps | Microsoft Docs
description: Patronen voor fout- en afhandeling van uitzonderingen in Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="e39b0-103">Voor het afhandelen van fouten en uitzonderingen in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e39b0-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="e39b0-104">Logische Apps van Azure biedt uitgebreide hulpprogramma's en patronen toohelp u ervoor zorgen dat uw integraties zijn robuust en robuuste tegen fouten.</span><span class="sxs-lookup"><span data-stu-id="e39b0-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="e39b0-105">Integratiearchitectuur inhouden Hallo uitdaging om zeker tooappropriately ingang uitvaltijd of problemen van afhankelijke systemen.</span><span class="sxs-lookup"><span data-stu-id="e39b0-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="e39b0-106">Logic Apps om de foutafhandeling een uitstekende ervaring, zodat u Hallo hulpprogramma's die u nodig hebt tooact op uitzonderingen en fouten in uw werkstromen.</span><span class="sxs-lookup"><span data-stu-id="e39b0-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="e39b0-107">Beleid voor opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="e39b0-107">Retry policies</span></span>

<span data-ttu-id="e39b0-108">Een beleid voor opnieuw proberen is Hallo meest eenvoudige type uitzondering en de foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="e39b0-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="e39b0-109">Als een eerste aanvraag is een time-out of mislukt (elke aanvraag die in een 429 resulteert of 5xx-antwoord), dit beleid wordt gedefinieerd of Hallo actie moet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="e39b0-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="e39b0-110">Standaard hebben alle handelingen. opnieuw proberen 4 extra keer via intervallen 20 seconden.</span><span class="sxs-lookup"><span data-stu-id="e39b0-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="e39b0-111">Als de eerste aanvraag Hallo ontvangt een `500 Internal Server Error` antwoord Hallo workflowengine pauzeert voor 20 seconden en pogingen Hallo aanvraag opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e39b0-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="e39b0-112">Hallo werkstroom blijft als nadat alle pogingen antwoord Hallo nog steeds een uitzondering of mislukken is, en markeert de actiestatus als Hallo `Failed`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="e39b0-113">U kunt beleid voor opnieuw proberen configureren in Hallo **invoer** voor een bepaalde actie.</span><span class="sxs-lookup"><span data-stu-id="e39b0-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="e39b0-114">Bijvoorbeeld, kunt u een beleid voor opnieuw proberen tootry wel 4 tijdstippen configureren via 1 uur.</span><span class="sxs-lookup"><span data-stu-id="e39b0-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="e39b0-115">Zie voor volledige informatie over eigenschappen voor de invoer [werkstroomacties en Triggers][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="e39b0-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="e39b0-116">Als u uw HTTP-actie tooretry 4 keer wilden en tien minuten tussen elke poging wacht, gebruikt u Hallo definitie te volgen:</span><span class="sxs-lookup"><span data-stu-id="e39b0-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="e39b0-117">Zie voor meer informatie over ondersteunde syntaxis Hallo [beleid voor opnieuw proberen sectie in werkstroomacties en Triggers][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="e39b0-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="e39b0-118">Catch-fouten met Hallo RunAfter eigenschap</span><span class="sxs-lookup"><span data-stu-id="e39b0-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="e39b0-119">Elke logische app actie wordt gedeclareerd welke acties moeten worden voltooid voordat Hallo actie wordt gestart, zoals het bestellen van Hallo stappen in uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="e39b0-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="e39b0-120">In de definitie van de actie hello, deze volgorde staat bekend als Hallo `runAfter` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e39b0-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="e39b0-121">Deze eigenschap is een object dat wordt beschreven welke acties en de actie status Hallo actie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e39b0-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="e39b0-122">Alle acties die zijn toegevoegd via Hallo Logic App-ontwerper zijn standaard te`runAfter` Hallo in de vorige stap als hello vorige stap `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="e39b0-123">U kunt deze waarde toofire acties echter aanpassen wanneer vorige acties hebben `Failed`, `Skipped`, of een mogelijke set van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e39b0-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="e39b0-124">Indien u wenste de tooadd een item tooa Service Bus-onderwerp aangewezen na een specifieke actie `Insert_Row` mislukt, kunt u Hallo na `runAfter` configuratie:</span><span class="sxs-lookup"><span data-stu-id="e39b0-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="e39b0-125">Kennisgeving Hallo `runAfter` eigenschap toofire is ingesteld als hello `Insert_Row` in te grijpen `Failed`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="e39b0-126">toorun hello actie als Hallo Actiestatus `Succeeded`, `Failed`, of `Skipped`, gebruik de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="e39b0-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="e39b0-127">Acties die worden uitgevoerd en voltooid na een voorgaande actie is mislukt, zijn gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="e39b0-128">Dit gedrag betekent dat als u met succes catch alle fouten in een werkstroom Hallo zelf voert is gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="e39b0-129">Scopes en -resultaten tooevaluate acties</span><span class="sxs-lookup"><span data-stu-id="e39b0-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="e39b0-130">Vergelijkbare toohow na afzonderlijke acties kan worden uitgevoerd, kunt u ook groeperen acties binnen een [bereik](../logic-apps/logic-apps-loops-and-scopes.md), die fungeren als een logische groepering van acties.</span><span class="sxs-lookup"><span data-stu-id="e39b0-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="e39b0-131">Scopes zijn nuttig voor het ordenen van uw logische app acties, zowel voor het uitvoeren van statistische evaluaties van de status van een scope Hallo.</span><span class="sxs-lookup"><span data-stu-id="e39b0-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="e39b0-132">Hallo-bereik zelf krijgt de status nadat alle acties in een bereik hebt.</span><span class="sxs-lookup"><span data-stu-id="e39b0-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="e39b0-133">Hallo bereik status wordt bepaald door hello dezelfde criteria als een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="e39b0-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="e39b0-134">Als de laatste actie Hallo in een vertakking uitvoering `Failed` of `Aborted`, de status van de Hallo `Failed`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="e39b0-135">toofire specifieke acties op fouten die hebben plaatsgevonden binnen bereik hello, kunt u `runAfter` met een bereik dat is gemarkeerd als `Failed`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="e39b0-136">Als *eventuele* acties in het bereik van Hallo mislukken, uitgevoerd nadat een scope kunt mislukt u maakt een toocatch één actie fouten.</span><span class="sxs-lookup"><span data-stu-id="e39b0-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="e39b0-137">Hallo-context van fouten met resultaten ophalen</span><span class="sxs-lookup"><span data-stu-id="e39b0-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="e39b0-138">Hoewel het afvangen van fouten van een scope nuttig is, kunt u ook context toohelp die u precies welke bewerkingen is mislukt, begrijpt en eventuele fouten of statuscodes die zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e39b0-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="e39b0-139">Hallo `@result()` Werkstroomfunctie voorzien in context over Hallo resultaat van alle acties in een bereik.</span><span class="sxs-lookup"><span data-stu-id="e39b0-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="e39b0-140">`@result()`neemt een enkele parameter, de naam van het bereik en retourneert een matrix met alle Hallo actie resultaten uit binnen dat bereik.</span><span class="sxs-lookup"><span data-stu-id="e39b0-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="e39b0-141">Deze actie-objecten bevatten Hallo dezelfde als Hallo kenmerken `@actions()` object, met inbegrip van actie-begintijd, eindtijd actie Actiestatus, actie invoer, actie correlatie-id's en actie levert.</span><span class="sxs-lookup"><span data-stu-id="e39b0-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="e39b0-142">de context van de toosend van acties die is mislukt binnen een bereik, die u gemakkelijk kunt combineren een `@result()` werken met een `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="e39b0-143">een actie tooexecute *voor elk* actie in een bereik die `Failed`, filter Hallo matrix van resultaten tooactions die is mislukt, kan worden gekoppeld `@result()` met een  **[matrix van Filter](../connectors/connectors-native-query.md)**  actie en een  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  lus.</span><span class="sxs-lookup"><span data-stu-id="e39b0-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="e39b0-144">U kunt Hallo gefilterde resultaten matrix en een actie uitvoeren voor elke fout met Hallo **ForEach** lus.</span><span class="sxs-lookup"><span data-stu-id="e39b0-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="e39b0-145">Hier volgt een voorbeeld, gevolgd door een gedetailleerde uitleg, die een HTTP POST-aanvraag met de antwoordtekst Hallo van acties die is mislukt binnen bereik Hallo verzendt `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="e39b0-146">Hier volgt een gedetailleerd overzicht toodescribe wat er gebeurt:</span><span class="sxs-lookup"><span data-stu-id="e39b0-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="e39b0-147">tooget hello resultaat van alle acties in `My_Scope`, Hallo **matrix van Filter** actie filters `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="e39b0-148">voorwaarde voor Hallo **matrix van Filter** is `@result()` item met de status gelijk te`Failed`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="e39b0-149">Deze voorwaarde filtert Hallo matrix met alle actie resultaten van `My_Scope` tooan matrix met alleen resultaten van de actie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e39b0-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="e39b0-150">Voer een **voor elk** actie op Hallo **gefilterd matrix** levert.</span><span class="sxs-lookup"><span data-stu-id="e39b0-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="e39b0-151">Een actie in deze stap wordt uitgevoerd *voor elk* actie resultaat die eerder is gefilterd is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e39b0-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="e39b0-152">Als één actie in het Hallo-bereik is mislukt, de acties in Hallo Hallo `foreach` slechts eenmaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e39b0-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="e39b0-153">Veel mislukte acties zorgen ervoor dat één actie per is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e39b0-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="e39b0-154">Verzenden van een HTTP POST op Hallo `foreach` antwoordtekst, item of `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="e39b0-155">Hallo `@result()` item vorm is dezelfde als Hallo Hallo `@actions()` vorm en kan worden geparseerd Hallo op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="e39b0-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="e39b0-156">Twee aangepaste headers met de naam van de mislukte actie Hallo omvatten `@item()['name']` Hallo uitvoeren client tracerings-ID is mislukt `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="e39b0-157">Ter referentie: Hier volgt een voorbeeld van een enkel `@result()` item, weergegeven Hallo `name`, `body`, en `clientTrackingId` eigenschappen die in het vorige voorbeeld Hallo worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="e39b0-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="e39b0-158">Buiten een `foreach`, `@result()` retourneert een matrix van deze objecten.</span><span class="sxs-lookup"><span data-stu-id="e39b0-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="e39b0-159">tooperform verschillende uitzonderingsverwerking patronen, kunt u Hallo expressies eerder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e39b0-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="e39b0-160">U mogelijk kiest tooexecute een enkele uitzonderingsverwerking actie buiten bereik Hallo die Hallo volledige gefilterde matrix van fouten accepteert en verwijder Hallo `foreach`.</span><span class="sxs-lookup"><span data-stu-id="e39b0-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="e39b0-161">U kunt ook andere nuttige eigenschappen van Hallo opnemen `@result()` antwoord eerder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e39b0-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="e39b0-162">Azure diagnoses en telemetrie</span><span class="sxs-lookup"><span data-stu-id="e39b0-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="e39b0-163">Hello vorige patronen zijn goede manier toohandle fouten en uitzonderingen in een uitvoering, maar u kunt ook zien en reageren tooerrors onafhankelijk van Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e39b0-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="e39b0-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) biedt een eenvoudige manier toosend alle werkstroom gebeurtenissen (met inbegrip van alle uitvoeren en de actie status) tooan Azure Storage-account of een Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e39b0-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="e39b0-165">tooevaluate statussen worden uitgevoerd, kunt u Hallo logboeken en metrische gegevens controleren of ze in elke gewenste controleprogramma publiceren.</span><span class="sxs-lookup"><span data-stu-id="e39b0-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="e39b0-166">Een mogelijke mogelijkheid is toostream alle Hallo gebeurtenissen tot en met Azure Event Hub in [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="e39b0-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="e39b0-167">In de Stream Analytics, kunt u schrijven live query's uit alle afwijkingen, gemiddelden of storingen van Hallo diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="e39b0-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="e39b0-168">Stream Analytics kunt tooother gegevensbronnen zoals wachtrijen, onderwerpen, SQL, Azure Cosmos DB en Power BI eenvoudig uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e39b0-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e39b0-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e39b0-169">Next Steps</span></span>

* [<span data-ttu-id="e39b0-170">Zie hoe een klant builds foutafhandeling met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e39b0-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="e39b0-171">Meer voorbeelden van Logic Apps en scenario's zoeken</span><span class="sxs-lookup"><span data-stu-id="e39b0-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="e39b0-172">Meer informatie over hoe toocreate geautomatiseerde implementaties voor logic apps</span><span class="sxs-lookup"><span data-stu-id="e39b0-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="e39b0-173">Logische apps maken en implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e39b0-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
