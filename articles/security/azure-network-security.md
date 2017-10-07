---
title: aaaAzure netwerkbeveiliging | Microsoft Docs
description: Meer informatie over cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure-netwerkbeveiliging

We weten dat beveiliging taak in de cloud Hallo en het is belangrijk dat u tijdig en informatie over Azure-beveiliging. Een van de Hallo beste redenen-toouse Azure voor uw toepassingen en services is tootake profiteren van Azure breed scala aan mogelijkheden en hulpprogramma's voor beveiliging. Deze hulpprogramma's en mogelijkheden helpen mogelijke toocreate veilige oplossingen maken op Hallo Azure-platform.

Microsoft Azure biedt vertrouwelijkheid, integriteit en beschikbaarheid van klantgegevens, maar ook transparante accountability. toohelp u beter te begrijpen Hallo netwerk beveiligingsmechanismen geïmplementeerd in Microsoft Azure vanuit het perspectief van de klant Hallo van verzameling, geschreven in dit artikel, 'Azure Network Security' tooprovide uitgebreide bekijkt hello netwerkbeveiliging besturingselementen die beschikbaar zijn met Microsoft Azure.

Dit artikel is bedoeld tooinform u over Hallo breed scala aan netwerk die u bepaalt tooenhance Hallo beveiliging van Hallo-oplossingen die u implementeert in Azure kunt configureren. Als u geïnteresseerd bent in wat Microsoft toosecure Hallo netwerk infrastructuurresources van Hallo Azure-platform zelf, Zie hello Azure-Beveiligingssectie in Hallo [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Azure-platform

Azure is een openbare cloud service-platform die ondersteuning biedt voor een brede selectie van besturingssystemen, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten.  Linux-containers kan worden uitgevoerd met Docker-integratie; bouwen van apps met JavaScript, Python, .NET, PHP, Java en Node.js; Build back-ends voor iOS, Android en Windows apparaten. Azure-cloudservices ondersteuning Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen.

Wanneer u bouwen op of IT-middelen migreren naar een openbare cloud serviceprovider, u zijn afhankelijk van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met services en Hallo besturingselementen Hallo opgeven deze toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven kunnen voldoen aan de beveiligingsvereisten. Bovendien Azure biedt een uitgebreide verzameling configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw organisatie implementaties kunt aanpassen.

## <a name="abstract"></a>Abstracte

Microsoft openbare cloud-services leveren hyperschaal services en -infrastructuur, bedrijfsniveau mogelijkheden en veel keuzes voor hybride verbindingen. U kunt deze services via Internet Hallo of met Azure ExpressRoute, waarmee u verbinding met het particuliere netwerk tooaccess. Hallo Microsoft Azure-platform, kunt u tooseamlessly uw infrastructuur in Hallo cloud uitbreiden en het bouwen van meerdere lagen architecturen. Bovendien kunt derden uitgebreide mogelijkheden inschakelen door het aanbieden van beveiligingsservices en virtuele apparaten.

Azure netwerkservices maximaliseren flexibiliteit, beschikbaarheid, tolerantie, beveiliging en integriteit standaard. Dit technisch document bevat informatie over de netwerkfuncties Hallo van Azure en informatie over hoe Azure systeemeigen beveiliging functies toohelp in klanten gebruiken kunnen hun informatie-assets beveiligen.

Hallo bedoeld doelgroepen voor dit technisch document opnemen:

- Technische managers, netwerkbeheerders en ontwikkelaars die op zoek bent naar beveiligingsoplossingen beschikbaar en ondersteund in Azure.

-   Kleine en middelgrote ondernemingen of proces leidinggevenden willen tooget een overzicht op hoog niveau hello Azure netwerktechnologieën en services die relevant voor discussies over netwerkbeveiliging in hello Azure openbare cloud zijn.

## <a name="azure-networking-big-picture"></a>Azure networking grote afbeelding
Microsoft Azure omvat een robuuste netwerken infrastructuur toosupport uw toepassing en de vereisten voor service-connectiviteit. Netwerkverbinding is tussen de bronnen in Azure, tussen on-premises en Azure gehoste bronnen, en tooand van Hallo Internet en Azure.

![Azure Networking grote afbeelding](media/azure-network-security/azure-network-security-fig-1.png)

Hallo [Azure netwerkinfrastructuur](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) schakelt u toosecurely andere Azure-resources tooeach verbinding met virtuele netwerken (vnet's). Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure-cloud netwerk toegewezen tooyour abonnement. U kunt VNets tooyour on-premises netwerken kunt verbinden.

Azure ondersteunt toegewezen WAN-koppeling connectiviteit tooyour on-premises netwerk en een Azure-netwerk met [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Hallo koppeling tussen Azure en uw site maakt gebruik van een speciale verbinding die verloopt niet Hallo via openbaar Internet. Als uw Azure-toepassing wordt uitgevoerd in meerdere datacenters, kunt u [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute aanvragen van gebruikers op intelligente wijze over exemplaren van de toepassing hello. U kunt ook verkeer tooservices niet wordt uitgevoerd in Azure als ze toegankelijk vanaf Internet Hallo zijn versturen.

## <a name="enterprise-view-of-azure-networking-components"></a>Enterprise-weergave van Azure netwerkonderdelen
Azure heeft veel netwerkonderdelen die relevant toonetwork beveiliging discussies zijn. we deze netwerkonderdelen beschrijven en de focus op Hallo beveiliging gerelateerde toothem uitgeeft.

> [!Note]
> Niet alle aspecten van de Azure-netwerken worden beschreven: bespreken we alleen de toobe belangrijke meegenomen in plannen en ontwerpen van een veilige netwerkinfrastructuur rond uw services en toepassingen die u in Azure implementeert.

In dit artikel wordt worden behandeld Hallo volgende Azure enterprise netwerkmogelijkheden:

-   Netwerkverbinding

-   Hybride verbindingen

-   Beveiligingsmechanismen

-   Netwerkvalidatie van het

### <a name="basic-network-connectivity"></a>Netwerkverbinding

Hallo [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) service kunt u toosecurely andere Azure-resources tooeach verbinding met virtuele netwerken (VNet). Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure-infrastructuur toegewezen tooyour netwerkabonnement. U kunt ook verbinding maken met andere VNets tooeach en tooyour on-premises netwerken die gebruikmaken van de site-naar-site VPN-verbindingen en toegewezen [WAN-koppelingen](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Netwerkverbinding](media/azure-network-security/azure-network-security-fig-2.png)

Hallo begrijpen VMs toohost servers te gebruiken in Azure, is Hallo vraag hoe deze VMs tooa netwerk zijn verbonden. Hallo antwoord is dat virtuele machines verbinding maken met tooan [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Azure virtuele netwerken zijn zoals Hallo virtuele u netwerken lokale gebruiken met uw eigen virtualisatieoplossingen platform, zoals Microsoft Hyper-V- of VMware.

#### <a name="intra-vnet-connectivity"></a>Intra-VNet-connectiviteit

U verbinding kunt maken met andere VNets tooeach, resources inschakelen tooeither VNet toocommunicate met elkaar verbonden via VNets. U kunt een of beide van de volgende opties tooconnect VNets tooeach andere hello gebruiken:

- **Peering:** kunnen bronnen verbonden toodifferent Azure VNets binnen Hallo dezelfde Azure-locatie toocommunicate met elkaar. Hallo bandbreedte en de latentie tussen vnet Hallo Hallo dezelfde alsof Hallo resources verbonden toohello hetzelfde VNet. lezen van toolearn meer informatie over peering, [virtuele netwerk peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Peering](media/azure-network-security/azure-network-security-fig-3.png)

- **VNet-naar-VNet-verbinding:** kunnen bronnen verbonden Azure VNet toodifferent binnen Hallo dezelfde of verschillende Azure-locaties. In tegenstelling tot de peering, is bandbreedte tussen VNets beperkt, omdat het verkeer door een Azure VPN-Gateway moet lopen.

![VNet-naar-VNet-verbinding](media/azure-network-security/azure-network-security-fig-4.png)


meer over het VNets verbinden met een VNet-naar-VNet-verbinding, Hallo lezen toolearn [configureren van een VNet-naar-VNet-verbinding artikel](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Mogelijkheden voor virtuele Azure-netwerk:

Zoals u zien kunt, biedt een virtueel netwerk van Azure virtuele machines tooconnect toohello netwerk zodat ze verbinding met netwerkbronnen tooother op een veilige wijze maken kunnen. Basic-connectiviteit is echter alleen Hallo begin. Hallo blootstellen volgende mogelijkheden van Azure Virtual Network service Hallo beveiligingskenmerken van hello Azure Virtual Network:

-   Isolatie

-   Internetconnectiviteit

-   Azure-resource-connectiviteit

-   VNet-connectiviteit

-   On-premises connectiviteit

-   Filteren van verkeer

-   Routering

**Isolatie**

Vnet's zijn [geïsoleerde](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) van elkaar. U kunt afzonderlijke VNets voor ontwikkeling, testen en productie gebruik Hallo dezelfde maken [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) blokken adres. Als u daarentegen, kunt u meerdere VNets die gebruikmaken van verschillende CIDR-adresblokken en netwerken met elkaar verbinden. U kunt een VNet segmenteren in meerdere subnetten.

Azure biedt interne naamomzetting voor VM's en [Cloudservices](https://azure.microsoft.com/services/cloud-services/) rolinstanties verbonden tooa VNet. U kunt een VNet-toouse desgewenst uw eigen DNS-servers, in plaats van Azure interne naamomzetting configureren.

U kunt meerdere VNets binnen elke Azure implementeren [abonnement](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) en Azure [regio](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json). Elke VNet is geïsoleerd van andere vnet's. U kunt voor elk VNet:

-   Geef een aangepaste persoonlijke IP-adresruimte met behulp van openbare en persoonlijke (RFC 1918)-adressen. Azure wijst bronnen verbonden toohello VNet een particulier IP-adres van de adresruimte hello, u toewijzen.

-   Segmenteer Hallo VNet in een of meer subnetten en een deel van Hallo VNet-ruimte tooeach adressubnet toewijzen.

-   Gebruik Azure verschafte naamomzetting of geef dat uw eigen DNS-server voor gebruik door resources verbonden tooa VNet. meer informatie over naamomzetting in vnet's, Hallo lezen toolearn [naamomzetting voor VM's en Cloudservices](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Verbinding met internet**

Alle [Azure virtuele Machines (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) en Cloud Services-rolexemplaren verbonden tooa VNet hebben toegang tot Internet, toohello standaard. U kunt ook een inkomend toospecific resources, inschakelen indien nodig. (VM) en Cloud Services-rolexemplaren verbonden tooa VNet hebben toegang tot Internet, toohello standaard. U kunt ook een inkomend toospecific resources, inschakelen indien nodig.

Alle resources verbonden tooa VNet hebben uitgaande verbinding toohello Internet standaard. Hallo privé IP-adres van bron Hallo is Bronnetwerk adres (snat omzetten) tooa openbaar IP-adres vertaald door hello Azure-infrastructuur. U kunt Hallo standaard connectiviteit wijzigen door het implementeren van aangepaste Routering en het filteren van verkeer. meer informatie over uitgaande internetverbinding lezen Hallo toolearn [inzicht in uitgaande verbindingen in Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate inkomende tooAzure resources uit Hallo Internet of toocommunicate uitgaande toohello Internet zonder snat omzetten, een resource moet een openbaar IP-adres worden toegewezen. meer informatie over openbare IP-adressen, Hallo lezen toolearn [openbare IP-adressen](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Azure-resource-connectiviteit**

[Azure-resources](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) zoals Cloudservices en virtuele machines kunnen worden verbonden toohello hetzelfde VNet. Hallo resources verbinding kunnen maken van andere tooeach met particuliere IP-adressen, zelfs als ze zich in verschillende subnetten. Azure biedt standaardroutering tussen subnetten, VNets en on-premises netwerken, zodat u niet tooconfigure hebt en beheren van routes.

U kunt verschillende Azure-resources tooa VNet, zoals virtuele Machines (VM), Cloud Services-App Service-omgevingen en virtuele-Machineschaalsets verbinden. Virtuele machines verbinding tooa subnet binnen een VNet maken via een netwerkinterface (NIC). meer informatie over NIC's, Hallo lezen toolearn [netwerkinterfaces](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**VNet-connectiviteit**

[VNets](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) , kunt u verbonden tooeach andere bronnen inschakelen tooany VNet toocommunicate verbonden met een resource op een andere VNet.

U verbinding kunt maken met andere VNets tooeach, resources inschakelen tooeither VNet toocommunicate met elkaar verbonden via VNets. U kunt een of beide van de volgende opties tooconnect VNets tooeach andere hello gebruiken:

- **Peering:** kunnen bronnen verbonden toodifferent Azure VNets binnen Hallo dezelfde Azure-locatie toocommunicate met elkaar. Hallo bandbreedte en de latentie tussen VNets is hetzelfde als als Hallo bronnen zijn verbonden toohello Hallo Hallo dezelfde VNet.toolearn meer informatie over peering, lezen Hallo [virtuele netwerk peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **VNet-naar-VNet-verbinding:** kunnen bronnen verbonden Azure VNet toodifferent binnen Hallo dezelfde of verschillende Azure-locaties. In tegenstelling tot de peering, is bandbreedte tussen VNets beperkt, omdat het verkeer door een Azure VPN-Gateway moet lopen. toolearn meer over het VNets verbinden met een VNet-naar-VNet-verbinding. meer lezen Hallo toolearn [een VNet-naar-VNet-verbinding configureren](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**On-premises connectiviteit**

Vnet's te kunnen worden verbonden[lokale](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) netwerken via persoonlijke netwerkverbindingen tussen uw netwerk en Azure of een site-naar-site VPN-verbinding via Internet Hallo.

U kunt verbinding maken uw lokale netwerk tooa VNet met elke combinatie van Hallo volgende opties:

- **Punt-naar-site virtueel particulier netwerk (VPN):** tot stand gebracht tussen een enkele PC verbonden tooyour netwerk en Hallo VNet. Dit verbindingstype is handig als u alleen aan de slag met Azure of voor ontwikkelaars, omdat hiervoor weinig of geen wijzigingen tooyour bestaande netwerk. Hallo-verbinding gebruikt Hallo SSTP protocol tooprovide gecodeerde communicatie via Internet Hallo tussen Hallo PC en Hallo VNet. Hallo latentie voor een punt-naar-site VPN-verbinding is onvoorspelbare aangezien Hallo verkeer Hallo Internet passeert.

- **Site-naar-site-VPN:** tot stand gebracht tussen uw VPN-apparaat en een Azure VPN-Gateway. Dit verbindingstype kunt een on-premises-resource autoriseren van tooaccess een VNet. Hallo-verbinding is een VPN IPsec/IKE waarmee gecodeerde communicatie via Internet Hallo tussen uw on-premises apparaat en hello Azure VPN-gateway. Hallo latentie voor een site-naar-site-verbinding is onvoorspelbare aangezien Hallo verkeer Hallo Internet passeert.

- **Azure ExpressRoute:** tot stand gebracht tussen uw netwerk en Azure, via een ExpressRoute-partner. Deze verbinding is een privéverbinding. Verkeer komt geen Hallo Internet passeren. Hallo latentie voor een ExpressRoute-verbinding is voorspelbaar omdat verkeer Hallo Internet niet passeren. meer informatie over alle Hallo vorige verbindingsopties lezen Hallo toolearn [gatewayverbindingsdiagrammen topologie](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Verkeer filteren**

Virtuele machine en Cloud Services-rolexemplaren [netwerkverkeer](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) kunnen binnenkomende en uitgaande worden gefilterd op de bron-IP-adres en poort, doel-IP-adres en poort en protocol.

U kunt filteren netwerkverkeer tussen subnetten op met behulp van een of beide Hallo volgende opties:

- **Netwerkbeveiligingsgroepen (NSG):** elke NSG kan meerdere binnenkomende en uitgaande beveiligingsregels voor verbindingen die u in staat toofilter verkeer door de bron en doel-IP-adres, poort en protocol stellen bevatten. U kunt een NSG tooeach NIC op een virtuele machine kunt toepassen. U kunt ook een NSG toohello subnet een NIC of andere Azure-resource is verbonden met. meer informatie over nsg's, Hallo lezen toolearn [Netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Virtuele netwerkapparaten:** een virtueel netwerk-apparaat is een virtuele machine uitvoeren van software waarmee een netwerkfunctie, zoals een firewall. Een lijst met beschikbare NVAs weergeven in hello Azure Marketplace. NVAs zijn ook beschikbaar met WAN-optimalisatie en andere netwerkapparaten verkeer functies. NVAs worden doorgaans gebruikt voor de gebruiker gedefinieerde of BGP-routes. U kunt ook een NVA toofilter-verkeer tussen vnet's gebruiken.

**Routering**

U kunt eventueel Azure standaard routering met BGP-routes via een netwerkgateway of configureren van uw eigen routes overschrijven.

Azure maakt routetabellen waarmee bronnen verbonden tooany subnet in een VNet toocommunicate met elkaar, standaard. U kunt ofwel implementeren of beide volgende opties toooverride Hallo Hallo standaardroutes die Azure maakt:

- **Gebruiker gedefinieerde routes:** kunt u aangepaste routetabellen met routes die regelen waarin verkeer wordt gerouteerd toofor elk subnet. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [gebruiker gedefinieerde routes](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **BGP-routes:** als u verbinding maakt met uw VNet tooyour on-premises netwerk via een Azure VPN-Gateway of ExpressRoute-verbinding, BGP-routes tooyour vnet's kunnen worden doorgegeven.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Hybride verbinding met internet: tooan on-premises netwerk verbinding maken
U kunt verbinding maken uw lokale netwerk tooa VNet met elke combinatie van Hallo volgende opties:

-   Internetconnectiviteit

-   Punt-naar-site VPN (P2S VPN)

-   Site-naar-Site VPN (S2S VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Verbinding met Internet

Als de naam ervan wordt voorgesteld, toegankelijk verbinding met Internet uw workloads van Hallo Internet, doordat u verschillende openbare eindpunten tooworkloads die in het virtuele netwerk Hallo live beschikbaar. Deze werkbelastingen kunnen worden blootgesteld met [Internet gerichte Load Balancer](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) of toohello VM gewoon toewijzen van een openbare IP-adres. Op deze manier wordt deze mogelijk voor op Hallo Internet toobe kunnen tooreach alles opgegeven dat de virtuele machine, een hostfirewall [netwerkbeveiligingsgroepen (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), en [zelfgedefinieerde Routes](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) toestaan die toohappen.

In dit scenario kan u een toepassing die toobe openbare toohello Internet behoeften beschikbaar en kunnen tooconnect tooit van overal of van specifieke locaties, afhankelijk van de configuratie van uw werkbelastingen Hallo.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>Punt-naar-Site VPN- of Site-naar-Site VPN
Deze twee valt in Hallo dezelfde categorie. Ze zowel uw VNet toohave een VPN-Gateway nodig en u kunt verbinding maken met behulp van een VPN-Client voor uw werkstation als onderdeel van Hallo tooit [punt-naar-Site-configuratie](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) of u kunt uw on-premises configureren [VPN-apparaat](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe kunnen tooterminate een site-naar-site-VPN. Op deze manier on-premises apparaten kunnen verbinding maken tooresources binnen Hallo VNet.

Een punt-naar-Site (P2S)-configuratie kunt u een beveiligde verbinding te maken van een individuele client computer tooa virtueel netwerk. P2S is een VPN-verbinding via SSTP (Secure Socket Tunneling Protocol).

![Punt-naar-Site VPN](media/azure-network-security/azure-network-security-fig-5.png)

Punt-naar-Site-verbindingen zijn nuttig wanneer de gewenste tooconnect tooyour VNet vanaf een externe locatie, zoals vanaf thuis of een conferentie center, of wanneer u slechts enkele clients hebt die tooconnect tooa-netwerk nodig hebt.

Voor P2S-verbindingen hebt u geen VPN-apparaat of een openbaar IP-adres nodig. U Hallo VPN-verbinding van de clientcomputer Hallo tot stand brengen. P2S wordt manier tooconnect tooAzure daarom niet aanbevolen als u een permanente verbinding van de vele on-premises apparaten en computers tooyour Azure-netwerk nodig.

![Site-naar-Site VPN](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Zie voor meer informatie over punt-naar-Site-verbindingen Hallo [punt-naar-Site VA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel.

Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit. Deze verbinding plaatsvindt Hallo van Internet en kunt u te 'tunnel' gegevens in een versleutelde verbinding tussen uw netwerk en Azure. Site-naar-site VPN is een beveiligde, volwassen technologie die is geïmplementeerd door bedrijven van elke grootte jarenlang. Tunnel-versleuteling wordt uitgevoerd met [IPsec-tunnelmodus](https://technet.microsoft.com/library/cc786385.aspx).

Site-naar-site VPN is een technologie voor het vertrouwde, betrouwbare en tot stand gebracht, verkeer binnen Hallo tunnel Hallo Internet passeren. Bovendien is de bandbreedte relatief beperkte tooa maximum van ongeveer 200 Mbps.

Als u een uitzonderlijke niveau van beveiliging of prestaties voor uw cross-premises verbindingen vereist, wordt u aangeraden dat u Azure ExpressRoute voor uw cross-premises-connectiviteit gebruiken. ExpressRoute is een speciale WAN koppeling tussen uw on-premises locatie of een Exchange-hostingprovider. Omdat dit een telco verbinding, worden uw gegevens niet via Hallo Internet worden verzonden en is daarom niet blootgestelde toohello potentiële risico's in de communicatie via Internet.

> [!Note]
> Zie voor meer informatie over VPN-gateways over [VPN-gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Specifieke WAN-verbinding
Microsoft Azure ExpressRoute kunt u uw on-premises netwerken in hello Azure via een speciale persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider uitbreiden.

ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. ExpressRoute-verbindingen toooffer kan dit meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo.

![ Specifieke WAN-verbinding](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Voor meer informatie over tooconnect de tooMicrosoft van uw netwerk met behulp van ExpressRoute, Zie [ExpressRoute connectiviteitsmodellen](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) en [technisch overzicht van ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Als met de Hallo site-naar-site VPN-opties kunt ExpressRoute u ook tooconnect tooresources die niet noodzakelijkerwijs in slechts één VNet. Afhankelijk van Hallo SKU, kunt u in feite too10 VNets verbinden. Als er Hallo [premium-invoegtoepassing](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), verbindingen tooup too100 vnet's zijn mogelijk, afhankelijk van de bandbreedte. meer informatie over wat dit soort verbindingen bekijken, zoals, lezen toolearn [gatewayverbindingsdiagrammen topologie](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Beveiligingsmechanismen
Een virtueel netwerk van Azure biedt een veilige, logische netwerk dat is geïsoleerd van andere virtuele netwerken en veel beveiligingsmechanismen die u voor uw on-premises netwerken ondersteunt. Klanten maken hun eigen structuur met behulp van: subnetten: ze hun eigen persoonlijke IP-adresbereik gebruiken, routetabellen configureren en beveiligingsgroepen, het netwerk toegangsbeheer (ACL's), gateways en virtuele apparaten toorun hun werkbelastingen in Hallo cloud.

Hallo volgen beveiligingsmechanismen die kunt u op uw virtuele Azure-netwerken gebruiken:

-   Netwerk-toegangsbeheer

-   Gebruiker gedefinieerde Routes

-   Beveiliging van netwerkapparaat

-   Application Gateway

-   Azure-Web Application Firewall

-   Network beschikbaarheid Control

#### <a name="network-access-controls"></a>Netwerk-toegangsbeheer
Hoewel hello Azure Virtual Network (VNet) de basis Hallo van Azure model voor netwerken vormt en isolatie en bescherming biedt, Hallo [Netwerkbeveiligingsgroep groepen (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) zijn Hallo belangrijkste hulpprogramma waarmee u tooenforce en beheer van netwerkverkeer regels op netwerkniveau Hallo.

![ Netwerk-toegangsbeheer](media/azure-network-security/azure-network-security-fig-8.png)


U kunt toegang door toestaan of weigeren van communicatie tussen Hallo werkbelastingen binnen een virtueel netwerk, van systemen op klantnetwerken via cross-premises-connectiviteit te controleren of directe communicatie met Internet.

Hallo-diagram zowel VNets en nsg's zich bevinden in een bepaalde laag in hello Azure algemene beveiliging stack, waarbij nsg's, UDR en virtuele netwerkapparaten gebruikte toocreate beveiliging grenzen tooprotect Hallo implementaties van toepassingen in Hallo beveiligd netwerk kunnen zijn.

Nsg's een 5-tuple tooevaluate verkeer wordt gebruikt (en worden gebruikt in Hallo regels die u configureert voor Hallo NSG):

-   [Bron en doel-IP-adres](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Bron- en doelserver poort](https://technet.microsoft.com/library/dd197515)

-   Protocol: [Transmission controleprotocol (TCP)](https://technet.microsoft.com/library/cc940037.aspx) of [User Datagram Protocol (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Dit betekent dat u kunt de toegang tussen een enkele virtuele machine en een groep van virtuele machines of een enkel VM-tooanother één virtuele machine, of tussen volledige subnetten. Houd er rekening mee dat dit eenvoudige filterregels voor pakketten, is niet volledig pakketinspecties opnieuw. Er is geen protocol validatie of het niveau van de id's of de mogelijkheid van de IP-Adressen in een Netwerkbeveiligingsgroep.

Een NSG wordt geleverd met enkele ingebouwde regels waarmee u houden moet rekening. Dit zijn:

-   **Alle verkeer binnen een specifieke virtuele netwerk:** alle virtuele machines op Hallo hetzelfde virtuele Azure-netwerk met elkaar communiceren.

-   **Azure load balancing tooinbound toestaan:** met deze regel kunnen het verkeer van alle bronadressen adres tooany bestemming voor hello Azure load balancer.

-   **Alle binnenkomende weigeren:** met deze regel blokkeert al het verkeer bron Hallo Internet die u expliciet zijn toegestaan.

-   **Toestaan dat alle verkeer uitgaand toohello Internet:** met deze regel kunnen virtuele machines tooinitiate verbindingen toohello Internet. Als u niet dat deze verbindingen geïnitieerd wilt, of u kunt een regel tooblock toocreate deze verbindingen afdwingen geforceerde tunneling.

#### <a name="system-routes-and-user-defined-routes"></a>Systeemroutes en door gebruiker gedefinieerde routes

Wanneer u virtuele machines (VM's) tooa virtueel netwerk (VNet) in Azure toevoegt, ziet u dat Hallo virtuele machines kunnen toocommunicate met elkaar via Hallo netwerk, automatisch worden. U hoeft niet toospecify een gateway, ondanks het feit Hallo virtuele machines in verschillende subnetten.

Hallo geldt ook voor communicatie vanaf Hallo VMs toohello Internet en zelfs tooyour on-premises netwerk wanneer u een hybride verbinding is tussen Azure tooyour eigenaar datacenter aanwezig is.

![Systeemroutes](media/azure-network-security/azure-network-security-fig-9.png)

Deze communicatiestroom is mogelijk omdat een reeks system routes toodefine hoe IP-verkeersstromen maakt gebruik van Azure. Systeemroutes bepalen de communicatiestroom Hallo in Hallo volgen scenario's:

-   Hallo van binnen hetzelfde subnet.

-   Van een subnet tooanother binnen een VNet.

-   Van virtuele machines toohello Internet.

-   Van een VNet tooanother VNet via een VPN-gateway.

-   Van een VNet tooanother VNet via VNet-Peering ([Service Chaining](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   Van een VNet tooyour on-premises netwerk via een VPN-gateway.

Veel bedrijven hebben strikte beveiliging en nalevingsvereisten waarvoor lokale inspectie van pakketten tooenforce alle netwerk specifieke beleidsregels. Azure biedt een mechanisme aangeroepen [geforceerde tunneling](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) dat verkeer van Hallo VMs tooon-premises routeert door een aangepaste route maken of door [Border Gateway Protocol (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) advertenties via ExpressRoute- of VPN.

Geforceerde tunneling in Azure wordt geconfigureerd via het virtuele netwerk zelfgedefinieerde routes (UDR). Omleiden van verkeer tooan lokale site wordt uitgedrukt als een standaardroute toohello Azure VPN-gateway.

Hallo volgende sectie vindt u Hallo beperking van het Hallo-routeringstabel en -routes voor een virtuele Azure-netwerk:

-   Elk virtueel netwerksubnet heeft een ingebouwd systeem-routeringstabel. Hallo system routeringstabel heeft Hallo volgende drie groepen van routes:

 -  **Lokale VNet routes:** rechtstreeks toohello bestemming virtuele machines in Hallo hetzelfde virtuele netwerk

 - **Op de lokale routes:** toohello Azure VPN-gateway

 -  **Standaardroute:** rechtstreeks toohello Internet. Pakketten die bestemd zijn toohello privé IP-adressen niet wordt gedekt door de vorige twee Hallo routes worden verwijderd.

-   U kunt met Hallo-release van de gebruiker gedefinieerde routes, een routering tabel tooadd een standaardroute maken en vervolgens koppelen Hallo routering tabel tooyour VNet subnet tooenable geforceerde tunneling op deze subnetten.

-   U moet tooset "standaardsite" tussen Hallo cross-premises lokale sites verbonden toohello virtueel netwerk.

-   Geforceerde tunneling moet worden gekoppeld aan een VNet met een VPN-gateway voor dynamische routering (geen statische gateway genoemd).

- ExpressRoute geforceerde tunneling via dit mechanisme niet is geconfigureerd, maar in plaats daarvan wordt ingeschakeld door kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies.

> [!Note]
> Zie voor meer informatie, Hallo [ExpressRoute-documentatie](https://azure.microsoft.com/documentation/services/expressroute/) voor meer informatie.

#### <a name="network-security-appliances"></a>Beveiliging van netwerkapparaten
Netwerkbeveiligingsgroepen en door de gebruiker gedefinieerde Routes kunt zorgen voor een zekere mate van netwerkbeveiliging op Hallo netwerk- en lagen Hallo [OSI-model](https://en.wikipedia.org/wiki/OSI_model), gaat er toobe situaties waarbij moet of wilt u tooenable beveiliging op een hoger niveau van de netwerkstack Hallo. In dergelijke situaties wordt aangeraden dat u een virtueel netwerk beveiligingsapparaten geleverd door Azure partners implementeert.

![Beveiliging van netwerkapparaten](./media/azure-network-security/azure-network-security-fig-10.png)

Azure-netwerk beveiligingsapparaten VNet beveiligings- en netwerkfuncties te verbeteren, en ze zijn beschikbaar via meerdere leveranciers via Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com). Deze virtuele beveiligingsapparaten kunnen geïmplementeerde tooprovide zijn:

-   Maximaal beschikbare firewalls

-   Inbraakdetectie voorkomen

-   Inbraakdetectie

-   Web application firewalls (WAFs)

-   WAN-optimalisatie

-   Routering

-   Taakverdeling

-   VPN

-   Certificaatbeheer

-   Active Directory

-   Multifactor-verificatie

#### <a name="application-gateway"></a>Toepassingsgateway

[Microsoft Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) is een toegewezen virtueel apparaat waarmee een toepassing levering controller (ADC) als een service.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-11.png)

Toepassingsgateway kunt u toooptimize web farm prestaties en beschikbaarheid door het offloaden van CPU intensief SSL-beëindiging toohello toepassingsgateway (SSL-offloading). Het bevat ook een andere laag 7 routering mogelijkheden, waaronder:

-   Round-robin distributie van het binnenkomende verkeer

-   Sessie cookies gebaseerde affiniteit

-   URL-pad gebaseerde routering

-   Mogelijkheid toohost meerdere websites achter één Application Gateway


Een [web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) is ook beschikbaar als onderdeel van de toepassingsgateway Hallo. Dit biedt bescherming tooweb toepassingen van algemene web beveiligingsproblemen en aanvallen. Application Gateway kan worden geconfigureerd als een Internetgericht gateway, interne enige gateway of een combinatie van beide.

Application Gateway WAF kan worden uitgevoerd in de modus voor detectie of te voorkomen. Er is een algemene gebruiksvoorbeeld voor beheerders toorun in detectie modus tooobserve verkeer voor schadelijke patronen. Zodra een potentiële aanvallen zijn gedetecteerd, schakelen tooprevention modus verdachte inkomend verkeer wordt geblokkeerd.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-12.png)

Bovendien Application Gateway WAF helpt u bij het bewaken van webtoepassingen tegen aanvallen met een realtime WAF logboek die is geïntegreerd met [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) en [Azure Security Center](https://azure.microsoft.com/services/security-center/) tootrack WAF waarschuwingen en trends gemakkelijk bewaken.

opgemaakte JSON-logboek Hallo gaat rechtstreeks van de klant toohello storage-account. U hebt volledige controle over deze logboeken en uw eigen bewaarbeleidsregels kunt toepassen.

U kunt ook deze logboeken opnemen in uw eigen analytics-systeem met [Azure Log integratie](https://aka.ms/AzLog). WAF Logboeken ook worden geïntegreerd met [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) zodat u de logboekanalyse OMS kunt tooexecute geavanceerde fijnmazig query's.

#### <a name="azure-web-application-firewall-waf"></a>Azure-web application firewall (WAF)

Webtoepassingen zijn steeds meer doelen van aanvallen die gebruikmaken van algemene bekende beveiligingsproblemen, zoals SQL-injectie, cross-site scripting aanvallen en andere aanvallen die worden weergegeven in Hallo [OWASP top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Zo wordt voorkomen dat dergelijke aanvallen in toepassing hello vereist strengere onderhoud, patchen en controle op meerdere lagen van de topologie van de servicetoepassing Hallo.

 ![Azure-Web Application Firewall (WAF)](./media/azure-network-security/azure-network-security-fig-13.png)

Een gecentraliseerde [web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) kunt beschermen tegen aanvallen via Internet en beveiligingsbeheer zonder eventuele wijzigingen in de toepassing.

Een WAF oplossing kan ook beveiligingsrisico tooa sneller reageren door een bekend beveiligingsprobleem met een centrale locatie en beveiliging van elk van de afzonderlijke webtoepassingen patchen. Bestaande toepassingsgateways kunnen eenvoudig toepassingsgateway voor geconverteerde tooa web application firewall is ingeschakeld worden.

#### <a name="network-availability-controls"></a>Beschikbaarheid netwerkfuncties

Er zijn verschillende opties toodistribute-netwerkverkeer met Microsoft Azure. Deze opties werken verschillend. Ze hebben een eigen functieset en ondersteunen verschillende scenario's. Ze kunnen elk afzonderlijk worden gebruikt, maar ook worden gecombineerd.

Hieronder worden Hallo netwerkfuncties beschikbaarheid:

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Azure Load balancer**

Biedt hoge beschikbaarheid en netwerkprestaties tooyour toepassingen. Het is een laag 4 (TCP, UDP) load balancer die binnenkomend verkeer over orde exemplaren van services gedefinieerd in een set met gelijke taakverdeling distribueert.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer kan worden geconfigureerd voor:

-   Taakverdeling saldo binnenkomende Internet verkeer toovirtual machines. Deze configuratie wordt ook wel [internetgerichte taakverdeling](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Load balance verkeer tussen virtuele machines in een virtueel netwerk, tussen virtuele machines in de cloud-services of tussen virtuele machines in een virtueel netwerk met cross-premises en lokale computers. Deze configuratie wordt ook wel [interne load balancing](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Doorsturen externe verkeer tooa specifieke virtuele machine.

Alle resources in de cloud Hallo moeten een openbare IP-adres toobe bereikbaar is vanaf Internet Hallo. Hallo-cloudinfrastructuur in Azure maakt gebruik van niet-routeerbare IP-adressen voor de bronnen. Azure maakt gebruik van NAT (Netwerkadresomzetting) met openbare IP-adressen toocommunicate toohello Internet.

 **Toepassingsgateway**

 Toepassingsgateway werkt op laag van de toepassing hello (laag 7 in Hallo OSI-netwerkstack verwijzing). Het fungeert als een reverse proxy-service wordt beëindigd Hallo clientverbinding en doorsturen van aanvragen tooback-end-eindpunten.

 **Het Traffic manager**

Microsoft Azure Traffic Manager kunt u toocontrol Hallo distributie van gebruikersverkeer voor service-eindpunten in verschillende datacenters. Service-eindpunten die worden ondersteund door Traffic Manager bevatten Azure virtuele machines, Web-Apps en cloudservices. U kunt Traffic Manager ook gebruiken met externe eindpunten die niet van Azure zijn.

Traffic Manager gebruikt Hallo System DNS (Domain Name) toodirect toohello van de meest geschikte eindpunt op basis clientaanvragen van een [verkeersroutering methode](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) en Hallo-status van het Hallo-eindpunten. Traffic Manager biedt een reeks verkeersroutering methoden toosuit verschillende groepen van toepassingen behoeften, eindpunt health [bewaking](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring), en automatische failover. Traffic Manager is een robuuste toofailure, met inbegrip van Hallo falen van een volledige Azure-regio.

Azure Traffic Manager kunt u toocontrol Hallo distributie van verkeer tussen de eindpunten van uw toepassing. Een eindpunt is een internetgerichte service die wordt gehost binnen of buiten Azure.

Traffic Manager biedt twee belangrijke voordelen:

-   Distributie van verkeer op basis van tooone van verschillende [verkeersroutering methoden](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Doorlopende bewaking van de status van endpoint](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) en automatische failover wanneer eindpunten mislukken.

Wanneer een client tooconnect tooa service probeert, moet deze eerst Hallo DNS-naam van Hallo service tooan IP-adres oplossen. Hallo-client maakt vervolgens verbinding toothat IP-adres tooaccess Hallo service. Traffic Manager maakt gebruik van DNS-toodirect clients toospecific service-eindpunten op basis van regels Hallo van Hallo verkeersroutering methode. Clients rechtstreeks verbinding gemaakt toohello ingeschakeld eindpunt. Traffic Manager is niet een proxy of gateway. Traffic Manager doorgeven tussen Hallo client- en Hallo Hallo-verkeer niet te zien.

### <a name="azure-network-validation"></a>Validatie van de Azure-netwerk

Validatie van de Azure-netwerk is tooensure die hello Azure-netwerk wordt uitgevoerd als deze is geconfigureerd en validatie kan worden gedaan met behulp van Hallo services en functies beschikbaar toomonitor Hallo netwerk. Met Azure-netwerk-Watcher u toegang hebt tot een breed spectrum van logboekregistratie en diagnostische mogelijkheden waarmee u met insights toounderstand uw netwerkervaring voor prestaties en de status. Deze mogelijkheden zijn toegankelijk via de Portal, Power Shell, CLI, Rest-API en SDK.

Azure bedrijfsbeveiliging verwijst toohello services, besturingselementen en functies beschikbaar toousers voor het beveiligen van hun gegevens, toepassingen en andere elementen in Microsoft Azure. Azure operationele beveiliging is gebaseerd op een framework dat Hallo kennis die is opgedaan met een verschillende mogelijkheden die de unieke tooMicrosoft, met inbegrip van Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Centre Hallo Hallo zijn opgenomen programma en grondige kennis van Hallo cyberbeveiliging security threat Liggend.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure-netwerk-watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure Storage analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Azure resourcemanager

Hallo mensen en processen die Microsoft Azure werken zijn mogelijk Hallo belangrijkste beveiligingsfunctie van Hallo-platform. Deze sectie beschrijft de functies van de globale datacenterinfrastructuur van Microsoft die helpen verbeteren en onderhouden van beveiliging, bedrijfscontinuïteit en privacy.

Hallo-infrastructuur voor uw toepassing bestaat meestal uit van veel onderdelen, zoals een virtuele machine, storage-account en virtueel netwerk of een web-app, database, databaseserver en services van derden. Deze onderdelen moet u niet zien als afzonderlijke entiteiten, maar als onderdelen die één entiteit vormen en aan elkaar zijn gerelateerd en afhankelijk zijn van elkaar. U wilt dat toodeploy, beheren en ze als een groep te controleren. Azure Resource Manager kunt u toowork met Hallo resources in uw oplossing als een groep.

U kunt implementeren, bijwerken of verwijderen van alle Hallo resources voor uw oplossing in een enkele, gecoördineerde bewerking. Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie. Resource Manager biedt beveiliging, controle en functies toohelp tagging u uw resources beheren na implementatie.

**Hallo voordelen van het gebruik van Resource Manager**

Resource Manager biedt diverse voordelen:

-   U kunt implementeren, beheren en bewaken van alle Hallo resources voor uw oplossing als een groep in plaats van deze resources afzonderlijk te verwerken.

-   U kunt herhaaldelijk implementeren van uw oplossing gedurende de ontwikkelingscyclus Hallo en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status.

-   U kunt uw infrastructuur beheren via declaratieve sjablonen in plaats van scripts.

-   U kunt Hallo afhankelijkheden tussen resources, zodat deze zijn geïmplementeerd in de juiste volgorde Hallo definiëren.

-   Omdat op rollen gebaseerde toegangsbeheer (RBAC) is geïntegreerd in het beheerplatform hello, kunt u access control-tooall services toepassen in de resourcegroep.

-   U kunt tags toepassen tooresources toologically organiseren alle Hallo resources in uw abonnement.

-   U kunt facturering voor uw organisatie verduidelijken door kosten voor een groep resources delen tag weer te geven.

> [!Note]
> Resource Manager biedt een nieuwe manier toodeploy en beheren van uw oplossingen. Als u hebt gebruikt eerdere implementatiemodel Hallo en toolearn over Hallo wijzigingen, Zie [Understanding Resource Manager-implementatie en klassieke implementatie](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Azure-netwerk logboekregistratie en controle

Azure biedt veel extra toomonitor, detecteren, voorkomen van en reageren toonetwork beveiligingsgebeurtenissen. Hallo meest krachtige hulpprogramma's beschikbaar tooyou op dit gebied onder andere:

-   Network Watcher

-   Resource niveau Netwerkbewaking

-   Log Analytics

### <a name="network-watcher"></a>Netwerk-watcher

[Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -bewaking op basis van een Scenario bij Hallo-functies in netwerk-Watcher wordt geleverd. Deze service omvat pakketopname, volgende hop, IP-stroom controleren, groep beveiligingsweergave, NSG stroom Logboeken. Scenario niveau bewaking biedt een end-tooend-weergave van netwerkbronnen in contrast tooindividual resource netwerkbewaking.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

Netwerk-Watcher is een regionale service waarmee u toomonitor en onderzoeken van voorwaarden op een netwerk scenario niveau in, en naar Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.

Netwerk-Watcher heeft momenteel Hallo volgende mogelijkheden:

#### <a name="topology"></a>Topologie

[Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) retourneert een grafiek van netwerkbronnen in een virtueel netwerk. Hallo-grafiek wordt Hallo koppeling tussen Hallo resources toorepresent Hallo end tooend verbinding met het netwerk. In Hallo portal retourneert topologie Hallo bronobjecten op aan de hand van de basis van het virtuele netwerk. Hallo relaties zijn afgebeeld met lijnen tussen Hallo bronnen buiten Hallo netwerk-Watcher regio, zelfs als in Hallo bron de groep niet worden weergegeven. Hallo bronnen geretourneerd in de portal weergave Hallo zijn een subset van Hallo netwerkonderdelen die diagram worden weergegeven aan. toosee hello volledige lijst met netwerkresources, kunt u [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) of [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Resources worden geretourneerd worden Hallo verbinding tussen ze gemodelleerd onder twee-relaties.

- **Containment** -virtueel netwerk bevat een Subnet, waardoor een NIC. bevat

- **Gekoppeld** -A NIC is gekoppeld aan een virtuele machine.

#### <a name="variable-packet-capture"></a>Variabele pakketopname

Netwerk-Watcher [variabele pakketopname](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) kunt u toocreate pakket vastleggen sessies tootrack verkeer tooand van een virtuele machine. Pakketopname helpt toodiagnose netwerk afwijkingen beide reactief en proactivity. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.

Pakketopname is een uitbreiding van virtuele machine die op afstand via het netwerk-Watcher wordt gestart. Deze mogelijkheid kan Hallo last van een pakketopname handmatig worden uitgevoerd op de gewenste Hallo virtuele machine, die kostbare tijd bespaart vergemakkelijken. Pakketopname kan worden geactiveerd via Hallo-portal, PowerShell, CLI of REST-API. Er is een voorbeeld van hoe pakketopname kan worden geactiveerd met waarschuwingen van de virtuele Machine.

#### <a name="ip-flow-verify"></a>IP-stroom controleren

[IP-stromen controleren](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) controleert of een pakket wordt toegestaan of geweigerd tooor van een virtuele machine op basis van 5-tuple informatie. Deze informatie bestaat uit de richting, protocol, lokaal IP-, externe IP-, lokale poort en externe poort. Als hello-pakket is geweigerd door een beveiligingsgroep, wordt Hallo-naam van Hallo-regel die geweigerd hello-pakket geretourneerd. Terwijl de IP-bron- of doelserver kan worden gekozen, deze functie kan beheerders die Analyseer snel problemen met de netwerkverbinding van of toohello internet en van of toohello on-premises omgeving.

IP-stromen controleren is bedoeld voor een netwerkinterface van een virtuele machine. Netwerkverkeer is geverifieerd op basis van Hallo geconfigureerd instellingen tooor van netwerkinterface. Deze functie is handig bij de bevestiging als toegangsroutes en uitgaande verkeer tooor van een virtuele machine wordt geblokkeerd door een regel in een Netwerkbeveiligingsgroep.

#### <a name="next-hop"></a>Volgende hop

Hiermee wordt bepaald Hallo [volgende hop](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) voor pakketten worden gerouteerd in hello Azure Network-Fabric, als u toodiagnose ieder inschakelen onjuist geconfigureerd gebruiker gedefinieerde routes. Verkeer van een virtuele machine wordt verzonden tooa bestemming op basis van Hallo effectieve routes die zijn gekoppeld aan een NIC. Volgende hop opgehaald Hallo volgend hoptype en IP-adres van een pakket vanuit een specifieke virtuele machine en de NIC. Dit helpt toodetermine als hello pakket gerichte toohello bestemming wordt of het Hallo-verkeer wordt zwarte gaan is.

Ook wordt de volgende hop Hallo routetabel die zijn gekoppeld aan de volgende hop Hallo. Tijdens het opvragen van een volgende hop als Hallo route is gedefinieerd als een gebruiker gedefinieerde route worden die route geretourneerd. Anders retourneert de volgende hop 'Systeemroute'.

#### <a name="security-group-view"></a>beveiliging groep weergeven

Hallo effectieve en toegepaste beveiligingsregels voor verbindingen die worden toegepast op een virtuele machine opgehaald. Netwerkbeveiligingsgroepen zijn gekoppeld op het subnetniveau van een of een NIC-niveau. Wanneer gekoppeld op het subnetniveau van een, geldt deze tooall Hallo VM-exemplaren in Hallo subnet. Netwerk [beveiligingsgroep weergave](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) retourneert alle Hallo geconfigureerd nsg's en regels die zijn gekoppeld op een niveau-NIC en subnet voor een virtuele machine biedt meer informatie over het Hallo-configuratie. Bovendien worden Hallo effectieve beveiligingsregels voor verbindingen voor elk van de Hallo NIC's in een virtuele machine opgehaald. Met behulp van de Netwerkbeveiligingsgroep weergeven, kunt u een virtuele machine op netwerk beveiligingsproblemen zoals open poorten beoordelen. U kunt ook valideren als de Netwerkbeveiligingsgroep werkt zoals verwacht op basis van een [vergelijking tussen Hallo geconfigureerd en effectieve beveiligingsregels Hallo](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>NSG-Flow-logboekregistratie

 Logboeken van de stroom voor Netwerkbeveiligingsgroepen kunt u toocapture gerelateerde tootraffic logboeken die worden toegestaan of geweigerd door Hallo beveiligingsregels voor verbindingen in groep Hallo. Hallo-stroom wordt gedefinieerd door de gegevens van een 5-tuple: bron-IP, doel-IP, bronpoort, doelpoort en -Protocol.

[Netwerkbeveiligingsgroep stroom logboeken](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Virtuele netwerkgateway en verbinding probleemoplossing

Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure. Een van deze mogelijkheden resource is het oplossen van problemen. [Het oplossen van resource](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) kan worden aangeroepen door PowerShell, CLI of REST-API. Als deze wordt aangeroepen, netwerk-Watcher Hallo status van een virtuele netwerkgateway of een verbinding inspecteert en retourneert de bevindingen zijn.

Deze sectie leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor het oplossen van resource.

-   [Problemen met een virtuele netwerkgateway](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Problemen met een verbinding](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Netwerk-abonnementen

[Netwerk-abonnementen](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) voorzien van details van Hallo informatie over het gebruik van elk van de netwerkbron Hallo in een abonnement in een regio tegen Hallo kunt u het maximum aantal bronnen die beschikbaar zijn.

#### <a name="configuring-diagnostics-log"></a>Configuratie van diagnostische gegevens logboek

Netwerk-Watcher biedt een [diagnostische logboeken](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) weergeven. Deze weergave bevat alle netwerkresources die ondersteuning bieden voor diagnostische gegevens vastleggen. U kunt in deze weergave inschakelen en uitschakelen van netwerkresources snel en gemakkelijk.

### <a name="network-resource-level-monitoring"></a>Resource niveau netwerkbewaking

Hallo volgende functies zijn beschikbaar voor het niveau Broncontrole:

#### <a name="audit-log"></a>Controlelogboek

Bewerkingen die worden uitgevoerd als onderdeel van de configuratie van netwerken Hallo worden geregistreerd. Deze controlelogboeken essentiële tooestablish verschillende conformiteit zijn. Deze logboeken kunnen worden weergegeven in hello Azure-portal of opgehaald met behulp van Microsoft-hulpprogramma's zoals Power BI of hulpprogramma's van derden. Controlelogboeken zijn beschikbaar via het Hallo-portal, PowerShell, CLI en Rest-API.

> [!Note]
> Zie voor meer informatie over controlelogboeken [bewerkingen met Resource Manager controleren](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Controlelogboeken zijn beschikbaar voor bewerkingen die op alle netwerkbronnen.


#### <a name="metrics"></a>Metrische gegevens

Metrische gegevens zijn metingen van de prestaties en prestatiemeteritems die gedurende een periode worden verzameld. Metrische gegevens zijn momenteel beschikbaar voor de toepassingsgateway. Metrische gegevens kunnen worden gebruikt tootrigger waarschuwingen op basis van de drempelwaarde. Azure Application Gateway standaard bewaakt Hallo status van alle resources in de back-end-pool en worden alle bronnen die niet in orde beschouwd uit Hallo groep automatisch verwijderd. Toepassingsgateway blijft toomonitor Hallo slecht exemplaren en voegt deze toe back-toohello goede back-end-pool zodra deze beschikbaar komen en reageren toohealth-tests. Toepassingsgateway verzendt Hallo statuscontroles Hello dezelfde poort die is gedefinieerd in Hallo back-end-HTTP-instellingen. Deze configuratie zorgt ervoor dat Hallo-test is het testen van Hallo dezelfde poort dat klanten tooconnect toohello back-end gebruikt.

> [!Note]
> Zie [Application Gateway Diagnostics](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview hoe metrische gegevens gebruikte toocreate waarschuwingen kunnen worden.

#### <a name="diagnostic-logs"></a>Diagnostische logboeken

Periodieke en eigen initiatief gebeurtenissen zijn gemaakt door netwerkbronnen en vastgelegd in de storage-accounts, tooan Event Hub of Log Analytics verzonden. Deze logboeken bieden inzicht in het Hallo-status van een resource. Deze logboeken kunnen worden weergegeven in de hulpprogramma's, zoals Power BI en Log Analytics. hoe diagnostische logboeken tooview, gaat u naar toolearn [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Diagnostische logboeken beschikbaar zijn voor [Load Balancer](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [Netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), Routes, en [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Netwerk-Watcher biedt dat een diagnostische logboeken weergeven. Deze weergave bevat alle netwerkresources die ondersteuning bieden voor diagnostische gegevens vastleggen. U kunt in deze weergave inschakelen en uitschakelen van netwerkresources snel en gemakkelijk.

### <a name="log-analytics"></a>Log Analytics

[Meld u Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) is een service in [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) die uw cloud en on-premises omgevingen toomaintain bewaakt de beschikbaarheid en prestaties. Gegevens die zijn gegenereerd door de resources in uw cloud en on-premises omgevingen en van andere bewaking extra tooprovide analysis over meerdere bronnen worden verzameld.

Log Analytics biedt Hallo oplossingen voor het bewaken van uw netwerken te volgen:

-   Netwerk-Prestatiemeter (NPM)

-   Azure Application Gateway analytics

-   Netwerkbeveiligingsgroep Azure analytics

#### <a name="network-performance-monitor-npm"></a>Netwerk-Prestatiemeter (NPM)
Hallo [netwerk Prestatiemeter](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) management-oplossing is een oplossing die wordt bewaakt Hallo health, beschikbaarheid en bereikbaarheid van netwerken voor netwerkbeheer.

Gebruikte toomonitor connectiviteit tussen is:

-   openbare cloud en on-premises

-   datacenters en gebruikerslocaties (filialen)

-   de subnetten die als host fungeert voor verschillende lagen van een toepassing met meerdere lagen.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Azure application gateway analyses in logboekanalyse

Hallo logboeken te volgen worden voor Toepassingsgateways ondersteund:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Hallo volgende metrische gegevens worden voor Toepassingsgateways ondersteund:

-   doorvoer van 5 minuten

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Azure-netwerk-beveiligingsanalyse groep in logboekanalyse

Hallo worden volgende logboeken ondersteund voor [netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** bevat vermeldingen voor welke NSG regels toegepaste tooVMs en de exemplaar-rollen op basis van MAC-adres zijn. Hallo-status voor deze regels worden verzameld om de 60 seconden.

- **NetworkSecurityGroupRuleCounter:** bevat vermeldingen voor hoe vaak elke NSG regel is toegepast toodeny of verkeer toestaan.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over beveiliging door het lezen van enkele van de onderwerpen over onze uitgebreide beveiliging:

-   [Log Analytics voor Netwerkbeveiligingsgroepen (nsg's)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Networking innovaties die onderbreking station Hallo cloud](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: Hallo switch netwerksoftware die ook door Hallo algemene Microsoft-Cloud](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Hoe Microsoft maakt voor de snelle en betrouwbare globaal netwerk](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Licht up netwerk innovatie](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
