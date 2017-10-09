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
# <a name="logic-apps-loops-scopes-and-debatching"></a>Lussen, bereiken en debatching van logische apps
  
Logic Apps biedt een aantal manieren toowork met matrices, verzamelingen, batches en lussen binnen een werkstroom.
  
## <a name="foreach-loop-and-arrays"></a>ForEach-lus en matrices
  
Logic Apps kunt u tooloop ten opzichte van een set van gegevens en een actie uitvoert voor elk item.  Dit is mogelijk via Hallo `foreach` in te grijpen.  In de ontwerpfunctie hello, kunt u tooadd een voor elke lus.  Na het Hallo-matrix die u wenst dat tooiterate via selecteren, kunt u beginnen acties toe te voegen.  Momenteel beperkt tooonly één actie per foreach lus, maar deze beperking wordt in Hallo weken binnenkort worden opgeheven.  Binnen de lus Hallo kunt u eenmaal wat er op elke waarde van de matrix Hallo gebeuren moet toospecify beginnen.

Als weergave code wordt gebruikt, kunt u een voor elke lus zoals hieronder.  Dit is een voorbeeld van een voor elke lus die voor elke e-mailadres dat 'microsoft.com' bevat een e-mailbericht verzendt:

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
  
  Een `foreach` actie matrices van too5, 000 rijen kunt doorlopen.  Elke herhaling wordt parallel uitgevoerd standaard.  

### <a name="sequential-foreach-loops"></a>Sequentiële ForEach lussen

een lus foreach tooexecute opeenvolgend, Hallo tooenable `Sequential` optie bij bewerking moet worden toegevoegd.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Pas de lus
  
  U kunt een actie of een reeks acties uitvoeren totdat er een voorwaarde wordt voldaan.  Hallo meest voorkomende scenario voor dit is het aanroepen van een eindpunt totdat u antwoord Hallo die u zoekt.  In de ontwerpfunctie hello, kunt u tooadd een tot lus.  Na het toevoegen van acties binnen de lus hello, kunt u Hallo afsluiten voorwaarde instellen, evenals Hallo lus limieten.  Er is een vertraging van 1 minuut tussen de cycli lus.
  
  Als weergave code wordt gebruikt, kunt u een totdat de lus, zoals hieronder.  Dit is een voorbeeld van een aanroep van een HTTP-eindpunt totdat Hallo antwoordtekst Hallo-waarde 'Voltooid heeft'.  De taak voltooid wanneer beide 
  
  * HTTP-antwoord heeft de status 'Voltooid'
  * Er is geprobeerd 1 uur
  * Het is 100 keer herhaald
  
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
  
## <a name="spliton-and-debatching"></a>SplitOn en debatching

Een trigger wordt soms een matrix van items die u wilt toodebatch en start een werkstroom per artikel.  Kan dit worden bereikt via Hallo `spliton` opdracht.  Als uw swagger trigger is opgegeven voor een nettolading met een matrix is standaard een `spliton` wordt toegevoegd en een reeks per object te starten.  SplitOn kan alleen worden toegevoegd tooa trigger.  Dit kan handmatig worden geconfigureerd of overschreven in de codeweergave definitie.  SplitOn kunt momenteel matrices van too5, 000 items debatch.  U kunt geen een `spliton` en ook implementeren Hallo synchrone antwoord patroon.  Een werkstroom aangeroepen die heeft een `response` actie bovendien te`spliton` wordt asynchroon uitgevoerd en een onmiddellijke verzonden `202 Accepted` antwoord.  

SplitOn kan worden opgegeven in de weergave van de code als Hallo voorbeeld te volgen.  Hiermee ontvangt een matrix van items en debatches op elke rij.

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

## <a name="scopes"></a>Scopes

Het is mogelijk toogroup een reeks acties samen met een bereik.  Dit is vooral handig voor het implementeren van afhandeling van uitzonderingen.  U kunt in de ontwerpfunctie Hallo toevoegen van een nieuwe scope en gaan alle acties daarbinnen toevoegen.  U kunt bereiken definiëren in de codeweergave Hallo volgende:


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