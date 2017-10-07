---
title: Overzicht van Functions aaaAzure | Microsoft Docs
description: Begrijpen hoe toouse Azure Functions toooptimize asynchrone workloads in minuten.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Een inleiding tooAzure fungeert  
Azure Functions is een oplossing voor het eenvoudig uitvoeren van kleine stukjes code of 'functies' in de cloud Hallo. U kunt alleen Hallo code schrijven dat u nodig hebt voor Hallo probleem bij de hand, zonder dat u een hele toepassing of Hallo infrastructuur toorun deze. Met Functions wordt ontwikkelen nog efficiënter en kunt u de door u gewenste programmeertaal gebruiken, zoals C#, F#, Node.js, Python of PHP. Betaalt alleen voor Hallo tijd die uw code wordt uitgevoerd en Azure tooscale vertrouwen, indien nodig. Met Azure Functions kunt u toepassingen zonder server ontwikkelen op Microsoft Azure.

Dit onderwerp bevat een globaal overzicht van Azure Functions. Als u wilt toojump rechts in en aan de slag met Azure Functions, beginnen met een [uw eerste Azure-functie maken](functions-create-first-azure-function.md). Als u meer technische informatie over functies zoekt, raadpleegt u Hallo [referentie voor ontwikkelaars](functions-reference.md).

## <a name="features"></a>Functies
Hier volgen een aantal essentiële functies van Azure Functions:

* **Keuze van taal**: schrijf functies met C#, F#, Node.js, Python, PHP, batch, bash of elk uitvoerbaar bestand.
* **Betalen per gebruik prijzen model** : betaal alleen voor Hallo tijd besteed aan het uitvoeren van uw code. Zie Hallo verbruik hosting-optie in Hallo plannen [prijzen sectie](#pricing).  
* **Breng uw eigen afhankelijkheden mee**: Functions ondersteunt NuGet en NPM, zodat u uw favoriete bibliotheken kunt gebruiken.  
* **Geïntegreerde beveiliging**: beveilig HTTP-geactiveerde functies met OAuth-providers zoals Azure Active Directory, Facebook, Google, Twitter en Microsoft-account.  
* **Eenvoudige integratie**: maak eenvoudig gebruik van Azure-services en Software-as-a-Service (SaaS)-producten. Zie Hallo [integraties sectie](#integrations) voor enkele voorbeelden.  
* **Flexibel ontwikkelen** - Code van uw functies direct in Hallo portal of stel doorlopende integratie en implementeer uw code via GitHub, Visual Studio Team Services en andere [ondersteunde ontwikkelprogramma's](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Open source** -runtime van Hallo Functions is open source en [beschikbaar op GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>Wat kan ik doen met Functions?
Azure Functions is een uitstekende oplossing voor het verwerken van gegevens, integreren van systemen, werken met het internet der dingen (IoT) Hallo en het bouwen van eenvoudige API's en microservices. Houd rekening met functies voor taken, zoals de installatiekopie of verwerking, onderhouden van bestanden of alle taken die u wilt dat toorun volgens een schema. 

Functions biedt sjablonen tooget u gestart met de belangrijkste scenario's, waaronder de volgende Hallo:

* **BlobTrigger** -proces Azure Storage-blobs wanneer ze toocontainers worden toegevoegd. Deze functie kunt u bijvoorbeeld gebruiken voor het wijzigen van de grootte van afbeeldingen.
* **EventHubTrigger** -reageren tooevents bezorgd tooan Azure Event Hub. Dit is met name handig voor toepassingsinstrumentatie, verwerking van gebruikerservaringen of werkstromen en scenario's met betrekking tot het Internet of Things (IoT).
* **Generic webhook**: verwerk HTTP-webhook-aanvragen van services die webhooks ondersteunen.
* **GitHub webhook** -reageren tooevents die in uw GitHub-opslagplaatsen voorkomen. Zie voor een voorbeeld [Een webhook of API-functie maken](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -Hallo uitvoering van uw code te activeren met behulp van een HTTP-aanvraag.
* **QueueTrigger** -toomessages reageren binnenkomen in een Azure Storage-wachtrij. Zie voor een voorbeeld [maken van een Azure-functie die wordt gebonden tooan Azure service](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -verbinding maken met uw code tooother Azure-services of on-premises services door luisterende toomessage wachtrijen. 
* **ServiceBusTopicTrigger** -verbinding maken met uw code tooother Azure-services of on-premises services door tootopics abonneren. 
* **TimerTrigger**: voer opschoonacties of andere batchtaken uit volgens een vooraf gedefinieerd schema. Zie voor een voorbeeld [Een functie voor gebeurtenisverwerking maken](functions-create-an-event-processing-function.md)

Azure Functions ondersteunt *triggers*, die zijn manieren toostart uitvoering van uw code en *bindingen*, die zijn manieren toosimplify coderen voor invoer-en uitvoergegevens. Zie voor een gedetailleerde beschrijving van het Hallo-triggers en bindingen van Azure Functions biedt [Azure Functions triggers en bindingen naslaginformatie](functions-triggers-bindings.md).

## <a name="integrations"></a>Integraties
Azure Functions integreert met diverse services van Azure en derden. Deze services kunnen uw functie activeren en het uitvoeren starten, of fungeren als invoer en uitvoer voor uw code. Hallo volgende service-integraties worden ondersteund door Azure Functions. 

* Azure Cosmos DB
* Azure Event Hubs 
* Azure Mobile Apps (tabellen)
* Azure Notification Hubs
* Azure Service Bus (wachtrijen en onderwerpen)
* Azure Storage (blob, wachtrijen en tabellen) 
* GitHub (webhooks)
* On-premises (met Service Bus)
* Twilio (SMS-berichten)

## <a name="pricing"></a>Wat kost Functions?
Azure Functions heeft twee soorten prijsstelling, Hallo kiezen die het beste past bij uw behoeften: 

* **Plan voor verbruik** : wanneer de functie wordt uitgevoerd, biedt Azure alle benodigde rekenbronnen Hallo. U hebt geen tooworry over het resourcebeheer van de en u betaalt alleen voor Hallo tijd dat uw code wordt uitgevoerd. 
* **App Service-abonnement**: voer uw functies net zo uit als uw web-apps, mobiele apps en API-apps. Wanneer u App Service al voor andere toepassingen gebruikt, kunt u uw functies kunt uitvoeren op Hallo dezelfde zonder extra kosten plannen. 

Volledige prijsinformatie is beschikbaar op Hallo [pagina met prijzen voor Functions](https://azure.microsoft.com/pricing/details/functions/). Zie voor meer informatie over het schalen van uw functies [hoe tooscale Azure Functions](functions-scale.md).

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste Azure-functie maken](functions-create-first-azure-function.md)  
  Meteen en maak uw eerste functie met hello Azure Functions-snelstartgids. 
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)  
  Biedt meer technische informatie over hello Azure Functions-runtime en een referentie voor het coderen van functies en definiëren van triggers en bindingen.
* [Azure Functions testen](functions-test-a-function.md)  
  Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.
* [Hoe tooscale Azure Functions](functions-scale.md)  
  Beschrijft de serviceabonnementen die beschikbaar zijn met Azure Functions, zoals Hallo verbruik hosting plannings- en hoe toochoose Hallo juiste abonnement. 
* [Meer informatie over Azure App Service](../app-service/app-service-value-prop-what-is.md)  
  Azure Functions maakt gebruik van hello Azure App Service-platform voor kernfunctionaliteit zoals implementaties, omgevingsvariabelen en diagnostische gegevens. 

