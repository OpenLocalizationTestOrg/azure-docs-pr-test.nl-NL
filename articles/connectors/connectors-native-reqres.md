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
# <a name="get-started-with-hello-request-and-response-components"></a>Aan de slag met Hallo-aanvraag en antwoord-onderdelen
Hallo Components aanvraag en -antwoord in een logische app, kunt u in realtime tooevents reageren.

U kunt bijvoorbeeld:

* Reageren op tooan HTTP-aanvraag met gegevens uit een on-premises database via een logische app.
* Een logische app vanaf een externe webhook-gebeurtenis geactiveerd.
* Een logische app met de actie aanvraag en -antwoord uit in een andere logische app aanroepen.

tooget gestart met Hallo-aanvraag en antwoord-acties in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Hallo HTTP-aanvraag trigger gebruiken
Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app. [Meer informatie over triggers](connectors-overview.md).

Hier volgt een van de voorbeeldreeks hoe tooset van een HTTP van Hallo Logic App-ontwerper aanvragen.

1. Hallo-trigger toevoegen **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** in uw logische app. U kunt desgewenst een JSON-schema (met behulp van een hulpprogramma zoals [JSONSchema.net](http://jsonschema.net)) voor Hallo aanvraagtekst. Hierdoor kunnen Hallo designer toogenerate tokens voor eigenschappen in Hallo HTTP-aanvraag.
2. Nog een actie toevoegen zodat u Hallo logische app kunt opslaan.
3. Na het opslaan van Hallo logische app, kunt u Hallo HTTP-aanvraag-URL ophalen van Hallo aanvraag kaart.
4. Een HTTP POST (kunt u een hulpprogramma zoals [Postman](https://www.getpostman.com/)) toohello URL triggers Hallo logische app.

> [!NOTE]
> Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord toohello aanroeper onmiddellijk geretourneerd. U kunt Hallo antwoord actie toocustomize een antwoord.
> 
> 

![Antwoord trigger](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Hallo HTTP-antwoord actie gebruiken
Hallo HTTP-antwoord actie is alleen geldig wanneer u deze gebruikt in een werkstroom die wordt geactiveerd door een HTTP-aanvraag. Als u een actie antwoord niet definieert een `202 ACCEPTED` antwoord toohello aanroeper onmiddellijk geretourneerd.  U kunt een antwoord-actie bij elke stap in de werkstroom Hallo toevoegen. Hallo logische app alleen houdt Hallo inkomende aanvraag open voor één minuut op een reactie.  Na een minuut, als er geen antwoord is verzonden vanuit workflow hello (en een actie antwoord in de definitie van de Hallo bestaat) een `504 GATEWAY TIMEOUT` toohello aanroeper wordt geretourneerd.

Hier ziet u hoe tooadd een actie van de HTTP-antwoord:

1. Selecteer Hallo **nieuwe stap** knop.
2. Kies **een actie toevoegen**.
3. Typ in het zoekvak Hallo actie, **antwoord** toolist Hallo antwoord in te grijpen.
   
    ![Selecteer Hallo antwoord actie](./media/connectors-native-reqres/using-action-1.png)
4. In de parameters die vereist voor de HTTP-antwoordbericht Hallo zijn toevoegen.
   
    ![Volledige Hallo antwoord actie](./media/connectors-native-reqres/using-action-2.png)
5. Klik op Hallo linkerbovenhoek van Hallo werkbalk toosave en uw logische app worden beide opslaan en publiceren (activeren).

## <a name="request-trigger"></a>Aanvraag trigger
Hier vindt u details Hallo Hallo-trigger die ondersteuning biedt voor deze connector. Er is een trigger één aanvraag.

| Trigger | Beschrijving |
| --- | --- |
| Aanvraag |Deze gebeurtenis treedt op wanneer er een HTTP-aanvraag wordt ontvangen |

## <a name="response-action"></a>Antwoord actie
Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector. Er is een enkele antwoordthread-actie kan alleen worden gebruikt wanneer u gaat vergezeld van een aanvraag-trigger.

| Actie | Beschrijving |
| --- | --- |
| Antwoord |Retourneert dat een antwoord toohello gecorreleerde HTTP-aanvraag |

### <a name="trigger-and-action-details"></a>Details van de trigger en action
Hallo volgende tabellen beschrijven Hallo invoervelden voor Hallo trigger en action en bijbehorende uitvoerdetails Hallo.

#### <a name="request-trigger"></a>Aanvraag trigger
Hallo Hieronder volgt een invoerveld voor de trigger Hallo van een binnenkomende HTTP-aanvraag.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| JSON-Schema |Schema |Hallo JSON-schema van de aanvraagtekst Hallo HTTP |

<br>

**Uitvoerdetails**

Hallo hieronder vindt u uitvoerdetails voor Hallo-aanvraag.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Headers |object |Aanvraagheaders |
| Hoofdtekst |object |Request-object |

#### <a name="response-action"></a>Antwoord actie
Hallo volgen invoervelden voor Hallo HTTP-antwoord in te grijpen. A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Status Code * |statusCode |Hallo HTTP-statuscode |
| Headers |Headers |Een JSON-object van een antwoord headers tooinclude |
| Hoofdtekst |Hoofdtekst |Hallo-antwoordtekst |

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).

