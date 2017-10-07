---
title: aaaOverview van Azure Event Hubs toegewezen capaciteit | Microsoft Docs
description: Overzicht van Microsoft Azure Event Hubs toegewezen capaciteit.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Overzicht van Event Hubs Dedicated

*Event Hubs toegewezen* capaciteit biedt één tenant implementaties voor klanten met Hallo zwaarste vereisten. Op volledige schaal Azure Event Hubs inkomend kan meer dan 2 miljoen gebeurtenissen per seconde of too2 GB per seconde telemetrie met volledig duurzame opslag- en onderliggende tweede latentie. Deze ook schakelt geïntegreerde oplossingen door de verwerking van realtime en batch op Hallo hetzelfde systeem. Met Event Hubs-archief is opgenomen in de aanbieding hello, kunt u Hallo complexiteit van uw oplossing reduceren doordat één stream realtime en op basis van batch pijplijnen ondersteunen.

Hallo vergelijkt volgende tabel Hallo beschikbaar Servicelagen van Event Hubs. Hallo Event Hubs Dedicated aanbieding is een vaste maandbedrag vergeleken toousage prijzen voor de meeste functies van de standaard- en Basic. Hallo toegewezen laag biedt Hallo functies van Hallo standaard-plan, maar met enterprise scale capaciteit voor klanten met veeleisende werkbelastingen. 

| Functie | Basic | Standard | Toegewezen |
| --- |:---:|:---:|:---:|
| Ingangsgebeurtenissen | Betalen per miljoen gebeurtenissen | Betalen per miljoen gebeurtenissen | Inbegrepen |
| Doorvoereenheid (1 MB per seconde inkomend, uitgaande van 2 MB per seconde) | Betalen per uur | Betalen per uur | Inbegrepen |
| Berichtgrootte | 256 kB | 256 kB | 1 MB |
| Beleid voor uitgevers | N.v.t. | Ja | Ja |     
| Consumergroepen | 1 - standaard | 20 | 20 |
| Berichtherhaling | Ja | Ja | Ja |
| Maximum aantal Throughput Units | 20 | 20 (flexibele too100)  | 1 CU≈200 |
| Brokered Connections | 100 opgenomen | 1000 opgenomen | 100 K opgenomen |
| Extra Brokered Connections | N.v.t. | Ja | Ja |
| Bewaartermijn voor berichten | 1 dag inbegrepen | 1 dag inbegrepen | Omhoog too7 dagen opgenomen |
| Archief (Preview) | N.v.t.   | Betalen per uur | Inbegrepen |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Voordelen van Event Hubs toegewezen capaciteit

Hallo volgende voordelen zijn beschikbaar bij gebruik van Event Hubs toegewezen:

* Één tenant hosten met geen ruis van andere tenants.
* Bericht grootte too1 MB neemt toe naarmate vergeleken too256 KB voor Standard- en Basic.
* Herhaalbare prestaties elke keer.
* Capaciteit toomeet die uw burst moet worden gegarandeerd.
* Schaalbaar tussen 1 en 8 capaciteitseenheden (CU) – bieden too2 miljoen inkomende gebeurtenissen per seconde.
  * Hallo scale beheren CUs voor Event Hubs Dedicated, waarin elke CU ongeveer Hallo equivalent van 200 doorvoereenheden (TU) kunt opgeven.
* Onderhoud nul: we beheren taakverdeling, OS-updates, beveiligingspatches en partitioneren.
* Vaste maandelijkse prijzen.

Event Hubs toegewezen verwijdert u ook sommige Hallo doorvoer beperkingen van Hallo standaard aanbieding. Doorvoereenheden in Basic en Standard lagen machtigen too1000 gebeurtenissen per seconde of 1 MB per seconde van toegangsroutes per TU en dubbele die hoeveelheid uitgaande. Hallo speciale scale aanbieding heeft geen beperkingen op toegangsroutes en uitgaande gebeurtenis telt. Deze limieten vallen alleen Hallo verwerkingscapaciteit Hallo aangeschaft event hubs.

Deze service is gericht op Hallo grootste telemetrie gebruikers en is beschikbaar toocustomers met een enterprise agreement.

## <a name="how-tooonboard"></a>Hoe tooonboard

Hallo Event Hubs specifiek platform wordt aangeboden via een enterprise-overeenkomst met verschillende grootten van CUs. Elke CU biedt ongeveer Hallo equivalent van 200 doorvoereenheden. U kunt de capaciteit van de omhoog of omlaag schalen in de gehele Hallo maand toomeet uw behoeften door toe te voegen of te verwijderen van CUs. Hallo toegewezen planning is uniek in dat er een meer praktijkervaring onboarding van Hallo Event Hubs product team tooget Hallo flexibele implementatie die geschikt is voor u. 

## <a name="next-steps"></a>Volgende stappen
Neem contact op met uw Microsoft-vertegenwoordiger of Microsoft Support tooget aanvullende informatie over Event Hubs toegewezen capaciteit. U kunt ook meer informatie over Event Hubs via Hallo koppelingen te volgen:

Ga naar Hallo koppelingen volgen voor gedetailleerde informatie over prijzen:

- [Prijzen van Event Hubs toegewezen](https://azure.microsoft.com/pricing/details/event-hubs/). U kunt ook contact opnemen met uw Microsoft-vertegenwoordiger of Microsoft Support tooget aanvullende informatie over Event Hubs toegewezen capaciteit.
- Hallo [Event Hubs Veelgestelde vragen over](event-hubs-faq.md) bevat informatie over de prijzen en antwoorden op enkele veelgestelde vragen over Event Hubs. 
