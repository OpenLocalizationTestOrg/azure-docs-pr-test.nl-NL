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
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Voor het afhandelen van fouten en uitzonderingen in Azure Logic Apps

Logische Apps van Azure biedt uitgebreide hulpprogramma's en patronen toohelp u ervoor zorgen dat uw integraties zijn robuust en robuuste tegen fouten. Integratiearchitectuur inhouden Hallo uitdaging om zeker tooappropriately ingang uitvaltijd of problemen van afhankelijke systemen. Logic Apps om de foutafhandeling een uitstekende ervaring, zodat u Hallo hulpprogramma's die u nodig hebt tooact op uitzonderingen en fouten in uw werkstromen.

## <a name="retry-policies"></a>Beleid voor opnieuw proberen

Een beleid voor opnieuw proberen is Hallo meest eenvoudige type uitzondering en de foutafhandeling. Als een eerste aanvraag is een time-out of mislukt (elke aanvraag die in een 429 resulteert of 5xx-antwoord), dit beleid wordt gedefinieerd of Hallo actie moet opnieuw proberen. Standaard hebben alle handelingen. opnieuw proberen 4 extra keer via intervallen 20 seconden. Als de eerste aanvraag Hallo ontvangt een `500 Internal Server Error` antwoord Hallo workflowengine pauzeert voor 20 seconden en pogingen Hallo aanvraag opnieuw. Hallo werkstroom blijft als nadat alle pogingen antwoord Hallo nog steeds een uitzondering of mislukken is, en markeert de actiestatus als Hallo `Failed`.

U kunt beleid voor opnieuw proberen configureren in Hallo **invoer** voor een bepaalde actie. Bijvoorbeeld, kunt u een beleid voor opnieuw proberen tootry wel 4 tijdstippen configureren via 1 uur. Zie voor volledige informatie over eigenschappen voor de invoer [werkstroomacties en Triggers][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Als u uw HTTP-actie tooretry 4 keer wilden en tien minuten tussen elke poging wacht, gebruikt u Hallo definitie te volgen:

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

Zie voor meer informatie over ondersteunde syntaxis Hallo [beleid voor opnieuw proberen sectie in werkstroomacties en Triggers][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Catch-fouten met Hallo RunAfter eigenschap

Elke logische app actie wordt gedeclareerd welke acties moeten worden voltooid voordat Hallo actie wordt gestart, zoals het bestellen van Hallo stappen in uw werkstroom. In de definitie van de actie hello, deze volgorde staat bekend als Hallo `runAfter` eigenschap. Deze eigenschap is een object dat wordt beschreven welke acties en de actie status Hallo actie uitvoeren. Alle acties die zijn toegevoegd via Hallo Logic App-ontwerper zijn standaard te`runAfter` Hallo in de vorige stap als hello vorige stap `Succeeded`. U kunt deze waarde toofire acties echter aanpassen wanneer vorige acties hebben `Failed`, `Skipped`, of een mogelijke set van deze waarden. Indien u wenste de tooadd een item tooa Service Bus-onderwerp aangewezen na een specifieke actie `Insert_Row` mislukt, kunt u Hallo na `runAfter` configuratie:

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

Kennisgeving Hallo `runAfter` eigenschap toofire is ingesteld als hello `Insert_Row` in te grijpen `Failed`. toorun hello actie als Hallo Actiestatus `Succeeded`, `Failed`, of `Skipped`, gebruik de volgende syntaxis:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Acties die worden uitgevoerd en voltooid na een voorgaande actie is mislukt, zijn gemarkeerd als `Succeeded`. Dit gedrag betekent dat als u met succes catch alle fouten in een werkstroom Hallo zelf voert is gemarkeerd als `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Scopes en -resultaten tooevaluate acties

Vergelijkbare toohow na afzonderlijke acties kan worden uitgevoerd, kunt u ook groeperen acties binnen een [bereik](../logic-apps/logic-apps-loops-and-scopes.md), die fungeren als een logische groepering van acties. Scopes zijn nuttig voor het ordenen van uw logische app acties, zowel voor het uitvoeren van statistische evaluaties van de status van een scope Hallo. Hallo-bereik zelf krijgt de status nadat alle acties in een bereik hebt. Hallo bereik status wordt bepaald door hello dezelfde criteria als een uitvoering. Als de laatste actie Hallo in een vertakking uitvoering `Failed` of `Aborted`, de status van de Hallo `Failed`.

toofire specifieke acties op fouten die hebben plaatsgevonden binnen bereik hello, kunt u `runAfter` met een bereik dat is gemarkeerd als `Failed`. Als *eventuele* acties in het bereik van Hallo mislukken, uitgevoerd nadat een scope kunt mislukt u maakt een toocatch één actie fouten.

### <a name="getting-hello-context-of-failures-with-results"></a>Hallo-context van fouten met resultaten ophalen

Hoewel het afvangen van fouten van een scope nuttig is, kunt u ook context toohelp die u precies welke bewerkingen is mislukt, begrijpt en eventuele fouten of statuscodes die zijn geretourneerd. Hallo `@result()` Werkstroomfunctie voorzien in context over Hallo resultaat van alle acties in een bereik.

`@result()`neemt een enkele parameter, de naam van het bereik en retourneert een matrix met alle Hallo actie resultaten uit binnen dat bereik. Deze actie-objecten bevatten Hallo dezelfde als Hallo kenmerken `@actions()` object, met inbegrip van actie-begintijd, eindtijd actie Actiestatus, actie invoer, actie correlatie-id's en actie levert. de context van de toosend van acties die is mislukt binnen een bereik, die u gemakkelijk kunt combineren een `@result()` werken met een `runAfter`.

een actie tooexecute *voor elk* actie in een bereik die `Failed`, filter Hallo matrix van resultaten tooactions die is mislukt, kan worden gekoppeld `@result()` met een  **[matrix van Filter](../connectors/connectors-native-query.md)**  actie en een  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  lus. U kunt Hallo gefilterde resultaten matrix en een actie uitvoeren voor elke fout met Hallo **ForEach** lus. Hier volgt een voorbeeld, gevolgd door een gedetailleerde uitleg, die een HTTP POST-aanvraag met de antwoordtekst Hallo van acties die is mislukt binnen bereik Hallo verzendt `My_Scope`.

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

Hier volgt een gedetailleerd overzicht toodescribe wat er gebeurt:

1. tooget hello resultaat van alle acties in `My_Scope`, Hallo **matrix van Filter** actie filters `@result('My_Scope')`.

2. voorwaarde voor Hallo **matrix van Filter** is `@result()` item met de status gelijk te`Failed`. Deze voorwaarde filtert Hallo matrix met alle actie resultaten van `My_Scope` tooan matrix met alleen resultaten van de actie is mislukt.

3. Voer een **voor elk** actie op Hallo **gefilterd matrix** levert. Een actie in deze stap wordt uitgevoerd *voor elk* actie resultaat die eerder is gefilterd is mislukt.

    Als één actie in het Hallo-bereik is mislukt, de acties in Hallo Hallo `foreach` slechts eenmaal worden uitgevoerd. 
    Veel mislukte acties zorgen ervoor dat één actie per is mislukt.

4. Verzenden van een HTTP POST op Hallo `foreach` antwoordtekst, item of `@item()['outputs']['body']`. Hallo `@result()` item vorm is dezelfde als Hallo Hallo `@actions()` vorm en kan worden geparseerd Hallo op dezelfde manier.

5. Twee aangepaste headers met de naam van de mislukte actie Hallo omvatten `@item()['name']` Hallo uitvoeren client tracerings-ID is mislukt `@item()['clientTrackingId']`.

Ter referentie: Hier volgt een voorbeeld van een enkel `@result()` item, weergegeven Hallo `name`, `body`, en `clientTrackingId` eigenschappen die in het vorige voorbeeld Hallo worden geparseerd. Buiten een `foreach`, `@result()` retourneert een matrix van deze objecten.

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

tooperform verschillende uitzonderingsverwerking patronen, kunt u Hallo expressies eerder weergegeven. U mogelijk kiest tooexecute een enkele uitzonderingsverwerking actie buiten bereik Hallo die Hallo volledige gefilterde matrix van fouten accepteert en verwijder Hallo `foreach`. U kunt ook andere nuttige eigenschappen van Hallo opnemen `@result()` antwoord eerder weergegeven.

## <a name="azure-diagnostics-and-telemetry"></a>Azure diagnoses en telemetrie

Hello vorige patronen zijn goede manier toohandle fouten en uitzonderingen in een uitvoering, maar u kunt ook zien en reageren tooerrors onafhankelijk van Hallo worden uitgevoerd. 
[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) biedt een eenvoudige manier toosend alle werkstroom gebeurtenissen (met inbegrip van alle uitvoeren en de actie status) tooan Azure Storage-account of een Azure Event Hub. tooevaluate statussen worden uitgevoerd, kunt u Hallo logboeken en metrische gegevens controleren of ze in elke gewenste controleprogramma publiceren. Een mogelijke mogelijkheid is toostream alle Hallo gebeurtenissen tot en met Azure Event Hub in [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). In de Stream Analytics, kunt u schrijven live query's uit alle afwijkingen, gemiddelden of storingen van Hallo diagnostische logboeken. Stream Analytics kunt tooother gegevensbronnen zoals wachtrijen, onderwerpen, SQL, Azure Cosmos DB en Power BI eenvoudig uitvoeren.

## <a name="next-steps"></a>Volgende stappen

* [Zie hoe een klant builds foutafhandeling met Azure Logic Apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Meer voorbeelden van Logic Apps en scenario's zoeken](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Meer informatie over hoe toocreate geautomatiseerde implementaties voor logic apps](../logic-apps/logic-apps-create-deploy-template.md)
* [Logische apps maken en implementeren met Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
