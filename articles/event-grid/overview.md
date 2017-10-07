---
title: overzicht van de gebeurtenis raster aaaAzure
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Een inleiding tooAzure gebeurtenis raster

Azure Event raster kunt u tooeasily build toepassingen met architectuur op basis van gebeurtenissen. U selecteren hello Azure resource die u wilt toosubscribe aan, en geven Hallo gebeurtenis-handler of WebHook eindpunt toosend Hallo gebeurtenis. Gebeurtenis raster bevat ingebouwde ondersteuning voor gebeurtenissen die afkomstig zijn van de Azure-services, zoals de storage-blobs en resourcegroepen. Gebeurtenis raster heeft ook aangepaste ondersteuning voor de toepassing en gebeurtenissen van derden, met behulp van aangepaste onderwerpen en aangepaste webhooks. 

U kunt filters tooroute specifieke gebeurtenissen toodifferent eindpunten, multicast toomultiple eindpunten, gebruiken en zorg ervoor dat uw gebeurtenissen op betrouwbare wijze worden bezorgd. Gebeurtenis raster ook met ingebouwde ondersteuning voor aangepaste en derden gebeurtenissen.

Voor de preview-versie Hallo gebeurtenis raster ondersteunt **westus2** en **westcentralus** locaties. Andere regio's worden toegevoegd.

Dit artikel bevat een overzicht van Azure Event raster. Als u tooget met raster gebeurtenis wordt gestart wilt, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).

![Gebeurtenis raster functionele model](./media/overview/event-grid-functional-model.png)

Blob Storage is momenteel niet openbaar beschikbaar als een publisher.

## <a name="concepts"></a>Concepten

Er zijn vijf concepten in Azure gebeurtenis raster waarmee u aan de slag:

* **Gebeurtenissen** -wat is er gebeurd.
* **Gebeurtenisuitgevers bronnen** - Hallo gebeurtenis heeft plaatsgevonden.
* **Onderwerpen over** -Hallo eindpunt waar de gebeurtenissen voor het verzenden van uitgevers.
* **Abonnementen voor gebeurtenissen** -Hallo eindpunt of de ingebouwde mechanisme tooroute gebeurtenissen, soms toomultiple handlers. Abonnementen worden ook gebruikt door handlers toointelligently binnenkomende Filtergebeurtenissen.
* **Gebeurtenis-handlers** - app Hallo of kruisreagerende toohello-gebeurtenis.

Zie voor meer informatie over deze concepten [concepten in Azure gebeurtenis raster](concepts.md).

## <a name="capabilities"></a>Functionaliteit

Hier volgen enkele van de belangrijkste functies van Azure Event raster Hallo:

* **Eenvoud** -punt en klik op tooaim-gebeurtenissen van uw Azure-resource tooany gebeurtenis-handler of het eindpunt.
* **Geavanceerde filters** -Filter op de gebeurtenis type of een gebeurtenis publiceren pad tooensure gebeurtenis-handlers alleen relevante gebeurtenissen ontvangen.
* **Fan-out** -meerdere eindpunten toohello abonneren dezelfde gebeurtenis toosend kopieën van Hallo gebeurtenis tooas veel plaatsen indien nodig.
* **Betrouwbaarheid** -gebruikmaken van 24 uur opnieuw proberen met exponentieel uitstel tooensure gebeurtenissen worden geleverd.
* **Betalen per gebeurtenis** : betaal alleen voor Hallo bedrag u gebeurtenis raster.
* **Hoge doorvoersnelheid** -hoog volume werkbelastingen voor gebeurtenis raster bouwen met ondersteuning voor miljoenen gebeurtenissen per seconde.
* **Ingebouwde gebeurtenissen** - slag snel gebruiksklaar met ingebouwde gebeurtenissen resource gedefinieerd.
* **Aangepaste gebeurtenissen** -gebeurtenis raster route, filter en betrouwbaar afleveren aangepaste gebeurtenissen in uw app gebruiken.

## <a name="built-in-publisher-and-handler-integration"></a>Ingebouwde publisher en de handler-integratie

Azure biedt gebeurtenisondersteuning voor ingebouwde met meerdere services, waaronder zowel uitgevers en handlers.

### <a name="publishers"></a>Uitgevers

Op dit moment hebben hello volgende Azure-services een ingebouwde publisher ondersteuning voor gebeurtenis raster:

* Resourcegroepen (beheerbewerkingen)
* Azure-abonnementen (beheerbewerkingen)
* Event Hubs
* Aangepaste-onderwerpen

Andere Azure-services worden van dit jaar met toegevoegd.

### <a name="handlers"></a>Handlers

Op dit moment hebben hello volgende Azure-services een ingebouwde handler ondersteuning voor gebeurtenis raster: 

* Azure Functions
* Logic Apps
* Azure Automation
* Webhooks.

Andere Azure-services worden van dit jaar met toegevoegd.

## <a name="what-can-i-do-with-event-grid"></a>Wat kan ik doen met gebeurtenis raster

Azure Event raster biedt verschillende mogelijkheden die aanzienlijk zonder server verbeteren, ops automatisering en integratie werk: 

### <a name="serverless-application-architectures"></a>Architecturen voor serverloze toepassingen

![Toepassing zonder server](./media/overview/serverless_web_app.png)

Event Grid verbindt gegevensbronnen en gebeurtenis-handlers. Bijvoorbeeld, gebeurtenis raster tooinstantly trigger-een zonder server functie toorun installatiekopie analyse telkens wanneer een nieuwe foto is toegevoegd tooa blob storage-container gebruiken. 

### <a name="ops-automation"></a>OPS Automation

![Ops-automatisering](./media/overview/Ops_automation.png)

Gebeurtenis raster kunt u toospeed automation en afdwingen van beleid vereenvoudigen. Zo kan Event Grid een melding sturen naar Azure Automation wanneer er een virtuele machine is gemaakt of wanneer er een SQL-database in gebruik wordt genomen. Deze gebeurtenissen kunnen worden gebruikt tooautomatically Controleer of-configuraties zijn compatibel zijn, metagegevens in de operations-hulpprogramma's, tag virtuele machines of werkitems bestand geplaatst.

### <a name="application-integration"></a>Integratie van toepassingen

![Integratie van toepassingen](./media/overview/app_integration.png)

Event Grid verbindt uw app met andere services. Bijvoorbeeld een aangepaste onderwerp toosend van uw app gebeurtenis gegevens tooEvent raster en maken en te profiteren van de geavanceerde routering, betrouwbare aflevering directe integratie met Azure. U kunt ook gebeurtenis raster met Logic Apps tooprocess gegevens overal en gebruiken zonder code te schrijven. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Hoe wordt gebeurtenis raster van andere integratie van Azure-services?

Gebeurtenis raster is een eventing backplane waarmee gebeurtenisafhankelijke, reactieve programmering. Het is nauw geïntegreerd met Azure-services en kan worden geïntegreerd met services van derden. Hallo-gebeurtenisbericht bevat Hallo-informatie die u nodig hebt tooreact toochanges in services en toepassingen. Raster gebeurtenis is niet een gegevens-pijplijn en bezorgt geen daadwerkelijke Hallo-object dat is bijgewerkt.

Service Bus is geschikt voor traditionele enterprise-toepassingen waarvoor transacties, rangschikken, detectie van duplicaten en onmiddellijk consistentie. Gebeurtenis raster is ontworpen voor snelheid, schaal, breedte en lage kosten in een reactieve model. Het is uitermate geschikt tooserverless architectuur.

Gebeurtenis raster vormt een aanvulling op andere Azure-services zoals Logic Apps en Event Hubs. Raster gebeurtenistriggers Hallo logic app toobegin de workflow. Event Hubs werkt met gebeurtenis raster doordat u tooreact tooevents van Event Hubs vastleggen en build inkomende en transformatie gegevenspijplijnen.

## <a name="how-much-does-event-grid-cost"></a>Wat kost gebeurtenis raster?

Azure gebeurtenis raster maakt gebruik van een prijsmodel voor betalen per gebeurtenis, zodat u alleen betaalt voor wat u gebruikt.

Gebeurtenis raster kost $0,60 per miljoen operations ($0,30 tijdens de preview) en Hallo eerst 100.000 bewerking per maand zijn gratis. Bewerkingen worden gedefinieerd als gebeurtenis inkomend, geavanceerde overeen, levering poging en management aanroepen.  Meer informatie vindt u op Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Volgende stappen

* [Maken en zich abonneren toocustom gebeurtenissen](custom-event-quickstart.md) meteen en beginnen met het verzenden van uw eigen aangepaste gebeurtenissen tooany eindpunt met behulp van hello Azure gebeurtenis raster Quick Start.
* [Met Logic Apps als een gebeurtenis-Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) een zelfstudie over het bouwen van een app met Logic Apps tooreact tooevents gepusht door gebeurtenis raster.
* [Gebeurtenis raster REST API-referentiemateriaal](/rest/api/eventgrid)  
  Biedt meer technische informatie over hello Azure gebeurtenis raster en een verwijzing voor het beheer van abonnementen, doorsturen en filteren.
