---
title: aaaAzure Service Bus-berichten architectuuroverzicht | Microsoft Docs
description: Hierin wordt beschreven Hallo-bericht architectuur voor het verwerken van Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Service Bus-architectuur
Dit artikel wordt beschreven Hallo-bericht architectuur voor het verwerken van Azure Service Bus.

## <a name="service-bus-scale-units"></a>Service Bus-schaaleenheden
Service Bus is georganiseerd op *schaaleenheden*. Een schaaleenheid is een implementatie-eenheid en bevat alle onderdelen vereist uitvoeren Hallo-service. Elke regio implementeert een of meer Service Bus-schaaleenheden.

Een Service Bus-naamruimte is toegewezen tooa schaaleenheid. Hallo schaaleenheid verwerkt alle typen Service Bus-entiteiten (wachtrijen, onderwerpen, abonnementen). Een Service Bus-schaaleenheid bestaat uit Hallo volgende onderdelen:

* **Een set gateway-knooppunten.** Gateway-knooppunten verifiëren inkomende aanvragen. Elk gateway-knooppunt heeft een openbaar IP-adres.
* **Een set berichtbrokerknooppunten.** Berichtbrokerknooppunten verwerken aanvragen over berichtentiteiten.
* **Een gateway-store.** Hallo gateway-store bevat Hallo-gegevens voor elke entiteit die is gedefinieerd in deze schaaleenheid. Hallo gateway-store is bovenop een SQL Azure database geïmplementeerd.
* **Meerdere berichten-stores.** Berichten-stores bevatten Hallo-berichten van alle wachtrijen, onderwerpen en abonnementen die zijn gedefinieerd in deze schaaleenheid. Het bevat ook alle abonnementsgegevens. Tenzij [berichtentiteiten partitioneren](service-bus-partitioning.md) is ingeschakeld, een wachtrij of onderwerp toegewezen tooone berichten-store is. Abonnementen worden opgeslagen in Hallo dezelfde berichten-store als het bovenliggende onderwerp. Met uitzondering van Service Bus [Premium Messaging](service-bus-premium-messaging.md), Hallo-berichten-stores bovenop SQL Azure-databases zijn geïmplementeerd.

## <a name="containers"></a>Containers
Aan elke berichtentiteit is een specifieke container toegewezen. Een container is een logische constructie die gebruikmaakt van precies één messaging store toostore alle relevante gegevens voor deze container. Elke container is tooa messaging-knooppunt toegewezen. Er zijn meestal meer containers dan berichtbrokerknooppunten. Elk berichtbrokerknooppunt laadt daarom meerdere containers. Hallo-distributie van containers tooa berichtbrokerknooppunt is zodanig georganiseerd dat alle berichtbrokerknooppunten evenwichtig worden belast. Als Hallo Hallo load patroon wijzigingen (bijvoorbeeld een Hallo containers opgehaald bezet) of als een tijdelijk niet beschikbaar is berichtbrokerknooppunt, wordt containers herverdeeld over Hallo berichtbrokerknooppunten.

## <a name="processing-of-incoming-messaging-requests"></a>Verwerken van inkomende berichtaanvragen
Wanneer een client een aanvraag tooService Bus verzendt, doorgestuurd hello Azure load balancer tooany van Hallo gateway-knooppunten. Hallo gateway-knooppunt machtigt Hallo-aanvraag. Als Hallo aanvraag betrekking heeft op een Berichtentiteit (wachtrij, onderwerp, abonnement), wordt Hallo gateway-knooppunt zoekt Hallo entiteit in Hallo gateway-store en bepaalt in welke messaging store Hallo entiteit zich bevindt. Vervolgens controleert het knooppunt welk berichtbrokerknooppunt deze container wordt momenteel wordt uitgevoerd en stuurt Hallo aanvraag toothat messaging-knooppunt. Hallo messaging broker knooppunt Hallo-aanvraag wordt verwerkt en Hallo entiteitsstatus bij in de container-store Hallo-updates. Hallo messaging broker knooppunt vervolgens verzendt Hallo antwoord back toohello gateway-knooppunt, waarmee een juiste reactie back toohello client die oorspronkelijke uitgegeven Hallo-aanvraag wordt verzonden.

![Verwerken van inkomende berichtaanvragen](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Volgende stappen
Nu dat u een overzicht van Service Bus-architectuur hebt gelezen, gaat u naar Hallo volgende koppelingen voor meer informatie:

* [Overzicht van Service Bus-berichten](service-bus-messaging-overview.md)
* [Grondbeginselen van Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Een oplossing voor berichten in de wachtrij met behulp van Service Bus-wachtrijen](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


