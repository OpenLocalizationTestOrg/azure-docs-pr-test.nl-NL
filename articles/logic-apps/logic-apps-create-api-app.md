---
title: aaaCreate web-API's & REST-API's als connectors - Azure Logic Apps | Microsoft Docs
description: Web-API's & REST-API's toocall uw API's, services of systemen in werkstromen voor systeemintegraties met Azure Logic Apps maken
keywords: Web-API's, REST-API's, connectors, werkstromen, systeemintegraties
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Maken van aangepaste API's als connectors voor logic apps

Hoewel Azure Logic Apps biedt [100 + ingebouwde verbindingslijnen](../connectors/apis-list.md) dat u in logic app werkstromen gebruiken kunt, kunt u toocall API's, systemen, en services die niet beschikbaar als connectors. U kunt uw eigen aangepaste API's waarmee acties en triggers toouse in logic apps kunt maken. Hier volgen andere redenen waarom u toocreate uw eigen wellicht API's te gebruiken als connectors in logic apps:

* Breid uw huidige systeem integratie en werkstromen voor integratie.
* Klanten uw service toomanage professionele of persoonlijke taken gebruikt helpen.
* Vouw Hallo reach, detectie en gebruik voor uw service.

In principe connectors web-API's die gebruikmaken van de REST voor pluggable interfaces zijn [Swagger-metagegevensindeling](http://swagger.io/specification/) voor documentatie en JSON als hun exchange gegevensindeling. Omdat connectors REST-API's die via HTTP-eindpunten communiceren zijn, kunt u een andere taal, zoals .NET, Java of Node.js, voor het bouwen van connectors. U kunt ook uw API's hosten op [Azure App Service](../app-service/app-service-value-prop-what-is.md), een platform-as-a-service (PaaS) die het beste eenvoudigste en meest schaalbare manieren Hallo biedt voor het hosten van de API. 

Aangepaste API's toowork met logic apps, uw API kan bieden [ *acties* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) die specifieke taken uitvoeren in logic app werkstromen. Uw API kan ook fungeren als een [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) die een werkstroom van logic app wordt gestart wanneer een opgegeven voorwaarde voldoet aan de nieuwe gegevens of een gebeurtenis. Dit onderwerp wordt beschreven algemene patronen die u uitvoeren kunt voor het bouwen van acties en triggers in uw API op basis van Hallo-gedrag dat u wilt dat uw tooprovide API.

> [!TIP] 
> Hoewel u uw API's als kunt implementeren [web-apps](../app-service-web/app-service-web-overview.md), overweeg dan de implementatie van uw API's als [API-apps](../app-service-api/app-service-api-apps-why-best-platform.md), zodat u uw taak gemakkelijker wanneer ontwikkelen, hosten en API's in Hallo cloud en on-premises gebruiken. Er geen toochange code in de API's, u hoeft de code tooan API-app te implementeren. Meer informatie over hoe te [API-apps die zijn gemaakt met ASP.NET bouwen](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), of [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Voor voorbeelden van API-App voor logic apps zijn gebouwd, gaat u naar Hallo [Azure Logic Apps GitHub-opslagplaats](http://github.com/logicappsio) of [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Nuttige hulpmiddelen

Een aangepaste API werkt het beste met logic apps als Hallo API ook heeft een [Swagger-document](http://swagger.io/specification/) die beschrijft de bewerkingen en parameters Hallo-API's.
Veel bibliotheken, zoals [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), Hallo Swagger-bestand kan automatisch worden gegenereerd voor u. tooannotate hello Swagger-bestand voor de weergavenamen en eigenschaptypen, u kunt ook [TRex](https://github.com/nihaue/TRex) zodat uw Swagger-bestand goed samen met logische apps werkt.

<a name="actions"></a>

## <a name="action-patterns"></a>Actie patronen

Voor logic apps tooperform taken uw aangepaste API moet bieden [ *acties*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Elke bewerking in uw API maps tooan in te grijpen. Een basic actie is een domeincontroller die accepteert HTTP-aanvragen en retourneert HTTP-antwoorden. Een logische app verzendt dus bijvoorbeeld een HTTP-aanvraag tooyour web-app of API-app. Uw app wordt vervolgens een HTTP-antwoord geretourneerd, samen met de inhoud die Hallo logic app kunt verwerken.

U kunt een HTTP-aanvraagmethode schrijven in uw API en beschrijven die methode in een Swagger-bestand voor een standaard-actie. Vervolgens kunt u uw API rechtstreeks met aanroepen een [HTTP-actie](../connectors/connectors-native-http.md) of een [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) in te grijpen. Standaard antwoorden moeten worden geretourneerd binnen Hallo [aanvraag time-outlimiet](./logic-apps-limits-and-config.md). 

![Standaard actie-patroon](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake een logische app geduld terwijl uw API langer actief taken zijn voltooid, uw API kan volgen Hallo [asynchrone polling patroon](#async-pattern) of Hallo [asynchrone webhook patroon](#webhook-actions) in dit onderwerp beschreven. Stel voor een vergelijking waarmee u verschillende gedrag van deze patronen visualiseren, Hallo-proces voor het ordenen van een aangepaste taart van een bakkerij. Hallo polling patroon komt overeen met Hallo gedrag waar u Hallo bakkerij elke toocheck 20 minuten aanroepen of Hallo taart gereed is. Hallo webhook patroon mirrors Hallo gedrag waar Hallo bakkerij u om uw telefoonnummer vraagt zodat deze u aanroepen kunnen wanneer Hallo taart gereed is.

Voor voorbeelden, gaat u naar Hallo [Logic Apps GitHub-opslagplaats](https://github.com/logicappsio). Ook meer informatie over [gebruiksmeting voor acties](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Uitvoeren van langlopende taken worden uitgevoerd met Hallo polling actie patroon

uw API taken uitvoeren die kunnen worden uitgevoerd, langer dan Hallo toohave [time-outlimiet van aanvraag](./logic-apps-limits-and-config.md), kunt u Hallo asynchrone polling patroon. Dit patroon heeft uw API wilt werken in een afzonderlijke thread, maar blijft een actieve verbinding toohello Logic Apps-engine. Op die manier Hallo logische app heeft geen time-out of Ga door met de volgende stap in de werkstroom Hallo Hallo voordat uw API werkende is voltooid.

Hier volgt de algemene patroon Hallo:

1. Zorg ervoor dat de engine Hallo weet dat uw API Hallo aanvraag geaccepteerd en is gestart.
2. Wanneer Hallo engine volgende aanvragen voor de taakstatus van de maakt, kunt u Hallo engine weten wanneer uw API Hallo-taak is voltooid.
3. Relevante gegevens toohello engine terug zodat Hallo logic app werkstroom kan worden voortgezet.

<a name="bakery-polling-action"></a>Nu toepassing hello vorige bakkerij overeenkomstige toohello polling patroon en stel dat u een bakkerij en volgorde een aangepaste taart voor levering aanroepen. Hallo-proces voor het maken van Hallo taart kost tijd en u toowait op Hallo telefoon niet wilt dat tijdens het Hallo bakkerij werkt op Hallo taart. Hallo bakkerij wordt bevestigd dat uw bestelling en moet u elke 20 minuten voor de status van de Hallo taart aanroepen. Na 20 minuten doorgeven, u Hallo bakkerij aanroepen, maar ze laat u weten dat uw taart wordt niet uitgevoerd en dat u in een andere 20 minuten aanroepen moet. Dit proces en weer schakelen wordt vervolgd totdat u aanroept en Hallo bakkerij kunt u zien dat uw bestelling klaar is, en de taart levert. 

Dus laten we dit patroon polling weer worden toegewezen. Hallo bakkerij geeft uw aangepaste API gebruiken, terwijl u Hallo taart klant, Hallo Logic Apps-engine vertegenwoordigen. Wanneer het Hallo-engine roept de API met een aanvraag, wordt uw API bevestigt Hallo-aanvraag en reageert met Hallo tijdsinterval wanneer Hallo-engine kunt taakstatus controleren. Hallo-engine blijft controle taakstatus totdat uw API reageert dat die Hallo-taak wordt uitgevoerd en retourneert gegevens tooyour logische app, die vervolgens werkstroom doorgaat. 

![Polling actie patroon](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Hier vindt u specifieke stappen Hallo voor uw API-toofollow, vanuit het oogpunt van Hallo-API's van beschreven:

1. Wanneer uw API wordt een HTTP-aanvraag toostart werkt, onmiddellijk retourneren een HTTP `202 ACCEPTED` antwoord Hello `location` header verderop in deze stap wordt beschreven. Dit antwoord kunt Hallo Logic Apps engine weten dat uw API is Hallo aanvraag, geaccepteerde Hallo aanvraaglading (gegevens invoeren) en wordt nu verwerkt. 
   
   Hallo `202 ACCEPTED` antwoord moet bestaan uit deze kopteksten:
   
   * *Vereist*: A `location` header waarmee wordt aangegeven Hallo absoluut pad tooa URL waar Hallo Logic Apps-engine de taakstatus van uw API kan controleren

   * *Optionele*: A `retry-after` geeft het aantal seconden dat engine Hallo Hallo-header moet worden gewacht voordat het Hallo controleren `location` URL van taakstatus. 

     Hallo-engine controleert standaard elke 20 seconden. een ander interval toospecify omvatten Hallo `retry-after` -header en het Hallo aantal seconden totdat de volgende poll Hallo.

2. Nadat u Hallo opgegeven tijd, Hallo Logic Apps polls Hallo engine `location` URL toocheck taakstatus. Uw API moet deze controles uitvoeren en deze antwoorden retourneren:
   
   * Als het Hallo-taak is voltooid, geretourneerd met een HTTP `200 OK` antwoord, samen met de Hallo antwoord nettolading (invoer voor de volgende stap Hallo).

   * Als Hallo taak nog wordt verwerkt, geretourneerd met een andere HTTP `202 ACCEPTED` antwoord, maar met Hallo dezelfde kopteksten, zoals de oorspronkelijke antwoord Hallo.

Als uw API na dit patroon, hebt u geen toodo iets in Hallo logic app werkstroom definitie toocontinue taakstatus controleren. Wanneer Hallo engine opgehaald met een HTTP `202 ACCEPTED` antwoord en een geldig `location` koptekst, Hallo engine respecteert Hallo asynchrone patroon en controles Hallo `location` header tot uw API een niet-202-antwoord retourneert.

> [!TIP]
> Bekijk dit voor een asynchrone patroon voorbeeld [asynchrone controller antwoord voorbeeld in GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Uitvoeren van langlopende taken worden uitgevoerd met Hallo webhook actie patroon

Als alternatief kunt u Hallo webhook patroon voor langlopende taken en asynchrone verwerking. Dit patroon heeft Hallo logische app 'callback"van uw API-toofinish verwerken voordat u doorgaat werkstroom wacht. Deze retouraanroep is een HTTP POST die door de URL van een bericht tooa verzonden wanneer een gebeurtenis plaatsvindt. 

<a name="bakery-webhook-action"></a>Nu toepassing hello vorige bakkerij overeenkomstige toohello webhook patroon en stel dat u een bakkerij en volgorde een aangepaste taart voor levering aanroepen. Hallo-proces voor het maken van Hallo taart kost tijd en u toowait op Hallo telefoon niet wilt dat tijdens het Hallo bakkerij werkt op Hallo taart. Hallo bakkerij wordt bevestigd dat uw bestelling, maar dit moment kunt u ze geven uw telefoonnummer zodat deze u aanroepen kunnen wanneer Hallo taart wordt uitgevoerd. Deze tijd ziet Hallo bakkerij u wanneer uw bestelling gereed is en de taart te bezorgen.

Wanneer we dit patroon webhook opnieuw toewijst, vertegenwoordigt Hallo bakkerij uw aangepaste API gebruiken, terwijl u, Hallo taart klant, vertegenwoordigen Hallo Logic Apps-engine. Hallo-engine roept de API met een aanvraag en bevat een URL "callback".
Als het Hallo-taak is voltooid, wordt uw API wordt Hallo URL toonotify Hallo-engine gebruikt en gegevens tooyour logische app, die vervolgens werkstroom doorgaat retourneren. 

Instellen voor dit patroon worden twee eindpunten op uw domeincontroller: `subscribe` en`unsubscribe`

*  `subscribe`eindpunt: wanneer de uitvoering van uw API-actie in de werkstroom Hallo bereikt, Hallo Logic Apps aanroepen Hallo engine `subscribe` eindpunt. Deze stap zorgt ervoor dat Hallo logic app toocreate een callback-URL die uw API worden opgeslagen en wacht Hallo retouraanroep van uw API wanneer werk is voltooid. Uw API en vervolgens teruggebeld met een HTTP POST toohello-URL en wordt elke geretourneerde inhoud en -koppen als invoer toohello logische app wordt doorgegeven.

* `unsubscribe`eindpunt: als Hallo logische app uitgevoerd wordt geannuleerd, Hallo Logic Apps aanroepen Hallo engine `unsubscribe` eindpunt. Uw API kunt Hallo callback URL registratie en stop alle processen indien nodig.

![Webhook actie patroon](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Op dit moment ondersteunt Hallo Logic App-ontwerper detecterende webhook eindpunten via Swagger niet. Daarom voor dit patroon u tooadd moet een [ **Webhook** actie](../connectors/connectors-native-webhook.md) en geef Hallo-URL, kopteksten en hoofdtekst voor uw aanvraag. Zie ook [werkstroomacties en triggers](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass in Hallo retouraanroep-URL, kunt u Hallo `@listCallbackUrl()` Werkstroomfunctie in een van de vorige velden Hallo indien nodig.

> [!TIP]
> Bekijk dit voor een voorbeeld van de webhook-patroon [webhook trigger voorbeeld in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Trigger patronen

Uw aangepaste API kan fungeren als een [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) die een logische app wordt gestart wanneer een opgegeven voorwaarde voldoet aan de nieuwe gegevens of een gebeurtenis. Deze trigger kunt regelmatig te controleren of wachten en luisteren voor nieuwe gegevens of gebeurtenissen op uw service-eindpunt. Als voldoet aan de nieuwe gegevens of een gebeurtenis Hallo opgegeven voorwaarde, Hallo trigger wordt geactiveerd en begint met het Hallo logische app, die toothat trigger luistert. toostart logische apps op deze manier uw API kan volgen Hallo [ *polling trigger* ](#polling-triggers) of Hallo [ *webhook trigger* ](#webhook-triggers) patroon. Deze patronen zijn vergelijkbaar tootheir collega's voor [acties polling](#async-pattern) en [webhookacties](#webhook-actions). Ook meer informatie over [gebruiksmeting voor triggers](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Controleren op nieuwe gegevens of gebeurtenissen regelmatig met de Hallo polling triggerpatroon

Een *polling trigger* fungeert veel op Hallo [polling actie](#async-pattern) eerder in dit onderwerp wordt beschreven. Hallo Logic Apps-engine roept periodiek en controleert Hallo trigger eindpunt voor nieuwe gegevens of gebeurtenissen. Als Hallo engine nieuwe gegevens of een gebeurtenis die voldoet aan de opgegeven voorwaarde wordt gevonden, wordt Hallo trigger wordt geactiveerd. Hallo-engine maakt vervolgens een logic app-exemplaar waarmee Hallo gegevens als invoer worden verwerkt. 

![Polling-triggerpatroon](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Elke aanvraag polling telt als een actie wordt uitgevoerd, zelfs wanneer er geen logic app-exemplaar wordt gemaakt. tooprevent verwerking Hallo dezelfde gegevens meerdere keren, de trigger moet opruimen van de gegevens die al is gelezen en toohello logische app zijn doorgegeven.

Hier vindt u specifieke stappen voor een trigger polling, vanuit het oogpunt van Hallo-API's van beschreven:

| Nieuwe gegevens of gebeurtenis gevonden?  | API-reactie | 
| ------------------------- | ------------ |
| Gevonden | Retourneren van een HTTP `200 OK` status met Hallo antwoord nettolading (invoer voor de volgende stap). <br/>Dit antwoord maakt een logische app-exemplaar en begint met het Hallo-werkstroom. |
| Niet gevonden | Retourneren van een HTTP `202 ACCEPTED` status met een `location` header en een `retry-after` header. <br/>Hallo voor triggers, `location` header moet ook bevatten een `triggerState` query-parameter is meestal een 'tijdstempel'. Uw API kan gebruiken deze id tootrack Hallo laatste keer dat Hallo logic app is geactiveerd. |

Bijvoorbeeld tooperiodically Controleer uw service voor nieuwe bestanden, kunt u een polling-trigger die deze problemen heeft bouwen:

| Aanvraag bevat `triggerState`? | API-reactie |
| -------------------------------- | -------------|
| Nee | Retourneren van een HTTP `202 ACCEPTED` status plus een `location` header met `triggerState` toohello huidige tijd instellen en Hallo `retry-after` too15 interval in seconden. |
| Ja | Controleer uw service voor bestanden die zijn toegevoegd na Hallo `DateTime` voor `triggerState`. |

| Aantal bestanden gevonden | API-reactie |
| --------------------- | -------------|
| Één bestand | Retourneren van een HTTP `200 OK` status en Hallo inhoud nettolading, update `triggerState` toohello `DateTime` van Hallo bestand geretourneerd en `retry-after` too15 interval in seconden. |
| Meerdere bestanden | Retourneren van één bestand op een moment en een HTTP- `200 OK` status, update `triggerState`, en set Hallo `retry-after` too0 interval in seconden. </br>Deze stappen laten weten dat meer gegevens beschikbaar zijn en die motor Hallo onmiddellijk Hallo gegevens van Hallo-URL in Hallo opvragen moet Hallo-engine `location` header. |
| Er worden geen bestanden | Retourneren van een HTTP `202 ACCEPTED` status, worden niet gewijzigd `triggerState`, en set Hallo `retry-after` too15 interval in seconden. |

> [!TIP]
> Voor een voorbeeld polling triggerpatroon, Bekijk dit [poll trigger controller voorbeeld in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Wacht en luistert naar nieuwe gegevens of gebeurtenissen met de Hallo webhook triggerpatroon

Een trigger webhook is een *push-signaal* die wordt gewacht en luistert naar nieuwe gegevens of gebeurtenissen op uw service-eindpunt. Als het voldoet aan de nieuwe gegevens of een gebeurtenis wordt Hallo opgegeven voorwaarde Hallo trigger wordt geactiveerd en maakt u een logische app-exemplaar, die vervolgens Hallo gegevens als invoer verwerkt.
Webhook-triggers veel op Hallo fungeren [webhookacties](#webhook-actions) eerder in dit onderwerp beschreven en worden ingesteld met `subscribe` en `unsubscribe` eindpunten. 

* `subscribe`eindpunt: wanneer u toevoegen en de trigger van een webhook niet opslaan in uw logische app, Hallo Logic Apps aanroepen Hallo engine `subscribe` eindpunt. Deze stap zorgt ervoor dat Hallo logic app toocreate een callback-URL die uw API worden opgeslagen. Wanneer er nieuwe gegevens of een gebeurtenis die voldoet aan de opgegeven voorwaarde hello, wordt uw API teruggebeld met een HTTP POST toohello-URL. Hallo inhoud nettolading en -koppen doorgeven als invoer toohello logische app.

* `unsubscribe`eindpunt: als Hallo webhook trigger of volledige logische app wordt verwijderd, Hallo Logic Apps aanroepen Hallo engine `unsubscribe` eindpunt. Uw API kunt Hallo callback URL registratie en stop alle processen indien nodig.

![Webhook triggerpatroon](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Op dit moment ondersteunt Hallo Logic App-ontwerper detecterende webhook eindpunten via Swagger niet. Daarom voor dit patroon u tooadd moet een [ **Webhook** trigger](../connectors/connectors-native-webhook.md) en geef Hallo-URL, kopteksten en hoofdtekst voor uw aanvraag. Zie ook [HTTPWebhook trigger](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass in Hallo retouraanroep-URL, kunt u Hallo `@listCallbackUrl()` Werkstroomfunctie in een van de vorige velden Hallo indien nodig.
>
> tooprevent verwerking Hallo dezelfde gegevens meerdere keren, de trigger moet opruimen van de gegevens die al is gelezen en toohello logische app zijn doorgegeven.

> [!TIP]
> Bekijk dit voor een voorbeeld van de webhook-patroon [webhook trigger controller voorbeeld in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Implementeren en aangepaste API's beveiligd tegen aanroepen

Na het maken van uw aangepaste API's, instellen van uw API's voor de implementatie zodat u veilig kunt aanroepen. Meer informatie over hoe te[implementeren, aanroepen en beveiligt u aangepaste API's voor logic apps](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Aangepaste API's tooAzure publiceren

toomake uw aangepaste API's beschikbaar voor openbare gebruik in Azure, dienen de benoeming toohello [Microsoft Azure-gecertificeerd programma](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Help opvragen

Voor specifieke hulp met aangepaste API's, neem contact op met [ customapishelp@microsoft.com ](mailto:customapishelp@microsoft.com).

tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Volgende stappen

* [Meten van gebruik voor activiteiten en triggers](logic-apps-pricing.md)
* [Inhoudstypen verwerken](./logic-apps-content-type.md)
* [Fouten en uitzonderingen verwerken](./logic-apps-exception-handling.md)
* [Toegang tot beveiligde tooyour logic apps](./logic-apps-securing-a-logic-app.md)
* [Bel, trigger of nesten van logic apps met HTTP-eindpunten](./logic-apps-http-endpoint.md)