---
title: aaaChoose tussen stroom, Logic Apps, functies en WebJobs | Microsoft Docs
description: Vergelijken en contrast Hallo voor cloud integratieservices van Microsoft en bepalen welke service (s) die u moet gebruiken.
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: Microsoft stroom, stroom, logische apps, azure-functies, functies, azure webjobs, webjobs, verwerking, dynamische compute zonder server architectuur van gebeurtenis
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Kiezen tussen Stroom, Logische apps, Functies en WebJobs
Dit artikel wordt vergeleken en Hallo-services in de cloud Microsoft hello, die u alle van problemen met integratie en automatisering van bedrijfsprocessen oplossen kunt te volgen in tegenstelling tot:

* [Microsoft-stroom](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Azure App Service API](../app-service-web/web-sites-create-web-jobs.md)

Al deze services zijn nuttig wanneer 'lijmen' samen verschillende systemen. Ze kunnen alle definiëren invoer, acties, voorwaarden en uitvoer. U kunt elk van deze uitvoeren op een planning of trigger. Echter elke service voegt een unieke set van waarde en deze te vergelijken is niet een vraag van 'welke service is de beste Hallo?' maar een van de 'welke service is het beste geschikt is voor deze situatie?' Een combinatie van deze services is vaak de beste manier Hallo toorapidly een schaalbare, volledige van aanbevolen integratieoplossing bouwen.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Vs stroom. Logic Apps
Kan bespreken we Microsoft Flow en Azure Logic Apps samen omdat ze beide *configuratie eerste* integratieservices, maakt het eenvoudig toobuild processen en werkstromen en integreren met verschillende SaaS- en enterprise toepassingen. 

* Stroom is ingebouwd in Logic Apps
* Ze Hallo hebben dezelfde werkstroomontwerper
* [Connectors](../connectors/apis-list.md) dat werk in een kan ook worden gebruikt in andere Hallo

Stromen dankzij een eenvoudige integratie van office worker tooperform (bijvoorbeeld SMS voor belangrijke e-mailberichten ophalen) zonder tussenkomst van ontwikkelaars of IT. Op Hallo daarentegen, Logic Apps kunt inschakelen geavanceerde of bedrijfskritieke integraties (bijvoorbeeld B2B processen) waarop de procedures DevOps en beveiliging op bedrijfsniveau vereist zijn. Het is gebruikelijk om een werkstroom business toogrow overtijd complexiteit. Dienovereenkomstig, kunt u beginnen met een stroom op het eerste vervolgens deze tooa logische app converteren naar behoefte.

Hallo kunt volgende tabel u bepalen of de stroom of Logic Apps geschikt voor een bepaalde integratie is.

|  | Stroom | Logic Apps |
| --- | --- | --- |
| Doelgroep |Office-werknemers, zakelijke gebruikers |IT-professionals, ontwikkelaars |
| Scenario's |Self-service |Essentiële |
| Hulpprogramma voor ontwerp |In de browser en de mobiele app, alleen de UI |In de browser en [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [codeweergave](../logic-apps/logic-apps-author-definitions.md) beschikbaar |
| DevOps |Ad-hoc ontwikkelen in productie |Source control, testen, ondersteuning, en automatisering en beheerbaarheid in [Azure Resource Management](../logic-apps/logic-apps-arm-provision.md) |
| Ervaring beheerder |[https://flow.Microsoft.com](https://flow.microsoft.com) |[https://Portal.Azure.com](https://portal.azure.com) |
| Beveiliging |Standaardprocedures: [gegevens onafhankelijkheid](https://wikipedia.org/wiki/Technological_Sovereignty), [versleuteling in rust](https://wikipedia.org/wiki/Data_at_rest#Encryption) voor gevoelige gegevens, enzovoort. |Beveiligingscontrole van Azure: [Azure-beveiliging](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Security Center](https://azure.microsoft.com/services/security-center/), [controlelogboeken](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/), en meer. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Vs functies. Webtaken
Kan bespreken we Azure Functions en Azure App Service WebJobs samen omdat ze beide *code first* integration services en ontworpen voor ontwikkelaars. Hiermee kunt u toorun een script of een stuk code in het antwoord toovarious gebeurtenissen, zoals [nieuwe opslag Blobs](functions-bindings-storage.md) of [een aanvraag WebHook](functions-bindings-http-webhook.md). Hier volgen de overeenkomsten: 

* Beide zijn gebouwd op [Azure App Service](../app-service/app-service-value-prop-what-is.md) en profiteer van functies, zoals [bronbeheer](../app-service-web/app-service-continuous-deployment.md), [verificatie](../app-service/app-service-authentication-overview.md), en [bewaking](../app-service-web/web-sites-monitor.md).
* Beide zijn services ontwikkelaars zijn gericht.
* Zowel ondersteunen standaard scripts en programmeertalen.
* Hebben beide NuGet en NPM ondersteunen.

Functies is Hallo natuurlijke evolutie van WebJobs in dat het beste dingen Hallo over WebJobs neemt en ze aanzienlijk verbeterd. Hallo verbeteringen zijn onder andere: 

* Gestroomlijnde dev-, test en uitvoeren van code rechtstreeks in de browser Hallo.
* Ingebouwde integratie met meer Azure-services en -services 3rd derden, zoals [GitHub WebHooks](https://developer.github.com/webhooks/creating/).
* Betalen per gebruik, geen toopay nodig voor een [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Automatische, [dynamische schaling](functions-scale.md).
* Voor bestaande klanten van App Service, op App Service-abonnement nog steeds mogelijk (tootake profiteren van resources onder gebruikt).
* Integratie met Logic Apps.

Hallo volgende tabel geeft een overzicht van Hallo verschillen tussen de functies en WebJobs:

|  | Functies | Webtaken |
| --- | --- | --- |
| Schalen |Configurationless schalen |schalen met App Service-abonnement |
| Prijzen |Betalen per gebruik of een deel van de App Service-abonnement |Onderdeel van App Service-abonnement |
| Uitvoeren van het type |geactiveerd, geplande (met timertrigger) |geactiveerde, continue, geplande |
| Trigger-gebeurtenissen |[timer](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, Slack)](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [Azure Service Bus](functions-bindings-service-bus.md), [Azure Storage](functions-bindings-storage.md) |[Azure Storage](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Azure Servicebus](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| In de browser-ontwikkeling |Ondersteund | Niet ondersteund |
| Venster scripting |experimentele |Ondersteund |
| PowerShell |experimentele |Ondersteund |
| C# |Ondersteund |Ondersteund |
| F# |Ondersteund |Niet ondersteund |
| Bash |experimentele |Ondersteund |
| PHP |experimentele |Ondersteund |
| Python |experimentele |Ondersteund |
| Javascript |Ondersteund |Ondersteund |

Hiermee wordt aangegeven of toouse functies of WebJobs uiteindelijk afhankelijk van wat u al met App Service doet. Als u een App Service-app waarvan u toorun codefragmenten wilt hebt en u toomanage wilt ze samen in dezelfde DevOps-omgeving hello, moet u WebJobs. Als u wilt dat toorun codefragmenten voor andere Azure-services of zelfs 3rd apps van derden, of als u wilt dat uw codefragmenten integratie te afzonderlijk van uw App Service-apps beheren, of als u toocall uw codefragmenten van een logische app wilt, moet u ook te profiteren van alle Hallo-verbeteringen in functies.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Stroom, Logic Apps en functies samen
Zoals eerder vermeld afhankelijk welke service beste geschikt tooyou is van uw situatie. 

* Gebruik voor eenvoudige business optimization, vervolgens stroom.
* Als uw integratiescenario te voor stroom is geavanceerde of u DevOps-mogelijkheden en beveiliging conformiteit moet, gebruikt u Logic Apps.
* Als een stap in uw integratiescenario maximaal aangepaste omzetting of speciale code vereist, een functie-app vervolgens schrijven en vervolgens een functie activeren als een actie in uw logische app.

U kunt een logische app aanroepen in een stroom. U kunt ook een functie in een logische app en een logische app in een functie aanroepen. Hallo-integratie tussen stroom, Logic Apps en functies blijven tooimprove overuren. U kunt bouwen iets in een service en andere services gebruiken in Hallo. Geldt voor elke investering u in deze drie technologieën is daarom nuttig.

## <a name="next-steps"></a>Volgende stappen
Aan de slag met elk van Hallo services door het maken van uw eerste stroom, logische app, functie-app of webtaak. Klik op een Hallo koppelingen te volgen:

* [Aan de slag met Microsoft-Flow](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Uw eerste Azure-functie maken](functions-create-first-azure-function.md)
* [WebJobs implementeren met Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Of meer informatie over deze integratieservices krijgen met Hallo koppelingen te volgen:

* [Gebruik van Azure Functions & Azure App Service voor integratiescenario's door Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Eenvoudige aangebracht door Jeroen Lamanna integraties](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logische Apps Live Webcast](http://aka.ms/logicappslive)
* [Microsoft stromen Veelgestelde vragen over](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Azure WebJobs documentatiebronnen](../app-service-web/websites-webjobs-resources.md)

