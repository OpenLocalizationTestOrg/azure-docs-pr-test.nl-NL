---
title: aaaOverview van Azure zonder server | Microsoft Docs
description: Krachtige oplossingen maken in de cloud Hallo zonder toothink over infrastructuur.
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Overzicht van Azure zonder server met functies en Logic Apps

Zonder server toepassingen bieden voordelen van een toename van de snelheid van de ontwikkeling van, vermindering van de vereiste code en eenvoud binnen de schaal.  In dit artikel wordt in verschillende kenmerken Hallo zonder server oplossingen en Azure zonder server-producten.

## <a name="what-is-serverless"></a>Wat is zonder server?

Zonder server betekent niet dat er zijn geen servers: het betekent Hallo developer geen tooworry over servers.  Een groot deel van de traditionele toepassingsontwikkeling is beantwoorden van vragen rond schalen, hosting en controle van oplossingen toomeet Hallo eisen van de toepassing hello.  Met zonder server, worden deze vragen afgehandeld als onderdeel van Hallo-oplossing.  Bovendien worden zonder server toepassingen gefactureerd op een plan op basis van verbruik.  Als de toepassing hello nooit gebruikt wordt, is nooit kosten met zich mee ontstaan.  Deze functies kunnen ontwikkelaars toofocus uitsluitend op Hallo zakelijke logica van Hallo-oplossing.

Hallo core services in Azure rond zonder server zijn [Azure Functions](https://azure.microsoft.com/services/functions/) en [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).  Beide oplossingen Hallo principes van de bovenstaande Volg en kunnen ontwikkelaars toobuild robuuste cloud-toepassingen met minimale code.

## <a name="what-are-azure-functions"></a>Wat zijn de Azure Functions?

Azure Functions is een oplossing voor het eenvoudig uitvoeren van kleine stukjes code of 'functies' in de cloud Hallo. U kunt alleen Hallo code schrijven dat u nodig hebt voor Hallo probleem bij de hand, zonder dat u een hele toepassing of Hallo infrastructuur toorun deze. Functies kunnen aanbrengen ontwikkelen nog efficiënter en kunt u de gewenste programmeertaal, zoals C#, F #, Node.js, Python of PHP. Betaalt alleen voor Hallo tijd die uw code wordt uitgevoerd en Azure schaalt naar behoefte.

Als u wilt toojump rechts in en aan de slag met Azure Functions, beginnen met een [uw eerste Azure-functie maken](../azure-functions/functions-create-first-azure-function.md). Als u meer technische informatie over functies zoekt, raadpleegt u Hallo [referentie voor ontwikkelaars](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>Wat zijn Azure Logic Apps?

Logische Apps van Azure biedt een manier toosimplify en schaalbare integraties en werkstromen in Hallo cloud implementeren. Het biedt een visuele ontwerpfunctie toomodel en automatiseren als een reeks stappen een werkstroom wordt aangeroepen.  Er zijn [veel connectors](../connectors/apis-list.md) via cloud en on-premises services tooquickly verbinding maken met een app zonder server tooother API's.  Een logische app begint met een trigger (like "wanneer een account is toegevoegd tooDynamics CRM') en nadat starten kunt beginnen met veel combinaties acties, conversies en voorwaarde logica.  Logic Apps is een uitstekende keuze wanneer verschillende Azure-functies in een proces - organiseren, vooral wanneer Hallo proces vereist interactie met een extern systeem of de API.

tooget gestart met Logic Apps, te beginnen met [maken van uw eerste logische app](logic-apps-create-a-logic-app.md).  Als u meer technische informatie over Logic Apps zoekt, raadpleegt u Hallo [referentie voor ontwikkelaars](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Hoe kan ik bouwen en implementeren zonder server-toepassingen in Azure?

Azure biedt een uitgebreide set hulpprogramma's voor ontwikkeling, implementatie en beheer van apps zonder server.  Apps kunnen worden gebouwd rechtstreeks in hello Azure-portal of met [tooling vanuit Visual Studio](logic-apps-serverless-get-started-vs.md).  Wanneer een toepassing ontwikkeld deze kan worden [onmiddellijk geïmplementeerd](logic-apps-create-deploy-template.md).  Azure biedt ook bewaking voor zonder server apps.  Deze controle kan worden geopend vanuit hello Azure-portal via Hallo API SDK's of met geïntegreerde tooling tooOMS en Application Insights.

## <a name="next-steps"></a>Volgende stappen

* [Het bouwen van een app zonder server in Visual Studio aan de slag](logic-apps-serverless-get-started-vs.md)
* [Maak een klant insights dashboard met zonder server](logic-apps-scenario-social-serverless.md)
* [Een implementatiesjabloon voor een logische app bouwen](logic-apps-create-deploy-template.md)