---
title: aaaConnect apps en gegevens te integreren met werkstromen - Azure Logic Apps | Microsoft Docs
description: Maak werkstromen en automatiseer processen door met apps verbinding te maken en gegevens te integreren met Azure Logic Apps.
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Wat zijn Logic Apps?
Logische Apps bieden een manier toosimplify en schaalbare integraties en werkstromen in Hallo cloud implementeren. Het biedt een visuele ontwerpfunctie toomodel en uw automatiseren als een reeks stappen bekend als een werkstroom.  Er zijn [veel connectors](../connectors/apis-list.md) via de cloud en on-premises tooquickly Hallo die is geïntegreerd in de services en protocollen.  Een logische app begint met een trigger (like "wanneer een account is toegevoegd tooDynamics CRM') en nadat veel combinaties van acties, conversies en voorwaarde logica met het starten beginnen kunt.

Hallo voordelen van het gebruik van Logic Apps zijn Hallo volgende:  

* Tijd besparen door complexe processen met eenvoudige toounderstand design tools ontwerpen
* Patronen en werkstromen naadloos implementeren, die anders zouden zijn moeilijk tooimplement in code
* Snel aan de slag met voorbeelden
* Uw logic app aanpassen met uw eigen API’s, code en acties
* Verbinding maken en synchroniseren van verschillende systemen on-premises en Hallo cloud
* Opbouwen van BizTalk-server, API Management, Azure Functions en Azure Service Bus met eersteklas integratieondersteuning

Logic Apps is een volledig beheerde iPaaS (integratie Platform als een Service) zodat ontwikkelaars niet toohave tooworry over het bouwen die als host fungeert, schaalbaarheid, beschikbaarheid en beheer.  Logic Apps wordt automatisch toomeet vraag opschalen.

![App-ontwerper voor stromen](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Zoals eerder vermeld kunt u met Logic Apps bedrijfsprocessen automatiseren. Hieronder vindt u enkele voorbeelden:  

* Verplaats bestanden geüpload tooan FTP-server in Azure Storage
* Proces- en routeorders verspreid over de cloud en on-premises systemen
* Bewaken alle tweets over een bepaalde onderwerp, Hallo gevoel analyseren en waarschuwingen en taken voor items die moeten worden opvolgen maken.

Dergelijke scenario's kunnen worden geconfigureerd via de visuele ontwerpfunctie Hallo en zonder één regel code te schrijven. Ga nu aan de slag met het [bouwen van een logische app][create].  Na het schrijven - kan een logische app[snel worden geïmplementeerd en opnieuw geconfigureerd](../logic-apps/logic-apps-create-deploy-template.md) over verschillende omgevingen en regio’s.

## <a name="why-logic-apps"></a>Waarom Logic Apps?
Logic Apps worden snelheid en schaalbaarheid naar Hallo enterprise integration-ruimte.  Hallo gebruiksgemak Hallo ontwerper van de verschillende beschikbare triggers en acties en krachtige beheerprogramma's maken het centraliseren van uw API's eenvoudiger dan ooit.  Wanneer bedrijven naar digitalization verplaatst, kunt Logic Apps u tooconnect verouderde en geavanceerde systemen samen.

Bovendien met onze [Enterprise Integration-Account] [ biztalk] kunt u de schaal toomature integratiescenario's met Hallo macht van een [XML-berichtenservice] [ xml], [handelspartnerbeheer][tpm], en meer.

* **Eenvoudig toouse ontwerpfuncties** -Logic Apps kunnen worden ontworpen end-to-end in Hallo browser of met Visual Studio-hulpprogramma's. Beginnen met een trigger - van een eenvoudige planning toowhen die een probleem met de GitHub wordt gemaakt. Vervolgens een willekeurig aantal acties met uitgebreide galerie met connectors Hallo indelen.
* **API's eenvoudig verbinding** -zelfs samenstellingstaken die gemakkelijk toodescribe zijn moeilijk tooimplement in code. Logic Apps maakt het eenvoudig tooconnect verschillende systemen. Wilt u tooconnect uw marketingoplossing cloud tooyour lokale factureringssysteem? Wilt u toocentralize via API's en systemen met een Enterprise Service Bus-berichtenservice? Logische apps zijn Hallo snelste, meest betrouwbare manier toodeliver oplossingen toothese problemen.
* **Snel aan de slag van sjablonen** -toohelp die u aan de slag we bieden een [galerie met sjablonen] [ templates] waarmee u toorapidly enkele algemene oplossingen maken. Geavanceerde oplossingen voor B2B toosimple SaaS-connectiviteit en zelfs enkele net 'voor het plezier' - Hallo galerie is de snelste manier tooget Hallo gestart met Hallo kracht van Logic Apps.
* **Standaard uitbreidbaar** -Zie niet Hallo-connector die u nodig? Logic Apps is ontworpen toowork door uw eigen API's en code. u kunt eenvoudig uw eigen toouse API-app als een aangepaste connector maken of aanroep doen naar een [Azure-functie](https://functions.azure.com) tooexecute codefragmenten van code op aanvraag. 
* **Echte paardenkracht bij integratie** - Start eenvoudig en groei wanneer dat nodig is. Logic Apps kan eenvoudig gebruikmaken van Hallo kracht van BizTalk, van Microsoft bedrijfstak toonaangevende oplossing tooenable integratie professionals toobuild Hallo integratieoplossingen ze nodig hebben. Meer informatie over Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Concept van Logic Apps
Hallo Hieronder volgen enkele Hallo belangrijke onderdelen Hallo Logic Apps-ervaring. 

* **Werkstroom** -Logic Apps biedt een grafisch toomodel uw bedrijfsprocessen als een reeks stappen of een werkstroom.
* **Beheerde Connectors** -uw logische apps toegang nodig tot toodata en services. Beheerde connectors specifiek tooaid worden gemaakt wanneer u verbinding maakt tooand werken met uw gegevens. Hallo-lijst van connectors die nu beschikbaar in [beheerde connectors][managedapis].
* **Triggers** - Sommige Beheerde Connectoren kunnen ook werken als trigger. Een trigger start een nieuw exemplaar van een werkstroom op basis van een bepaalde gebeurtenis, zoals Hallo aankomst van een e-mailbericht of een wijziging in uw Azure Storage-account.
* **Acties** -elke stap na Hallo trigger in een werkstroom wordt een actie genoemd. Elke actie is doorgaans toegewezen tooan-bewerking op uw beheerde connector of aangepaste API-apps.
* **Enterprise Integration Pack** - Voor meer geavanceerde integratiescenario’s omvat Logic Apps functies van BizTalk. BizTalk is Microsoft’s toonaangevende integratieplatform. Hallo Enterprise Integration Pack connectors kunnen u tooeasily validatie, transformatie en meer in tooyour logische App werkstromen bevatten.

## <a name="getting-started"></a>Aan de slag
* tooget gestart met Logic Apps, volgt u Hallo [een logische App maken] [ create] zelfstudie.  
* [Algemene voorbeelden en scenario's weergeven](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Met Logic Apps kunt u bedrijfsprocessen automatiseren](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Meer informatie over hoe tooIntegrate uw systemen met Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
