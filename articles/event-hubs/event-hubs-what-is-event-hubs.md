---
title: aaaWhat is Azure Event Hubs en waarom gebruiken | Microsoft Docs
description: Overzicht en inleiding tooAzure Event Hubs - Cloud-scale telemetrie opname van websites, apps en apparaten
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Wat is Event Hubs?

Azure Event Hubs is een uiterst schaalbaar platform voor het streamen van gegevens en een gebeurtenisopneemservice die miljoenen gebeurtenissen per seconde kan opnemen en verwerken. Event Hubs kan gebeurtenissen, gegevens of telemetrie die wordt geproduceerd door gedistribueerde software en apparaten verwerken en opslaan. Gegevens verzonden tooan event hub kan worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters. Met de Hallo mogelijkheid tooprovide [mogelijkheden voor publiceren / abonneren](https://msdn.microsoft.com/library/aa560414.aspx) met een lage latentie en zeer grote hoeveelheden Event Hubs fungeert als Hallo 'aan' ramp' voor Big Data.

## <a name="why-use-event-hubs"></a>Het nut van Event Hubs

De verwerkingsmogelijkheden voor gebeurtenissen en telemetrie van Event Hubs zijn ideaal voor:

* Toepassingsinstrumentatie
* Verwerking van gebruikerservaringen of werkstromen
* Internet of Things (IoT)-scenario’s

Event Hubs maakt bijvoorbeeld het bijhouden van het gebruik van mobiele apps mogelijk, evenals het verzamelen van informatie over gegevensverkeer van web-farms, het vastleggen van spelgebeurtenissen in consolegames en het verzamelen van telemetriegegevens van industriële machines, verbonden voertuigen of andere apparaten.

## <a name="azure-event-hubs-overview"></a>Overzicht van Azure Event Hubs

Hallo algemene rol die Event Hubs in oplossingsarchitecturen speelt is Hallo 'voordeur' van een gebeurtenispijplijn vaak aangeduid als een *event ingestor*. Een event ingestor is een onderdeel of service die gebeurtenisuitgevers en gebeurtenis consumenten toodecouple Hallo productie van een stroom gebeurtenissen van Hallo gebruik van deze gebeurtenissen tussen. Hallo ziet volgende figuur deze architectuur:

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Event Hubs biedt de mogelijkheid voor het verwerken van een berichtenstroom, maar sommige van de kenmerken wijken af van wat u gewend bent bij traditionele zakelijke tools voor berichtenverzending. De mogelijkheden van Event Hubs zijn gebaseerd op maximale doorvoer en scenario's voor de verwerking van gebeurtenissen. Als zodanig Event Hubs wijkt af van [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging en wordt niet geïmplementeerd voor een aantal Hallo-mogelijkheden die beschikbaar zijn voor [Service Bus-berichtenservice](/azure/service-bus-messaging/) entiteiten, zoals de onderwerpen.

## <a name="event-hubs-features"></a>Functies van Event Hubs

Event Hubs Hallo volgen de belangrijkste elementen bevat:

- [**Gebeurtenisuitgevers producenten**](event-hubs-features.md#event-publishers): een entiteit die gegevens tooan event hub verzendt. Een gebeurtenis wordt gepubliceerd via AMQP 1.0 of HTTPS.
- [**Vastleggen**](event-hubs-features.md#capture): Hiermee kunt u toocapture Event Hubs gegevensstromen en op te slaan in een Azure Blob storage-account.
- [**Partities**](event-hubs-features.md#partitions): Hiermee elke consumer tooonly lezen voor een specifieke subset of partitie van Hallo stroom gebeurtenissen.
- [**SAS-tokens**](event-hubs-features.md#sas-tokens): identificeert en Hallo gebeurtenisuitgever verifieert.
- [**Gebeurtenisconsumenten**](event-hubs-features.md#event-consumers): een entiteit die gebeurtenisgegevens van een gebeurtenishub leest. Gebeurtenisconsumenten maken verbinding via AMQP 1.0. 
- [**Consumergroepen**](event-hubs-features.md#consumer-groups): biedt elk veelvoud toepassing met een afzonderlijke weergave van de gebeurtenisstroom Hallo verbruikt, die consumenten tooact afzonderlijk inschakelen.
- [**Doorvoereenheden**](event-hubs-features.md#capacity): vooraf aangeschafte capaciteitseenheden. Per partitie is maximaal één doorvoereenheid mogelijk.

Zie voor technische informatie over deze en andere functies van Event Hubs Hallo [overzicht van Event Hubs functies](event-hubs-features.md). 

## <a name="next-steps"></a>Volgende stappen

Zie [Prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) voor gedetailleerde informatie over prijzen van Event Hubs.

Voor meer informatie over Event Hubs, gaat u naar Hallo koppelingen volgen:

* Aan de slag met een [Event Hubs-zelfstudie](event-hubs-dotnet-standard-getstarted-send.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)
* [Voorbeeldtoepassingen die gebruikmaken van Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

