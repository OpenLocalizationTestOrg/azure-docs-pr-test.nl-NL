---
title: aaaWebhook-connector voor Azure Logic Apps | Microsoft Docs
description: Hoe toouse webhookacties en triggers tooperform acties zoals matrix van Filter vanuit logic apps
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Aan de slag met Hallo webhook-connector

Met de Hallo webhook actie en de trigger, kunt u starten, onderbreken en hervatten van stromen tooperform deze taken:

* Activeren van een [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) wanneer een item wordt ontvangen
* Wachten op een goedkeuring voordat u doorgaat een werkstroom

Meer informatie over [hoe toocreate aangepaste API's die ondersteuning bieden voor een webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Hallo webhook trigger te gebruiken

Een [ *trigger* ](connectors-overview.md) is een gebeurtenis die een werkstroom van logic app start. Een trigger webhook is op basis van gebeurtenissen en niet afhankelijk is van polling voor nieuwe items. Zoals Hallo [aanvraag trigger](connectors-native-reqres.md), Hallo logische app wordt geactiveerd Hallo instant dat een gebeurtenis plaatsvindt. Hallo webhook trigger registreert een *retouraanroep URL* tooa service en wordt die URL toofire Hallo logic app als nodig is.

Hier volgt een voorbeeld ziet u hoe tooset van een HTTP activeren in Hallo Logic App-ontwerper. Hallo stappen wordt ervan uitgegaan dat u al hebt geïmplementeerd of toegang hebben tot een API die volgt op Hallo [webhook abonneren en zich afmelden patroon in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Hallo abonneren aanroep wordt gemaakt wanneer een logische app wordt opgeslagen met een nieuwe webhook of gewijzigd van uitgeschakelde tooenabled. Hallo opzeggen aanroep gedaan wanneer een logische app webhook trigger wordt verwijderd en opgeslagen of gewijzigd van ingeschakeld toodisabled.

**tooadd hello webhook trigger**

1. Hallo toevoegen **HTTP-Webhook** trigger als Hallo eerste stap in een logische app.
2. Vult Hallo parameters voor webhook Hallo abonneren en zich afmelden aanroepen.

   Deze stap volgt hetzelfde patroon als Hallo Hallo [HTTP-actie](connectors-native-http.md) indeling.

     ![HTTP-Trigger](./media/connectors-native-webhook/using-trigger.png)

3. Voeg ten minste één actie.
4. Klik op **opslaan** toopublish Hallo logische app. Deze stap aanroepen Hallo abonneren eindpunt met Hallo callback URL nodig tootrigger deze logische app.
5. Wanneer Hallo zorgt ervoor dat service een `HTTP POST` toohello retouraanroep-URL, Hallo logic app deze gebeurtenis wordt gestart en bevat geen gegevens doorgegeven aan Hallo-aanvraag.

## <a name="use-hello-webhook-action"></a>Hallo webhook actie gebruiken

Een [ *actie* ](connectors-overview.md) wordt een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. Registreert een webhook-actie een *retouraanroep URL* met een service en wordt er gewacht totdat het Hallo-URL wordt aangeroepen voordat het wordt hervat. Hallo ['Goedkeuring E-mail verzenden'](connectors-create-api-office365-outlook.md) is een voorbeeld van een connector die volgt op dit patroon. U kunt dit patroon uitbreiden naar een service via Hallo webhook actie. 

Hier volgt een voorbeeld ziet u hoe tooset een webhook actie in Logic App-ontwerper Hallo. Deze stappen wordt ervan uitgegaan dat u al hebt geïmplementeerd of toegang hebben tot een API die volgt op Hallo [webhook abonneren en zich afmelden patroon dat wordt gebruikt in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Hallo abonneren aanroep gedaan wanneer u een logische app Hallo webhook actie uitvoert. Hallo opzeggen aanroep gedaan wanneer een uitvoering is geannuleerd tijdens het wachten op reactie of voordat Hallo logic app een optreedt time-out.

**een actie webhook tooadd**

1. Kies **nieuwe stap** > **een actie toevoegen**.

2. Typ in het zoekvak hello, 'webhook' toofind hello **HTTP-Webhook** in te grijpen.

    ![Selecteer de queryactie](./media/connectors-native-webhook/using-action-1.png)

3. Hallo parameters invullen voor Hallo webhook abonneren en aanroepen afmelden

   Deze stap volgt hetzelfde patroon als Hallo Hallo [HTTP-actie](connectors-native-http.md) indeling.

     ![Volledige queryactie](./media/connectors-native-webhook/using-action-2.png)
   
   Tijdens runtime abonneren Hallo logic app aanroepen Hallo eindpunt na deze stap is bereikt.

4. Klik op **opslaan** toopublish Hallo logische app.

## <a name="technical-details"></a>Technische details

Hier vindt u meer informatie over het Hallo-triggers en acties die webhook ondersteunt.

## <a name="webhook-triggers"></a>Webhook-triggers

| Actie | Beschrijving |
| --- | --- |
| HTTP-Webhook |Zich abonneren een retouraanroep URL tooa service die Hallo URL toofire logische app naar behoefte kunt aanroepen. |

### <a name="trigger-details"></a>Details van de trigger

#### <a name="http-webhook"></a>HTTP-Webhook

Zich abonneren een retouraanroep URL tooa service die Hallo URL toofire logische app naar behoefte kunt aanroepen.
Een * betekent verplicht veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Abonneren methode * |Methode |HTTP-methode toouse voor abonneren op aanvraag |
| Abonneren URI * |URI |HTTP-URI toouse voor abonneren op aanvraag |
| Afmelden methode * |Methode |HTTP-methode toouse voor afmelding |
| Afmelden URI * |URI |HTTP-URI toouse voor afmelding |
| Hoofdtekst abonneren |Hoofdtekst |Hoofdtekst van de HTTP-aanvraag voor het abonneren |
| Headers abonneren |Headers |HTTP-aanvraagheaders voor abonneren |
| Abonneren verificatie |Verificatie |HTTP-verificatie toouse voor abonneren. [Zie HTTP connector](connectors-native-http.md#authentication) voor meer informatie |
| Hoofdtekst afmelden |Hoofdtekst |Hoofdtekst van de HTTP-aanvraag voor afmelden |
| Headers afmelden |Headers |HTTP-aanvraagheaders voor afmelden |
| Verificatie afmelden |Verificatie |HTTP-verificatie toouse voor afmelden. [Zie HTTP connector](connectors-native-http.md#authentication) voor meer informatie |

**Uitvoerdetails**

Webhook-aanvraag

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Headers |object |Webhook-aanvraagheaders |
| Hoofdtekst |object |Webhook request-object |
| Statuscode |int |Statuscode van aanvraag Webhook |

## <a name="webhook-actions"></a>Webhookacties

| Actie | Beschrijving |
| --- | --- |
| HTTP-Webhook |Zich abonneren een retouraanroep URL tooa service die Hallo URL tooresume een stap in de workflow naar behoefte kunt aanroepen. |

### <a name="action-details"></a>Actiedetails

#### <a name="http-webhook"></a>HTTP-Webhook

Zich abonneren een retouraanroep URL tooa service die Hallo URL tooresume een stap in de workflow naar behoefte kunt aanroepen.
Een * betekent verplicht veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Abonneren methode * |Methode |HTTP-methode toouse voor abonneren op aanvraag |
| Abonneren URI * |URI |HTTP-URI toouse voor abonneren op aanvraag |
| Afmelden methode * |Methode |HTTP-methode toouse voor afmelding |
| Afmelden URI * |URI |HTTP-URI toouse voor afmelding |
| Hoofdtekst abonneren |Hoofdtekst |Hoofdtekst van de HTTP-aanvraag voor het abonneren |
| Headers abonneren |Headers |HTTP-aanvraagheaders voor abonneren |
| Abonneren verificatie |Verificatie |HTTP-verificatie toouse voor abonneren. [Zie HTTP connector](connectors-native-http.md#authentication) voor meer informatie |
| Hoofdtekst afmelden |Hoofdtekst |Hoofdtekst van de HTTP-aanvraag voor afmelden |
| Headers afmelden |Headers |HTTP-aanvraagheaders voor afmelden |
| Verificatie afmelden |Verificatie |HTTP-verificatie toouse voor afmelden. [Zie HTTP connector](connectors-native-http.md#authentication) voor meer informatie |

**Uitvoerdetails**

Webhook-aanvraag

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Headers |object |Webhook-aanvraagheaders |
| Hoofdtekst |object |Webhook request-object |
| Statuscode |int |Statuscode van aanvraag Webhook |

## <a name="next-steps"></a>Volgende stappen

* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Andere connectors zoeken](apis-list.md)