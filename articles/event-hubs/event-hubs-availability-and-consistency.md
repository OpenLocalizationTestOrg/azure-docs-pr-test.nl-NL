---
title: aaaAvailability en consistentie in Azure Event Hubs | Microsoft Docs
description: Hoe tooprovide Hallo maximale hoeveelheid beschikbaarheid en consistentie met behulp van Azure Event Hubs partities.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Beschikbaarheid en consistentie in Event Hubs

## <a name="overview"></a>Overzicht
Maakt gebruik van Azure Event Hubs een [partitioneren model](event-hubs-features.md#partitions) tooimprove beschikbaarheid en garandeert binnen een enkele event hub. Bijvoorbeeld, als een event hub vier partities heeft en een van deze partities van één server tooanother in een bewerking voor de taakverdeling wordt verplaatst, kunt u nog steeds verzenden en ontvangen van de drie andere partities. Bovendien meer partities, kunt u toohave meer gelijktijdige lezers verwerken van uw gegevens, de geaggregeerde doorvoer te verbeteren. Inzicht in Hallo gevolgen van het partitioneren en rangschikken in een gedistribueerde systeem is een kritieke aspect van het ontwerp van de oplossing.

toohelp Hallo compromis tussen ordening en beschikbaarheid uitgelegd, Zie Hallo [CAP stelling van](https://en.wikipedia.org/wiki/CAP_theorem), ook wel van Brewer stelling van. Deze stelling van komen aan bod Hallo keuze tussen de consistentie, beschikbaarheid en tolerantie van de partitie.

De Brewer stelling van consistentie en beschikbaarheid wordt als volgt gedefinieerd:
* Partitie-tolerantie: Hallo mogelijkheid van een gegevensverwerking system toocontinue verwerken van gegevens, zelfs als er een partitie-fout optreedt.
* Beschikbaarheid: een knooppunt niet mislukken retourneert een redelijke antwoord binnen een redelijk tijdsbestek (met geen fouten of time-outs).
* Consistentiecontrole: Lees is gegarandeerd tooreturn Hallo meest recente schrijven voor een bepaalde client.

## <a name="partition-tolerance"></a>Partitie tolerantie
Event Hubs is gebaseerd op een gepartitioneerde gegevensmodel. U kunt het aantal partities Hallo configureren in uw event hub tijdens de installatie, maar u kunt deze waarde later wijzigen. Omdat u partities met Event Hubs gebruiken moet, hebt u toomake een beslissing over de beschikbaarheid en consistentie voor uw toepassing.

## <a name="availability"></a>Beschikbaarheid
Hallo eenvoudigste manier tooget de slag met Event Hubs is toouse Hallo standaardgedrag. Als u een nieuwe maakt `EventHubClient` object ingesteld en Hallo `Send` methode, uw gebeurtenissen worden automatisch verdeeld tussen de partities in de event hub. Dit gedrag kunt Hallo grootste hoeveelheid tijd.

Dit model is voor gebruiksvoorbeelden waarvoor Hallo maximale tijd voorkeur.

## <a name="consistency"></a>Consistentie
In sommige gevallen kan Hallo ordening van gebeurtenissen belangrijk zijn. U kunt bijvoorbeeld uw back-end-systeem tooprocess een bijwerkopdracht voordat een verwijderopdracht. In dat geval kunt u kunt Hallo partitiesleutel ingesteld op een gebeurtenis of gebruik een `PartitionSender` object tooonly verzenden gebeurtenissen tooa bepaalde partitie. Hiermee zorgt u ervoor dat wanneer deze gebeurtenissen worden gelezen uit het Hallo-partitie, worden gelezen in volgorde.

Houd er rekening mee dat als Hallo bepaalde partitie toowhich die u verzendt niet beschikbaar is, u een foutmelding ontvangt met deze configuratie. Als u een affiniteit tooa één partitie, hoeft geen verzendt Hallo Event Hubs-service als een punt voor vergelijking, uw gebeurtenis toohello volgende beschikbare partitie.

Een mogelijke oplossing tooensure ordening tegelijkertijd ook tijd, zou tooaggregate gebeurtenissen zijn als onderdeel van uw toepassing voor gebeurtenisverwerking. Hallo gemakkelijkste manier tooaccomplish dit toostamp wordt de gebeurtenis met een eigenschap aangepaste sequence number. Hallo volgende code toont een voorbeeld:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

In dit voorbeeld verzendt uw tooone gebeurtenis van de beschikbare partities Hallo in uw event hub en bijbehorende volgnummer Hallo ingesteld van uw toepassing. Deze oplossing vereist status toobe door uw toepassing verwerking bewaard, maar uw afzenders biedt een eindpunt dat waarschijnlijker toobe beschikbaar is.

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Overzicht van Event Hubs-service](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
