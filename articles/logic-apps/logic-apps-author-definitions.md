---
title: aaaDefine werkstromen met JSON - Azure Logic Apps | Microsoft Docs
description: Hoe toowrite werkstroomdefinities in JSON voor logic apps
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="f9093-103">Werkstroomdefinities voor logische apps met JSON maken</span><span class="sxs-lookup"><span data-stu-id="f9093-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="f9093-104">U kunt de werkstroomdefinities voor de maken [Azure Logic Apps](logic-apps-what-are-logic-apps.md) met eenvoudig, declaratief JSON-taal.</span><span class="sxs-lookup"><span data-stu-id="f9093-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="f9093-105">Als u nog niet gedaan hebt, moet u rekening houden [hoe toocreate uw eerste logische app met Logic App-ontwerper](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9093-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f9093-106">Zie ook Hallo [volledige naslaginformatie voor Hallo werkstroom Definition Language](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="f9093-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="f9093-107">Herhaal de stappen via een lijst</span><span class="sxs-lookup"><span data-stu-id="f9093-107">Repeat steps over a list</span></span>

<span data-ttu-id="f9093-108">tooiterate via een matrix heeft too10, 000 items en een actie uitvoert voor elk item, gebruikt u Hallo [foreach type](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="f9093-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="f9093-109">Afhandelen van fouten als er iets mis gaat</span><span class="sxs-lookup"><span data-stu-id="f9093-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="f9093-110">Normaal gesproken gewenste tooinclude een *herstel stap* : bepaalde logica die wordt uitgevoerd *als* een of meer van uw aanroepen mislukken.</span><span class="sxs-lookup"><span data-stu-id="f9093-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="f9093-111">In dit voorbeeld ontvangt gegevens van verschillende locaties, maar als het Hallo-aanroep is mislukt, willen we tooPOST een bericht ergens zodat we later omlaag die is mislukt bijhouden kunt:</span><span class="sxs-lookup"><span data-stu-id="f9093-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="f9093-112">toospecify die `postToErrorMessageQueue` alleen wordt uitgevoerd na `readData` heeft `Failed`, gebruik Hallo `runAfter` eigenschap, bijvoorbeeld een lijst van mogelijke waarden toospecify zodat `runAfter` kan worden `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="f9093-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="f9093-113">Ten slotte omdat in dit voorbeeld wordt nu Hallo fout verwerkt, wordt niet langer markeren Hallo run as- `Failed`.</span><span class="sxs-lookup"><span data-stu-id="f9093-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="f9093-114">Omdat we Hallo stap voor het verwerken van deze fout in dit voorbeeld hebt toegevoegd, Hallo uitvoeren heeft `Succeeded` maar één stap `Failed`.</span><span class="sxs-lookup"><span data-stu-id="f9093-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="f9093-115">Twee of meer stappen parallel uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f9093-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="f9093-116">toorun meerdere acties parallel Hallo `runAfter` eigenschap moet gelijkwaardige tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="f9093-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="f9093-117">In dit voorbeeld beide `branch1` en `branch2` zijn ingesteld toorun na `readData`.</span><span class="sxs-lookup"><span data-stu-id="f9093-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="f9093-118">Als gevolg hiervan beide vertakkingen parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9093-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="f9093-119">Hallo tijdstempel voor beide vertakkingen is identiek.</span><span class="sxs-lookup"><span data-stu-id="f9093-119">hello timestamp for both branches is identical.</span></span>

![Parallel](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="f9093-121">Twee parallelle vertakkingen koppelen</span><span class="sxs-lookup"><span data-stu-id="f9093-121">Join two parallel branches</span></span>

<span data-ttu-id="f9093-122">U kunt deelnemen aan twee acties die zijn ingesteld toorun parallel door toe te voegen items toohello `runAfter` eigenschap zoals in het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9093-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Parallel](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="f9093-124">Lijst met items tooa andere configuratie toewijzen</span><span class="sxs-lookup"><span data-stu-id="f9093-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="f9093-125">Volgende, stel willen we tooget andere inhoud op basis van Hallo-waarde van een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f9093-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="f9093-126">We kunnen een overzicht van waarden toodestinations maken als een parameter:</span><span class="sxs-lookup"><span data-stu-id="f9093-126">We can create a map of values toodestinations as a parameter:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

<span data-ttu-id="f9093-127">In dit geval krijgen we eerst een lijst met artikelen.</span><span class="sxs-lookup"><span data-stu-id="f9093-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="f9093-128">Op basis van het Hallo-categorie die is gedefinieerd als een parameter, Hallo tweede stap maakt gebruik van een kaart toolook up Hallo-URL voor het Hallo-inhoud ophalen.</span><span class="sxs-lookup"><span data-stu-id="f9093-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="f9093-129">Enkele voorbeelden van momenten toonote hier:</span><span class="sxs-lookup"><span data-stu-id="f9093-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="f9093-130">Hallo [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) functie gecontroleerd of Hallo categorie overeenkomt met een van de Hallo bekend gedefinieerde categorieën.</span><span class="sxs-lookup"><span data-stu-id="f9093-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="f9093-131">Nadat we Hallo categorie hebt ontvangen, kunnen we pull-hallo item uit Hallo-toewijzing met vierkante haken:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="f9093-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="f9093-132">Proces tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="f9093-132">Process strings</span></span>

<span data-ttu-id="f9093-133">Hier kunt u verschillende functies toomanipulate tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="f9093-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="f9093-134">Stel bijvoorbeeld dat we hebben een tekenreeks dat we toopass tooa systeem willen, maar we zijn ervan overtuigd over het afhandelen van de juiste voor codering niet.</span><span class="sxs-lookup"><span data-stu-id="f9093-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="f9093-135">Een mogelijkheid is toobase64 coderen van deze tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f9093-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="f9093-136">Echter tooavoid aanhalingstekens in een URL, gaan we tooreplace enkele tekens.</span><span class="sxs-lookup"><span data-stu-id="f9093-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="f9093-137">We willen ook een subtekenreeks van de naam van de order Hallo omdat de eerste vijf tekens Hallo niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f9093-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="f9093-138">Werkdagen van binnen toooutside:</span><span class="sxs-lookup"><span data-stu-id="f9093-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="f9093-139">Hallo ophalen [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) voor de naam van Hallo besteller, dus we terughalen Hallo totaal aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="f9093-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="f9093-140">Aftrekken 5 aangezien we een kortere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f9093-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="f9093-141">Pas Hallo [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="f9093-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="f9093-142">We beginnen bij index `5` en ga Hallo rest van Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f9093-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="f9093-143">Deze tooa subtekenreeks converteren [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f9093-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="f9093-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)alle Hallo `+` tekens `-` tekens.</span><span class="sxs-lookup"><span data-stu-id="f9093-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="f9093-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)alle Hallo `/` tekens `_` tekens.</span><span class="sxs-lookup"><span data-stu-id="f9093-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="f9093-146">Werken met datums en tijden</span><span class="sxs-lookup"><span data-stu-id="f9093-146">Work with Date Times</span></span>

<span data-ttu-id="f9093-147">Datums en tijden kan handig zijn met name wanneer u probeert toopull gegevens uit een gegevensbron die natuurlijk biedt geen ondersteuning voor *triggers*.</span><span class="sxs-lookup"><span data-stu-id="f9093-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="f9093-148">U kunt ook datums en tijden voor het vinden van hoe lang verschillende stappen nemen.</span><span class="sxs-lookup"><span data-stu-id="f9093-148">You can also use Date Times for finding how long various steps are taking.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="f9093-149">In dit voorbeeld we Hallo extraheren `startTime` uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9093-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="f9093-150">Vervolgens we Hallo huidige tijd niet ophalen en afgetrokken van één seconde:</span><span class="sxs-lookup"><span data-stu-id="f9093-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="f9093-151">U kunt andere tijdseenheden, zoals `minutes` of `hours`.</span><span class="sxs-lookup"><span data-stu-id="f9093-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="f9093-152">Ten slotte kunnen we deze twee waarden vergelijken.</span><span class="sxs-lookup"><span data-stu-id="f9093-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="f9093-153">Als de eerste waarde Hallo lager dan de tweede waarde hello, wordt meer dan één seconde is verstreken sinds Hallo volgorde voor het eerst is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f9093-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="f9093-154">tooformat datums, kunnen we tekenreeks formatters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f9093-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="f9093-155">Bijvoorbeeld, tooget hello RFC1123, gebruiken we [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="f9093-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="f9093-156">Zie toolearn over datumopmaak [werkstroom Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="f9093-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="f9093-157">Implementatieparameters voor verschillende omgevingen</span><span class="sxs-lookup"><span data-stu-id="f9093-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="f9093-158">Implementatie levenscycli hebben doorgaans een ontwikkelomgeving, een testomgeving en een productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f9093-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="f9093-159">Bijvoorbeeld, kunt u dezelfde definitie in alle deze omgevingen Hallo maar verschillende databases gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f9093-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="f9093-160">Evenzo kunt u toouse dezelfde definitie Hallo over verschillende regio's voor hoge beschikbaarheid, maar elke logic app-exemplaar tootalk toothat regio van database wilt.</span><span class="sxs-lookup"><span data-stu-id="f9093-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="f9093-161">Dit scenario verschilt van de parameters op te nemen *runtime* waar in plaats daarvan moet u Hallo `trigger()` werken zoals in het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9093-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="f9093-162">U kunt beginnen met een basisdefinitie zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f9093-162">You can start with a basic definition like this example:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

<span data-ttu-id="f9093-163">In de werkelijke Hallo `PUT` aanvragen voor Hallo logic apps, kunt u de parameter Hallo bieden `uri`.</span><span class="sxs-lookup"><span data-stu-id="f9093-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="f9093-164">Omdat een standaardwaarde niet meer bestaat, is deze parameter in Hallo logic app nettolading vereist:</span><span class="sxs-lookup"><span data-stu-id="f9093-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="f9093-165">In elke omgeving, kunt u een andere waarde opgeven voor Hallo `connection` parameter.</span><span class="sxs-lookup"><span data-stu-id="f9093-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="f9093-166">Zie voor alle opties die u hebt voor het maken en beheren van logic apps hello, Hallo [REST API-documentatie](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9093-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
