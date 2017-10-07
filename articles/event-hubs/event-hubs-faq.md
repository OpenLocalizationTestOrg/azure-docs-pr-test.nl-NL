---
title: Veelgestelde vragen over Event-Hubs aaaAzure | Microsoft Docs
description: Azure Event Hubs Veelgestelde vragen (FAQ)
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Veelgestelde vragen over Event Hubs

## <a name="general"></a>Algemeen

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Wat is Hallo verschil tussen Event Hubs Basic en Standard lagen?

Hallo Standard-laag van Azure Event Hubs biedt functies dan beschikbaar in de basisstaffel Hallo is. Hallo volgende functies zijn opgenomen in de standaard:
* Langere bewaartermijn van gebeurtenis
* Extra brokered verbindingen met een overschrijding kosten meer dan Hallo dat is opgenomen
* Meer dan één groep Consumer
* [Vastleggen](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Zie voor meer informatie over prijzen voor lagen, waaronder Event Hubs is toegewezen, Hallo [Event Hubs prijsinformatie](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>Wat zijn de doorvoereenheden Event Hubs?

U selecteren expliciet doorvoereenheden Event Hubs, hetzij via hello Azure-portal of Event Hubs Resource Manager-sjablonen. Doorvoereenheden toepassen tooall event hubs in een Event Hubs-naamruimte en elke doorvoereenheid kunt Hallo naamruimte toohello volgende mogelijkheden:

* Too1 MB per seconde van ingangsgebeurtenissen (gebeurtenissen verzonden naar een event hub), maar niet meer dan 1000 ingangsgebeurtenissen, beheerbewerkingen of besturingselement API-aanroepen per seconde.
* Too2 MB per seconde van uitgaande gebeurtenissen (gebeurtenissen van een event hub gebruikt).
* Up too84 GB gebeurtenis opslag (volstaat voor Hallo 24-uurs bewaartermijn).

Event Hubs doorvoereenheden per uur worden gefactureerd, op basis van het maximum aantal eenheden dat is geselecteerd tijdens de opgegeven uur Hallo Hallo.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Hoe kan ik Event Hubs eenheid doorvoerlimieten afgedwongen?
Hallo totaal inkomend doorvoer of Hallo totaal inkomend snelheid van gebeurtenissen over alle event hubs in een naamruimte Hallo geaggregeerde doorvoer eenheid rechten overschrijdt, afzenders zijn beperkt als er fouten optreden die aangeeft dat inkomende hello quotum is overschreden.

Hallo totaal aantal uitgaande doorvoer of Hallo totale uitgaande tarief over alle event hubs in een naamruimte Hallo geaggregeerde doorvoer eenheid rechten overschrijdt, ontvangers zijn beperkt als er fouten optreden die aangeeft dat Hallo uitgaande quotum is overschreden. Inkomende en uitgaande quota worden afzonderlijk afgedwongen, zodat geen afzender leiden de gebeurtenis verbruik tooslow omlaag tot kan, noch kan een ontvanger te voorkomen dat gebeurtenissen in een event hub worden verzonden.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>Is er een limiet van het aantal doorvoereenheden die kunnen worden geselecteerd Hallo?
Er is een standaardquotum van 20 doorvoereenheden per naamruimte. U kunt een grotere quotum van doorvoereenheden aanvragen door het indienen van een ondersteuningsticket. Hallo 20 doorvoer eenheid limiet overschrijdt zijn bundels beschikbaar in 20-100 doorvoereenheden. Houd er rekening mee dat meer dan 20 doorvoereenheden Hallo mogelijkheid toochange Hallo aantal doorvoereenheden verwijdert zonder een ondersteuningsticket indienen.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>Zijn er gebruik van een enkele AMQP verbinding toosend en ontvangen van meerdere event hubs?
Ja, zolang alle Hallo event hubs in Hallo zijn dezelfde naamruimte.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>Wat is de maximale bewaarperiode Hallo voor gebeurtenissen?
Event Hubs standaardcategorie ondersteunt momenteel een maximale bewaarperiode van 7 dagen. Houd er rekening mee event hubs zijn niet bedoeld als een permanente gegevensarchief. Bewaarperiode groter is dan 24 uur zijn bedoeld voor scenario's waarin het handige tooreplay een gebeurtenis in stream is Hallo dezelfde systemen; bijvoorbeeld, tootrain of Controleer of u een nieuwe machine learning-model op bestaande gegevens. Als u bewaren dan 7 dagen-bericht moet, waardoor [Event Hubs vastleggen](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) op uw event hub Hallo gegevens ophaalt uit uw event hub toohello Storage-account of een Azure Data Lake-Service-account van uw keuze. Een kosten op basis van uw aangeschafte doorvoereenheid leidt ertoe dat vastleggen inschakelen.

### <a name="where-is-azure-event-hubs-available"></a>Waar Azure Event Hubs beschikbaar is?
Azure Event Hubs is beschikbaar in alle ondersteunde Azure-regio's. Voor een lijst, gaat u naar Hallo [Azure-regio's](https://azure.microsoft.com/regions/) pagina.  

## <a name="best-practices"></a>Aanbevolen procedures

### <a name="how-many-partitions-do-i-need"></a>Het aantal partities moet ik gebruiken?
Houd er rekening mee dat het aantal partities voor een event hub Hallo worden niet moet gewijzigd na de installatie. Daarom is het belangrijk toothink over hoeveel partities die u nodig hebt voordat u aan de slag. 

Event Hubs is ontworpen tooallow een lezer één partitie per consumergroep. Gebruik in de meeste gevallen Hallo standaardinstelling van vier partities is voldoende. Als u op zoek bent tooscale verwerking van gebeurtenissen, kunt u tooconsider extra partities toe te voegen. Er is geen limiet specifieke doorvoer op een andere partitie, maar Hallo geaggregeerde doorvoer in uw naamruimte wordt beperkt door het aantal doorvoereenheden Hallo. Als u het aantal doorvoereenheden Hallo in uw naamruimte verhoogt, kunt u extra partities tooallow gelijktijdige lezers tooachieve hun eigen maximale doorvoer.

Echter als er een model waarin uw toepassing een bepaalde partitie van affiniteit tooa heeft, waardoor het aantal partities Hallo mogelijk niet van een voordeel tooyou. Zie voor meer informatie over deze [beschikbaarheid en consistentie](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Prijzen

### <a name="where-can-i-find-more-pricing-information"></a>Waar vind ik meer informatie over de prijzen
Zie voor meer informatie over prijzen van Event Hubs Hallo [Event Hubs prijsinformatie](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>Is er kosten met zich mee voor het bewaren van gebeurtenissen van Event Hubs voor meer dan 24 uur?
Hallo Event Hubs standaardcategorie staat toe dat bericht bewaren perioden van meer dan 24 uur, maximaal 7 dagen. Als Hallo Hallo kunt u het totale aantal opgeslagen gebeurtenissen Hallo opslag toegestane voor het aantal geselecteerde doorvoereenheden (84 GB per doorvoereenheid) hello groot, Hallo-grootte die langer is dan de toegestane Hallo wordt in rekening gebracht op Hallo gepubliceerd Azure Blob storage-snelheid. Hallo opslag toegestane in elke doorvoereenheid bevat alle kosten voor opslag voor de bewaarperiode van 24 uur (standaardinstelling Hallo) zelfs als toohello maximale inkomende toegestane doorvoereenheid Hallo is gebruikt.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Hoe Hallo Event Hubs opslaggrootte berekend en in rekening gebracht?
totale grootte van alle opgeslagen gebeurtenissen, met inbegrip van een interne overhead voor gebeurtenissen, kopteksten of op schijf opslag structuren in alle event hubs Hallo wordt gedurende de dag hello gemeten. Hallo na dag Hallo wordt Hallo opslag piekgrootte berekend. Hallo dagelijkse opslag vergoeding wordt berekend op basis van Hallo minimum aantal doorvoereenheden die zijn geselecteerd tijdens Hallo dag (elke doorvoereenheid biedt een correctie van 84 GB). Als de totale grootte Hallo overschrijdt Hallo berekend dagelijks opslag toegestane, Hallo overtollige opslag wordt gefactureerd met behulp van Azure Blob storage tarieven (op Hallo **lokaal redundante opslag** snelheid).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Hoe kan ik Event Hubs ingangsgebeurtenissen berekend?
Elke gebeurtenis verzonden tooan event hub, telt als een factureerbare bericht. Een *inkomend gebeurtenis* is gedefinieerd als een gegevenseenheid die kleiner is dan of gelijk too64 KB. De gebeurtenis die kleiner is dan of gelijk too64 KB groot wordt beschouwd als een factureerbare gebeurtenis toobe. Als Hallo gebeurtenis groter dan 64 KB is, wordt het aantal gebeurtenissen dat factureerbare Hallo berekend volgens de gebeurtenisgrootte toohello in veelvouden van 64 KB. Bijvoorbeeld, een 8 KB gebeurtenis verzonden toohello event hub wordt gefactureerd als een gebeurtenis, maar een 96 KB-bericht verzonden toohello event hub wordt gefactureerd als twee gebeurtenissen.

Gebeurtenissen van een event hub, alsmede beheerbewerkingen en besturingselement aanroepen zoals controlepunten worden niet meegeteld als factureerbare ingangsgebeurtenissen maar doorlopen up toohello doorvoer eenheid toegestane verbruikt.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Pas brokered verbinding kosten tooEvent Hubs?
Verbinding gelden alleen wanneer Hallo AMQP-protocol wordt gebruikt. Er zijn geen kosten verbinding voor het verzenden van gebeurtenissen met behulp van HTTP, ongeacht het Hallo-nummer van het verzenden van systemen of apparaten. Als u van plan toouse AMQP bent (bijvoorbeeld tooachieve efficiënter gebeurtenis streamen of tooenable bidirectionele communicatie in de opdracht en controle IoT-scenario's), Zie Hallo [Event Hubs prijsgegevens](https://azure.microsoft.com/pricing/details/event-hubs/) pagina voor meer informatie over het veel verbindingen zijn opgenomen in elke servicecategorie.

### <a name="how-is-event-hubs-capture-billed"></a>Hoe wordt Event Hubs Capture gefactureerd?
Vastleggen is ingeschakeld wanneer een gebeurtenis-hub in de naamruimte Hallo Hallo vastleggen optie ingeschakeld is. Vastleggen van Event Hubs wordt per uur gefactureerd per doorvoereenheid hebt aangeschaft. Als Hallo doorvoereenheid count wordt vergroot of verkleind, weerspiegelt Event Hubs vastleggen facturering deze wijzigingen in de hele intervallen van uren. Zie voor meer informatie over Event Hubs vastleggen facturering [Event Hubs prijsgegevens](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>Ik krijgt voor het opslagaccount Hallo die ik voor het vastleggen van Event Hubs selecteren?
Vastleggen maakt gebruik van een opslagaccount dat u opgeeft wanneer ingeschakeld voor een event hub. Als dit uw storage-account is, worden eventuele wijzigingen voor deze configuratie gefactureerd tooyour Azure-abonnement.

## <a name="quotas"></a>Quota

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Zijn er geen quota's die zijn gekoppeld aan de Event Hubs?
Zie voor een lijst van alle Event Hubs quota [quota](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>Wat zijn enkele Hallo uitzonderingen die worden gegenereerd door de Event Hubs en hun voorgestelde acties?
Zie voor een lijst van mogelijke Event Hubs uitzonderingen [uitzonderingen overzicht](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Diagnostische logboeken
Event Hubs ondersteunt twee typen [diagnostische logboeken](event-hubs-diagnostic-logs.md) -foutenlogboeken vastleggen en operationele logboeken - die beide worden weergegeven in json en kunnen worden ingeschakeld via hello Azure-portal.

### <a name="support-and-sla"></a>Ondersteuning en SLA
Technische ondersteuning voor Event Hubs is beschikbaar via Hallo [communityforums](https://social.msdn.microsoft.com/forums/azure/home). Ondersteuning bij facturering en abonnementsbeheer is gratis.

toolearn meer over onze SLA Zie Hallo [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/) pagina.

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
