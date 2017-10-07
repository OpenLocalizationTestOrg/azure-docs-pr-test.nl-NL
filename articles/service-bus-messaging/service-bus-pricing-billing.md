---
title: aaaService Bus prijzen en facturering | Microsoft Docs
description: Overzicht van Service Bus structuur prijzen.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Service Bus-prijzen en facturering
Service Bus wordt aangeboden in Basic, Standard en [Premium](service-bus-premium-messaging.md) lagen. U kunt een servicelaag voor elke Service Bus-Servicenaamruimte die u maakt en deze selectie laag kan toepassen op alle entiteiten in die naamruimte gemaakt.

> [!NOTE]
> Zie voor gedetailleerde informatie over de huidige Service Bus-prijzen Hallo [pagina met prijzen van Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/), en Hallo [Veelgestelde vragen over de Service Bus](service-bus-faq.md#pricing).
>
>

Service Bus maakt gebruik van Hallo twee meters voor wachtrijen en onderwerpen/abonnementen te volgen:

1. **Messaging-bewerkingen**: gedefinieerd als de API-aanroepen op basis van de wachtrij of onderwerp/abonnement service-eindpunten. Deze meter wordt vervangen door berichten verzonden of ontvangen als primaire eenheid Hallo van factureerbare geheugengebruik voor wachtrijen en onderwerpen/abonnementen.
2. **Brokered verbindingen**: gedefinieerd als Hallo maximum aantal permanente verbindingen op basis van wachtrijen, onderwerpen en abonnementen tijdens een opgegeven testperiode van één uur openen. Deze meter is alleen van toepassing in de standaardcategorie hello, waarin u extra verbindingen kunt openen (verbindingen werden voorheen beperkt too100 per onderwerp-wachtrij-abonnement) voor de kosten van een nominaal per verbinding.

Hallo **standaard** laag introduceert geleidelijk prijzen voor bewerkingen die worden uitgevoerd met wachtrijen en onderwerpen/abonnementen, wat resulteert in kortingen op basis van het volume van een too80% op Hallo hoogste gebruik niveaus. Er is ook een Standard-laag base kosten van $10 per maand, waardoor u tooperform u too12.5 miljoen bewerkingen per maand zonder extra kosten.

Hallo **Premium** laag biedt isolatie van resources op Hallo CPU en geheugen laag, zodat elke workload van een klant geïsoleerd wordt uitgevoerd. Deze resourcecontainer wordt een *Messaging-eenheid* genoemd. Aan elke Premium-naamruimte wordt ten minste één Messaging-eenheid toegewezen. U kunt voor elke Service Bus Premium-naamruimte 1, 2 of 4 Messaging-eenheden aanschaffen. Een enkele workload of entiteit kan meerdere messaging-eenheden omspannen en Hallo aantal messaging-eenheden kan naar wens, worden gewijzigd, hoewel facturering tegen een 24-uurs of dagelijks tarief plaatsvindt. Hallo-resultaat is voorspelbare en herhaalbare prestaties voor uw oplossing op basis van een Service Bus. Niet alleen zijn de prestaties beter voorspelbaar en beschikbaar, ze zijn ook sneller. 

Houd er rekening mee dat Hallo standaardcategorie base kosten in rekening wordt gebracht slechts één keer per maand per Azure-abonnement. Dit betekent dat wanneer u een één standaard-laag Service Bus-naamruimte gemaakt, kunt u zich kunt toocreate zo veel extra Standard naamruimten gewenste onder die dezelfde Azure-abonnement, zonder extra kosten baseren.

Hallo [Service Bus prijzen](https://azure.microsoft.com/pricing/details/service-bus/) tabel ziet u een functionele verschillen tussen de lagen Basic, Standard en Premium Hallo Hallo.

## <a name="messaging-operations"></a>Berichtbewerkingen
Als onderdeel van de nieuwe prijzen model hello, wordt facturering voor wachtrijen en onderwerpen/abonnementen gewijzigd. Deze entiteiten worden veranderen van facturering per bericht toobilling per bewerking. Een 'bewerking' verwijst tooany API-aanroep voor een wachtrij of onderwerp/abonnement service-eindpunt. Het gaat hierbij om bewerkingen voor beheer, verzenden/ontvangen en sessie-status.

| Type bewerking | Beschrijving |
| --- | --- |
| Beheer |Maken, lezen, bijwerken, verwijderen (CRUD) op basis van wachtrijen en onderwerpen/abonnementen. |
| Berichten |Verzenden en ontvangen berichten met wachtrijen en onderwerpen/abonnementen. |
| Sessiestatus |Ophalen of instellen van status van de sessie op een wachtrij of onderwerp/abonnement. |

Zie voor meer informatie kosten Hallo prijzen vermeld op Hallo [Service Bus prijzen](https://azure.microsoft.com/pricing/details/service-bus/) pagina.

## <a name="brokered-connections"></a>Brokered Connections
*Brokered verbindingen* ruimte gebruikspatronen klant die betrekking hebben op een groot aantal 'permanent verbonden' afzenders/ontvangers op basis van wachtrijen, onderwerpen en abonnementen. Permanent verbonden afzenders/ontvangers zijn die verbinding maken via de AMQP of HTTP met een niet-nul time-out (bijvoorbeeld HTTP-lange polling) ontvangen. HTTP-afzenders en ontvangers met een onmiddellijke time-out genereren geen brokered verbindingen.

Zie voor verbinding quota's en andere Servicelimieten hello [Service Bus-quota](service-bus-quotas.md) artikel.

Hallo standaardcategorie Hallo per naamruimte brokered verbindingslimiet verwijdert en statistische brokered verbinding gebruik telt over hello Azure-abonnement. Zie voor meer informatie, Hallo [Brokered verbindingen](https://azure.microsoft.com/pricing/details/service-bus/) tabel.

> [!NOTE]
> 1000 brokered verbindingen zijn opgenomen in Hallo Standard messaging-laag (via Hallo base kosten) en kunnen worden gedeeld door alle wachtrijen, onderwerpen en abonnementen binnen Azure-abonnement Hallo die zijn gekoppeld.
>
>

<br />

> [!NOTE]
> Facturering is gebaseerd op Hallo maximum aantal gelijktijdige verbindingen en wordt naar rato per uur op basis van 744 uur per maand.
>
>

| Premium-laag |
| --- |
| Brokered verbindingen zijn niet in rekening gebracht in Hallo Premium-laag. |

Zie voor meer informatie over brokered verbindingen Hallo [Veelgestelde vragen over](#faq) verderop in dit onderwerp.

## <a name="faq"></a>Veelgestelde vragen

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>Wat zijn brokered verbindingen en hoe ik ophalen in rekening gebracht voor hen?
Een brokered verbinding wordt gedefinieerd als een van de volgende Hallo:

1. Een AMQP-verbinding van een client tooa Service Bus-wachtrij of onderwerp/abonnement.
2. Een HTTP-aanroep tooreceive een bericht van een Service Bus-onderwerp of een wachtrij met een receive time-outwaarde die groter zijn dan nul.

Service Bus-kosten voor Hallo maximum aantal gelijktijdige brokered verbindingen die groter is dan Hallo opgenomen hoeveelheid (1000 Hallo Standard-laag). Pieken zijn gemeten op uurbasis naar rato door te delen door 744 uur per maand en via Hallo maandelijks facturering periode opgeteld. Hallo opgenomen hoeveelheid (1000 brokered verbindingen per maand) wordt toegepast op Hallo einde van de factureringsperiode Hallo tegen Hallo som van Hallo naar rato per uur pieken.

Bijvoorbeeld:

1. Elk van 10.000 apparaten verbindt via een enkele AMQP-verbinding en opdrachten ontvangt van een Service Bus-onderwerp. Hallo apparaten verzenden telemetrie gebeurtenissen tooan Event Hub. Als alle apparaten verbinding voor 12 uur per dag maken, Hallo verbinding kosten volgende van toepassing (in aanvulling tooany de kosten voor andere Service Bus-onderwerp): 10.000 verbindingen * 12 uur * 31 dagen / 744 = 5.000 brokered verbindingen. Na het Hallo maandelijkse tegoed van 1000 brokered verbindingen, zou worden in rekening gebracht voor 4000 brokered verbindingen met Hallo snelheid van $0,03 per brokered-verbinding voor een totaal van $120.
2. 10.000 apparaten ontvangen berichten van een Service Bus-wachtrij via HTTP, geven een time-out dan nul. Als alle apparaten verbinding voor elke dag van 12 uur maken, ziet u de volgende verbinding kosten Hallo (in aanvulling tooany andere Service Bus-kosten): 10.000 ontvangen van HTTP-verbindingen * 12 uur per dag * 744 uur-31 dagen = 5.000 brokered verbindingen.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Pas brokered verbinding kosten tooqueues en onderwerpen/abonnementen?
Ja. Er zijn geen kosten verbinding voor het verzenden van gebeurtenissen met behulp van HTTP, ongeacht het Hallo-nummer van het verzenden van systemen of apparaten. Gebeurtenissen ontvangen met HTTP met behulp van een time-out groter zijn dan nul, 'lange polling,', worden genoemd, genereert brokered verbinding kosten. AMQP-verbindingen genereren brokered verbinding kosten ongeacht of Hallo verbindingen worden gebruikte toosend of ontvangen. Houd er rekening mee dat brokered verbindingen 100 gratis in een Basic naamruimte zijn toegestaan. Dit is ook Hallo maximumaantal brokered verbindingen zijn toegestaan voor hello Azure-abonnement. Hallo zijn eerste 1.000 brokered verbindingen in alle standaard naamruimten in een Azure-abonnement opgenomen zonder extra kosten (anders dan Hallo base kosten). Omdat deze rechten onvoldoende toocover zijn pas veel service to service berichtverzending, meestal brokered verbinding kosten relevant als u toouse AMQP of HTTP lange-polling van plan met een groot aantal clients bent; bijvoorbeeld: tooachieve efficiënter gebeurtenis streamen of Activeer bidirectionele communicatie met veel apparaten of exemplaren van een toepassing.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over prijzen voor Service Bus Hallo [Service Bus pagina met prijzen](https://azure.microsoft.com/pricing/details/service-bus/).
* Zie Hallo [Veelgestelde vragen over de Service Bus](service-bus-faq.md#pricing) voor een aantal algemene veelgestelde vragen over servicebus-prijzen en facturering.

[Azure portal]: https://portal.azure.com
