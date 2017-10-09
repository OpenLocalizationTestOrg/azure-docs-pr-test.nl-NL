---
title: aaaCreate worden doorlopen en -bereiken of gegevens in werkstromen - Azure Logic Apps debatch | Microsoft Docs
description: Lussen tooiterate door de gegevens van groep acties bereiken, maken of gegevens toostart debatch meer werkstromen in Azure Logic Apps.
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
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="d48c3-103">Lussen, bereiken en debatching van logische apps</span><span class="sxs-lookup"><span data-stu-id="d48c3-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="d48c3-104">Logic Apps biedt een aantal manieren toowork met matrices, verzamelingen, batches en lussen binnen een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="d48c3-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="d48c3-105">ForEach-lus en matrices</span><span class="sxs-lookup"><span data-stu-id="d48c3-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="d48c3-106">Logic Apps kunt u tooloop ten opzichte van een set van gegevens en een actie uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="d48c3-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="d48c3-107">Dit is mogelijk via Hallo `foreach` in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="d48c3-108">In de ontwerpfunctie hello, kunt u tooadd een voor elke lus.</span><span class="sxs-lookup"><span data-stu-id="d48c3-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="d48c3-109">Na het Hallo-matrix die u wenst dat tooiterate via selecteren, kunt u beginnen acties toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="d48c3-110">Momenteel beperkt tooonly één actie per foreach lus, maar deze beperking wordt in Hallo weken binnenkort worden opgeheven.</span><span class="sxs-lookup"><span data-stu-id="d48c3-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="d48c3-111">Binnen de lus Hallo kunt u eenmaal wat er op elke waarde van de matrix Hallo gebeuren moet toospecify beginnen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="d48c3-112">Als weergave code wordt gebruikt, kunt u een voor elke lus zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="d48c3-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="d48c3-113">Dit is een voorbeeld van een voor elke lus die voor elke e-mailadres dat 'microsoft.com' bevat een e-mailbericht verzendt:</span><span class="sxs-lookup"><span data-stu-id="d48c3-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="d48c3-114">Een `foreach` actie matrices van too5, 000 rijen kunt doorlopen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="d48c3-115">Elke herhaling wordt parallel uitgevoerd standaard.</span><span class="sxs-lookup"><span data-stu-id="d48c3-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="d48c3-116">Sequentiële ForEach lussen</span><span class="sxs-lookup"><span data-stu-id="d48c3-116">Sequential ForEach loops</span></span>

<span data-ttu-id="d48c3-117">een lus foreach tooexecute opeenvolgend, Hallo tooenable `Sequential` optie bij bewerking moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d48c3-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="d48c3-118">Pas de lus</span><span class="sxs-lookup"><span data-stu-id="d48c3-118">Until loop</span></span>
  
  <span data-ttu-id="d48c3-119">U kunt een actie of een reeks acties uitvoeren totdat er een voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="d48c3-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="d48c3-120">Hallo meest voorkomende scenario voor dit is het aanroepen van een eindpunt totdat u antwoord Hallo die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="d48c3-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="d48c3-121">In de ontwerpfunctie hello, kunt u tooadd een tot lus.</span><span class="sxs-lookup"><span data-stu-id="d48c3-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="d48c3-122">Na het toevoegen van acties binnen de lus hello, kunt u Hallo afsluiten voorwaarde instellen, evenals Hallo lus limieten.</span><span class="sxs-lookup"><span data-stu-id="d48c3-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="d48c3-123">Er is een vertraging van 1 minuut tussen de cycli lus.</span><span class="sxs-lookup"><span data-stu-id="d48c3-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="d48c3-124">Als weergave code wordt gebruikt, kunt u een totdat de lus, zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="d48c3-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="d48c3-125">Dit is een voorbeeld van een aanroep van een HTTP-eindpunt totdat Hallo antwoordtekst Hallo-waarde 'Voltooid heeft'.</span><span class="sxs-lookup"><span data-stu-id="d48c3-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="d48c3-126">De taak voltooid wanneer beide</span><span class="sxs-lookup"><span data-stu-id="d48c3-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="d48c3-127">HTTP-antwoord heeft de status 'Voltooid'</span><span class="sxs-lookup"><span data-stu-id="d48c3-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="d48c3-128">Er is geprobeerd 1 uur</span><span class="sxs-lookup"><span data-stu-id="d48c3-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="d48c3-129">Het is 100 keer herhaald</span><span class="sxs-lookup"><span data-stu-id="d48c3-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="d48c3-130">SplitOn en debatching</span><span class="sxs-lookup"><span data-stu-id="d48c3-130">SplitOn and debatching</span></span>

<span data-ttu-id="d48c3-131">Een trigger wordt soms een matrix van items die u wilt toodebatch en start een werkstroom per artikel.</span><span class="sxs-lookup"><span data-stu-id="d48c3-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="d48c3-132">Kan dit worden bereikt via Hallo `spliton` opdracht.</span><span class="sxs-lookup"><span data-stu-id="d48c3-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="d48c3-133">Als uw swagger trigger is opgegeven voor een nettolading met een matrix is standaard een `spliton` wordt toegevoegd en een reeks per object te starten.</span><span class="sxs-lookup"><span data-stu-id="d48c3-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="d48c3-134">SplitOn kan alleen worden toegevoegd tooa trigger.</span><span class="sxs-lookup"><span data-stu-id="d48c3-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="d48c3-135">Dit kan handmatig worden geconfigureerd of overschreven in de codeweergave definitie.</span><span class="sxs-lookup"><span data-stu-id="d48c3-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="d48c3-136">SplitOn kunt momenteel matrices van too5, 000 items debatch.</span><span class="sxs-lookup"><span data-stu-id="d48c3-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="d48c3-137">U kunt geen een `spliton` en ook implementeren Hallo synchrone antwoord patroon.</span><span class="sxs-lookup"><span data-stu-id="d48c3-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="d48c3-138">Een werkstroom aangeroepen die heeft een `response` actie bovendien te`spliton` wordt asynchroon uitgevoerd en een onmiddellijke verzonden `202 Accepted` antwoord.</span><span class="sxs-lookup"><span data-stu-id="d48c3-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="d48c3-139">SplitOn kan worden opgegeven in de weergave van de code als Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="d48c3-140">Hiermee ontvangt een matrix van items en debatches op elke rij.</span><span class="sxs-lookup"><span data-stu-id="d48c3-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="d48c3-141">Scopes</span><span class="sxs-lookup"><span data-stu-id="d48c3-141">Scopes</span></span>

<span data-ttu-id="d48c3-142">Het is mogelijk toogroup een reeks acties samen met een bereik.</span><span class="sxs-lookup"><span data-stu-id="d48c3-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="d48c3-143">Dit is vooral handig voor het implementeren van afhandeling van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="d48c3-144">U kunt in de ontwerpfunctie Hallo toevoegen van een nieuwe scope en gaan alle acties daarbinnen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d48c3-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="d48c3-145">U kunt bereiken definiëren in de codeweergave Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d48c3-145">You can define scopes in code-view like hello following:</span></span>


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