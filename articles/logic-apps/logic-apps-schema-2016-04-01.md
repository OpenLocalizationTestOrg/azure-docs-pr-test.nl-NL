---
title: aaaSchema updates 1 juni 2016 - Azure Logic Apps | Microsoft Docs
description: JSON-definities voor Azure Logic Apps maken met schemaversie 2016-06-01
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Schema-updates voor Azure Logic Apps - 1 juni 2016

Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die het maken van logische apps meer betrouwbare en gemakkelijker toouse:

* [Scopes](#scopes) kunt u een groep of acties nesten als een verzameling van acties.
* [Voorwaarden en lussen](#conditions-loops) zijn nu klas acties.
* Nauwkeurigere ordening voor het uitvoeren van acties met Hallo `runAfter` eigenschap vervangen`dependsOn`

uw logische apps van 1 augustus 2015 Hallo tooupgrade preview-schema toohello 1 juni 2016 schema [uitchecken sectie Hallo-upgrade](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Scopes

Dit schema bevat bereiken, waarmee u groep samen of nest acties in de andere. Een voorwaarde kan bijvoorbeeld een voorwaarde bevatten. Meer informatie over [bereik syntaxis](../logic-apps/logic-apps-loops-and-scopes.md), of in dit voorbeeld basic bereik bekijken:

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a>Voorwaarden en lussen wijzigingen

Zijn parameters die zijn gekoppeld aan één actie in het schema van vorige versies, de voorwaarden en lussen. Dit schema liftonderhoud deze beperking, zodat de voorwaarden en lussen nu worden weergegeven als actietypen. Meer informatie over [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md), of dit eenvoudige voorbeeld voor een actie voorwaarde bekijken:

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a>de eigenschap 'runAfter'

Hallo `runAfter` eigenschap vervangt `dependsOn`, mits nauwkeuriger wanneer u Hallo uitvoeren om acties opgeeft die is gebaseerd op Hallo status van vorige acties.

Hallo `dependsOn` eigenschap is gelijk aan 'hello actie is uitgevoerd en is geslaagd', ongeacht hoe vaak de gewenste tooexecute een actie op basis van of de vorige actie Hallo geslaagd is, mislukt of overgeslagen. Hallo `runAfter` eigenschap die flexibel als een object dat Hiermee geeft u alle Hallo actienamen waarna Hallo-object wordt uitgevoerd. Deze eigenschap bepaalt ook een matrix van statussen die geaccepteerd als triggers worden. Bijvoorbeeld, als u toorun wilde nadat lukt de stap A en ook na stap B is gelukt of mislukt, u samenstellen dit `runAfter` eigenschap:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Uw schema bijwerken

Toohello upgraden duurt nieuwe schema slechts een paar stappen uitvoeren. Hallo upgradeproces bevat uitgevoerd Hallo upgrade-script, op te slaan als een nieuwe logische app, en als u wilt, mogelijk Hallo vorige logische app overschrijven.

1. Open uw logische app in Azure-portal hello.

2. Ga te**overzicht**. Kies op Hallo logic app werkbalk **Schema bijwerken**.
   
    ![Kies Schema bijwerken][1]
   
    Hallo wordt bijgewerkte definitie geretourneerd, die u kunt kopiëren en plakken in de resourcedefinitie van een, indien nodig. 
    Echter, we **aangeraden** u **OpslaanAls** toomake ervoor dat alle verbinding verwijzingen geldig in Hallo zijn bijgewerkt logische app.

3. Kies in de werkbalk van Hallo upgrade blade **OpslaanAls**.

4. Voer Hallo logica naam en status. toodeploy uw bijgewerkte logische app, kies **maken**.

5. Controleer of uw bijgewerkte logische app werkt zoals verwacht.
   
   > [!NOTE]
   > Als u van een trigger handmatig of aanvraag gebruikmaakt, Hallo callback URL wordt gewijzigd in de nieuwe logische app. Test Hallo nieuwe URL toomake ervoor Hallo end-to-end ervaren werkt. toopreserve vorige URL's die u via uw bestaande logische app kunt klonen.

6. *Optionele* toooverwrite uw vorige logische app met Hallo nieuwe schemaversie, op de werkbalk hello, kies **kloon**, het volgende te**Schema bijwerken**. Deze stap is nodig alleen als u tookeep Hallo dezelfde bron-ID of aanvraag trigger-URL van uw logische app.

### <a name="upgrade-tool-notes"></a>Opmerkingen bij de upgrade hulpprogramma

#### <a name="mapping-conditions"></a>Toewijzing van voorwaarden

In de definitie Hallo bijgewerkt kunt Hallo hulpprogramma u een zo goed mogelijke poging op true en false vertakking acties groeperen als bereik. Designer patroon in het bijzonder Hallo van `@equals(actions('a').status, 'Skipped')` moet worden weergegeven als een `else` in te grijpen. Als Hallo hulpprogramma onherkenbare patronen detecteert, mogelijk Hallo hulpprogramma echter afzonderlijke voorwaarden voor zowel Hallo waar en ONWAAR vertakking Hallo maken. U kunt acties opnieuw toewijzen na de upgrade, indien nodig.

#### <a name="foreach-loop-with-condition"></a>'foreach' lus met voorwaarde

In het nieuwe schema hello, kunt u Hallo actie tooreplicate Hallo filterpatroon van een `foreach` lus met een voorwaarde per object, maar deze wijziging automatisch moet gebeuren wanneer u een upgrade uitvoert. Hallo voorwaarde wordt een filteractie voordat Hallo foreach-lus voor het retourneren van een reeks items die overeenkomen met de voorwaarde Hallo en deze reeks wordt doorgegeven aan Hallo foreach-actie. Zie voor een voorbeeld [lussen en -scopes](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Resourcetags

Na de upgrade, worden resourcetags verwijderd, zodat u ze voor Hallo bijgewerkt werkstroom moet opnieuw instellen.

## <a name="other-changes"></a>Andere wijzigingen

### <a name="renamed-manual-trigger-toorequest-trigger"></a>'Manual' trigger too'request hernoemd ' trigger

Hallo `manual` triggertype is afgeschaft en hernoemd te`request` met type `http`. Deze wijziging maakt meer consistentie voor Hallo soort patroon dat Hallo trigger gebruikte toobuild is.

### <a name="new-filter-action"></a>Nieuwe 'filter' actie

een grote matrix omlaag kleiner aantal items, nieuwe Hallo tooa toofilter `filter` type accepteert een matrix en een voorwaarde, Hallo voorwaarde voor elk item wordt geëvalueerd en resulteert in een matrix met items die voldoen aan de voorwaarde Hallo.

### <a name="restrictions-for-foreach-and-until-actions"></a>Beperkingen voor 'foreach' en 'tot' acties

Hallo `foreach` en `until` lus beperkte tooa één actie zijn.

### <a name="new-trackedproperties-for-actions"></a>Nieuwe 'trackedProperties' voor acties

Acties hebt nu een extra eigenschap met de naam `trackedProperties`, namelijk op hetzelfde niveau toohello `runAfter` en `type` eigenschappen. Dit object geeft bepaalde actie invoer of uitvoer die u wilt dat tooinclude in hello Azure diagnostische telemetrie, verzonden als onderdeel van een werkstroom. Bijvoorbeeld:

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a>Volgende stappen
* [Werkstroomdefinities voor logic apps maken](../logic-apps/logic-apps-author-definitions.md)
* [Van implementatiesjablonen maken voor logische apps](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
