---
title: Routering aaaAsymmetric | Microsoft Docs
description: Dit artikel begeleidt u bij Hallo problemen die van de klant mogelijk geconfronteerd met asymmetrische routering in een netwerk met meerdere koppelingen tooa bestemming.
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Asymmetrische routering met meerdere netwerkpaden
In dit artikel wordt uitgelegd hoe uitgaand en binnenkomend netwerkverkeer verschillende routes kan nemen wanneer er meerdere paden beschikbaar zijn tussen netwerkbron en -bestemming.

De belangrijke toounderstand twee concepten toounderstand asymmetrische routering. Een is Hallo effect van meerdere netwerkpaden. Hallo andere is hoe apparaten, zoals een firewall, status houden. Dit soort apparaten worden stateful apparaten genoemd. Een combinatie van deze twee factoren maakt scenario's waarvoor verkeer is verwijderd door een stateful apparaat omdat Hallo stateful apparaat dat verkeer afkomstig met het Hallo-apparaat zelf is niet detecteren.

## <a name="multiple-network-paths"></a>Meerdere netwerkpaden
Wanneer een bedrijfsnetwerk heeft slechts één koppeling toohello Internet via hun internetprovider alle verkeer tooand van Hallo Internet wordt verzonden Hallo hetzelfde pad. Bedrijven worden vaak meerdere circuits aanschaffen als redundante paden, tooimprove netwerk bedrijfstijd. Als dit gebeurt, wordt het mogelijk dat verkeer dat wordt verstuurd buiten het netwerk hello, toohello Internet, verloopt via een koppeling en Hallo retourneren verkeer verloopt via een andere koppeling. Dit wordt doorgaans asymmetrische routering genoemd. Omgekeerde netwerkverkeer wordt een ander pad van de oorspronkelijke overdracht Hallo asymmetrische routering.

![Netwerk met meerdere paden](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Hoewel deze voornamelijk op Hallo Internet optreedt, asymmetrische routering ook van toepassing tooother combinaties van meerdere paden. Dit geldt, bijvoorbeeld, zowel tooan internetpad en een persoonlijk pad die toohello hetzelfde doel en toomultiple persoonlijke paden die gaat toohello hetzelfde doel.

Elke router langs Hallo manier van bron toodestination, berekent Hallo best pad tooreach een bestemming. Hallo is van router bepaling van de best mogelijke pad gebaseerd op twee belangrijkste factoren:

* Routering tussen externe netwerken is gebaseerd op een routeringsprotocol, het Border Gateway Protocol (BGP). BGP-advertisements van neighbors duurt en ze worden uitgevoerd door een reeks stappen toodetermine Hallo best pad toohello bedoeld bestemming. Hallo beste pad worden opgeslagen in de routeringstabel.
* Hallo-lengte van een subnetmasker in die zijn gekoppeld aan een route is van invloed routering paden. Als een router ontvangt meerdere advertenties voor Hallo hetzelfde IP-adres, maar met verschillende subnetmaskers Hallo router Hallo aankondiging met een langere subnetmasker voorkeur omdat deze is beschouwd als een meer specifieke route.

## <a name="stateful-devices"></a>Stateful apparaten
Routers kijken Hallo IP-header van een pakket voor de routering. Sommige apparaten zoeken zelfs dieper in Hallo-pakket. Normaal gesproken kijken deze apparaten naar Layer4- (Transmission Control Protocol of TCP; of User Datagram Protocol of UDP), of zelfs Layer7-headers (toepassingslaag). Dergelijke apparaten zijn beveiligingsapparaten of apparaten die de bandbreedte optimaliseren. 

Een firewall is een algemeen voorbeeld van een stateful apparaat. Een firewall toestaat of weigert een pakket toopass via de interfaces op basis van verschillende velden zoals protocol TCP/UDP-poort en URL-headers. Dit niveau van pakketinspecties plaatst een zware belasting op Hallo apparaat verwerken. tooimprove prestaties Hallo firewall inspecteert Hallo eerste pakket van een stroom. Als het Hallo pakket tooproceed toestaat, blijven in de tabel staat informatie over de gebeurtenisstroom Hallo. Alle latere pakketten gerelateerde toothis stroom zijn toegestaan op basis van de aanvankelijke bepaling Hallo. Een pakket dat deel uitmaakt van een bestaande stroom op Hallo firewall mogelijk binnenkomen. Als Hallo firewall geen vorige staat informatie over het heeft, zakt Hallo firewall hello-pakket.

## <a name="asymmetric-routing-with-expressroute"></a>Asymmetrische routering met ExpressRoute
Als u tooMicrosoft verbinding via Azure ExpressRoute, wordt uw wijzigingen in het netwerk als volgt:

* U hebt meerdere koppelingen tooMicrosoft. Een koppeling is uw bestaande verbinding met Internet en andere Hallo is via ExpressRoute. Sommige tooMicrosoft verkeer kan Hallo Internet doorlopen, maar keert u terug via ExpressRoute of vice versa.
* U ontvangt specifiekere IP-adressen via ExpressRoute. Dus voor verkeer van uw netwerk tooMicrosoft voor services die worden aangeboden via ExpressRoute, eigenlijk routers altijd voor ExpressRoute.

toounderstand hello effect dat deze twee wijzigingen op een netwerk, hebben we eens enkele scenario's. Als een voorbeeld hebt u slechts één circuit toohello Internet en u alle Microsoft-services via Internet Hallo verbruiken. Hallo-verkeer van uw netwerk tooMicrosoft en terug traverses Hallo dezelfde internetkoppeling tot stand en Hallo firewall passeren. Hallo firewall records Hallo stroom als eerste pakket Hallo ziet en pakketten zijn toegestaan, omdat Hallo stroom in tabel Hallo bestaat geretourneerd.

![Asymmetrische routering met ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

Vervolgens schakelt u ExpressRoute in, en gebruikt u services die door Microsoft worden aangeboden nu via ExpressRoute. Alle andere services van Microsoft worden via Internet Hallo verbruikt. Aan de rand die is verbonden tooExpressRoute implementeert u een afzonderlijke firewall. Microsoft adverteert specifiekere voorvoegsels tooyour netwerk via ExpressRoute voor bepaalde services. Uw infrastructuur voor de routering kiest ExpressRoute als Hallo voorkeurspad voor deze voorvoegsels. Als u geen aankondigingen uw openbare IP-adressen tooMicrosoft via ExpressRoute doet worden, wordt Microsoft communiceert met uw openbare IP-adressen via Hallo Internet. Doorsturen verkeer van uw netwerk tooMicrosoft ExpressRoute gebruikt en omgekeerde verkeer van Microsoft hello Internet gebruikt. Wanneer Hallo firewall aan de rand van Hallo ziet een antwoordpakket voor een stroom die niet wordt gevonden in tabel hello, komt het Hallo terugkerend verkeer.

Als u toouse Hallo dezelfde netwerkadresomzetting (NAT)-groep voor ExpressRoute en Hallo Internet kiest, ziet u vergelijkbare problemen met Hallo clients in uw netwerk op particuliere IP-adressen. Aanvragen voor services zoals Windows Update gaat via Internet Hallo omdat het IP-adressen voor deze services niet worden geadverteerd via ExpressRoute. Hallo terugkerend verkeer komt echter weer via ExpressRoute. Als Microsoft een IP-adres met ontvangt Hallo hetzelfde subnetmasker van Hallo Internet en een ExpressRoute, het ExpressRoute verkiest boven Hallo Internet. Als een firewall of een andere stateful-apparaat dat zich op de rand van uw netwerk en gerichte ExpressRoute geen eerdere informatie over Hallo stroom heeft, deze hello-pakketten die deel uitmaken van de stroom toothat worden weggelaten.

## <a name="asymmetric-routing-solutions"></a>Oplossingen voor asymmetrische routering
U hebt twee manieren toosolve Hallo probleem asymmetrische routering. Een is via de Routering en andere Hallo is door gebruik te maken op basis van een bron NAT (snat omzetten).

### <a name="routing"></a>Routering
Zorg ervoor dat uw openbare IP-adressen verbindingen van aangekondigde tooappropriate wide area network (WAN). Bijvoorbeeld, als u toouse Hallo Internet voor verificatieverkeer en ExpressRoute voor uw e-verkeer wilt, moet u niet aangekondigd in uw Active Directory Federation Services (AD FS) openbare IP-adressen via ExpressRoute. Zorg ook niet tooexpose een lokale AD FS-tooIP serveradressen die Hallo router ontvangt via ExpressRoute. Routes die worden ontvangen via ExpressRoute zijn meer specifiek, zodat ze ExpressRoute Hallo voorkeurspad voor verificatie verkeer tooMicrosoft. Dit veroorzaakt asymmetrische routering.

Als u wilt dat toouse ExpressRoute voor verificatie, zorgt u ervoor dat u AD FS openbare IP-adressen worden geadverteerd via ExpressRoute zonder NAT bevinden. Op deze manier verkeer dat afkomstig is van Microsoft en probeert het tooan lokale AD FS-server wordt via ExpressRoute. Terugkerend verkeer van de klant tooMicrosoft maakt gebruik van ExpressRoute omdat het gewenste route Hallo via Hallo Internet.

### <a name="source-based-nat"></a>Brongebaseerde NAT
Een andere oplossing voor problemen met asymmetrische routering is het gebruik van SNAT. U hebt bijvoorbeeld niet openbaar IP-adres van een on-premises Simple Mail Transfer Protocol (SMTP) server Hallo geadverteerd via ExpressRoute omdat u van plan toouse Hallo Internet voor dit type communicatie bent. Een aanvraag afkomstig is met Microsoft en wordt vervolgens tooyour lokale SMTP-server Hallo Internet passeert. U snat omzetten Hallo binnenkomende aanvraag tooan interne IP-adres. Omgekeerde verkeer van Hallo SMTP-server gaat toohello edge-firewall (die u gebruikt voor NAT) in plaats van via ExpressRoute. Hallo terugkerend verkeer teruggaan via Hallo Internet.

![Brongebaseerde NAT-netwerkconfiguratie](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Detectie van asymmetrische routering
Traceroute is Hallo aanbevolen manier toomake ervoor dat het netwerkverkeer Hallo verwacht pad passeert. Als u verwacht verkeer vanaf uw lokale SMTP-server tooMicrosoft tootake Hallo Internet-pad dat, verwacht Hallo traceroute uit Hallo SMTP-server tooOffice 365 is. Hallo resultaat valideert dat verkeer inderdaad uw netwerk naar Hallo Internet en niet naar ExpressRoute verlaat.

