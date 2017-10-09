---
title: aaaAuto doorsturen Azure Service Bus-berichtentiteiten | Microsoft Docs
description: Hoe een Service Bus toochain wachtrij of abonnement tooanother wachtrij of onderwerp.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Service Bus-entiteiten met automatisch doorsturen Chaining

Hallo Service Bus *automatisch doorsturen* functie kunt u een wachtrij toochain of abonnement tooanother wachtrij of onderwerp dat deel uitmaakt van Hallo dezelfde naamruimte. Wanneer automatisch doorsturen is ingeschakeld, wordt Service Bus automatisch verwijdert van berichten die worden geplaatst in de eerste wachtrij Hallo of -abonnement (bron) en plaatst deze in de tweede Hallo-wachtrij of onderwerp (doel). Houd er rekening mee dat het nog steeds mogelijk toosend bericht toohello doelentiteit rechtstreeks is. Het is ook niet mogelijk toochain een subwachtrij, zoals een wachtrij voor onbestelbare berichten, tooanother wachtrij of onderwerp.

## <a name="using-auto-forwarding"></a>Automatisch doorsturen gebruiken
U kunt automatisch doorsturen inschakelen door de instelling Hallo [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] of [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] eigenschappen op Hallo [QueueDescription] [ QueueDescription] of [SubscriptionDescription] [ SubscriptionDescription] objecten voor Hallo-bron, zoals in Hallo volgende voorbeeld.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

Hallo doelentiteit moet bestaan op Hallo moment Hallo bronentiteit wordt gemaakt. Hallo doelentiteit bestaat niet, dan Service Bus een uitzondering geretourneerd wanneer gestelde toocreate Hallo bronentiteit.

U kunt automatisch doorsturen tooscale uit een onderwerp. Service Bus-limieten Hallo [aantal abonnementen op een bepaald onderwerp](service-bus-quotas.md) too2, 000. Door het tweede niveau onderwerpen maken, kunt u gebruikmaken van aanvullende abonnementen. Opmerking zelfs als u niet afhankelijk is van Hallo Hallo Service Bus-beperking van het aantal abonnementen, het toevoegen van een tweede verificatieniveau onderwerpen Hallo kunt verbeteren totale doorvoer van uw onderwerp.

![Automatisch doorsturen scenario][0]

U kunt ook automatisch doorsturen toodecouple afzenders van berichten van ontvangers. Neem bijvoorbeeld een ERP-systeem dat uit drie modules bestaat: volgorde verwerking, voorraadbeheer en customer relationship management. Elk van deze modules worden berichten die in de wachtrij in een bijbehorende onderwerp zijn gegenereerd. Els en Bob zijn vertegenwoordigers die geïnteresseerd zijn in alle berichten die betrekking tootheir klanten hebben. tooreceive die berichten, Alice en Bob maken een persoonlijke wachtrij en een abonnement op elk Hallo ERP-onderwerpen die alle berichten tootheir wachtrij automatisch doorsturen.

![Automatisch doorsturen scenario][1]

Als Els op vakantie, haar persoonlijke wachtrij, in plaats van Hallo ERP onderwerp gaat, wordt opgevuld. In dit scenario, omdat een verkoopmedewerker niet alle berichten ontvangen bereiken geen Hallo ERP onderwerpen ooit quotum.

## <a name="auto-forwarding-considerations"></a>Automatisch doorsturen overwegingen

Als Hallo doelentiteit stelt samen te veel berichten en Hallo quotum wordt overschreden, of Hallo doelentiteit is uitgeschakeld, Hallo bronentiteit voegt Hallo-berichten tooits [wachtrij voor onbestelbare berichten](service-bus-dead-letter-queues.md) tot er ruimte in het Hallo-doel is (of Hallo entiteit opnieuw is ingeschakeld). Deze berichten blijven in de wachtrij voor onbestelbare berichten Hallo toolive zodat u moet expliciet ontvangen en van de wachtrij voor onbestelbare berichten Hallo verwerken.

Het verdient de voorkeur dat u een beperkt aantal abonnementen op Hallo eerste niveau onderwerp en veel abonnementen op Hallo tweede niveau onderwerpen hebt voor het koppelen van afzonderlijke onderwerpen tooobtain een samengestelde onderwerp met veel abonnementen. Bijvoorbeeld een eerste niveau onderwerp met 20 abonnementen, elk van deze teruggekoppeld tooa tweede niveau onderwerp met 200 abonnementen toestaat voor een hogere doorvoer dan een onderwerp van het eerste niveau met 200 abonnementen elk teruggekoppeld tooa tweede niveau onderwerp met 20 abonnementen .

Service Bus stuklijsten één bewerking voor elk bericht. Bijvoorbeeld, verzendt een bericht tooa onderwerp met 20 abonnementen, elk van deze tooauto doorsturen berichten tooanother wachtrij of onderwerp, wordt in rekening gebracht als 21 bewerkingen als alle abonnementen van het eerste niveau ontvangt een kopie van het Hallo-bericht geconfigureerd.

een abonnement dat is keten tooanother wachtrij of onderwerp toocreate, Hallo maker van Hallo abonnement moet hebben **beheren** machtigingen op het Hallo-bron- en Hallo doelentiteit. Verzenden van berichten toohello bron onderwerp vereist alleen **verzenden** machtigingen op Hallo bron onderwerp.

## <a name="next-steps"></a>Volgende stappen

Zie voor gedetailleerde informatie over het automatisch doorsturen Hallo naslagonderwerpen voor het volgende:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn meer informatie over Service Bus-prestatieverbeteringen, Zie 

* [Aanbevolen procedures voor verbeterde prestaties met behulp van Service Bus-berichtenservice](service-bus-performance-improvements.md)
* [Gepartitioneerde berichtentiteiten][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
