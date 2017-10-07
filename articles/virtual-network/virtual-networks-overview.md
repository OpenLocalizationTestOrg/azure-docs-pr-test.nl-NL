---
title: aaaAzure Virtual Network | Microsoft Docs
description: Meer informatie over Azure Virtual Network-concepten en functies.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Azure Virtual Network

Hallo Azure Virtual Network service kunt u toosecurely andere Azure-resources tooeach verbinding met virtuele netwerken (vnet's). Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement. U kunt ook VNets tooyour on-premises netwerk verbinden. Hallo volgende afbeelding ziet u Hallo-mogelijkheden van hello Azure Virtual Network service:

![Netwerkdiagram](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn meer informatie over Hallo na Azure Virtual Network-mogelijkheden, klikt u op Hallo mogelijkheden:
- **[Isolatie:](#isolation)**  VNets die zijn geïsoleerd van elkaar. U kunt afzonderlijke VNets voor ontwikkeling, testen en productie te maken die Hallo gebruik dezelfde CIDR-adresblokken. Als u daarentegen, kunt u meerdere VNets die gebruikmaken van verschillende CIDR-adresblokken en netwerken met elkaar verbinden. U kunt een VNet segmenteren in meerdere subnetten. Azure biedt interne naamomzetting voor virtuele machines en Cloud Services-rolexemplaren verbonden tooa VNet. U kunt een VNet-toouse desgewenst uw eigen DNS-servers, in plaats van Azure interne naamomzetting configureren.
- **[Verbinding met Internet:](#internet)**  alle Azure virtuele Machines (VM) en Cloud Services-rolexemplaren verbonden tooa VNet hebben toegang tot Internet, toohello standaard. U kunt ook een inkomend toospecific resources, inschakelen indien nodig.
- **[Azure-resource connectiviteit:](#within-vnet)**  Azure-resources zoals Cloudservices en virtuele machines kunnen worden verbonden toohello hetzelfde VNet. Hallo resources verbinding kunnen maken van andere tooeach met particuliere IP-adressen, zelfs als ze zich in verschillende subnetten. Azure biedt standaardroutering tussen subnetten, VNets en on-premises netwerken, zodat u niet tooconfigure hebt en beheren van routes.
- **[VNet-connectiviteit:](#connect-vnets)**  VNets, kunt u andere verbonden tooeach tooany VNet toocommunicate inschakelen resources worden verbonden met een resource op een andere VNet.
- **[Lokale connectiviteit:](#connect-on-premises)**  VNets verbonden tooon-premises netwerken via persoonlijke netwerkverbindingen tussen uw netwerk en Azure of een site-naar-site VPN-verbinding via Internet Hallo kan zijn.
- **[Wordt verkeer gefilterd:](#filtering)**  VM en Cloud Services-rol exemplaren netwerkverkeer kan worden gefilterd binnenkomend en uitgaand op bron-IP-adres en poort, doel-IP-adres en poort en protocol.
- **[Routering:](#routing)**  kunt u eventueel Azure standaard routering met BGP-routes via een netwerkgateway of configureren van uw eigen routes overschrijven.

## <a name = "isolation"></a>Netwerkisolatie en segmentering

U kunt meerdere VNets binnen elke Azure implementeren [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) en Azure [regio](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region). Elke VNet is geïsoleerd van andere vnet's. U kunt voor elk VNet:
- Geef een aangepaste persoonlijke IP-adresruimte met behulp van openbare en persoonlijke (RFC 1918)-adressen. Azure wijst bronnen verbonden toohello VNet een particulier IP-adres van de adresruimte Hallo die u toewijzen.
- Segmenteer Hallo VNet in een of meer subnetten en een deel van Hallo VNet-ruimte tooeach adressubnet toewijzen.
- Gebruik Azure verschafte naamomzetting of geef dat uw eigen DNS-server voor gebruik door resources verbonden tooa VNet. meer informatie over naamomzetting in vnet's, Hallo lezen toolearn [naamomzetting voor VM's en Cloudservices](virtual-networks-name-resolution-for-vms-and-role-instances.md) artikel.

## <a name = "internet"></a>Verbinding maken met Internet toohello
Alle resources verbonden tooa VNet hebben uitgaande verbinding toohello Internet standaard. Hallo privé IP-adres van bron Hallo is Bronnetwerk adres (snat omzetten) tooa openbaar IP-adres vertaald door hello Azure-infrastructuur. meer informatie over uitgaande internetverbinding lezen Hallo toolearn [inzicht in uitgaande verbindingen in Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) artikel. U kunt Hallo standaard connectiviteit wijzigen door het implementeren van aangepaste Routering en het filteren van verkeer.

toocommunicate inkomende tooAzure resources uit Hallo Internet of toocommunicate uitgaande toohello Internet zonder snat omzetten, een resource moet een openbaar IP-adres worden toegewezen. meer informatie over openbare IP-adressen, Hallo lezen toolearn [openbare IP-adressen](virtual-network-public-ip-address.md) artikel.

## <a name="within-vnet"></a>Verbinding maken met Azure-resources
U kunt verschillende Azure-resources tooa VNet, zoals virtuele Machines (VM), Cloud Services-App Service-omgevingen en virtuele-Machineschaalsets verbinden. Virtuele machines verbinding tooa subnet binnen een VNet maken via een netwerkinterface (NIC). meer informatie over NIC's, Hallo lezen toolearn [netwerkinterfaces](virtual-network-network-interface.md) artikel.

## <a name="connect-vnets"></a>Verbinding maken met virtuele netwerken

U verbinding kunt maken met andere VNets tooeach, resources inschakelen tooeither VNet toocommunicate met elkaar verbonden via VNets. U kunt een of beide van de volgende opties tooconnect VNets tooeach andere hello gebruiken:
- **Peering:** kunnen bronnen verbonden toodifferent Azure VNets binnen Hallo dezelfde Azure-locatie toocommunicate met elkaar. Hallo bandbreedte en de latentie tussen VNets is Hallo Hallo dezelfde alsof Hallo resources verbonden toohello hetzelfde VNet. toolearn meer informatie over peering, lezen Hallo [virtuele netwerk peering](virtual-network-peering-overview.md) artikel.
- **VNet-naar-VNet-verbinding:** kunnen bronnen verbonden Azure VNet toodifferent binnen Hallo dezelfde of verschillende Azure-locaties. In tegenstelling tot de peering, is bandbreedte tussen VNets beperkt, omdat het verkeer door een Azure VPN-Gateway moet lopen. meer over het VNets verbinden met een VNet-naar-VNet-verbinding, Hallo lezen toolearn [een VNet-naar-VNet-verbinding configureren](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.

## <a name="connect-on-premises"></a>Tooan on-premises netwerk verbinding maken

U kunt verbinding maken uw lokale netwerk tooa VNet met elke combinatie van Hallo volgende opties:
- **Punt-naar-site virtueel particulier netwerk (VPN):** tot stand gebracht tussen een enkele PC verbonden tooyour netwerk en Hallo VNet. Dit verbindingstype is handig als u alleen aan de slag met Azure of voor ontwikkelaars, omdat hiervoor weinig of geen wijzigingen tooyour bestaande netwerk. Hallo-verbinding gebruikt Hallo SSTP protocol tooprovide gecodeerde communicatie via Internet Hallo tussen Hallo PC en Hallo VNet. Hallo latentie voor een punt-naar-site VPN-verbinding is onvoorspelbare, aangezien Hallo verkeer Hallo Internet passeert.
- **Site-naar-site-VPN:** tot stand gebracht tussen uw VPN-apparaat en een Azure VPN-Gateway. Dit verbindingstype kunt een on-premises-resource autoriseren van tooaccess een VNet. Hallo-verbinding is een VPN IPSec/IKE waarmee gecodeerde communicatie via Internet Hallo tussen uw on-premises apparaat en hello Azure VPN-gateway. Hallo latentie voor een site-naar-site-verbinding is onvoorspelbaar zijn, aangezien Hallo verkeer Hallo Internet passeert.
- **Azure ExpressRoute:** tot stand gebracht tussen uw netwerk en Azure, via een ExpressRoute-partner. Deze verbinding is een privéverbinding. Verkeer komt geen Hallo Internet passeren. Hallo latentie voor een ExpressRoute-verbinding is betrouwbaar, aangezien verkeer Hallo Internet niet passeren.

meer informatie over alle Hallo vorige verbindingsopties lezen Hallo toolearn [gatewayverbindingsdiagrammen topologie](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) artikel.

## <a name="filtering"></a>Filteren van netwerkverkeer
U kunt filteren netwerkverkeer tussen subnetten op met behulp van een of beide Hallo volgende opties:
- **Netwerkbeveiligingsgroepen (NSG):** elke NSG kan meerdere binnenkomende en uitgaande beveiligingsregels voor verbindingen die u in staat toofilter verkeer door de bron en doel-IP-adres, poort en protocol stellen bevatten. U kunt een NSG tooeach NIC op een virtuele machine kunt toepassen. U kunt ook een NSG toohello subnet een NIC of andere Azure-resource is verbonden met. meer informatie over nsg's, Hallo lezen toolearn [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) artikel.
- **Virtuele apparaten (NVA):** een NVA is een virtuele machine uitvoeren van software waarmee een netwerkfunctie, zoals een firewall. Een lijst met beschikbare NVAs weergeven in Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). NVAs zijn ook beschikbaar met WAN-optimalisatie en andere netwerkapparaten verkeer functies. NVAs worden doorgaans gebruikt voor de gebruiker gedefinieerde of BGP-routes. U kunt ook een NVA toofilter-verkeer tussen vnet's gebruiken.

## <a name="routing"></a>Doorsturen van netwerkverkeer

Azure maakt routetabellen waarmee bronnen verbonden tooany subnet in een VNet toocommunicate met elkaar, standaard. U kunt ofwel implementeren of beide volgende opties toooverride Hallo Hallo standaardroutes die Azure maakt:
- **Gebruiker gedefinieerde routes:** kunt u aangepaste routetabellen met routes die regelen waarin verkeer wordt gerouteerd toofor elk subnet. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.
- **BGP-routes:** als u verbinding maakt met uw VNet tooyour on-premises netwerk via een Azure VPN-Gateway of ExpressRoute-verbinding, BGP-routes tooyour vnet's kunnen worden doorgegeven.

## <a name="pricing"></a>Prijzen

Er zijn geen kosten voor virtuele netwerken, subnetten, routetabellen of netwerk-beveiligingsgroepen. Uitgaande bandbreedtegebruik van Internet, openbare IP-adressen, virtueel netwerk peering, VPN-Gateways en ExpressRoute elke, hebben hun eigen structuren prijzen. Weergave Hallo [virtueel netwerk](https://azure.microsoft.com/pricing/details/virtual-network), [VPN-Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway), en [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) prijzen van pagina's voor meer informatie.

## <a name="faq"></a>Veelgestelde vragen

Veelgestelde vragen over Virtual Network tooreview Zie Hallo [Veelgestelde vragen over het virtuele netwerk](virtual-networks-faq.md) artikel.


## <a name="next-steps"></a>Volgende stappen

- Maken van uw eerste VNet en verbinding maken met een paar virtuele machines tooit, via Hallo stappen in Hallo [maken van uw eerste virtuele netwerk](virtual-network-get-started-vnet-subnet.md) artikel.
- Maken van een punt-naar-site-verbinding tooa VNet via Hallo stappen in Hallo [een punt-naar-site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.
- Meer informatie over een aantal Hallo andere sleutel [mogelijkheden netwerk](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) van Azure.
