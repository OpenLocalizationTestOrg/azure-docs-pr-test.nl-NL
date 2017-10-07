---
title: aaaService Bus asynchrone messaging | Microsoft Docs
description: Beschrijving van de asynchrone Azure Service Bus-berichtenservice.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Asynchrone berichtpatronen en hoge beschikbaarheid

Asynchrone berichten kan worden geïmplementeerd in een aantal verschillende manieren. Met wachtrijen, onderwerpen en abonnementen ondersteunt Azure Service Bus asynchronism via een winkel en voorwaarts mechanisme. Verzenden van berichten tooqueues en onderwerpen in de normale werking (synchrone) en berichten ontvangen van wachtrijen en abonnementen. Toepassingen die u schrijft, is afhankelijk van deze entiteiten worden altijd beschikbaar. Wanneer Hallo entiteitsstatus gewijzigd vanwege tooa verschillende omstandigheden, moet u een manier tooprovide een verminderde functionaliteit entiteit die voldoen aan de meeste behoeften.

Toepassingen gebruiken doorgaans asynchrone messaging patronen tooenable een aantal scenario's voor communicatie. U kunt bouwen toepassingen waarin clients berichten tooservices, verzenden kunnen zelfs wanneer het Hallo-service wordt niet uitgevoerd. Voor toepassingen die zich bursts van communicatie voordoen, kunt een wachtrij niveau Hallo laden door een plaats toobuffer communicatie. Ten slotte kunt u een eenvoudige maar effectieve load balancer toodistribute berichten over meerdere machines.

In volgorde toomaintain beschikbaarheid van elk van deze entiteiten, kunt u een aantal verschillende manieren waarop deze entiteiten niet beschikbaar voor een duurzame berichtensysteem kunnen voorkomen. We zien over het algemeen Hallo entiteit is niet beschikbaar tooapplications die we schrijven in Hallo volgende verschillende manieren worden:

* Kan geen toosend berichten.
* Kan geen tooreceive berichten.
* Kan geen toomanage entiteiten (maken, ophalen, bijwerken of verwijderen van entiteiten).
* Kan geen toocontact Hallo-service.

Voor elk van deze oorzaken bestaan fout verschillende modi waarmee een toepassing toocontinue tooperform werkt op een bepaald niveau verminderde functionaliteit. Bijvoorbeeld, een systeem waarmee u kunt berichten verzenden, maar deze niet ontvangen kunt nog steeds orders van klanten ontvangen maar die orders kan niet worden verwerkt. In dit onderwerp worden de mogelijke problemen die kunnen optreden en hoe deze problemen worden verholpen. Service Bus is een aantal oplossingen die u moet kiezen voor geïntroduceerd en in dit onderwerp worden ook Hallo regels Hallo voor het gebruik van deze oplossingen aanmelden.

## <a name="reliability-in-service-bus"></a>Betrouwbaarheid in Servicebus
Er zijn verschillende manieren toohandle bericht en de entiteit problemen en er zijn richtlijnen voor Hallo juiste gebruik van deze oplossingen. richtlijnen voor toounderstand hello, eerst moet u begrijpen wat in de Service Bus kan mislukken. Vervaldatum toohello ontwerp van Azure systemen al deze problemen toobe tijdelijke vaak. Op een hoog niveau uitzien Hallo andere oorzaken van niet beschikbaar zijn als volgt:

* Beperking van een extern systeem waarvan Service Bus afhankelijk is. Beperking optreedt van de interacties met opslagruimte en rekencapaciteit resources.
* Probleem voor een systeem waarop de Service Bus afhankelijk is. Een bepaald gedeelte van de opslag kan bijvoorbeeld problemen optreden.
* Fout van Service Bus op één subsysteem. In dit geval een rekenknooppunt kunt krijgen tot een inconsistente status heeft en moet opnieuw worden opgestart, waardoor alle entiteiten fungeert tooload saldo tooother knooppunten. Dit kan een korte periode van trage berichtverwerking op zijn beurt veroorzaken.
* Fout van Service Bus in een Azure-datacenter. Dit is een 'Onherstelbare fout' waarover Hallo system onbereikbaar voor het aantal minuten of enkele uren is.

> [!NOTE]
> Hallo term **opslag** kan betekenen zowel Azure Storage en Azure SQL.
> 
> 

Service Bus bevat een aantal oplossingen voor deze problemen. Hallo volgende secties worden besproken elk probleem en hun respectieve oplossingen beschreven.

### <a name="throttling"></a>Beperking
Met Service Bus kunt beperking gezamenlijke bericht snelheid management. Elke afzonderlijke Service Bus-knooppunten ook nieuwste veel entiteiten. Elk van deze entiteiten maakt eisen op Hallo systeem in termen van CPU, geheugen, opslag en andere facetten. Wanneer een van deze facetten gebruik detecteert die gedefinieerde drempelwaarden overschrijdt, Service Bus een bepaalde aanvraag kunt weigeren. Hallo aanroeper ontvangt een [ServerBusyException] [ ServerBusyException] en pogingen na 10 seconden.

Als een risicobeperking moet Hallo code Hallo leesfout en alle nieuwe pogingen van het Hallo-bericht is gestopt voor ten minste 10 seconden. Aangezien Hallo fout tussen onderdelen van de klant-toepassing hello optreden kan, verwacht wordt dat elk Hallo Pogingslogica onafhankelijk worden uitgevoerd. Hallo-code kunt Hallo waarschijnlijkheid wordt beperkt door in te schakelen op een wachtrij of onderwerp partitioneren verminderen.

### <a name="issue-for-an-azure-dependency"></a>Probleem met een Azure-afhankelijkheid
Andere onderdelen in Azure kunnen van tijd tot tijd hebben problemen met de service. Wanneer een besturingssysteem dat gebruikmaakt van Service Bus wordt bijgewerkt, kan dat systeem tijdelijk zich bijvoorbeeld minder mogelijkheden. toowork rond dit soort problemen, Service Bus regelmatig onderzoekt en oplossingen implementeert. Neveneffecten van deze oplossingen worden weergegeven. Bijvoorbeeld toohandle tijdelijke problemen met opslag, Service Bus een systeem waarmee bericht verzenden operations toowork consistent worden geïmplementeerd. Vervaldatum toohello aard van Hallo risicobeperking, een verzonden bericht too15 minuten tooappear in Hallo van invloed op een wachtrij of -abonnement nemen en klaar voor een ontvangstbewerking. Normaal gesproken de meeste entiteiten wordt dit probleem zich niet. Echter, gezien Hallo aantal entiteiten in de Service Bus in Azure, deze beperking is soms nodig voor een kleine subset van Service Bus-klanten.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Service Bus-fout op een enkele subsysteem
Met elke toepassing, omstandigheden kunnen leiden tot een interne onderdeel van Service Bus toobecome inconsistent. Wanneer Service Bus gedetecteerd, worden gegevens verzameld van Hallo toepassing tooaid bij het oplossen van wat is er gebeurd. Zodra het Hallo-gegevens worden verzameld, Hallo-toepassing wordt opnieuw gestart in een poging tooreturn het tooa consistente status. Dit proces wordt uitgevoerd vrij snel en resulteert in een entiteit wordt niet beschikbaar voor up tooa toobe enkele minuten weergegeven hoewel typische uitvaltijden veel korter zijn.

In dergelijke gevallen Hallo clienttoepassing genereert een [System.TimeoutException] [ System.TimeoutException] of [MessagingException] [ MessagingException] uitzondering. Service Bus bevat een beperking voor dit probleem in de vorm Hallo van geautomatiseerde client Pogingslogica. Zodra de tijd tussen elke poging Hallo is verbruikt en het Hallo-bericht is niet bezorgd, u kunt verkennen met andere functies, zoals [naamruimten gekoppeld][paired namespaces]. Gekoppelde naamruimten hebben andere waarschuwingen die worden beschreven in dit artikel.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Fout van Service Bus in een Azure-datacenter
de meest waarschijnlijke reden Hallo wegens een fout in een Azure-datacenter is een mislukte upgrade-implementatie van Service Bus- of een afhankelijke systeem. Zoals Hallo platform is gekomen, is de kans op Hallo van dit type fout verminderd. Een datacenter-fout kan ook gebeuren om redenen die Hallo volgende opnemen:

* Elektrische storing (voeding en genereren power verdwijnen).
* De verbinding (internet pauze tussen uw clients en Azure).

In beide gevallen veroorzaakt een noodgeval natuurlijke of kunstmatige Hallo probleem. toowork dit en zorg ervoor dat u kunt nog steeds berichten verzenden, kunt u [naamruimten gekoppeld] [ paired namespaces] tooenable berichten toobe verzonden tooa tweede locatie terwijl primaire locatie Hallo opnieuw in orde wordt gemaakt. Zie voor meer informatie [aanbevolen procedures voor de isolatie van toepassingen tegen storingen van de Service Bus en noodsituaties][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Gekoppelde naamruimten
Hallo [naamruimten gekoppeld] [ paired namespaces] functie ondersteunt scenario's waarin een Service Bus-entiteit of implementatie binnen een datacenter niet meer beschikbaar is. Terwijl deze gebeurtenis treedt op zelden, moeten gedistribueerde systemen nog worden voorbereid toohandle slechtste gebruiksscenario's. Normaal gesproken treedt deze gebeurtenis op omdat sommige element waarvan Service Bus afhankelijk is, is een korte termijn probleem opgetreden. beschikbaarheid van toomaintain tijdens een storing Service Bus gebruikers kunnen gebruiken twee afzonderlijke naamruimten, bij voorkeur in afzonderlijke datacenters, toohost messaging-entiteiten. Hallo rest van dit gedeelte maakt gebruik van Hallo volgende terminologie:

* Primaire naamruimte: Hallo naamruimte waarmee uw toepassing, voor verzend communiceert- en ontvangstbewerkingen.
* Secundaire naamruimte: Hallo naamruimte die als een primaire back-toohello-naamruimte fungeert. Toepassingslogica communiceert niet met deze naamruimte.
* Failover-interval: Hallo hoeveelheid tijd tooaccept normale fouten voordat de toepassing hello verandert van Hallo primaire toohello secundaire naamruimte.

Ondersteuning voor naamruimten gekoppeld *verzenden beschikbaarheid*. Beschikbaarheid van bewaart Hallo mogelijkheid toosend berichten verzenden beschikbaarheid van toouse verzenden, uw toepassing moet voldoen aan Hallo volgens de vereisten:

1. Berichten worden alleen ontvangen van primaire Hallo-naamruimte.
2. Verzonden berichten tooa gegeven wachtrij of onderwerp mogelijk een verkeerde volgorde binnenkomen.
3. Berichten in een sessie mogelijk een verkeerde volgorde binnenkomen. Dit is een onderbreking van de normale functionaliteit van sessies. Dit betekent dat uw toepassing gebruikmaakt van berichten van sessies toologically groeperen.
4. Sessiestatus wordt alleen op primaire Hallo-naamruimte bijgehouden.
5. Hallo primaire wachtrij kunt online komen en berichten worden geaccepteerd voordat de secundaire wachtrij Hallo biedt alle berichten in de primaire wachtrij Hallo starten.

Hallo uit te voeren bespreken Hallo API's, hoe Hallo API's worden geïmplementeerd en bevat voorbeeldcode die gebruikmaakt van Hallo-functie. Houd er rekening mee dat er facturering gevolgen die zijn gekoppeld aan deze functie zijn.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Hallo MessagingFactory.PairNamespaceAsync API
Hallo gekoppelde naamruimten functie bevat Hallo [PairNamespaceAsync] [ PairNamespaceAsync] methode op Hallo [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] klasse:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Hallo-taak is voltooid, Hallo naamruimte koppelen is ook als voltooid en gereed tooact bij voor alle [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], of [TopicClient] [ TopicClient] gemaakt met de Hallo [MessagingFactory] [ MessagingFactory] exemplaar. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] is basisklasse voor Hallo Hallo verschillende soorten koppelen die beschikbaar met zijn een [MessagingFactory] [ MessagingFactory] object. Hallo alleen afgeleide klasse is momenteel een met de naam [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], die Hallo verzenden beschikbaarheidsvereisten implementeert. [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] een constructors die zijn gebaseerd op elkaar heeft. Bekijkt hello constructor Hello meeste parameters, kunt u begrijpen Hallo gedrag van Hallo andere constructors.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Deze parameters hebben Hallo betekenis te volgen:

* *secondaryNamespaceManager*: een geïnitialiseerd [NamespaceManager] [ NamespaceManager] exemplaar voor de secundaire naamruimte Hallo die Hallo [PairNamespaceAsync] [ PairNamespaceAsync] methode tooset om secundaire naamruimte Hallo kunt gebruiken. Hallo naamruimte manager is gebruikte tooobtain Hallo lijst van wachtrijen in Hallo-naamruimte en toomake Hallo vereist achterstand wachtrijen zijn gedefinieerd. Als deze wachtrijen niet bestaan, worden ze gemaakt. [NamespaceManager] [ NamespaceManager] Hallo mogelijkheid toocreate een token met Hallo vereist **beheren** claim.
* *messagingFactory*: Hallo [MessagingFactory] [ MessagingFactory] exemplaar voor secundaire Hallo-naamruimte. Hallo [MessagingFactory] [ MessagingFactory] -object is gebruikte toosend en, indien hello [EnableSyphon] [ EnableSyphon] eigenschap is ingesteld, te**true** , Hallo achterstand wachtrijen berichten ontvangen.
* *backlogQueueCount*: aantal achterstand Hallo toocreate wachtrijen. Deze waarde moet ten minste 1 zijn. Bij het verzenden van berichten toohello achterstand, wordt een van deze wachtrijen willekeurig gekozen. Als u Hallo waarde too1 instelt, kunt wordt slechts één wachtrij ooit gebruikt. Wanneer dit gebeurt en Hallo een achterstand wachtrij fouten genereert, wordt Hallo-client is niet kunnen tootry een wachtrij verschillende achterstand en toosend uw bericht kan mislukken. Het is raadzaam om deze waarde toosome grotere waarde en standaard Hallo waarde too10 instellen. Kunt u deze tooa hogere of lagere waarde afhankelijk van hoeveel gegevens door uw toepassing verzendt per dag. Elke wachtrij achterstand kan up too5 GB aan berichten bevatten.
* *failoverInterval*: Hallo en de hoeveelheid tijd gedurende welke u fouten op de primaire naamruimte hello accepteren wilt voordat u overschakelt van een enkele entiteit via toohello secundaire naamruimte. Failovers optreden op basis van de entiteit met entiteit. Entiteiten in een enkele naamruimte bevinden vaak zich in verschillende knooppunten binnen een Service Bus. Een fout in één entiteit betekent niet dat een storing in een andere. U kunt deze waarde instellen te[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello secundaire onmiddellijk na de eerste, tijdelijke fout. Fouten die Hallo failover timer activeren zijn [MessagingException] [ MessagingException] in welke Hallo [IsTransient] [ IsTransient] eigenschap false is, of een [System.TimeoutException][System.TimeoutException]. Andere uitzonderingen, zoals [UnauthorizedAccessException] [ UnauthorizedAccessException] zorgen niet voor failover, omdat ze aangeeft die Hallo-client is onjuist geconfigureerd. Een [ServerBusyException] [ ServerBusyException] komt niet oorzaak failover omdat de juiste patroon Hallo toowait 10 seconden verzend het Hallo-bericht daarna opnieuw.
* *enableSyphon*: geeft aan dat dit bepaalde combinatie moet ook syphon berichten van Hallo secundaire back toohello primaire naamruimte. In het algemeen toepassingen die berichten verzenden moeten Stel deze waarde te**false**; toepassingen die berichten ontvangen moeten deze waarde te ingesteld**true**. Hallo reden hiervoor is vaak het geval is, zijn er minder bericht ontvangers dan afzenders van berichten. Afhankelijk van Hallo aantal ontvangers, kunt u toohave een enkele toepassing exemplaar ingang Hallo syphon rechten. Met behulp van veel ontvangers heeft facturering gevolgen voor elke wachtrij achterstand.

toouse Hallo code, maakt u een primaire [MessagingFactory] [ MessagingFactory] exemplaar, een secundaire [MessagingFactory] [ MessagingFactory] exemplaar, een secundair [NamespaceManager] [ NamespaceManager] exemplaar, en een [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] exemplaar. Hallo-aanroep kan net zo eenvoudig als Hallo volgende zijn:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Wanneer Hallo taak geretourneerd door Hallo [PairNamespaceAsync] [ PairNamespaceAsync] methode is voltooid, alles is ingesteld en klaar toouse. Voordat het Hallo-taak wordt geretourneerd, mogelijk niet voltooid al Hallo achtergrondwerk nodig zijn voor Hallo toowork rechts koppelen. Als gevolg hiervan moet u niet eerst verzenden van berichten, totdat de taak Hallo retourneert. Als er fouten opgetreden, zoals ongeldige referenties of fout toocreate Hallo achterstand wachtrijen, wordt deze uitzonderingen worden gegenereerd zodra Hallo-taak is voltooid. Nadat Hallo taak retourneert, controleren of Hallo wachtrijen zijn gevonden of is gemaakt door in Hallo [BacklogQueueCount] [ BacklogQueueCount] -eigenschap op uw [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] exemplaar. Voor Hallo voorafgaand aan code, die voor deze bewerking wordt als volgt weergegeven:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Volgende stappen
Nu dat u Hallo basisbeginselen van asynchrone in Service Bus-berichtenservice hebt geleerd, leest u meer informatie over [naamruimten gekoppeld][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
