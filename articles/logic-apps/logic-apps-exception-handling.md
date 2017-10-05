---
title: Fout & uitzonderingsverwerking - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="8cae7-103">Voor het afhandelen van fouten en uitzonderingen in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8cae7-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="8cae7-104">Logische Apps van Azure biedt uitgebreide hulpprogramma's en om te controleren of uw integraties zijn robuust en robuuste tegen fouten.</span><span class="sxs-lookup"><span data-stu-id="8cae7-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="8cae7-105">Integratiearchitectuur vormt het lastiger om ervoor te zorgen voor het afhandelen van op de juiste wijze uitvaltijd of problemen van afhankelijke systemen.</span><span class="sxs-lookup"><span data-stu-id="8cae7-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="8cae7-106">Logic Apps kunt u afhandelen van fouten een uitstekende ervaring, zodat u de hulpmiddelen die u nodig hebt om actie te ondernemen uitzonderingen en fouten in uw werkstromen.</span><span class="sxs-lookup"><span data-stu-id="8cae7-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="8cae7-107">Beleid voor opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="8cae7-107">Retry policies</span></span>

<span data-ttu-id="8cae7-108">Een beleid voor opnieuw proberen is het meest eenvoudige type uitzondering en de foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="8cae7-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="8cae7-109">Als een eerste aanvraag is een time-out of mislukt (elke aanvraag die in een 429 resulteert of 5xx-antwoord), dit beleid bepaalt of de actie moet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="8cae7-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="8cae7-110">Standaard hebben alle handelingen. opnieuw proberen 4 extra keer via intervallen 20 seconden.</span><span class="sxs-lookup"><span data-stu-id="8cae7-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="8cae7-111">Als de eerste aanvraag ontvangt een `500 Internal Server Error` antwoord wordt de werkstroom-engine voor 20 seconden wordt onderbroken en probeert u de aanvraag opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8cae7-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="8cae7-112">Als na alle pogingen het antwoord nog steeds een uitzondering of mislukt is, de werkstroom blijft en markeert de status van de actie als `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="8cae7-113">U kunt beleid voor opnieuw proberen in de **invoer** voor een bepaalde actie.</span><span class="sxs-lookup"><span data-stu-id="8cae7-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="8cae7-114">U kunt bijvoorbeeld een beleid voor opnieuw proberen om te proberen wel 4 keer via 1 uur.</span><span class="sxs-lookup"><span data-stu-id="8cae7-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="8cae7-115">Zie voor volledige informatie over eigenschappen voor de invoer [werkstroomacties en Triggers][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="8cae7-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="8cae7-116">Als u uw HTTP-actie 4 keer opnieuw proberen en wacht tien minuten tussen elke poging wilt, gebruikt u de volgende definitie:</span><span class="sxs-lookup"><span data-stu-id="8cae7-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

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

<span data-ttu-id="8cae7-117">Zie voor meer informatie over ondersteunde syntaxis de [beleid voor opnieuw proberen sectie in werkstroomacties en Triggers][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="8cae7-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="8cae7-118">Catch-fouten met de eigenschap RunAfter</span><span class="sxs-lookup"><span data-stu-id="8cae7-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="8cae7-119">Elke logische app actie wordt gedeclareerd welke acties moeten worden voltooid voordat de actie wordt gestart, zoals het bestellen van de stappen in uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="8cae7-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="8cae7-120">In de definitie van de actie, deze volgorde staat bekend als de `runAfter` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8cae7-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="8cae7-121">Deze eigenschap is een object dat wordt beschreven welke acties en de actie status de actie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8cae7-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="8cae7-122">Standaard worden alle acties die zijn toegevoegd via de Logic App-ontwerper ingesteld op `runAfter` de vorige stap als de vorige stap `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="8cae7-123">U kunt deze waarde acties gestart wanneer de vorige acties hebben echter aanpassen `Failed`, `Skipped`, of een mogelijke set van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8cae7-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="8cae7-124">Als u wilt een item toevoegen aan een aangewezen Service Bus-onderwerp na een specifieke actie `Insert_Row` mislukt, kunt u de volgende `runAfter` configuratie:</span><span class="sxs-lookup"><span data-stu-id="8cae7-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

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

<span data-ttu-id="8cae7-125">U ziet de `runAfter` eigenschap is ingesteld moet worden gestart als de `Insert_Row` in te grijpen `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="8cae7-126">De actie wordt uitgevoerd als de status van de actie `Succeeded`, `Failed`, of `Skipped`, gebruik de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="8cae7-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="8cae7-127">Acties die worden uitgevoerd en voltooid na een voorgaande actie is mislukt, zijn gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="8cae7-128">Dit gedrag betekent dat als u met succes catch alle fouten in een werkstroom kan de sessie zelf is gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="8cae7-129">Scopes en resultaten acties evalueren</span><span class="sxs-lookup"><span data-stu-id="8cae7-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="8cae7-130">Vergelijkbaar met hoe u kunt uitvoeren nadat de afzonderlijke acties, kunt u ook groeperen acties binnen een [bereik](../logic-apps/logic-apps-loops-and-scopes.md), die fungeren als een logische groepering van acties.</span><span class="sxs-lookup"><span data-stu-id="8cae7-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="8cae7-131">Scopes zijn nuttig voor het ordenen van uw logische app acties, zowel voor het uitvoeren van statistische evaluaties van de status van een scope.</span><span class="sxs-lookup"><span data-stu-id="8cae7-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="8cae7-132">Het bereik zelf krijgt de status nadat alle acties in een bereik hebt.</span><span class="sxs-lookup"><span data-stu-id="8cae7-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="8cae7-133">De status van het bereik wordt bepaald met dezelfde criteria als een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="8cae7-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="8cae7-134">Als de laatste actie in een vertakking uitvoering `Failed` of `Aborted`, de status is `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="8cae7-135">Bepaalde acties voor fouten die hebben plaatsgevonden binnen het bereik wordt gestart, kunt u `runAfter` met een bereik dat is gemarkeerd als `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="8cae7-136">Als *eventuele* acties in het bereik mislukken, uitgevoerd nadat een scope kunt mislukt u één actie voor het opsporen van fouten.</span><span class="sxs-lookup"><span data-stu-id="8cae7-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="8cae7-137">De context van fouten met resultaten ophalen</span><span class="sxs-lookup"><span data-stu-id="8cae7-137">Getting the context of failures with results</span></span>

<span data-ttu-id="8cae7-138">Hoewel het afvangen van fouten van een scope nuttig is, kunt u ook context om te begrijpen precies welke bewerkingen is mislukt, en eventuele fouten of statuscodes die zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8cae7-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="8cae7-139">De `@result()` Werkstroomfunctie biedt de context van het resultaat van alle acties in een bereik.</span><span class="sxs-lookup"><span data-stu-id="8cae7-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="8cae7-140">`@result()`neemt een enkele parameter, de naam van het bereik en retourneert een matrix met alle actie resultaten uit binnen dat bereik.</span><span class="sxs-lookup"><span data-stu-id="8cae7-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="8cae7-141">Deze actie-objecten bevatten dezelfde kenmerken als de `@actions()` object, met inbegrip van actie-begintijd, eindtijd actie Actiestatus, actie invoer, actie correlatie-id's en actie levert.</span><span class="sxs-lookup"><span data-stu-id="8cae7-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="8cae7-142">Als u wilt verzenden context van de acties die is mislukt binnen een bereik, u gemakkelijk kunt combineren een `@result()` werken met een `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="8cae7-143">Uitvoeren van een actie *voor elk* actie in een bereik dat `Failed`, filter van de matrix van de resultaten naar acties die is mislukt, kan worden gekoppeld `@result()` met een  **[matrix van Filter](../connectors/connectors-native-query.md)**  actie en een  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  lus.</span><span class="sxs-lookup"><span data-stu-id="8cae7-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="8cae7-144">U kunt de gefilterde resultaten matrix en een actie uitvoeren voor elke fout met de **ForEach** lus.</span><span class="sxs-lookup"><span data-stu-id="8cae7-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="8cae7-145">Hier volgt een voorbeeld, gevolgd door een gedetailleerde beschrijving die stuurt een HTTP POST-aanvraag met de hoofdtekst van de reactie van alle acties die niet binnen het bereik `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

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

<span data-ttu-id="8cae7-146">Hier volgt een gedetailleerd overzicht naar beschreven wat er gebeurt:</span><span class="sxs-lookup"><span data-stu-id="8cae7-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="8cae7-147">Ophalen van het resultaat van alle acties in `My_Scope`, wordt de **matrix van Filter** actie filters `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="8cae7-148">De voorwaarde voor **matrix van Filter** is `@result()` item met de status is gelijk aan `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="8cae7-149">Deze voorwaarde filtert de matrix met alle actie resultaten van `My_Scope` naar een matrix met resultaten van de actie alleen mislukt.</span><span class="sxs-lookup"><span data-stu-id="8cae7-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="8cae7-150">Voer een **voor elk** actie op de **gefilterd matrix** levert.</span><span class="sxs-lookup"><span data-stu-id="8cae7-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="8cae7-151">Een actie in deze stap wordt uitgevoerd *voor elk* actie resultaat die eerder is gefilterd is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8cae7-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="8cae7-152">Als één actie in het bereik is mislukt, de acties in de `foreach` slechts eenmaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8cae7-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="8cae7-153">Veel mislukte acties zorgen ervoor dat één actie per is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8cae7-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="8cae7-154">Verzenden van een HTTP POST op de `foreach` antwoordtekst, item of `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="8cae7-155">De `@result()` item vorm is hetzelfde als de `@actions()` vorm en kan op dezelfde manier worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="8cae7-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="8cae7-156">Twee aangepaste headers met de naam van de mislukte actie opnemen `@item()['name']` en de mislukte tracerings-ID-client wordt uitgevoerd `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="8cae7-157">Ter referentie: Hier volgt een voorbeeld van een enkel `@result()` artikel, waarin de `name`, `body`, en `clientTrackingId` eigenschappen die in het vorige voorbeeld worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="8cae7-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="8cae7-158">Buiten een `foreach`, `@result()` retourneert een matrix van deze objecten.</span><span class="sxs-lookup"><span data-stu-id="8cae7-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="8cae7-159">Als u verschillende uitzonderingsverwerking patronen, kunt u de expressies die eerder is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8cae7-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="8cae7-160">U mogelijk wilt uitvoeren van een enkele uitzonderingsverwerking actie buiten het bereik dat de volledige gefilterde matrix van fouten accepteert en verwijder de `foreach`.</span><span class="sxs-lookup"><span data-stu-id="8cae7-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="8cae7-161">U kunt ook andere nuttige eigenschappen van de `@result()` antwoord eerder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8cae7-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="8cae7-162">Azure diagnoses en telemetrie</span><span class="sxs-lookup"><span data-stu-id="8cae7-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="8cae7-163">De vorige patronen uitstekende manier om te verwerken fouten en uitzonderingen in een uitvoering zijn, maar u kunt ook zien en reageren op fouten, onafhankelijk van de sessie zelf.</span><span class="sxs-lookup"><span data-stu-id="8cae7-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="8cae7-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) biedt een eenvoudige manier om alle werkstroomgebeurtenissen (met inbegrip van alle uitvoeren en de actie status) verzenden naar een Azure Storage-account of een Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="8cae7-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="8cae7-165">Om uitvoeren statussen, kunt u de logboeken en metrische gegevens controleren of ze in elke gewenste controleprogramma publiceren.</span><span class="sxs-lookup"><span data-stu-id="8cae7-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="8cae7-166">Een mogelijke mogelijkheid is om te streamen alle gebeurtenissen tot en met Azure Event Hub in [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="8cae7-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="8cae7-167">In de Stream Analytics, kunt u live query's uit alle afwijkingen, gemiddelden of mislukte schrijven van de diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="8cae7-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="8cae7-168">Stream Analytics kunt eenvoudig uitvoeren met andere gegevensbronnen zoals wachtrijen, onderwerpen, SQL, Azure Cosmos DB en Power BI.</span><span class="sxs-lookup"><span data-stu-id="8cae7-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cae7-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8cae7-169">Next Steps</span></span>

* [<span data-ttu-id="8cae7-170">Zie hoe een klant builds foutafhandeling met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8cae7-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="8cae7-171">Meer voorbeelden van Logic Apps en scenario's zoeken</span><span class="sxs-lookup"><span data-stu-id="8cae7-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="8cae7-172">Informatie over het maken van geautomatiseerde implementaties voor logic apps</span><span class="sxs-lookup"><span data-stu-id="8cae7-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="8cae7-173">Logische apps maken en implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cae7-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
