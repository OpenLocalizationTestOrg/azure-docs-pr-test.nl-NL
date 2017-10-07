---
title: "aaaAzure Service Bus Premium en Standard Messaging prijscategorie overzicht van Prijscategorieën | Microsoft Docs"
description: "Prijscategorieën voor Service Bus Premium en Standard Messaging"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Prijscategorieën voor Service Bus Premium en Standard Messaging

Service Bus Messaging, dat entiteiten zoals wachtrijen en onderwerpen omvat, combineert functies voor bedrijfsberichten met krachtige semantiek voor publiceren/abonneren in de cloud. Service Bus-berichtenservice wordt gebruikt als Hallo communicatie-backbone voor veel geavanceerde cloudoplossingen.

Hallo *Premium* laag van de Service Bus-berichtenservice adressen algemene klantaanvragen met betrekking schaal, prestaties en beschikbaarheid van bedrijfskritieke toepassingen. Hoewel Hallo functiesets bijna identiek zijn, zijn deze twee lagen van de Service Bus-berichtenservice ontworpen tooserve verschillende gebruiksscenario.

Hallo volgende tabel worden enkele belangrijke verschillen gemarkeerd.

| Premium | Standard |
| --- | --- |
| Hoge doorvoersnelheid |Variabele doorvoersnelheid |
| Voorspelbare prestaties |Variabele latentie |
| Vaste prijzen |Variabel omslagstelsel voor betalen per gebruik |
| Mogelijkheid tooscale workload omhoog en omlaag |N.v.t. |
| Grootte van het bericht too1 MB |De berichtgrootte van too256 KB |

**Service Bus Premium Messaging** biedt isolatie van resources op niveau van de CPU en geheugen hello, zodat elke workload van een klant geïsoleerd wordt uitgevoerd. Deze resourcecontainer wordt een *Messaging-eenheid* genoemd. Aan elke Premium-naamruimte wordt ten minste één Messaging-eenheid toegewezen. U kunt voor elke Service Bus Premium-naamruimte 1, 2 of 4 Messaging-eenheden aanschaffen. Een enkele workload of entiteit kan meerdere messaging-eenheden omspannen en Hallo aantal messaging-eenheden kan naar wens, worden gewijzigd, hoewel facturering tegen een 24-uurs of dagelijks tarief plaatsvindt. Hallo-resultaat is voorspelbare en herhaalbare prestaties voor uw oplossing op basis van een Service Bus.

Niet alleen zijn de prestaties beter voorspelbaar en beschikbaar, ze zijn ook sneller.  Service Bus Premium Messaging bouwt voort op Hallo opslag-engine is geïntroduceerd in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/). Premium Messaging is piekprestaties veel sneller dan met Hallo Standard-laag.

## <a name="premium-messaging-technical-differences"></a>Technische verschillen Premium Messaging

Hallo volgende secties worden enkele verschillen tussen Premium en Standard Messaging.

### <a name="partitioned-queues-and-topics"></a>Gepartitioneerde wachtrijen en onderwerpen

Gepartitioneerde wachtrijen en onderwerpen worden ondersteund in Premium Messaging. Deze entiteiten worden altijd gepartitioneerd (en kunnen niet worden uitgeschakeld). Echter, Premium gepartitioneerd wachtrijen en onderwerpen Hallo niet werken als in op dezelfde manier Hallo Standard- en Basic-lagen van de Service Bus-berichtenservice. Premium messaging wordt niet gebruikt SQL als gegevensarchief en niet langer heeft Hallo mogelijke concurrentie die zijn gekoppeld aan een gedeeld platform. Partitioneren is daardoor niet nodig tooimprove prestaties. Bovendien is Hallo partitie aantal gewijzigd van 16 partities in standaardberichten too2 partities in Premium. Met twee partities garandeert beschikbaarheid en een meer geschikt is voor Hallo Premium runtime-omgeving. 

Premium Messaging, wanneer u de grootte van een entiteit met Hallo opgeeft [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), dat formaat is verdelen gelijkmatig over Hallo 2 partities, in tegenstelling tot [standaard gepartitioneerde entiteiten](service-bus-partitioning.md#standard) in welke Hallo totale grootte is 16 keren Hallo opgegeven grootte. 

Zie [Gepartitioneerde wachtrijen en onderwerpen](service-bus-partitioning.md) voor meer informatie over partitioneren.

### <a name="express-entities"></a>Express-entiteiten

Omdat Premium Messaging wordt uitgevoerd in een volledig geïsoleerde runtime-omgeving, worden Express-entiteiten niet ondersteund in Premium-naamruimten. Zie voor meer informatie over snelle functie Hallo Hallo [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) eigenschap.

Als u code die wordt uitgevoerd onder Standard messaging en gewenste tooport het toohello Premium-laag, moet u ervoor dat Hallo [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) eigenschap is ingesteld, te**false** (Hallo standaardwaarde).

## <a name="get-started-with-premium-messaging"></a>Aan de slag met Premium Messaging

Aan de slag met Premium Messaging is eenvoudig en Hallo-proces is vergelijkbaar toothat van standaardberichten. U begint met [een naamruimte te maken](service-bus-create-namespace-portal.md). Zorg ervoor dat bij **Prijscategorie** de optie **Premium** is geselecteerd.

![maken-premium-naamruimte][create-premium-namespace]

U kunt ook [Premium-naamruimtes maken met behulp van Azure Resource Manager-sjablonen](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over Service Bus-berichtenservice Zie Hallo volgende onderwerpen.

* [Introducing Azure Service Bus Premium messaging (blogbericht)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducing Azure Service Bus Premium messaging (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Overzicht van Service Bus Messaging](service-bus-messaging-overview.md)
* [Hoe toouse Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
