---
title: overzicht van aaaAzure Service Bus-messaging | Microsoft Docs
description: Beschrijving van Service Bus-berichten en Azure Relay
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Service Bus-berichtenservice: flexibele levering van gegevens in de cloud Hallo
De Microsoft Azure Service Bus is een betrouwbare service voor de levering van informatie. Hallo-doel van deze service is toomake communicatie eenvoudiger. Wanneer twee of meer partijen tooexchange informatie wilt, moeten ze een organisator communicatie. De Service Bus is een brokered communicatiemechanisme, of een communicatiemechanisme van derden. Dit is vergelijkbaar tooa postservice in de fysieke wereld Hallo. Postservices maken het heel eenvoudig toosend verschillende soorten brieven en pakketten met tal van verschillende leveringsgaranties overal in Hallo wereld.

Vergelijkbare toohello postservice die brieven, Service Bus levert is flexibele levering van zowel Hallo afzender en ontvanger Hallo. Hallo berichtenservice zorgt ervoor dat Hallo informatie wordt afgeleverd, zelfs als Hallo twee partijen nooit beide online op Hallo dezelfde tijd of als ze niet beschikbaar op Hallo dezelfde exact tijd. Op deze manier is berichtenservice vergelijkbare toosending een letter, terwijl niet-brokered communicatie vergelijkbaar tooplacing een telefonische oproep (of hoe een telefonische oproep toobe - aanroep wachtstand en beller-ID vóór, die veel meer richting van brokered messaging gebruikt).

afzender Hallo-bericht kan ook verschillende leveringskenmerken zoals transacties, detectie van duplicaten, verloopt op basis van tijd en batchverzending vereisen. Ook deze patronen laten zich vergelijken met een postservice: herhaalde levering, vereisen van een handtekening, adreswijziging of intrekken van het bericht.

Service Bus ondersteunt twee verschillende berichtpatronen: *Azure Relay* en *Service Bus-berichten*.

## <a name="azure-relay"></a>Azure Relay
Hallo [WCF Relay](../service-bus-relay/relay-what-is-it.md) onderdeel van Azure Relay is een gecentraliseerde (maar maximale taakverdeling) service die ondersteuning biedt voor tal van verschillende transportprotocollen en webservicestandaarden. waaronder SOAP, WS-* en zelfs REST. Hallo [relay-service](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) biedt tal van verschillende relay-connectiviteitsopties en kan helpen om te onderhandelen over directe peer-to-peer-verbindingen wanneer het is mogelijk. Service Bus is geoptimaliseerd voor .NET-ontwikkelaars die werken met Hallo WCF Windows Communication Foundation (), beide met inachtneming van tooperformance en bruikbaarheid, en biedt volledige toegang tooits relay-service via SOAP en REST-interfaces. Daardoor kunnen SOAP-of REST-programmeermodel omgeving toointegrate met Service Bus.

Hallo relay-service ondersteunt traditionele berichten in één richting, aanvraag-/ antwoordberichten en peer-to-peerberichten. Ondersteunt tevens gebeurtenisdistributie via Internet tooenable voor publiceren / abonneren scenario's en bidirectionele socket-communicatie voor verbeterde point-to-point-efficiëntie. In Hallo relayed messaging-patroon maakt een on-premises-service toohello relay-service verbindt via een uitgaande poort en maakt een bidirectionele socket voor communicatie gebonden tooa bepaald rendezvous-adres. Hallo-client kan vervolgens communiceren met de Hallo on-premises-service door het verzenden van berichten toohello relay-service die gericht is op Hallo rendezvous-adres. Hallo relay-service wordt vervolgens 'relay' berichten toohello on-premises service via Hallo bidirectionele socket al ingevuld. Hallo client hoeft niet een rechtstreekse verbinding toohello lokale service, noch it vereist tooknow waarbij Hallo-service zich bevindt en Hallo lokale service hoeft niet poorten voor inkomend verkeer wordt geopend in Hallo firewall.

U starten Hallo-verbinding tussen uw on-premises-service en Hallo relay-service met een reeks WCF 'relay'-bindingen. Hallo relay-bindingen toegewezen achter de schermen hello, tootransport binding elementen ontworpen toocreate WCF-kanaalonderdelen die kunnen worden geïntegreerd met Service Bus in de cloud Hallo.

WCF Relay biedt veel voordelen, maar vereist Hallo-server en client tooboth online op Hallo dezelfde periode in volgorde toosend en ontvangen van berichten. Dit is niet optimaal voor HTTP-communicatie, in welke Hallo aanvragen mogelijk niet doorgaans lange levensduur hebben, noch voor clients die verbinding maken met alleen sporadisch zoals browsers, mobiele toepassingen, enzovoort. Brokered Messaging ondersteunt ontkoppelde communicatie en heeft voordelen op zich. Clients en servers kunnen wanneer nodig verbinding maken en hun bewerkingen asynchroon uitvoeren.

## <a name="brokered-messaging"></a>Brokered Messaging
Daarentegen toohello relay-schema, Service Bus-berichtenservice, of [brokered messaging](service-bus-queues-topics-subscriptions.md) worden beschouwd als asynchroon of 'tijdelijk ontkoppeld'. Producenten (afzenders) en consumenten (ontvangers) hebben geen toobe online op Hallo hetzelfde moment. Hallo berichteninfrastructuur slaat berichten veilig op in een 'broker' (zoals een wachtrij) tot Hallo verbruikende partij gereed tooreceive ze. Hierdoor Hallo onderdelen van Hallo gedistribueerde toepassing toobe losgekoppeld-hetzij vrijwillig; bijvoorbeeld voor onderhoud, hetzij vanwege het vastlopen van tooa onderdeel, zonder het hele systeem Hallo. Bovendien misschien de ontvangende toepassing hello alleen toocome online bepaalde tijdstippen gedurende Hallo dag, zoals een inventaris van een beheersysteem dat alleen vereiste toorun aan Hallo einde van de werkdag Hallo.

Hallo belangrijkste onderdelen van Hallo Service Bus brokered messaging-infrastructuur zijn wachtrijen, onderwerpen en abonnementen.  Hallo belangrijkste verschil is dat onderwerpen mogelijkheden voor publiceren/abonneren die kunnen worden gebruikt voor geavanceerde inhoud gebaseerde routering en logica voor aflevering, met inbegrip van toomultiple ontvangers verzenden ondersteunen. Deze onderdelen faciliteren nieuwe scenario’s voor asynchrone berichtverzending, zoals tijdelijke ontkoppeling, publiceren/abonneren en taakverdeling. Zie [Service Bus-wachtrijen, -onderwerpen en -abonnementen](service-bus-queues-topics-subscriptions.md) voor meer informatie over deze berichtentiteiten.

Zoals met Hallo Relay WCF-infrastructuur, Hallo brokered messaging wordt mogelijkheid opgegeven voor programmeurs van WCF en .NET Framework en via REST.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Service Bus-berichtenservice, Zie Hallo volgende onderwerpen.

* [Grondbeginselen van Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus-wachtrijen, -onderwerpen en -abonnementen](service-bus-queues-topics-subscriptions.md)
* [Hoe toouse Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* [Hoe toouse Service Bus-onderwerpen en abonnementen](service-bus-dotnet-how-to-use-topics-subscriptions.md)

