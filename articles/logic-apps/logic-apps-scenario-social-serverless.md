---
title: aaaScenario - Maak een klant insights dashboard met Azure zonder server | Microsoft Docs
description: Een voorbeeld van hoe u een dashboard toomanage klant feedback, sociale gegevens en meer met Azure Logic Apps en Azure Functions samenstellen kunt.
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
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Een realtime klant insights dashboard maken met Azure Logic Apps en Azure Functions

Azure zonder Server-hulpprogramma's bieden krachtige mogelijkheden tooquickly build en host toepassingen in de cloud Hallo, zonder toothink over infrastructuur.  In dit scenario wordt er een tootrigger dashboard maken op feedback van klanten, feedback met machine learning analyseren en insights publiceren een bron, zoals Power BI of Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Overzicht van scenario Hallo en hulpprogramma 's

In deze oplossing voor tooimplement order, we maken gebruik van Hallo twee belangrijke onderdelen van zonder server apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) en [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).

Logic Apps is een zonder server werkstroomengine in Hallo cloud.  Het biedt orchestration voor zonder Server-onderdelen en ook verbindt tooover 100 services en API's.  We gaan een logic app tootrigger op feedback van klanten maken voor dit scenario.  Hallo-connectors die bij het kruisreagerende toocustomer feedback helpen kunnen onder andere Outlook.com, Office 365, enquête Monkey, Twitter en een HTTP-aanvraag [van een webformulier](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Hallo-werkstroom hieronder, wordt er een hashtag op Twitter bewaken.

Functies bieden zonder server compute in Hallo cloud.  In dit scenario gebruiken we Azure Functions tooflag tweets van klanten op basis van een reeks vooraf gedefinieerde sleutel woorden.

de volledige oplossing Hallo kan worden [bouwen in Visual Studio](logic-apps-deploy-from-vs.md) en [geïmplementeerd als onderdeel van een sjabloon resource](logic-apps-create-deploy-template.md).  Er is ook video-overzicht van scenario Hallo [op Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Hallo logic app tootrigger bouwen op klantgegevens

Na [maken van een logische app](logic-apps-create-a-logic-app.md) in Visual Studio of hello Azure-portal:

1. Toevoegen van een trigger voor **op nieuwe Tweets** van Twitter
2. Hallo trigger toolisten tootweets configureren op een sleutelwoord of hashtag.

   > [!NOTE]
   > Hallo terugkeerpatroon eigenschap op Hallo trigger wordt bepaald hoe vaak Hallo logische app controleert op nieuwe items op triggers op basis van polling

   ![Voorbeeld van een trigger Twitter][1]

Deze app wordt nu gestart op alle nieuwe tweets.  We kunnen vervolgens worden die gegevens tweet en meer Hallo gevoel uitgedrukt inzicht in.  Voor deze gebruiken we Hallo [Azure cognitieve Service](https://azure.microsoft.com/services/cognitive-services/) toodetect gevoel van tekst.

1. Klik op **nieuwe stap**
1. Selecteer of zoek naar Hallo **Tekstanalyse** connector
1. Selecteer Hallo **detecteren gevoel** bewerking
1. Als u wordt gevraagd, geeft u een geldige sleutel cognitieve Services voor Hallo Text Analytics-service
1. Hallo toevoegen **Tweet tekst** als tekst tooanalyze Hallo.

Nu dat we Hallo tweet gegevens en inzichten op Hallo tweet hebt, kan een aantal andere connectors relevant zijn:
* Power BI - rijen tooStreaming gegevensset toevoegen: weergave tweets realtime op een Power BI-dashboard.
* Azure Data Lake - bestand toevoegen: gegevensset tooinclude van klant gegevens tooan Azure Data Lake analytics-taken toevoegen.
* SQL - rijen toevoegen: opslaan van gegevens in een database voor later gebruik.
* Vertraging - bericht verzenden: waarschuwing van een ongebruikt kanaal op negatieve feedback die acties vereist.

Een Azure-functie kan ook worden gebruikt toodo meer aangepaste compute boven op het Hallo-gegevens.

## <a name="enriching-hello-data-with-an-azure-function"></a>Hallo-gegevens uit te breiden met een Azure-functie

Voordat we een functie maken kunt, moeten we toohave een functie-app in ons Azure-abonnement.  Meer informatie over het maken van een Azure-functie in de portal Hallo kunnen [hier vinden](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Voor een functie toobe aangeroepen rechtstreeks vanuit een logische app, het moet een HTTP toohave activeren binding.  Aangeraden wordt Hallo **HttpTrigger** sjabloon.

In dit scenario zou aanvraagtekst Hallo Hallo Azure-functie Hallo tweet tekst zijn.  In de functiecode hello, gewoon definiëren logica op als Hallo tweet tekst een sleutel woord of woordgroep bevat.  Hallo-functie zelf kan worden gehouden zo eenvoudig of complex zo nodig voor Hallo scenario.

Aan het einde van de Hallo van Hallo-functie, moet u gewoon een antwoord toohello logische app met enkele gegevens retourneren.  Dit kan zijn van een eenvoudige Booleaanse waarde (bijvoorbeeld `containsKeyword`), of een complex object.

![Geconfigureerde Azure-functie stap][2]

> [!TIP]
> Bij het openen van een complexe antwoord van een functie in een logische app, moet u Hallo parseren JSON actie gebruiken.

Wanneer de functie Hallo is opgeslagen, kan worden toegevoegd in Hallo logische app die eerder is gemaakt.  In Hallo logische app:

1. Klik op tooadd een **nieuwe stap**
1. Selecteer Hallo **Azure Functions** connector
1. Selecteer een bestaande functie toochoose en blader toohello functie gemaakt
1. Verzenden in Hallo **Tweet tekst** voor Hallo **aanvraagtekst**

## <a name="running-and-monitoring-hello-solution"></a>Controleert Hallo-oplossing

Een van de voordelen van het ontwerpen van zonder Server integraties in Logic Apps Hallo is Hallo uitgebreide foutopsporing en bewakingsmogelijkheden.  Alle uitvoeren (huidige of historische) kan worden weergegeven uit in Visual Studio hello Azure-portal of via SDK's en Hallo REST-API.

Een van de Hallo eenvoudigste manieren tootest een logische app gebruikt Hallo **uitvoeren** knop in Hallo designer.  Te klikken op **uitvoeren** gaan toopoll Hallo-trigger om de vijf seconden totdat een gebeurtenis wordt gedetecteerd en een actuele weergave geven tijdens de voortgang van de Hallo uitvoeren.

Geschiedenis van vorige uitvoering kunnen worden weergegeven op de overzichtsblade Hallo in hello Azure-portal of met behulp van Visual Studio Cloud Explorer Hallo.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Maken van een implementatiesjabloon voor geautomatiseerde implementaties

Zodra een oplossing is ontwikkeld, kan deze worden vastgelegd en geïmplementeerd via een Azure-implementatie sjabloon tooany Azure-regio in Hallo wereld.  Dit is handig voor beide wijzigen parameters voor verschillende versies van deze werkstroom, maar ook voor het integreren van deze oplossing in een pijplijn build en release.  Informatie over het maken van een sjabloon voor de implementatie vindt [in dit artikel](logic-apps-create-deploy-template.md).

Azure Functions kunnen ook worden opgenomen in de implementatiesjabloon Hallo - zodat de volledige oplossing Hallo met alle afhankelijkheden kan worden beheerd als één sjabloon.  Een voorbeeld van een functie-implementatiesjabloon vindt u in Hallo [Azure quickstart sjabloon opslagplaats](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Volgende stappen

* [Zie andere voorbeelden en scenario's voor Azure Logic Apps](logic-apps-examples-and-scenarios.md)
* [Bekijk een videowalkthrough over het maken van deze oplossing voor end-to-end](http://aka.ms/logicappsdemo)
* [Meer informatie over hoe toohandle en catch uitzonderingen in een logische app](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png