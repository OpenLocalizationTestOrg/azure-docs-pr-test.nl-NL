---
title: Lussen en -scopes maken of gegevens in werkstromen - Azure Logic Apps debatch | Microsoft Docs
description: Lussen om te doorlopen gegevens, acties in bereiken,-groepen maken of debatch gegevens om meer werkstromen te starten in Azure Logic Apps.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="05cb7-103">Lussen, bereiken en debatching van logische apps</span><span class="sxs-lookup"><span data-stu-id="05cb7-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="05cb7-104">Logische Apps biedt een aantal manieren om te werken met matrices, verzamelingen, batches, en binnen een werkstroom een lus.</span><span class="sxs-lookup"><span data-stu-id="05cb7-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="05cb7-105">ForEach-lus en matrices</span><span class="sxs-lookup"><span data-stu-id="05cb7-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="05cb7-106">Logic Apps kunt u een set gegevens doorlopen en een actie uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="05cb7-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="05cb7-107">Dit is mogelijk via de `foreach` in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="05cb7-108">In de ontwerpfunctie, kunt u opgeven om toe te voegen een voor elke lus.</span><span class="sxs-lookup"><span data-stu-id="05cb7-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="05cb7-109">Na het selecteren van de matrix die u wilt doorlopen, kunt u beginnen acties toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="05cb7-110">U bent momenteel beperkt tot één actie per foreach lus, maar deze beperking wordt in de komende weken worden opgeheven.</span><span class="sxs-lookup"><span data-stu-id="05cb7-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="05cb7-111">Eenmaal binnen de lus kunt u beginnen om op te geven wat er moet gebeuren op elke waarde van de matrix.</span><span class="sxs-lookup"><span data-stu-id="05cb7-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="05cb7-112">Als weergave code wordt gebruikt, kunt u een voor elke lus zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="05cb7-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="05cb7-113">Dit is een voorbeeld van een voor elke lus die voor elke e-mailadres dat 'microsoft.com' bevat een e-mailbericht verzendt:</span><span class="sxs-lookup"><span data-stu-id="05cb7-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="05cb7-114">Een `foreach` actie kunt sequentieel over matrices maximaal 5000 rijen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="05cb7-115">Elke herhaling wordt parallel uitgevoerd standaard.</span><span class="sxs-lookup"><span data-stu-id="05cb7-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="05cb7-116">Sequentiële ForEach lussen</span><span class="sxs-lookup"><span data-stu-id="05cb7-116">Sequential ForEach loops</span></span>

<span data-ttu-id="05cb7-117">Om in te schakelen van een lus foreach uitvoeren opeenvolgend, de `Sequential` optie bij bewerking moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="05cb7-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="05cb7-118">Pas de lus</span><span class="sxs-lookup"><span data-stu-id="05cb7-118">Until loop</span></span>
  
  <span data-ttu-id="05cb7-119">U kunt een actie of een reeks acties uitvoeren totdat er een voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="05cb7-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="05cb7-120">De meest voorkomende scenario voor dit kan een eindpunt wordt aangeroepen totdat u het antwoord die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="05cb7-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="05cb7-121">In de ontwerpfunctie, kunt u opgeven om toe te voegen een tot lus.</span><span class="sxs-lookup"><span data-stu-id="05cb7-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="05cb7-122">Na het toevoegen van acties binnen de lus, kunt u de voorwaarde voor het afsluiten, evenals de lus instellen limieten.</span><span class="sxs-lookup"><span data-stu-id="05cb7-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="05cb7-123">Er is een vertraging van 1 minuut tussen de cycli lus.</span><span class="sxs-lookup"><span data-stu-id="05cb7-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="05cb7-124">Als weergave code wordt gebruikt, kunt u een totdat de lus, zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="05cb7-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="05cb7-125">Dit is een voorbeeld van een aanroep van een HTTP-eindpunt totdat de antwoordtekst de waarde heeft 'Voltooid'.</span><span class="sxs-lookup"><span data-stu-id="05cb7-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="05cb7-126">De taak voltooid wanneer beide</span><span class="sxs-lookup"><span data-stu-id="05cb7-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="05cb7-127">HTTP-antwoord heeft de status 'Voltooid'</span><span class="sxs-lookup"><span data-stu-id="05cb7-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="05cb7-128">Er is geprobeerd 1 uur</span><span class="sxs-lookup"><span data-stu-id="05cb7-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="05cb7-129">Het is 100 keer herhaald</span><span class="sxs-lookup"><span data-stu-id="05cb7-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="05cb7-130">SplitOn en debatching</span><span class="sxs-lookup"><span data-stu-id="05cb7-130">SplitOn and debatching</span></span>

<span data-ttu-id="05cb7-131">Een trigger wordt soms een matrix van items die u wilt debatch en starten van een werkstroom per artikel.</span><span class="sxs-lookup"><span data-stu-id="05cb7-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="05cb7-132">Dit kan worden geconfigureerd via de `spliton` opdracht.</span><span class="sxs-lookup"><span data-stu-id="05cb7-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="05cb7-133">Als uw swagger trigger is opgegeven voor een nettolading met een matrix is standaard een `spliton` wordt toegevoegd en een reeks per object te starten.</span><span class="sxs-lookup"><span data-stu-id="05cb7-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="05cb7-134">SplitOn kan alleen worden toegevoegd aan een trigger.</span><span class="sxs-lookup"><span data-stu-id="05cb7-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="05cb7-135">Dit kan handmatig worden geconfigureerd of overschreven in de codeweergave definitie.</span><span class="sxs-lookup"><span data-stu-id="05cb7-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="05cb7-136">Momenteel SplitOn kunt debatch matrices van maximaal 5.000 items.</span><span class="sxs-lookup"><span data-stu-id="05cb7-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="05cb7-137">U kunt geen een `spliton` en ook het patroon synchrone antwoord te implementeren.</span><span class="sxs-lookup"><span data-stu-id="05cb7-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="05cb7-138">Een werkstroom aangeroepen die heeft een `response` actie naast `spliton` wordt asynchroon uitgevoerd en een onmiddellijke verzonden `202 Accepted` antwoord.</span><span class="sxs-lookup"><span data-stu-id="05cb7-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="05cb7-139">SplitOn kan worden opgegeven in de weergave van de code als het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="05cb7-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="05cb7-140">Hiermee ontvangt een matrix van items en debatches op elke rij.</span><span class="sxs-lookup"><span data-stu-id="05cb7-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="05cb7-141">Scopes</span><span class="sxs-lookup"><span data-stu-id="05cb7-141">Scopes</span></span>

<span data-ttu-id="05cb7-142">Het is mogelijk een reeks acties samen met een scope groeperen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="05cb7-143">Dit is vooral handig voor het implementeren van afhandeling van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="05cb7-144">U kunt in de ontwerpfunctie voor toevoegen van een nieuwe scope en gaan alle acties daarbinnen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="05cb7-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="05cb7-145">U kunt bereiken definiëren in de codeweergave als volgt:</span><span class="sxs-lookup"><span data-stu-id="05cb7-145">You can define scopes in code-view like the following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```