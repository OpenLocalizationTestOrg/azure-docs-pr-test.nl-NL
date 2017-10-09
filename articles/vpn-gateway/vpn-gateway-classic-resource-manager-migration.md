---
title: aaaVPN Gateway klassieke tooResource Manager-migratie | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo VPN-Gateway klassieke tooResource Manager-migratie.
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>VPN-Gateway klassieke tooResource Manager-migratie
VPN-Gateways kunnen nu worden gemigreerd van klassiek tooResource Manager-implementatiemodel. U kunt meer lezen over Azure Resource Manager [functies en voordelen](../azure-resource-manager/resource-group-overview.md). In dit artikel wordt beschreven hoe toomigrate van klassieke implementaties toonewer resourcebeheer op basis van model. 

VPN-Gateways worden gemigreerd als onderdeel van de VNet-migratie van klassiek tooResource Manager. Deze migratie wordt een VNet per keer gedaan. Er is geen aanvullende vereiste in termen van toomigration in hulpprogramma's of vereisten. Migratiestappen zijn identiek tooexisting VNet migratie en worden beschreven op [IaaS resources migratie pagina](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Er is geen pad gegevens uitvaltijd tijdens de migratie en dus bestaande werkbelastingen toofunction zonder verlies van verbinding met lokale zou blijven tijdens de migratie. Hallo openbaar IP-adres die zijn gekoppeld aan Hallo VPN-gateway wordt niet gewijzigd tijdens het migratieproces Hallo. Dit betekent dat u niet tooreconfigure uw lokale router hoeft nadat de Hallo migratie is voltooid.  

Hallo-model in de Resource Manager verschilt van het klassieke model en bestaat uit de virtuele netwerkgateways, lokale netwerkgateways en verbindingsbronnen. Deze Hallo VPN-gateway zelf vertegenwoordigen, lokale-site op premises-adresruimte en de verbinding tussen Hallo twee respectievelijk Hallo. Nadat de migratie is voltooid uw gateways niet beschikbaar in het klassieke model en alle beheerbewerkingen op de virtuele netwerkgateways en lokale netwerkgateways verbindingsobjecten moeten worden uitgevoerd met behulp van Resource Manager-model.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
Meest voorkomende scenario's voor VPN-verbinding vallen klassieke tooResource Manager-migratie. Hallo ondersteund scenario's omvatten-

* Punt toosite connectiviteit
* Site-connectiviteit toosite met VPN-Gateway verbonden tooon premises locatie
* VNet-connectiviteit tooVNet tussen twee VNets met behulp van VPN-gateways
* Meerdere VNets verbonden toosame op de lokale locatie
* Meerdere site-connectiviteit
* Geforceerde tunneling VNets ingeschakeld

Scenario's die niet worden ondersteund:-  

* VNet met zowel de ExpressRoute-Gateway en de VPN-Gateway is momenteel niet ondersteund.
* Doorvoer scenario's waar VM-extensies verbonden tooon lokale servers zijn. Doorvoer VPN-verbinding beperkingen worden hieronder beschreven.

> [!NOTE]
> Validatie van de CIDR in Resource Manager-model is strikter dan Hallo een in het klassieke model. Voordat u migreert overeenstemming van de klassieke adresbereiken gegeven toovalid CIDR-notatie vóór Hallo-migratie. CIDR kan worden gevalideerd met behulp van een algemene CIDR validatiefuncties. VNet of lokale sites met ongeldige CIDR-bereiken wanneer gemigreerd zou leiden tot mislukte status.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>VNet tooVNet connectiviteit migratie
VNet-connectiviteit tooVNet in klassieke werd bereikt door het maken van een lokale site representatie van Hallo VNet verbonden. Klanten zijn vereist toocreate twee lokale sites die vertegenwoordigd Hallo twee VNets die toobe nodig met elkaar verbonden. Deze zijn en verbonden toohello overeenkomt met behulp van IPSec-tunnel tooestablish connectiviteit tussen VNets Hallo twee VNets. Dit model heeft beheerbaarheid uitdagingen omdat wijzigingen adresbereik in een VNet moeten ook worden beheerd in het bijbehorende lokale site representatie Hallo. Deze tijdelijke oplossing is niet meer nodig in het Resource Manager-model. Hallo-verbinding tussen de twee VNets rechtstreeks kan worden bereikt met het verbindingstype 'Vnet2Vnet' in verbindingsbron Hallo. 

![Schermopname van VNet tooVNet migratie.](./media/vpn-gateway-migration/migration1.png)

Tijdens de VNet-migratie wordt gedetecteerd die verbonden entiteit Hallo toocurrent VNet van VPN-gateway is een andere VNet en zorg ervoor dat zodra de migratie van beide VNets is voltooid, niet langer ziet u twee lokale sites Hallo die andere VNet. Hallo klassieke model van twee VPN-gateways, twee lokale sites en twee verbindingen tussen deze twee is getransformeerde tooResource Manager-model met twee VPN-gateways en twee verbindingen van het type Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Doorvoer VPN-verbinding
U kunt VPN-gateways configureren in een topologie zodanig zijn dat lokale connectiviteit voor een VNet wordt gerealiseerd door tooanother VNet rechtstreeks verbonden zijn met tooon-premises verbinding te maken. Dit is doorvoer VPN-verbindingen waarop exemplaren in de eerste VNet verbonden tooon lokale bronnen via onderweg toohello VPN-gateway in verbonden VNet rechtstreeks verbonden zijn met tooon-premises zijn. tooachieve deze configuratie in het klassieke implementatiemodel, moet u een lokale site dat is samengevoegd voorvoegsels die beide Hallo verbonden VNet en on-premises-adresruimte toocreate. Deze representational lokale site is en verbonden toohello VNet tooachieve doorvoer connectiviteit. Dit model klassieke heeft ook vergelijkbare beheerbaarheid uitdagingen omdat eventuele wijzigingen in de on-premises adresbereik moet ook worden ingesteld op Hallo van de lokale site voor Hallo aggregatie van het VNet en on-premises. Introductie van BGP-ondersteuning in Resource Manager ondersteunde gateways vereenvoudigt het beheer omdat hello verbonden gateways de routes van on-premises zonder handmatige wijzigingen tooprefixes leert.

![Schermopname van routeringsscenario doorvoer.](./media/vpn-gateway-migration/migration2.png)

Aangezien we tooVNet-VNet-connectiviteit transformeren zonder lokale sites, verliest Hallo onderweg scenario op-premises-connectiviteit voor VNet indirect verbonden tooon-premises. Hallo verlies van verbinding kan worden opgevangen volgt in de volgende twee manieren Hallo nadat de migratie is voltooid - 

* Schakel BGP op VPN-gateways die met elkaar zijn verbonden en tooon-premises. Connectiviteit zonder andere configuratiewijziging BGP inschakelen worden hersteld omdat routes worden geleerd en aangekondigd tussen VNet-gateways. Houd er rekening mee BGP-optie is alleen beschikbaar in Standard en hoger SKU's.
* Stel een expliciete verbinding van de betrokken VNet toohello lokale netwerkgateway voor on-premises locatie. Dit zou ook vereist voor het wijzigen van de configuratie op Hallo lokale router toocreate en IPsec-tunnel Hallo configureren.

## <a name="next-steps"></a>Volgende stappen
Nadat u hebt leren over de ondersteuning van VPN-gateway migratie gaat te[platform ondersteund migratie van IaaS-resources van klassieke tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget gestart.

