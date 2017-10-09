---
title: Veelgestelde vragen over ExpressRoute aaaAzure | Microsoft Docs
description: Hallo Veelgestelde vragen over ExpressRoute bevat informatie over ondersteunde Azure-Services, kosten, gegevens en verbindingen, SLA, Providers en locaties, bandbreedte en aanvullende technische gegevens.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Veelgestelde vragen ExpressRoute

## <a name="what-is-expressroute"></a>Wat is ExpressRoute?

ExpressRoute is een Azure-service waarmee u particuliere verbindingen maken tussen Microsoft-datacenters en infrastructuur on-premises of in een functie van de plaatsing. ExpressRoute-verbindingen gaan niet via het openbare Internet en bieden betere beveiliging, betrouwbaarheid Hallo en snelheden met lagere latenties dan gewone verbindingen via Internet Hallo.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Wat zijn de voordelen van het gebruik van ExpressRoute- en particuliere netwerkverbindingen Hallo?

ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. Ze bieden betere beveiliging, betrouwbaarheid en snelheden, met lagere en consistente latenties dan gewone verbindingen via Internet Hallo. In sommige gevallen met behulp van ExpressRoute-verbindingen tootransfer gegevens tussen on-premises apparaten en Azure aanzienlijke kostenvoordelen kan worden verkregen.

### <a name="where-is-hello-service-available"></a>Waar Hallo service beschikbaar is?

Deze pagina en beschikbaarheid van servicelocatie: [ExpressRoute-partners en locaties](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Hoe kan ik ExpressRoute tooconnect tooMicrosoft gebruiken als er geen samenwerking met een van de provider van ExpressRoute-partners Hallo?

U kunt een regionale luchtvaartmaatschappij selecteren en Ethernet-verbindingen tooone van Hallo ondersteund exchange land locaties van de provider. U kunt vervolgens met Microsoft op de locatie van de provider Hallo peer. Controleren van de laatste sectie van Hallo [ExpressRoute-partners en locaties](expressroute-locations.md) toosee als uw serviceprovider aanwezig zijn op Hallo exchange locaties. Vervolgens kunt u een ExpressRoute-circuit via Hallo serviceprovider tooconnect tooAzure bestellen.

### <a name="how-much-does-expressroute-cost"></a>Wat kost ExpressRoute?

Controleer [prijsinformatie](https://azure.microsoft.com/pricing/details/expressroute/) voor informatie over prijzen.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Hebben toobe dezelfde snelheid in Media Player Hallo als ik betaalt voor een ExpressRoute-circuit van een bepaalde bandbreedte VPN-verbinding ik aanschaffen bij mijn netwerkprovider Hallo?

Nee. U kunt een VPN-verbinding met een snelheid aanschaffen bij uw serviceprovider. Uw verbinding tooAzure is echter beperkt toohello ExpressRoute-circuit bandbreedte die u aanschaft.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Als ik voor een ExpressRoute-circuit van een bepaalde bandbreedte betalen, heb ik Hallo mogelijkheid tooburst up toohigher snelheden indien nodig?

Ja. ExpressRoute-circuits zijn geconfigureerde tooallow tooburst van tootwo tijden Hallo Bandbreedtelimiet die u hebt ontvangen zonder extra kosten. Neem contact op met uw serviceprovider toosee als deze functie wordt ondersteund.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Kan ik gebruiken Hallo particuliere netwerk verbinding met het virtuele netwerk en andere Azure-services tegelijk?

Ja. Een ExpressRoute-circuit nadat deze is ingesteld, kunt u tooaccess services binnen een virtueel netwerk en andere Azure-services tegelijk. U verbinden toovirtual netwerken via Hallo-pad voor persoonlijke peering en tooother services via Hallo-pad voor openbare peering.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>Biedt ExpressRoute een Service Level Agreement (SLA)?

Zie voor informatie Hallo [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) pagina.

## <a name="supported-services"></a>Ondersteunde services

ExpressRoute ondersteunt [drie Routeringsdomeinen](expressroute-circuit-peerings.md) voor verschillende soorten services.

### <a name="private-peering"></a>Persoonlijke peering

* Virtuele netwerken, inclusief alle virtuele machines en cloud-services

### <a name="public-peering"></a>Openbare peering

* Power BI
* Dynamics 365 voor Financiën en bewerkingen (voorheen bekend als Dynamics AX Online)
* De meeste hello Azure services Hello enkele uitzonderingen te volgen:
  * CDN
  * Visual Studio Team Services Load testen
  * Multi-Factor Authentication
  * Traffic Manager

### <a name="microsoft-peering"></a>Microsoft-peering

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 betrokkenheid van de klant-toepassingen (voorheen bekend als CRM Online)
  * Dynamics 365 voor verkoop
  * Dynamics 365 voor klantenservice
  * Dynamics 365 voor veld Service
  * Dynamics 365 voor Project-Service

## <a name="data-and-connections"></a>Gegevens en verbindingen

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Zijn er beperkingen met betrekking tot Hallo hoeveelheid gegevens die ik kunnen worden overgedragen met behulp van ExpressRoute?

We Stel een limiet op Hallo hoeveelheid gegevens overgedragen. Raadpleeg te[prijsinformatie](https://azure.microsoft.com/pricing/details/expressroute/) voor meer informatie over de tarieven voor bandbreedte.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Welke verbindingssnelheden worden ondersteund door ExpressRoute?

Ondersteunde bandbreedte-aanbiedingen:

50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps

### <a name="which-service-providers-are-available"></a>Welke serviceproviders zijn beschikbaar?

Zie [ExpressRoute-partners en locaties](expressroute-locations.md) voor Hallo lijst met serviceproviders en locaties.

## <a name="technical-details"></a>Technische details

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Wat zijn Hallo technische vereisten voor het verbinden van mijn lokale locatie tooAzure?

Zie [ExpressRoute vereisten pagina](expressroute-prerequisites.md) voor vereisten.

### <a name="are-connections-tooexpressroute-redundant"></a>Verbindingen tooExpressRoute redundante zijn?

Ja. Elk ExpressRoute-circuit heeft een redundante paar cross-verbindingen geconfigureerd tooprovide hoge beschikbaarheid.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Ik verliest als een van mijn ExpressRoute-koppelingen mislukken?

U wordt de verbinding niet verbroken als een Hallo over meerdere verbindingen mislukt. Een redundante verbinding is beschikbaar toosupport Hallo belasting van uw netwerk. Bovendien kunt u meerdere circuits maken in een andere peering locatie tooachieve fout herstelmogelijkheden.

### <a name="onep2plink"></a>Als ik wil niet CO-locatie op een cloudexchange en mijn serviceprovider point-to-point-verbinding biedt, moet ik tooorder twee fysieke verbindingen tussen mijn on-premises netwerk en Microsoft?

Als uw serviceprovider via Hallo fysieke verbinding tot stand twee virtuele Ethernet-circuits brengen kan, hoeft u slechts één fysieke verbinding. Hallo fysieke verbinding (bijvoorbeeld een Network) wordt beëindigd op een laag 1 (L1)-apparaat (Zie afbeelding Hallo). virtuele Hallo twee Ethernet-circuits zijn gelabeld met verschillende VLAN-id, één voor de primaire circuit hello, en één voor Hallo secundaire. Deze VLAN-id's zijn in Hallo buitenste 802.1Q Ethernet-header. Hallo binnenste 802.1Q Ethernet-header (niet weergegeven) is toegewezen tooa specifieke [ExpressRoute routeringsdomein](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>Kan ik uitbreiden met een van mijn VLAN's tooAzure ExpressRoute gebruiken?

Nee. Wij ondersteunen geen layer 2-connectiviteit uitbreidingen in Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Kan ik meer dan één ExpressRoute-circuit hebben in mijn abonnement?

Ja. U kunt meer dan één ExpressRoute-circuit hebben in uw abonnement. Hallo standaardlimiet is too10 ingesteld. U kunt contact opnemen met Microsoft Support tooincrease Hallo limiet, indien nodig.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Kan ik ExpressRoute-circuits van verschillende serviceproviders hebben?

Ja. U kunt ExpressRoute-circuits hebben met veel serviceproviders. Elk ExpressRoute-circuit is gekoppeld aan een serviceprovider. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Kan ik meerdere ExpressRoute-circuits in Hallo hebben dezelfde locatie?

Ja. U kunt meerdere ExpressRoute-circuits hebt, Hallo met dezelfde of verschillende providers op dezelfde locatie Hallo. U kan echter niet meer dan één ExpressRoute-circuit toohello koppelen virtuele netwerk van Hallo dezelfde locatie.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Hoe kan ik mijn virtuele netwerken tooan ExpressRoute-circuit verbinden

Hallo basisstappen zijn:

* Een ExpressRoute-circuit tot stand brengen en hebben Hallo serviceprovider inschakelen.
* U of Hallo-provider moet Hallo BGP peering (s) configureren.
* Koppeling Hallo virtueel netwerk toohello ExpressRoute-circuit.

Zie voor meer informatie [ExpressRoute-werkstromen voor circuitinrichting en circuitstatussen](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Zijn er connectiviteit grenzen voor mijn ExpressRoute-circuit?

Ja. Hallo [ExpressRoute-partners en locaties](expressroute-locations.md) artikel bevat een overzicht van Hallo connectiviteit grenzen voor een ExpressRoute-circuit. Verbinding voor een ExpressRoute-circuit is beperkt tooa één geopolitieke regio. Connectiviteit kan uitgevouwen toocross geopolitieke regio's worden doordat Hallo ExpressRoute premium-functie.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Kan ik toomore dan één virtueel netwerk tooan ExpressRoute-circuit koppelen

Ja. U kunt brengen van verbindingen van virtuele netwerken too10 op een standaard ExpressRoute-circuit en up too100 hebben op een [premium ExpressRoute-circuit](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Ik heb meerdere Azure-abonnementen die virtuele netwerken bevatten. Kan ik virtuele netwerken die zich in afzonderlijke abonnementen tooa één ExpressRoute-circuit verbinden?

Ja. U kunt autoriseren up too10 andere Azure-abonnementen toouse één ExpressRoute-circuit. Deze limiet kan worden verhoogd door in te schakelen Hallo ExpressRoute premium-functie.

Zie voor meer informatie [een ExpressRoute-circuit delen tussen meerdere abonnementen](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Virtuele netwerken verbonden toohello hetzelfde circuit geïsoleerd van elkaar zijn?

Nee. Vanuit een routering perspectief, alle virtuele netwerken gekoppelde toohello hetzelfde ExpressRoute-circuit deel uitmaken van hetzelfde routeringsdomein Hallo en zijn niet van elkaar geïsoleerd. Als u de isolatie versturen moet, moet u toocreate een afzonderlijke ExpressRoute-circuit.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Kan ik een virtueel netwerk verbonden toomore dan één ExpressRoute-circuit hebben?

Ja. U kunt één virtueel netwerk met up toofour ExpressRoute-circuits koppelen. Ze moeten worden geordend tot en met 4 verschillende [ExpressRoute-locaties](expressroute-locations.md).

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>Kan ik Hallo Internet openen vanuit Mijn virtuele netwerken verbonden tooExpressRoute circuits?

Ja. Als u hebt niet aangekondigd standaardroutes (0.0.0.0/0) of Internet route adresvoorvoegsels via Hallo BGP-sessie, kunt u toohello Internet vanaf een virtueel netwerk gekoppelde tooan ExpressRoute-circuit.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Kan ik Internet connectiviteit toovirtual netwerken verbonden tooExpressRoute circuits blokkeren?

Ja. U kunt standaard routes (0.0.0.0/0) tooblock alle Internet connectiviteit toovirtual machines geïmplementeerd in een virtueel netwerk en alle verkeer van via ExpressRoute-circuit Hallo routeren adverteren.

Als u standaardroutes bekendmaakt, dwingt we verkeer tooservices die worden aangeboden via openbare peering (zoals Azure-opslag en SQL-database) back tooyour premises. U hebt uw tooAzure routers tooreturn verkeer via de Hallo-pad voor openbare peering of via Internet Hallo tooconfigure.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Kan de gekoppelde toohello virtuele netwerken hetzelfde ExpressRoute-circuit praten tooeach andere?

Ja. Virtuele machines geïmplementeerd in virtuele netwerken verbonden toohello hetzelfde ExpressRoute-circuit met elkaar kan communiceren.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Kan ik site-naar-site-connectiviteit voor virtuele netwerken in combinatie met ExpressRoute gebruiken?

Ja. ExpressRoute kan worden gecombineerd met site-naar-site VPN-verbindingen.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Kan ik een virtueel netwerk verplaatsen van de site-naar-site / punt-naar-site-configuratie toouse ExpressRoute?

Ja. Hebt u toocreate een ExpressRoute-gateway in uw virtuele netwerk. Er is een kleine uitvaltijd die zijn gekoppeld aan het Hallo-proces.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Waarom is er een openbaar IP-adres die zijn gekoppeld aan Hallo ExpressRoute-gateway op een virtueel netwerk?

Hallo openbaar IP-adres wordt gebruikt voor interne management alleen. Dit openbare IP-adres is niet blootgestelde toohello Internet en geen vormt een beveiligingsrisico van het virtuele netwerk.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Wat kan ik tooconnect tooAzure opslag nodig via ExpressRoute?

U moet een ExpressRoute-circuit maken en configureren van routes voor openbare peering.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Zijn er beperkingen met betrekking tot Hallo aantal routes die ik kunt adverteren?

Ja. We accepteren van too4000 route voorvoegsels voor persoonlijke peering en 200 voor openbare peering en Microsoft-peering. 000 routes voor persoonlijke peering als u Hallo ExpressRoute premium-functie inschakelt, kunt u deze too10 verhogen.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Zijn er beperkingen voor IP-adresbereiken die ik via Hallo BGP-sessie kunt adverteren?

We accepteren geen persoonlijke voorvoegsels (RFC1918) in Hallo openbare en Microsoft-peering BGP-sessie.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Wat gebeurt er als ik Hallo BGP overschrijden?

BGP-sessies worden verwijderd. Ze worden opnieuw ingesteld zodra het Hallo-voorvoegsel aantal gaat Hallo limiet.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Wat is ExpressRoute BGP houdt tijd Hallo? Kan het worden aangepast?

Hallo wachtstand tijd is 180. Hallo keepalive-berichten worden verzonden om de 60 seconden. Deze worden instellingen opgelost op Hallo Microsoft side die niet kan worden gewijzigd. Het is mogelijk dat u andere timers tooconfigure en Hallo BGP-Sessieparameters wordt onderhandeld over dienovereenkomstig.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Nadat het adverteren van Hallo standaard route (0.0.0.0/0) toomy virtuele netwerken, kan ik mijn Azure VM's waarop Windows niet activeren. Hoe tooI dit oplossen?

Hallo volgende stappen uit te herkennen activeringsaanvraag hello Azure:

1. Tot stand brengen Hallo openbare-peering voor uw ExpressRoute-circuit.
2. Een DNS-zoekopdracht uitvoeren en Hallo IP-adres vinden met **kms.core.windows.net**
3. Hallo Key Management Service moet herkennen die activeringsaanvraag Hallo afkomstig is van Azure en eer Hallo aanvraag. Voer een van de Hallo drie taken te volgen:

   * Op uw on-premises netwerk route Hallo verkeer dat is bestemd voor Hallo IP-adres dat u hebt verkregen in stap 2 back tooAzure via openbare peering Hallo.
   * Uw NSP provider haar pincode Hallo verkeer back tooAzure via openbare peering Hallo hebben.
   * Een door de gebruiker gedefinieerde route die punten Hallo IP met Internet, zoals een volgende hop maken en toepassen toohello subnetten waar deze virtuele machines zijn.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Kan ik Hallo bandbreedte van een ExpressRoute-circuit wijzigen?

Ja, kunt u proberen tooincrease Hallo bandbreedte van uw ExpressRoute-circuit in hello Azure-portal of met behulp van PowerShell. Als er capaciteit is beschikbaar op Hallo van de fysieke poort waarop uw circuit is gemaakt, wordt uw wijziging slaagt. 

Als de wijziging is mislukt, betekent dit ofwel er niet voldoende capaciteit links op de huidige poort Hallo en moet u een nieuwe ExpressRoute-circuit met hogere bandbreedte Hallo toocreate, of dat er is geen extra capaciteit op die locatie, in dat geval kan het niet mogelijk tooincrease hello bandbreedte. 

Ook hebt u toofollow up met uw provider connectiviteit tooensure dat ze Hallo vertragingen in hun netwerken toosupport Hallo bandbreedte toename bijwerkt. U kunt Hallo bandbreedte van uw ExpressRoute-circuit echter niet, reduceren. U hebt toocreate een nieuwe ExpressRoute-circuit met lagere bandbreedte en verwijderen van oude Hallo-circuit.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Hoe wijzig ik de bandbreedte Hallo van een ExpressRoute-circuit?

U kunt bandbreedte van Hallo ExpressRoute-circuit met de REST-API of PowerShell cmdlet Hallo Hallo bijwerken.

## <a name="expressroute-premium"></a>ExpressRoute premium

### <a name="what-is-expressroute-premium"></a>Wat is ExpressRoute premium?

ExpressRoute premium is een verzameling van Hallo volgende kenmerken:

* Routering tabel heeft limiet verhoogd van 4000 routes too10, 000 routes voor persoonlijke peering.
* Aantal vnet's die verbonden toohello ExpressRoute-circuit worden kunnen verhoogd (de standaardwaarde is 10). Zie voor meer informatie, Hallo [ExpressRoute limieten](#limits) tabel.
* Connectiviteit tooOffice 365 en Dynamics 365.
* Globale connectiviteit via Hallo Microsoft Basisnetwerk. U kunt nu een VNet in een geopolitieke regio een ExpressRoute-circuit in een andere regio koppelen.<br>
    **Voorbeelden:**

    *  U kunt een VNet gemaakt in West-Europa tooan ExpressRoute-circuit in Silicon Valley gemaakt koppelen. 
    *  Op Hallo openbare peering, worden de voorvoegsels van andere geopolitieke regio's worden geadverteerd zodat u op verbinding, bijvoorbeeld SQL Azure in West-Europa een circuit in Silicon Valley maken kan.


### <a name="limits"></a>Hoeveel VNets kan ik koppelen tooan ExpressRoute-circuit als ik ExpressRoute premium ingeschakeld?

Hallo volgende tabellen tonen Hallo ExpressRoute limieten en Hallo aantal VNets per ExpressRoute-circuit:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Hoe kan ik ExpressRoute premium inschakelen?

Premium-functies voor ExpressRoute kunnen worden ingeschakeld wanneer het Hallo-functie is ingeschakeld en kunnen worden afgesloten door Hallo circuit status bij te werken. U kunt ExpressRoute premium inschakelen tijdens de aanmaak van circuit of Hallo REST-API kan aanroepen / PowerShell-cmdlet.

### <a name="how-do-i-disable-expressroute-premium"></a>Hoe kan ik ExpressRoute premium uitschakelen?

U kunt ExpressRoute premium uitschakelen door het aanroepen van Hallo REST-API of PowerShell-cmdlet. U moet ervoor zorgen dat u de standaardlimiet voor connectiviteit behoeften toomeet Hallo hebt aangepast voordat u ExpressRoute premium uitschakelen. Als het gebruik van uw schaalt buiten de standaardlimiet Hallo, mislukt de Hallo aanvraag toodisable ExpressRoute premium.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>Kan ik kies ik wil van premium-functieset Hallo Hallo-functies?

Nee. Hallo-functies, kan niet worden opgenomen. We kunnen alle functies inschakelen wanneer u ExpressRoute premium inschakelen.

### <a name="how-much-does-expressroute-premium-cost"></a>Wat kost ExpressRoute premium?

Raadpleeg te[prijsinformatie](https://azure.microsoft.com/pricing/details/expressroute/) voor kosten.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Betaal ik voor ExpressRoute premium bovendien toostandard kosten ExpressRoute?

Ja. ExpressRoute premium gelden boven op het ExpressRoute-circuit kosten en kosten die door de connectiviteitsprovider Hallo vereist.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute voor Office 365 en Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Hoe maak ik een ExpressRoute-circuit tooconnect tooOffice 365-services en Dynamics 365?

1. Bekijk Hallo [ExpressRoute vereisten pagina](expressroute-prerequisites.md) toomake zeker dat u voldoet aan de vereisten Hallo.
2. tooensure waarvoor u de verbinding in orde wordt voldaan, bekijkt hello lijst met serviceproviders en locaties in Hallo [ExpressRoute-partners en locaties](expressroute-locations.md) artikel.
3. Aan de hand van plan bent uw capaciteitsvereisten [netwerkplanning en prestatieafstemming voor Office 365](http://aka.ms/tune/).
4. Hallo stappen die worden vermeld in Hallo werkstromen tooset connectiviteit [ExpressRoute-werkstromen voor circuitinrichting en circuitstatussen](expressroute-workflows.md).

> [!IMPORTANT]
> Zorg ervoor dat u premium-invoegtoepassing voor ExpressRoute hebt ingeschakeld bij het configureren van connectiviteit tooOffice 365 services en Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>Heb ik nodig Azure tooenable openbare peering tooconnect tooOffice 365 services en Dynamics 365?

Nee, hoeft u alleen tooenable Microsoft-Peering. Verificatie verkeer tooAzure AD verzonden via Microsoft-Peering. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>Kunnen mijn bestaande ExpressRoute-circuits ondersteuning voor connectiviteit tooOffice 365 services en Dynamics 365?

Ja. Uw bestaande ExpressRoute-circuit kan worden geconfigureerd toosupport connectiviteit tooOffice 365 services. Zorg ervoor dat er voldoende capaciteit tooconnect tooOffice 365 services en dat u premium-invoegtoepassing hebt ingeschakeld. [Netwerkplanning en prestatieafstemming voor Office 365](http://aka.ms/tune/) helpt u van plan bent uw verbinding nodig heeft. Zie ook [maken en een ExpressRoute-circuit wijzigen](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Welke Office 365 services toegankelijk is via een ExpressRoute-verbinding?

Raadpleeg te[Office 365-URL's en IP-adresbereiken](http://aka.ms/o365endpoints) pagina voor een bijgewerkte lijst met services die via ExpressRoute worden ondersteund.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Hoeveel ondersteunt ExpressRoute voor Office 365-services en de kosten van Dynamics 365?

Office 365-services en Dynamics 365 moet premium-invoegtoepassing toobe is ingeschakeld. Zie Hallo [detailpagina met prijzen](https://azure.microsoft.com/pricing/details/expressroute/) voor kosten.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Welke regio's wordt ExpressRoute voor Office 365 ondersteund?

Zie [ExpressRoute-partners en locaties](expressroute-locations.md) voor meer informatie.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>Heb ik toegang tot Office 365 via Hallo Internet, zelfs als ExpressRoute is geconfigureerd voor mijn organisatie?

Ja. Office 365-service-eindpunten kunnen worden bereikt via Internet, Hallo Hoewel ExpressRoute is geconfigureerd voor uw netwerk. Als u zich in een locatie die is geconfigureerd tooconnect tooOffice 365 services via ExpressRoute, maakt u verbinding via ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Kan ik Office 365 US Government Community (GCC) services openen via een Azure US Government ExpressRoute-circuit?

Ja. Office 365 GCC service-eindpunten kunnen worden bereikt via hello Azure US Government ExpressRoute. Echter, Hallo u eerste nodig tooopen een ondersteuningsticket in Azure portal tooprovide Hallo voorvoegsels die u van plan bent tooadvertise tooMicrosoft. Uw verbinding tooOffice 365 GCC services worden vastgesteld na het Hallo-ondersteuningsticket is opgelost. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Dynamics 365 voor bewerkingen (voorheen bekend als Dynamics AX Online) toegankelijk is via een ExpressRoute-verbinding?

Ja. [Dynamics 365 voor bewerkingen](https://www.microsoft.com/dynamics365/operations) wordt gehost op Azure. U kunt inschakelen om openbare Azure-peering op uw ExpressRoute-circuit tooconnect tooit.

## <a name="route-filters-for-microsoft-peering"></a>Routefilters voor Microsoft-peering

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Ik ben inschakelen van de Microsoft-peering voor Hallo eerst, welke routes ik zien?

U ziet alle routes. U hebt een voorvoegsel van aankondigingen van routes filter tooyour circuit toostart tooattach. Zie voor instructies [routefilters configureren voor Microsoft-peering](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>Ik deze optie is ingeschakeld op de Microsoft-peering en nu ik poging tooselect Exchange Online ben, maar het geeft mij een fout die ik wil niet geautoriseerde toodo.

Wanneer u routefilters gebruikt, kunt elke klant inschakelen Microsoft-peering. Voor Office 365-services worden verbruikt, moet u echter nog steeds tooget geautoriseerd door Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Moet ik tooget autorisatie Dynamics 365 kunt inschakelen via het Microsoft-peering?

Nee, u hoeft niet autorisatie voor Dynamics 365. U kunt een regel maken en selecteer Dynamics 365 community zonder toestemming.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Ik heb al Microsoft-peering, hoe kan ik profiteren van routefilters?

U kunt een routefilter maken, selecteer Hallo services u wilt toouse en koppel Hallo filter tooyour Microsoft-peering. Zie voor instructies [routefilters configureren voor Microsoft-peering](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Ik heb Microsoft-peering op één locatie nu tooenable probeer op een andere locatie en ik ben geen voorvoegsels niet zien.

* Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.

* Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit. Standaard worden er geen voorvoegsels.
