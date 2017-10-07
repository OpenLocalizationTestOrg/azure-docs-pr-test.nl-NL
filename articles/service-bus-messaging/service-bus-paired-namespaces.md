---
title: Service Bus aaaAzure gekoppeld naamruimten | Microsoft Docs
description: Implementatiegegevens gekoppelde naamruimte en de kosten
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Implementatiegegevens naamruimte gekoppeld en de gevolgen kosten
Hallo [PairNamespaceAsync] [ PairNamespaceAsync] methode, met behulp van een [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] exemplaar, zichtbaar taken worden uitgevoerd namens jou. Omdat er worden kosten overwegingen wanneer u Hallo functie gebruikt, is het nuttig toounderstand die taken zodat u verwachten Hallo gedrag wanneer dit gebeurt. Hallo API stelt Hallo automatische gedrag namens jou te volgen:

* Het maken van achterstand wachtrijen.
* Het maken van een [MessageSender] [ MessageSender] -object dat wordt gesproken tooqueues of onderwerpen.
* Wanneer een Berichtentiteit niet beschikbaar is, verzendt ping-berichten toohello entiteit in een poging toodetect wanneer die entiteit weer beschikbaar.
* Eventueel maakt van een reeks 'bericht pompen' dat verplaatsen van berichten van Hallo achterstand wachtrijen toohello primaire wachtrijen.
* Coördineert sluiten/afgesloten Hallo primaire en secundaire [MessagingFactory] [ MessagingFactory] exemplaren.

Op een hoog niveau Hallo functie werkt als volgt: wanneer de primaire entiteit Hallo goed is, er geen gedragswijzigingen doorgevoerd. Wanneer Hallo [FailoverInterval] [ FailoverInterval] duur is verstreken, en de primaire entiteit Hallo ziet geen geslaagde verzendt na een tijdelijke [MessagingException] [ MessagingException] of een [TimeoutException][TimeoutException], Hallo gedrag na deze gebeurtenis treedt op:

1. Verzenden operations toohello primaire entiteit zijn uitgeschakeld en Hallo system pings Hallo primaire entiteit totdat pings kunnen worden bezorgd.
2. Een wachtrij willekeurige achterstand is geselecteerd.
3. [BrokeredMessage] [ BrokeredMessage] objecten zijn gerouteerde toohello achterstand wachtrij gekozen.
4. Als een verzenden bewerking toohello gekozen achterstand wachtrij is mislukt, die wachtrij opgehaald uit Hallo draaien en een nieuwe wachtrij is geselecteerd. Alle afzenders op Hallo [MessagingFactory] [ MessagingFactory] exemplaar van de fout Hallo meer.

Hallo cijfers na weer Hallo volgorde. Eerst verzendt Hallo afzender berichten.

![Gekoppelde naamruimten][0]

Bij fout toosend toohello primaire wachtrij begint Hallo afzender verzenden van berichten tooa willekeurig gekozen achterstand wachtrij. Tegelijk, wordt er een ping-taak gestart.

![Gekoppelde naamruimten][1]

Op dit moment Hallo-berichten zijn nog steeds in de secundaire wachtrij Hallo en niet de primaire wachtrij toohello zijn geleverd. Zodra Hallo primaire wachtrij weer in orde is, moet ten minste één proces Hallo syphon worden uitgevoerd. Hallo syphon biedt Hallo-berichten van alle Hallo verschillende achterstand wachtrijen toohello juiste bestemming entiteiten (wachtrijen en onderwerpen).

![Gekoppelde naamruimten][2]

Hallo rest van dit onderwerp wordt beschreven Hallo specifieke details over de werking van deze onderdelen.

## <a name="creation-of-backlog-queues"></a>Maken van wachtrijen achterstand
Hallo [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] object dat wordt doorgegeven toohello [PairNamespaceAsync] [ PairNamespaceAsync] methode geeft aan Hallo achterstand aantal wachtrijen dat u wilt dat toouse. Elke wachtrij achterstand wordt vervolgens gemaakt met de Hallo volgende eigenschappen expliciet ingesteld (alle andere waarden zijn ingesteld toohello [QueueDescription] [ QueueDescription] standaardwaarden):

| Pad | [primaire namespace] / x-servicebus-overdracht / [index] waarbij [index] is een waarde in [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| maxDeliveryCount |int zijn. MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue op |
| AutoDeleteOnIdle |TimeSpan.MaxValue op |
| LockDuration |1 minuut |
| EnableDeadLetteringOnMessageExpiration |De waarde True |
| EnableBatchedOperations |De waarde True |

Bijvoorbeeld Hallo eerste achterstand wachtrij gemaakt voor naamruimte **contoso** heet `contoso/x-servicebus-transfer/0`.

Bij het maken van wachtrijen Hallo Hallo code toosee eerst gecontroleerd als deze wachtrij bestaat. Hallo-wachtrij wordt gemaakt als Hallo wachtrij niet bestaat. Hallo-code niet opschonen 'extra' achterstand wachtrijen. Specifiek moet als hello toepassing met primaire naamruimte Hallo **contoso** aanvragen vijf achterstand wachtrijen, maar een achterstand wachtrij met Hallo pad `contoso/x-servicebus-transfer/7` bestaat, die extra achterstand wachtrij nog steeds aanwezig is, maar wordt niet gebruikt. Hallo-systeem kunt expliciet extra achterstand wachtrijen tooexist die niet worden gebruikt. Als de eigenaar van de naamruimte hello bent u verantwoordelijk voor het opschonen van ongebruikte/ongewenste achterstand wachtrijen. Hallo-reden voor deze beslissing is dat Service Bus kan niet weet welke doelen voor alle Hallo wachtrijen in uw naamruimte bestaat. Bovendien, als een wachtrij met de Hallo gegeven naam bestaat, maar voldoet niet aan de Hallo uitgegaan [QueueDescription][QueueDescription], en vervolgens uw redenen uw eigen voor veranderende Hallo standaardgedrag zijn. Er zijn geen garanties worden gemaakt voor wijzigingen toohello achterstand wachtrijen door uw code. Zorg ervoor dat tootest uw wijzigingen grondig.

## <a name="custom-messagesender"></a>Aangepaste MessageSender
Wanneer u verzendt, gaat u alle berichten via een interne [MessageSender] [ MessageSender] -object dat normaal gedraagt zich als alles werkt en toohello achterstand wachtrijen wordt omgeleid wanneer dingen 'verbreekt." Bij ontvangst van een tijdelijke fout, wordt een timer gestart. Na een [TimeSpan] [ TimeSpan] periode die bestaan uit Hallo [FailoverInterval] [ FailoverInterval] eigenschapswaarde waarover geen geslaagde berichten worden verzonden , Hallo failover is ingeschakeld. Op dit moment plaats hello volgende voor elke entiteit:

* Een ping-taak wordt uitgevoerd elke [PingPrimaryInterval] [ PingPrimaryInterval] toocheck als Hallo entiteit beschikbaar is. Wanneer deze taak is voltooid, wordt alle clientcode die gebruikmaakt van Hallo entiteit onmiddellijk gestart nieuwe berichten toohello primaire naamruimte verzenden.
* Toekomstige aanvragen toosend toothat dezelfde entiteit van een andere afzenders leidt ertoe dat Hallo [BrokeredMessage] [ BrokeredMessage] toosit in Hallo achterstand wachtrij toobe verstuurd worden gewijzigd. Hallo wijziging enkele eigenschappen verwijdert uit Hallo [BrokeredMessage] [ BrokeredMessage] object en slaat ze op elders. Hallo zijn volgende eigenschappen uitgeschakeld en onder een nieuwe alias, zodat Service Bus en Hallo SDK tooprocess berichten gelijkmatig toegevoegd:

| Oude naam van eigenschap | Nieuwe naam van eigenschap |
| --- | --- |
| sessie-id |x-ms-sessie-id |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-pad |

oorspronkelijke doelpad Hello wordt ook opgeslagen in het Hallo-bericht als een eigenschap met de naam x-ms-path. Dit ontwerp kunt berichten voor veel toocoexist voor entiteiten in een wachtrij één achterstand. Hallo-eigenschappen worden vertaald door Hallo syphon terug.

Hallo aangepaste [MessageSender] [ MessageSender] object problemen kan optreden wanneer berichten benadering Hallo 256 KB limiet en failover is ingeschakeld. Hallo aangepaste [MessageSender] [ MessageSender] object berichten voor alle wachtrijen en onderwerpen samen in Hallo achterstand wachtrijen worden opgeslagen. Dit object combineert berichten van veel primaire samen binnen Hallo achterstand wachtrijen. toohandle taakverdeling tussen veel clients die niet weet elk andere, Hallo SDK willekeurig wat neemt over van een achterstand wachtrij voor elk [QueueClient] [ QueueClient] of [TopicClient] [ TopicClient] u in code maken.

## <a name="pings"></a>Pings
Een ping-bericht is een lege [BrokeredMessage] [ BrokeredMessage] met de [ContentType] [ ContentType] eigenschap ingesteld tooapplication/vnd.ms-servicebus-ping en een [TimeToLive] [ TimeToLive] waarde van 1 seconde. Deze ping is een speciaal kenmerk in de Service Bus: Hallo-server biedt nooit een ping wanneer elk aanroepend aanvraagt een [BrokeredMessage][BrokeredMessage]. Dus u nooit hebt toolearn hoe tooreceive en deze berichten te negeren. Elke entiteit (unieke wachtrij of onderwerp) per [MessagingFactory] [ MessagingFactory] exemplaar per client zal worden gepingd wanneer deze worden beschouwd als toobe niet beschikbaar. Standaard is dit gebeurt eenmaal per minuut. Ping-berichten worden beschouwd als gewone Service Bus-berichten toobe en kunnen leiden tot kosten van bandbreedte en berichten. Zodra het Hallo-clients detecteren dat Hallo system beschikbaar is, stopt Hallo-berichten.

## <a name="hello-syphon"></a>Hallo syphon
Ten minste één uitvoerbaar programma in de toepassing hello moet actief zijn Hallo syphon. Hallo syphon voert een long poll ontvangen die 15 minuten duurt. Wanneer alle entiteiten beschikbaar zijn en hebt u 10 achterstand wachtrijen, Hallo toepassing die als host fungeert voor Hallo syphon aanroepen Hallo ontvangstbewerking 40 keer per uur, 960 keer per dag en 28800 keer in 30 dagen. Bij het Hallo syphon is actief met het verplaatsen van berichten uit Hallo achterstand toohello primaire wachtrij, krijgt elk bericht Hallo kosten (standaard kosten voor de grootte van het bericht en de bandbreedte van toepassing in alle fasen) te volgen:

1. Achterstand toohello verzenden.
2. Ontvangen van Hallo achterstand.
3. Toohello primaire verzenden.
4. Ontvangen van de primaire Hallo.

## <a name="closefault-behavior"></a>Sluit/fout gedrag
In een toepassing die als host fungeert voor Hallo syphon, eenmaal Hallo primaire of secundaire [MessagingFactory] [ MessagingFactory] bedrijfsstoringen of wordt afgesloten zonder de partner die ook wordt een fout opgetreden/gesloten en Hallo syphon deze status wordt gedetecteerd , Hallo syphon fungeert. Als andere Hallo [MessagingFactory] [ MessagingFactory] is niet afgesloten binnen 5 seconden Hallo syphon Hallo nog steeds openen wordt fault [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Volgende stappen
Zie [asynchrone messaging-patronen en hoge beschikbaarheid] [ Asynchronous messaging patterns and high availability] voor een gedetailleerde bespreking van de asynchrone Service Bus-berichtenservice. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
