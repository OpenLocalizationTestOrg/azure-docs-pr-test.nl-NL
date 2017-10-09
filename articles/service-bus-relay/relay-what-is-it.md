---
title: aaaWhat Azure Relay en waarom gebruiken overzicht | Microsoft Docs
description: Overzicht van Azure Relay
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>Wat is Azure Relay?

Hello Azure Relay service hybride toepassingen vereenvoudigt doordat u toosecurely services die zich in een zakelijke enterprise netwerk toohello openbare cloud, bevinden zonder dat een firewallverbinding tooopen vrijgegeven of vereisen Tussenkomende wijzigingen tooa infrastructuur van het bedrijfsnetwerk. Met Relay wordt een groot aantal verschillende transportprotocollen en webservicestandaarden ondersteund.

Hallo relay-service ondersteunt traditionele één richting, aanvraag/antwoord en peer-to-peer-verkeer. Het ondersteunt ook gebeurtenisdistributie via internet bereik tooenable publiceren/abonneren scenario's en bidirectionele socket-communicatie voor verbeterde point-to-point-efficiëntie. 

In Hallo relayed gegevensoverdracht patroon een on-premises-service toohello relay-service verbindt via een uitgaande poort en maakt een bidirectionele socket voor communicatie gebonden tooa bepaald rendezvous-adres. Hallo-client kan vervolgens communiceren met de Hallo on-premises-service door te sturen verkeer toohello relay-service die gericht is op Hallo rendezvous-adres. Hallo relay-service stuurt' vervolgens' data toohello on-premises service via een bidirectionele socket toegewezen tooeach-client. Hallo client hoeft niet een rechtstreekse verbinding toohello lokale service en is niet vereist tooknow waarbij Hallo-service zich bevindt en Hallo lokale service hoeft niet poorten voor inkomend verkeer op Hallo firewall openen.

Hallo sleutel mogelijkheid elementen geleverd door Relay communicatie in twee richtingen, niet-gebufferde zijn buiten de netwerkgrenzen van met TCP-achtige beperking, eindpunt detectie, verbindingsstatus en eindpuntbeveiliging overlapt. Hallo relay-mogelijkheden kunnen afwijken van de op netwerkniveau integratietechnologieën zoals VPN, in die relay bereik tooa één toepassingseindpunt op een enkele computer terwijl VPN-technologie is tot nu toe ingrijpender zoals is afhankelijk van het wijzigen van de netwerkomgeving Hallo .

Azure Relay heeft twee functies:

1. [Hybride verbindingen](#hybrid-connections) - gebruikt Hallo standard web openen sockets inschakelen van scenario's voor meerdere platforms.
2. [WCF-Relays](#wcf-relays) -tooenable externe procedureaanroepen weer dat gebruikmaakt van Windows Communication Foundation (WCF). Relay WCF is Hallo verouderde relay biedt dat veel klanten al met hun WCF programming modellen gebruiken.

Hybride verbindingen en WCF-Relays inschakelen beveiligde verbinding tooassets die bestaan in een bedrijfsnetwerk. Gebruik van een via andere Hallo is afhankelijk van uw specifieke behoeften, zoals beschreven in de volgende tabel Hallo:

|  | WCF-relay | Hybride verbindingen |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Open protocol op basis van standaarden** | |x |
| **Meerdere RPC-programmeringsmodellen** | |x |

## <a name="hybrid-connections"></a>Hybride verbindingen

Hallo [Azure Relay hybride verbindingen](relay-hybrid-connections-protocol.md) mogelijkheid is een beveiligde, open-protocol evolutie van Hallo bestaande Relay-functies die kunnen worden geïmplementeerd op elk platform en in elke taal waarvoor een basic WebSocket-mogelijkheid heeft die algemene webbrowsers bevat expliciet Hallo WebSocket-API. Hybride verbindingen zijn gebaseerd op HTTP en WebSockets.

### <a name="service-history"></a>Servicegeschiedenis

Hybride verbindingen supplants Hallo voormalige, op dezelfde manier met de naam 'BizTalk Services'-functie die is gebaseerd op Hallo Azure Service Bus WCF Relay. Hallo nieuwe hybride verbindingen mogelijkheid is een aanvulling op bestaande WCF Relay-functie Hallo en deze twee servicefuncties side-by-side in hello Azure Relay-service bestaat. De twee services delen een gateway, maar zijn verder afzonderlijke implementaties.

## <a name="wcf-relays"></a>WCF-relays

Hallo WCF Relay werkt voor Hallo volledige .NET Framework (NETFX) en voor WCF. U start Hallo-verbinding tussen uw on-premises-service en Hallo relay-service met een reeks WCF 'relay'-bindingen. Hallo relay-bindingen toegewezen achter de schermen hello, toonew transport binding elementen ontworpen toocreate WCF-kanaalonderdelen die kunnen worden geïntegreerd met Service Bus in de cloud Hallo.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Architectuur: verwerken van inkomende relay-aanvragen
Wanneer een client verzendt een aanvraag toohello [Azure Relay](/azure/service-bus-relay/) hello Azure load balancer-service stuurt deze tooany van Hallo gateway-knooppunten. Als Hallo-aanvraag een aanvraag voor luisteren is, maakt het Hallo-gateway-knooppunt een nieuwe relay. Als Hallo-aanvraag een verbinding aanvraag tooa specifieke relay is, verzendt Hallo gateway-knooppunt Hallo verbinding aanvraag toohello gateway-knooppunt dat eigenaar is van Hallo relay. Hallo gateway-knooppunt dat eigenaar is van Hallo relay verzendt een rendezvous aanvraag toohello luisterende client om Hallo listener toocreate een tijdelijk kanaal toohello gateway-knooppunt dat Hallo verbindingsaanvraag heeft ontvangen.

Wanneer Hallo relay-verbinding tot stand is gebracht, kunnen clients Hallo berichten uit via Hallo gateway-knooppunt dat wordt gebruikt voor Hallo rendezvous uitwisselen.

![Verwerken van inkomende WCF Relay-aanvragen](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Volgende stappen

* [Veelgestelde vragen over Relay](relay-faq.md)
* [Een naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Aan de slag met knooppunten](relay-hybrid-connections-node-get-started.md)

