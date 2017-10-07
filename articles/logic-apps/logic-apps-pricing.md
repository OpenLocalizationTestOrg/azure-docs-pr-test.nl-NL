---
title: aaaPricing & facturering - Azure Logic Apps | Microsoft Docs
description: Meer informatie over prijzen en facturering werking voor Azure Logic Apps.
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Prijsmodel voor logische apps
Logische Apps van Azure kunt u tooscale en integratie-werkstromen worden uitgevoerd in Hallo cloud.  Hieronder vindt u meer informatie over Hallo facturerings- en prijsstelling voor Logic Apps.
## <a name="consumption-pricing"></a>Prijzen voor verbruik
Nieuw gemaakte Logic Apps gebruiken voor een plan verbruik. Met Hallo Logic Apps verbruik prijsmodel betaalt u alleen voor wat u gebruikt.  Logische Apps zijn niet beperkt wanneer u een plan verbruik.
Alle acties die worden uitgevoerd in een uitvoering van een logische app-exemplaar zijn gemeten.
### <a name="what-are-action-executions"></a>Wat zijn actie uitvoeringen?
Elke stap in de definitie van een logische app is een actie, waaronder de triggers, control flow stappen zoals voorwaarden, scopes voor elke lussen totdat lussen doen, roept tooconnectors en aanroepen toonative acties.
Triggers zijn speciale handelingen die ontworpen tooinstantiate een nieuw exemplaar van een logische app zijn wanneer een bepaalde gebeurtenis plaatsvindt.  Er zijn diverse verschillende gedragingen voor triggers kunnen beïnvloeden hoe Hallo logische app datalimiet geldt.
* **Polling-trigger** – deze trigger controleert voortdurend een eindpunt totdat er een bericht dat voldoet aan de criteria Hallo ontvangt voor het maken van een exemplaar van een logische app.  Hallo polling-interval kan worden geconfigureerd in Hallo trigger in Hallo Logic App-ontwerper.  Elke aanvraag polling, telt zelfs als dit niet geen exemplaar van een logische app maken, als de uitvoering van een actie.
* **Webhook trigger** – deze trigger wordt gewacht op een client toosend deze een aanvraag voor een bepaald eindpunt.  Elke aanvraag verzonden toohello webhook eindpunt telt als de uitvoering van een actie. Hello aanvraag- en HTTP-Webhook trigger Hallo zijn beide webhook-triggers.
* **Terugkeerpatroon trigger** – deze trigger maakt een exemplaar van Hallo logische app op basis van het terugkeerpatroon Hallo geconfigureerd in het Hallo-trigger.  Een trigger terugkeerpatroon kan bijvoorbeeld geconfigureerde toorun elke drie dagen of zelfs elke minuut.

Trigger uitvoeringen in Hallo Logic Apps resourceblade in Hallo Trigger geschiedenis onderdeel weergegeven.

Alle acties die zijn uitgevoerd, of ze zijn geslaagd of mislukt als de uitvoering van een actie zijn datalimiet.  Acties die zijn overgeslagen vanwege tooa voorwaarde niet voldaan aan of acties die niet worden uitgevoerd omdat Hallo logische app beëindigd voordat de voltooid, worden niet meegeteld als actie-uitvoeringen.

Acties die worden uitgevoerd binnen lussen worden per herhaling van de lus Hallo meegeteld.  Bijvoorbeeld één actie in een voor elke lus doorloopt een lijst met 10 items worden geteld als Hallo aantal items in lijst hello (10) vermenigvuldigd met het aantal acties in Hallo lus (1) Hallo plus één voor het initiëren van de lus Hallo Hallo voor , die in dit voorbeeld zou zijn (10 * 1) + 1 = 11 actie uitvoeringen.
Uitgeschakelde Logic Apps kunnen geen nieuwe exemplaren geïnstantieerd, en daarom tijdens uitgeschakeld, worden niet in rekening gebracht.  Worden gelet dat na het uitschakelen van een logische app even de tijd voor Hallo exemplaren tooquiesce duurt voordat volledig wordt uitgeschakeld.
### <a name="integration-account-usage"></a>Gebruik van het Account integratie
Opgenomen in gebruik op basis van verbruik is een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) voor onderzoek, ontwikkeling en testdoeleinden zodat u toouse Hallo [B2B/EDI](logic-apps-enterprise-integration-b2b.md) en [XML-verwerking](logic-apps-enterprise-integration-xml.md)functies van Logic Apps zonder extra kosten. U kunt toocreate zijn maximaal één account per regio en opslaan van too10 overeenkomsten en 25 maps. Schema's, certificaten en partners hebben geen limieten en u zoveel naar wens kunt uploaden.

Bovendien toohello opnemen van integratieaccounts het energieverbruik, u kunt ook maken standaard integratieaccounts zonder deze beperkingen en met onze standaard SLA van Logic Apps. Zie voor meer informatie [Azure-prijzen](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>App Service-abonnementen
Logische apps eerder hebt gemaakt die verwijzen naar een App Service-Plan blijft toobehave als voor. Afhankelijk van het Hallo-plan is gekozen, worden beperkt na hello voorgeschreven dagelijkse uitvoeringen is overschreden, maar worden gefactureerd met behulp van Hallo actie uitvoering meter.
EA-klanten die een App Service-Plan in het abonnement waarvoor geen toobe expliciet die zijn gekoppeld aan logische App hello, hebt u Hallo opgenomen hoeveelheden wilt profiteren.  Bijvoorbeeld, als er een Standard-App Service-Plan in uw abonnement EA en een logische App in hetzelfde abonnement Hallo en niet in rekening gebracht voor 10.000 actie uitvoeringen per dag (Zie de volgende tabel). 

App Service-abonnementen en hun dagelijkse toegestane actie uitvoeringen:
|  | Gratis en gedeeld/eenvoudige | Standard | Premium |
| --- | --- | --- | --- |
| Actie-uitvoeringen per dag |200 |10.000 |50,000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Converteren van App Service-Plan tooConsumption prijzen
een logische App met een App Service-abonnement gekoppeld toochange tooa verbruik model verwijderen Hallo verwijzing toohello App Service-Plan in de definitie van logische Apps Hallo.  Deze wijziging kunt u doen met een aanroep tooa PowerShell-cmdlet:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Prijzen
Zie voor prijsinformatie, [Logic Apps prijzen](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Volgende stappen
* [Een overzicht van Logic Apps][whatis]
* [Uw eerste logische app maken][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

