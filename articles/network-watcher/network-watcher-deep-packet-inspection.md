---
title: aaaPacket inspectie met Azure-netwerk-Watcher | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse netwerk-Watcher tooperform grondige inspecties van pakketten verzameld van een virtuele machine
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Pakketinspecties met Azure-netwerk-Watcher

Hallo pakket vastleggen functie van netwerk-Watcher gebruikt, kunt u starten en beheren van sessies mogelijk op uw Azure VM's van Hallo-portal, PowerShell, CLI en programmatisch via Hallo SDK en de REST-API. Pakketopname kunt u tooaddress-scenario's waarvoor niveau pakketgegevens doordat Hallo-gegevens in een indeling die gemakkelijk kan worden gebruikt. Mogelijkheden van hulpprogramma tooinspect Hallo gegevens, kunt u onderzoeken communicaties tooand van uw virtuele machines en inzicht in het netwerkverkeer. Sommige toepassingen voorbeeld van Pakketgegevens vastleggen zijn onder andere: onderzoeken van problemen met netwerk of de toepassing, de pogingen misbruik en inbraakdetectie netwerk te detecteren of naleving van regelgeving onderhouden. In dit artikel, laten we zien hoe tooopen een pakket vastleggen bestand geleverd door netwerk-Watcher met behulp van een populaire open-source hulpprogramma. We bieden ook voorbeelden ziet u hoe toocalculate latentie van de verbinding abnormaal verkeer identificeren en netwerken statistieken onderzoeken.

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel gaat via een aantal vooraf geconfigureerde scenario's op een pakketopname die eerder is uitgevoerd. Deze scenario's illustreren mogelijkheden die aan de hand van een pakketopname kunnen worden geopend. Dit scenario wordt gebruikgemaakt van [WireShark](https://www.wireshark.org/) tooinspect hello pakketopname.

Dit scenario wordt ervan uitgegaan dat u al een pakketopname uitgevoerd op een virtuele machine. hoe toocreate een pakketopname gaat u naar toolearn [beheren pakket worden vastgelegd met Hallo portal](network-watcher-packet-capture-manage-portal.md) of met REST in via [pakket vastgelegd beheren met de REST-API](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Scenario

In dit scenario u:

* Bekijk een pakketopname

## <a name="calculate-network-latency"></a>Netwerklatentie berekenen

In dit scenario, laten we zien hoe tooview Hallo initiële Round Trip Time RTT () van een Transmission Control Protocol (TCP) conversatie plaatsvinden tussen twee eindpunten.

Als er een TCP-verbinding tot stand is gebracht, voert hello eerste drie pakketten die worden verzonden in Hallo verbinding een patroon vaak aangeduid tooas Hallo drie richtingen handshake. Door in de eerste twee hello-pakketten dat in deze handshake, een eerste verzoek van Hallo-client en een antwoord van Hallo server verzonden, kunnen we Hallo latentie berekenen wanneer deze verbinding tot stand is gebracht. Deze latentie is waarnaar wordt verwezen tooas Hallo Round Trip Time RTT (). Raadpleeg voor meer informatie over Hallo TCP-protocol en Hallo drie richtingen handshake toohello resource te volgen. https://support.Microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-handshake-via-TCP-IP

### <a name="step-1"></a>Stap 1

WireShark starten

### <a name="step-2"></a>Stap 2

Load Hallo **CAP** bestand van uw pakketopname. Dit bestand vindt u in Hallo blob het op onze lokaal op Hallo virtuele machine wordt opgeslagen, afhankelijk van hoe u geconfigureerd.

### <a name="step-3"></a>Stap 3

tooview Hallo initiële Round Trip Time RTT () in de TCP-gesprekken, wordt alleen het bekijken van Hallo eerst twee pakketten die zijn betrokken bij Hallo TCP-handshake. We gebruiken Hallo eerst twee pakketten in drie richtingen-handshake hello, die Hallo [SYN], [SYN, ACK] pakketten. Ze zijn met de naam van de vlaggen ingesteld in Hallo TCP-header. laatste Hallo-pakket in Hallo-handshake wordt hello [ACK]-pakket wordt niet gebruikt in dit scenario. Hallo [SYN] pakket wordt verzonden door Hallo-client. Zodra dit is ontvangen verzendt Hallo server hello [ACK]-pakket als een bevestiging ontvangen Hallo SYN van Hallo-client. Mogelijkheden van Hallo feit dat het antwoord van server Hallo weinig overhead vereist, berekenen we Hallo RTT door af te trekken Hallo tijd hello [SYN, ACK]-pakket is ontvangen door de client Hallo door hello tijd [SYN]-pakket is verzonden door de client Hallo.

WireShark met is deze waarde berekend voor ons.

eerste twee hello-pakketten toomore eenvoudig weergeven in drie richtingen handshake van Hallo TCP, maken we gebruik Hallo filtermogelijkheden geleverd door WireShark.

tooapply hello filter in WireShark, vouw Hallo 'Transmission Control Protocol' Segment van een pakket [SYN] in uw vastleggen en onderzoeken Hallo-vlaggen ingesteld in Hallo TCP-header.

Aangezien we toofilter op alle [SYN zoekt] en [SYN ACK] pakketten onder vlaggen cofirm dat Hallo Syn bits too1 is ingesteld, wordt rechts Klik op Hallo Syn bits -> toepassen als Filter -> geselecteerd.

![Afbeelding 7][7]

### <a name="step-4"></a>Stap 4

Nu dat u hebt gefilterd Hallo venster tooonly Zie pakketten met Hallo [SYN] foutstijlbit, kunt u eenvoudig selecteren conversaties u geïnteresseerd bent in tooview Hallo initiële RTT. Een eenvoudige manier tooview Hallo RTT in WireShark klikt Hallo dropdown is gemarkeerd als ' SEQ/ACK' analyse. Vervolgens ziet u Hallo die RTT weergegeven. In dit geval is Hallo RTT 0.0022114 seconden of 2.211 ms.

![afbeelding 8][8]

## <a name="unwanted-protocols"></a>Ongewenste protocollen

U kunt hebben veel toepassingen die worden uitgevoerd op de instantie van een virtuele machine die u hebt geïmplementeerd in Azure. Veel van deze toepassingen communiceren via Hallo-netwerk mogelijk zonder uw expliciete toestemming. Pakket vastleggen toostore netwerkcommunicatie gebruikt, kunt we hoe de toepassing wordt gesproken op Hallo netwerk en zoek naar problemen onderzoeken.

In dit voorbeeld we bekijken een eerdere pakketopname voor ongewenste protocollen die mogelijk aangeven onbevoegde communicatie van een toepassing die wordt uitgevoerd op uw computer uitgevoerd.

### <a name="step-1"></a>Stap 1

Met behulp van dezelfde vastleggen Klik in het vorige scenario op Hallo Hallo **statistieken** > **Protocol hiërarchie**

![Protocol hiërarchie menu][2]

Hallo protocol hiërarchie venster wordt weergegeven. Deze weergave bevat een lijst van alle Hallo-protocollen die werden gebruikt tijdens het Hallo opnamesessie en Hallo aantal pakketten verzonden en ontvangen met behulp van Hallo-protocollen. Deze weergave is handig voor het vinden van ongewenste netwerkverkeer op de virtuele machines of het netwerk.

![protocol configureren geopend][3]

Zoals u in de volgende schermopname hello ziet, moet u er verkeer dat gebruikmaakt van Hallo BitTorrent protocol, dat wordt gebruikt voor het delen van peer toopeer bestanden is. Als een beheerder verwacht u toosee BitTorrent verkeer niet op deze bepaalde virtuele machines. Nu u op de hoogte van dit verkeer, kunt u Hallo peer toopeer software geïnstalleerd op deze virtuele machine of blok Hallo verkeer met behulp van Netwerkbeveiligingsgroepen of een Firewall. U kunt bovendien toorun pakket opnamen volgens een schema ervoor kiezen zodat u kunt Hallo protocol gebruik regelmatig op uw virtuele machines bekijken. Voor een voorbeeld van hoe tooautomate netwerk in azure vindt u taken [netwerkbronnen met azure automation bewaken](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Meest bezochte bestemmingen en poorten vinden

Kennis van Hallo typen verkeer, Hallo eindpunten en Hallo-poorten die via gecommuniceerd is een belangrijk bij het bewaken of het oplossen van toepassingen en bronnen in uw netwerk. Met behulp van een bestand voor het vastleggen van pakket van boven, kunnen we snel leren Hallo bovenste bestemmingen onze VM communiceert en Hallo poorten worden gebruikt.

### <a name="step-1"></a>Stap 1

Met behulp van dezelfde vastleggen Klik in het vorige scenario op Hallo Hallo **statistieken** > **IPv4-statistieken** > **bestemmingen en poorten**

![venster van pakket vastleggen][4]

### <a name="step-2"></a>Stap 2

Zoals we bekijkt hello resultaten een regel opvalt, er zijn meerdere verbindingen via poort 111. Hallo meest gebruikte poort 3389, is dit extern bureaublad is en Hallo resterende RPC dynamische poorten zijn.

Hoewel dit verkeer betekenen er niets dat kan, is een poort die is gebruikt voor het aantal verbindingen en onbekende toohello-beheerder.

![Afbeelding 5][5]

### <a name="step-3"></a>Stap 3

Nu dat we hebben een out-of plaats poort filteren we onze vastleggen op basis van Hallo poort bepaald.

Hallo-filter in dit scenario zou zijn:

```
tcp.port == 111
```

We Hallo Filtertekst van boven in Hallo filter textbox invoeren en op ENTER drukken.

![Afbeelding 6][6]

Uit de resultaten hello, ziet u alle Hallo verkeer afkomstig is van een lokale virtuele machine op Hallo hetzelfde subnet. Als we nog steeds niet waarom dit verkeer plaatsvindt begrijpen, kunnen we verder hello-pakketten toodetermine waarom het aan te deze aanroepen op poort 111 brengen inspecteren. Met deze informatie kunnen we Hallo gepaste actie ondernemen.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over andere diagnostische functies van netwerk-Watcher Hallo in via [bewakingsoverzicht Azure-netwerk](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













