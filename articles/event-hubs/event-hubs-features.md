---
title: Event Hubs aaaAzure functies overzicht | Microsoft Docs
description: Overzicht en meer informatie over de functies van Azure Event Hubs
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Overzicht van Event Hubs-functies

Azure Event Hubs is een schaalbare verwerkingsservice die opgenomen en grote hoeveelheden gebeurtenissen en de gegevens, verwerkt met een lage latentie en hoge betrouwbaarheid. Zie [wat is er Event Hubs?](event-hubs-what-is-event-hubs.md) voor een overzicht van Hallo-service.

In dit artikel is gebaseerd op Hallo-informatie in Hallo [overzicht](event-hubs-what-is-event-hubs.md), en biedt technische en implementatie-informatie over Event Hubs-onderdelen en functies.

## <a name="event-publishers"></a>Gebeurtenisuitgevers

Elke entiteit die verzendt gegevens tooan event hub is een producent gebeurtenis of *gebeurtenisuitgever*. Gebeurtenisuitgevers kunnen gebeurtenissen publiceren met HTTPS of AMQP 1.0. Gebeurtenisuitgevers kunnen gebruiken een Shared Access Signature (SAS)-token tooidentify zelf tooan event hub, en een unieke identiteit hebben, of een algemene SAS-token.

### <a name="publishing-an-event"></a>Een gebeurtenis publiceren

U kunt een gebeurtenis publiceren met AMQP 1.0 of HTTPS. Event Hubs biedt [clientbibliotheken en klassen](event-hubs-dotnet-framework-api-overview.md) voor het publiceren van gebeurtenissen tooan event hub vanaf .NET-clients. Voor andere runtimes en platforms kunt u een AMQP 1.0-client gebruiken, zoals [Apache Qpid](http://qpid.apache.org/). U kunt gebeurtenissen afzonderlijk of batchgewijs publiceren. Eén publicatie (exemplaar met gebeurtenisgegevens) heeft een limiet van 256 kB, ongeacht of het om één gebeurtenis of om een batch gaat. Het publiceren van gebeurtenissen die groter is dan deze drempelwaarde resultaten in een fout. Het is een best practice voor uitgevers toobe niet bewust zijn van de partities binnen Hallo event hub en tooonly geeft een *partitiesleutel* (geïntroduceerd in de volgende sectie Hallo), of hun identiteit via de SAS-token.

Hallo keuze toouse AMQP of HTTPS is specifiek toohello gebruiksscenario. AMQP vereist Hallo tot stand brengen van een permanente bidirectionele socket in toevoeging tootransport level security (TLS) of SSL/TLS. AMQP heeft hogere netwerkkosten bij het initialiseren van Hallo-sessie, maar HTTPS extra SSL-overhead voor elke aanvraag vereist. AMQP biedt betere prestaties voor regelmatige uitgevers.

![Event Hubs](./media/event-hubs-features/partition_keys.png)

Event Hubs zorgt ervoor dat alle gebeurtenissen met een waarde voor de partitiesleutel worden afgeleverd in de volgorde en toohello dezelfde partitie. Als er partitiesleutels met uitgeversbeleid worden gebruikt, vervolgens Hallo identiteit van de uitgever Hallo en waarde van de partitiesleutel Hallo Hallo moet overeenkomen. Als deze niet overeenkomen, treedt er een fout op.

### <a name="publisher-policy"></a>Uitgeversbeleid

In Event Hubs kunt u gebeurtenisuitgevers nauwkeurig beheren met behulp van *uitgeversbeleid*. Uitgeversbeleid zijn Runtime-functies die zijn ontworpen toofacilitate grote aantallen onafhankelijke gebeurtenisuitgevers. Uitgeversbeleid implementeert gebruikt elke uitgever zijn eigen unieke id bij het publiceren van gebeurtenissen tooan event hub met Hallo mechanisme te volgen:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

U hoeft niet de namen van uitgevers toocreate tevoren, maar moeten deze Hallo SAS-token gebruikt bij het publiceren van een gebeurtenis, in volgorde tooensure onafhankelijke uitgeversidentiteiten overeenkomen. Als u uitgeversbeleid, Hallo **PartitionKey** waarde toohello de naam van uitgever is ingesteld. toowork juist deze waarden moeten overeenkomen.

## <a name="capture"></a>Capture

[Event Hubs vastleggen](event-hubs-capture-overview.md) kunt u tooautomatically vastleggen Hallo gegevensstromen in Event Hubs en sla het tooyour keuze van een Blob storage-account of een Azure Data Lake-Service-account. U kunt vastleggen inschakelen via hello Azure-portal en geef een minimale grootte en de tijd venster tooperform Hallo vastleggen. Met Event Hubs vastleggen u uw eigen Azure Blob Storage-account en -container opgeven of Azure Data Lake-Service-account, gebruikte toostore Hallo gegevens vastgelegd. Gegevensopname is geschreven in Hallo Apache Avro-indeling.

## <a name="partitions"></a>Partities

Event Hubs biedt berichtstromen via een gepartitioneerd gebruikspatroon waarbij elke consumer alleen een specifieke subset of partitie van de berichtenstroom Hallo leest. Dit patroon maakt een horizontale schaal voor de verwerking van gebeurtenissen mogelijk en biedt andere stroomgerichte functies die niet beschikbaar zijn in wachtrijen en onderwerpen.

Een partitie is een geordende reeks gebeurtenissen die in een Event Hub wordt bewaard. Als er nieuwere gebeurtenissen plaatsvinden, worden ze toegevoegd toohello einde van deze reeks. Een partitie kan worden beschouwd als een 'doorvoerlogboek'.

![Event Hubs](./media/event-hubs-features/partition.png)

Event Hubs behoudt gegevens voor een geconfigureerde bewaartijd die geldt voor alle partities in Hallo event hub. Gebeurtenissen verlopen op basis van tijd. U kunt ze niet expliciet verwijderen. Omdat partities onafhankelijk zijn en hun eigen reeks gegevens bevatten, groeien ze vaak met verschillende snelheden.

![Event Hubs](./media/event-hubs-features/multiple_partitions.png)

Hallo aantal partities wordt opgegeven bij het maken en moet tussen 2 en 32 liggen. Hallo partitie aantal is niet gewijzigd, zodat u op lange termijn scale overwegen bij het instellen van aantal partities. Partities zijn een mechanisme dat betrekking toohello downstreamparallelheid die is vereist heeft in de betrokken toepassingen. Hallo aantal partities in een event hub rechtstreeks is gekoppeld toohello nummer van gelijktijdige lezers u toohave verwacht. Contact opnemen met de Hallo Event Hubs team kunt u het aantal partities groter dan 32 Hallo verhogen.

Hoewel partities te herkennen en toodirectly kunnen worden verzonden, wordt verzendt rechtstreeks tooa partitie niet aanbevolen. In plaats daarvan kunt u hogere niveau constructies die zijn geïntroduceerd in Hallo [gebeurtenisuitgever](#event-publishers) en [capaciteit](#capacity) secties. 

Partities worden gevuld met een reeks gebeurtenisgegevens die Hallo hoofdtekst van Hallo gebeurtenis, een gebruiker gedefinieerde eigenschappenverzameling en metagegevens zoals de offset in Hallo partitie en het nummer in de stroomreeks Hallo bevat.

Zie voor meer informatie over partities en Hallo compromis tussen de beschikbaarheid en betrouwbaarheid Hallo [Programmeerhandleiding voor Event Hubs](event-hubs-programming-guide.md#partition-key) en Hallo [beschikbaarheid en consistentie in Event Hubs](event-hubs-availability-and-consistency.md) artikel .

### <a name="partition-key"></a>Partitiesleutel

U kunt een [partitiesleutel](event-hubs-programming-guide.md#partition-key) toomap inkomende gebeurtenisgegevens naar specifieke partities voor Hallo doel van de organisatie van de gegevens. Hallo partitiesleutel is een afzender opgegeven waarde in een event hub doorgegeven. Deze wordt verwerkt door een statische hash-functie die het Hallo-partitietoewijzing maakt. Als u bij het publiceren van een gebeurtenis geen partitiesleutel opgeeft, wordt er gebruikgemaakt van round robin-toewijzing.

Hallo gebeurtenisuitgever alleen op de hoogte van de partitiesleutel is Hallo partitie toowhich Hallo gebeurtenissen niet worden gepubliceerd. Deze ontkoppeling van sleutel en partitie schermt Hallo afzender van tooknow te komen over de downstreamverwerking Hallo hoeven. Een per apparaat of gebruiker unieke identiteit maakt een goede partitiesleutel, maar andere kenmerken, zoals Geografie kunnen ook worden gebruikt toogroup gerelateerde gebeurtenissen in een enkele partitie.

## <a name="sas-tokens"></a>SAS-tokens

Event Hubs maakt gebruikt *Shared Access Signatures*, die beschikbaar zijn op het niveau van Hallo naamruimte en event hub. Een SAS-token wordt gegenereerd uit een SAS-sleutel en is een SHA-hash of URL. gecodeerd in een specifieke indeling. Hallo-naam van Hallo-sleutel (beleid) en Hallo token gebruikt, Event Hubs Hallo hash opnieuw genereren en zich dus Hallo afzender verifiëren. Normaal gesproken worden SAS-tokens voor gebeurtenisuitgevers alleen gemaakt met bevoegdheden voor **verzenden** voor een specifieke Event Hub. Dit token URL-mechanisme met SAS is Hallo basis voor de uitgeversidentificatie die is geïntroduceerd in Hallo uitgeversbeleid. Zie [Shared Access Signature-verificatie met Service Bus](../service-bus-messaging/service-bus-sas.md) voor meer informatie over werken met SAS.

## <a name="event-consumers"></a>Gebeurtenisconsumers

Elke entiteit die gebeurtenisgegevens van een Event Hub leest, is een *gebeurtenisconsumer*. Alle Event Hubs-consumers maken verbinding via Hallo AMQP 1.0-sessie en gebeurtenissen worden geleverd via Hallo sessie zodra deze beschikbaar komen. Hallo-client heeft geen toopoll nodig voor beschikbaarheid van gegevens.

### <a name="consumer-groups"></a>Consumergroepen

Hallo mechanisme voor publiceren/abonneren van Event Hubs wordt ingeschakeld via de *consumergroepen*. Een consumergroep is een weergave (status, positie of offset) van een volledige Event Hub. Consumergroepen kunnen meerdere consumerende toepassingen tooeach hebben een afzonderlijke weergave van de gebeurtenisstroom Hallo en tooread Hallo stroom onafhankelijk in hun eigen tempo en met hun eigen worden verschoven.

In een stream verwerken architectuur, is elke downstream-toepassing gelijk tooa consumergroep. Als u toowrite gebeurtenis toolong term gegevensopslag wilt, is schrijftoepassing die een consumergroep. De complexe verwerking van gebeurtenissen kan vervolgens worden uitgevoerd door een andere, afzonderlijke consumergroep. U hebt alleen toegang tot partities via een consumergroep. Er mag maximaal 5 gelijktijdige lezers op een andere partitie per consumergroep; echter **het wordt aanbevolen dat op een andere partitie per consumergroep slechts één actieve ontvanger is**. Er is altijd een consumergroep standaard in een event hub en u kunt maken van too20 consumer-groepen voor een Standard-laag event hub.

Hallo-dit zijn voorbeelden van URI-conventie voor Hallo consumer groep:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Hallo toont volgende afbeelding Hallo Event Hubs stroom verwerkingsarchitectuur:

![Event Hubs](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Stroom-offsets

Een *offset* Hallo-positie van een gebeurtenis binnen een partitie is. U kunt een offset beschouwen als een clientcursor. Hallo offset is een bytenummering van Hallo-gebeurtenis. Deze offset kunt een gebeurtenis consumer (lezer) toospecify een punt in de gebeurtenisstroom Hallo waaruit ze toobegin lezen van gebeurtenissen wilt. U kunt Hallo offset opgeven als een tijdstempel of als een offsetwaarde. Consumers zijn zelf verantwoordelijk voor het opslaan van hun eigen offsetwaarden buiten Hallo Event Hubs-service. Binnen een partitie bevat elke gebeurtenis een offset.

![Event Hubs](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Controlepunten plaatsen

*Het plaatsen van controlepunten* is een proces waarbij lezers hun positie binnen de gebeurtenisvolgorde van een partitie markeren of vastleggen. Plaatsen van controlepunten is de verantwoordelijkheid Hallo van Hallo consumer en vindt plaats op basis van per partitie binnen een consumergroep. Deze verantwoordelijkheid betekent dat voor elke consumergroep de lezer van elke partitie moet bijhouden van de huidige positie in de gebeurtenisstroom Hallo en Hallo-service informeren kan wanneer het Hallo-gegevensstroom voltooid acht.

Als een lezer van een partitie verbroken wanneer dat verbinding wordt gemaakt begint het lezen bij Hallo controlepunt dat eerder is verzonden door Hallo laatste lezer van de betreffende partitie in de consumergroep. Hallo lezer verbinding maakt, wordt deze offset toohello event hub toospecify Hallo locatie op welke lezen toostart doorgegeven. Op deze manier kunt u gebeurtenissen voor het plaatsen van controlepunten tooboth markeren als 'voltooid' door downstream-toepassingen en tooprovide tolerantie als een failover tussen lezers die worden uitgevoerd op verschillende computers vindt plaats. Het is mogelijk tooreturn tooolder gegevens door te geven van een lagere offset uit dit proces voor het plaatsen van controlepunten. Via dit mechanisme zorgt het plaatsen van controlepunten voor failover-tolerantie en voor herhaling van gebeurtenisstromen.

### <a name="common-consumer-tasks"></a>Algemene taken voor consumers

Alle Event Hubs-consumers maken verbinding via een AMQP 1.0-sessie, een statusbewust bidirectioneel communicatiekanaal. Elke partitie heeft een AMQP 1.0-sessie die Hallo vervoer van Partitiespecifieke gebeurtenissen vergemakkelijkt.

#### <a name="connect-tooa-partition"></a>Verbinding maken met tooa partitie

Wanneer verbinding toopartitions maakt, is het algemene practice toouse een lease-mechanisme toocoordinate lezer verbindingen toospecific partities. Op deze manier is het mogelijk voor elke partitie in een consumer groep toohave slechts één actieve lezer. Het plaatsen van controlepunten, leasing en beheren van lezers zijn vereenvoudigd met behulp van Hallo [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) klasse voor .NET-clients. Hallo Event Processor Host is een intelligente-agent.

#### <a name="read-events"></a>Gebeurtenissen lezen

Nadat een AMQP 1.0-sessie en de koppeling is geopend voor een specifieke partitie, worden gebeurtenissen toohello AMQP 1.0-client geleverd door Hallo Event Hubs-service. Dit leveringsmechanisme maakt hogere doorvoer en lagere latentie mogelijk dan pull-mechanismen zoals HTTP GET. Toohello client verzenden van gebeurtenissen, bevat elk gebeurtenisgegeven belangrijke metagegevens, zoals Hallo offset en het volgnummer getal dat de gebruikte toofacilitate plaatsen van controlepunten op Hallo Gebeurtenisvolgorde zijn.

Gebeurtenisgegevens:
* Offset
* Volgnummer
* Hoofdtekst
* Gebruikerseigenschappen
* Systeemeigenschappen

Het is uw verantwoordelijkheid toomanage Hallo offset.

## <a name="capacity"></a>Capaciteit

Event Hubs is een uiterst schaalbare parallelle architectuur en er zijn enkele belangrijke factoren tooconsider wanneer dimensioneert of de schaal.

### <a name="throughput-units"></a>Doorvoereenheden

Hallo doorvoercapaciteit van Event Hubs wordt bepaald door *doorvoereenheden*. Doorvoereenheden zijn vooraf aangeschafte capaciteitseenheden. Eén doorvoereenheid bevat Hallo capaciteit te volgen:

* Inkomende gegevens: Up too1 MB per seconde of 1000 gebeurtenissen per seconde (afhankelijk van wat het eerst wordt bereikt)
* Uitgaande gegevens: Up too2 MB per seconde

Afgezien van de capaciteit van de Hallo Hallo doorvoereenheden hebt aangeschaft, inkomende gegevens worden beperkt en een [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) wordt geretourneerd. Uitgaande levert geen quotumgerelateerde uitzonderingen, maar is nog steeds beperkt toohello capaciteit van Hallo doorvoereenheden hebt aangeschaft. Als u uitzonderingen of hoger uitgaande toosee worden verwacht, niet zeker toocheck hoeveel doorvoereenheden u hebt aangeschaft voor Hallo-naamruimte. U kunt beheren doorvoereenheden op Hallo **Scale** blade van Hallo naamruimten in Hallo [Azure-portal](https://portal.azure.com). U kunt ook beheren doorvoereenheden programmatisch met behulp van Hallo [Event Hubs-API's](event-hubs-api-overview.md).

Doorvoereenheden worden per uur in rekening gebracht en zijn vooraf aangeschaft. Nadat u doorvoereenheden hebt aangeschaft, worden deze voor minimaal één uur in rekening gebracht. Up too20 doorvoereenheden kunnen worden aangeschaft voor een Event Hubs-naamruimte en worden gedeeld door alle Event Hubs in Hallo-naamruimte.

Meer doorvoereenheden kunnen worden gekocht in blokken van 20 too100 doorvoer eenheden, contact opnemen met de ondersteuning van Azure. Daarna kunt u ook blokken van 100 doorvoereenheden aanschaffen.

Het is raadzaam dat u een balans vinden doorvoer eenheden en partities tooachieve optimale schaal tussen. Per partitie is maximaal één doorvoereenheid mogelijk. Hallo aantal doorvoereenheden moet kleiner dan of gelijk toohello aantal partities in een event hub.

Zie voor gedetailleerde prijsinformatie Event Hubs [prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Volgende stappen

Voor meer informatie over Event Hubs, gaat u naar Hallo koppelingen volgen:

* Aan de slag met een [Event Hubs-zelfstudie][Event Hubs tutorial]
* [Programmeerhandleiding voor Event Hubs](event-hubs-programming-guide.md)
* [Beschikbaarheid en consistentie in Event Hubs](event-hubs-availability-and-consistency.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)
* [Voorbeelden van Event Hubs][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Voorbeelden van Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
