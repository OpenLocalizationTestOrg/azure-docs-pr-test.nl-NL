---
title: Kiezen tussen stroom, Logic Apps, functies en WebJobs | Microsoft Docs
description: Vergelijken en contrast de voor cloud integration services van Microsoft en bepalen welke service (s) die u moet gebruiken.
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
ms.openlocfilehash: da2ff16b5bdd7a0c171451930ce10427fe5bbda7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Kiezen tussen Stroom, Logische apps, Functies en WebJobs
Dit artikel wordt vergeleken en de volgende services in de Microsoft cloud, die u alle van problemen met integratie en automatisering van bedrijfsprocessen oplossen kunt in tegenstelling tot:

* [Microsoft-stroom](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Azure App Service API](../app-service-web/web-sites-create-web-jobs.md)

Al deze services zijn nuttig wanneer 'lijmen' samen verschillende systemen. Ze kunnen alle definiëren invoer, acties, voorwaarden en uitvoer. U kunt elk van deze uitvoeren op een planning of trigger. Echter elke service voegt een unieke set van waarde en deze te vergelijken is niet een vraag van 'welke service is het meest geschikt?' maar een van de 'welke service is het beste geschikt is voor deze situatie?' Een combinatie van deze services is vaak de beste manier om snel een schaalbare, volledig functionele integratieoplossing te bouwen.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Vs stroom. Logic Apps
Kan bespreken we Microsoft Flow en Azure Logic Apps samen omdat ze beide *configuratie eerste* integratieservices, kunt u gemakkelijk processen en werkstromen te bouwen en integreren met verschillende SaaS- en enterprise-toepassingen. 

* Stroom is ingebouwd in Logic Apps
* Ze hebben de dezelfde workflow designer
* [Connectors](../connectors/apis-list.md) dat werk in een kan ook worden gebruikt in de andere

Stromen machtigt elke werknemer office eenvoudige integraties uitvoeren (bijvoorbeeld SMS voor belangrijke e-mailberichten ophalen) zonder tussenkomst van ontwikkelaars of IT. Logic Apps kunt aan de andere kant geavanceerde of bedrijfskritieke integraties (bijvoorbeeld B2B processen) waarop de procedures DevOps en beveiliging op bedrijfsniveau vereist zijn. Het is gebruikelijk om een zakelijke werkstroom complexiteit overtijd groeien. Dienovereenkomstig, kunt u beginnen met een stroom op het eerste vervolgens converteren naar een logische app, indien nodig.

De volgende tabel kunt u bepalen of de stroom of Logic Apps geschikt voor een bepaalde integratie is.

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
Kan bespreken we Azure Functions en Azure App Service WebJobs samen omdat ze beide *code first* integration services en ontworpen voor ontwikkelaars. Hiermee kunt u, zoals een script of een stuk code in reactie op diverse gebeurtenissen uitvoeren [nieuwe opslag Blobs](functions-bindings-storage.md) of [een aanvraag WebHook](functions-bindings-http-webhook.md). Hier volgen de overeenkomsten: 

* Beide zijn gebouwd op [Azure App Service](../app-service/app-service-value-prop-what-is.md) en profiteer van functies, zoals [bronbeheer](../app-service-web/app-service-continuous-deployment.md), [verificatie](../app-service/app-service-authentication-overview.md), en [bewaking](../app-service-web/web-sites-monitor.md).
* Beide zijn services ontwikkelaars zijn gericht.
* Zowel ondersteunen standaard scripts en programmeertalen.
* Hebben beide NuGet en NPM ondersteunen.

Functies is de natuurlijke ontwikkeling van WebJobs in dat deze het beste dingen over WebJobs neemt en ze aanzienlijk verbeterd. De verbeteringen omvatten: 

* Gestroomlijnde dev-, test en uitvoeren van code rechtstreeks in de browser.
* Ingebouwde integratie met meer Azure-services en -services 3rd derden, zoals [GitHub WebHooks](https://developer.github.com/webhooks/creating/).
* Betalen per gebruik, hoeft te betalen voor een [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Automatische, [dynamische schaling](functions-scale.md).
* Voor bestaande klanten van App Service, op App Service-abonnement nog steeds mogelijk (om te profiteren van resources onder gebruikt).
* Integratie met Logic Apps.

De volgende tabel geeft een overzicht van de verschillen tussen de functies en WebJobs:

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

Of u functies of WebJobs uiteindelijk afhankelijk van wat u al met App Service doet. Als u een App Service-app die u wilt uitvoeren van codefragmenten hebt en u wilt deze gezamenlijk beheren in dezelfde DevOps-omgeving, moet u WebJobs. Als u wilt uitvoeren codefragmenten voor andere Azure-services of zelfs 3rd apps van derden, of als u wilt uw codefragmenten integratie afzonderlijk van uw App Service-apps worden beheerd, of als u wilt uw codefragmenten aanroepen vanuit een logische app, moet u profiteren van de verbeteringen in functies.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Stroom, Logic Apps en functies samen
Zoals eerder vermeld, welke service is het meest geschikt is voor u is afhankelijk van uw situatie. 

* Gebruik voor eenvoudige business optimization, vervolgens stroom.
* Als uw integratiescenario te voor stroom is geavanceerde of u DevOps-mogelijkheden en beveiliging conformiteit moet, gebruikt u Logic Apps.
* Als een stap in uw integratiescenario maximaal aangepaste omzetting of speciale code vereist, een functie-app vervolgens schrijven en vervolgens een functie activeren als een actie in uw logische app.

U kunt een logische app aanroepen in een stroom. U kunt ook een functie in een logische app en een logische app in een functie aanroepen. De integratie tussen stroom, Logic Apps en functies blijven overuren verbeteren. U kunt iets in één service maakt en gebruikt in de andere services. Geldt voor elke investering u in deze drie technologieën is daarom nuttig.

## <a name="next-steps"></a>Volgende stappen
Aan de slag met elk van de services door het maken van uw eerste stroom, logische app, functie-app of webtaak. Klik op een van de volgende koppelingen:

* [Aan de slag met Microsoft-Flow](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Uw eerste Azure-functie maken](functions-create-first-azure-function.md)
* [WebJobs implementeren met Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Of u meer informatie over deze integratieservices met de volgende koppelingen:

* [Gebruik van Azure Functions & Azure App Service voor integratiescenario's door Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Eenvoudige aangebracht door Jeroen Lamanna integraties](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logische Apps Live Webcast](http://aka.ms/logicappslive)
* [Microsoft stromen Veelgestelde vragen over](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Azure WebJobs documentatiebronnen](../app-service-web/websites-webjobs-resources.md)

