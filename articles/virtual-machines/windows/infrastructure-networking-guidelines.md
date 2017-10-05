---
title: Azure infrastructuur richtlijnen - Windows networking | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor het implementeren van virtuele netwerken in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e2d45973-5eba-4904-8ba0-1821f64feed7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 95303c8e393b759b03d3f64996510a830193ba46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-windows-vms"></a>Infrastructuur richtlijnen netwerken voor virtuele machines van Windows Azure 

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht in de vereiste stappen van de planning voor virtuele netwerken in Azure en connectiviteit tussen bestaande on-premises omgevingen.

## <a name="implementation-guidelines-for-virtual-networks"></a>Richtlijnen voor de implementatie voor virtuele netwerken
Beslissingen te nemen:

* Welk type virtueel netwerk hebt u nodig voor het hosten van uw IT-werkbelasting of de infrastructuur (alleen in de cloud of cross-premises)?
* Voor cross-premises virtuele netwerken, hoeveel adresruimte moet u voor het hosten van de subnetten en virtuele machines nu en in de toekomst redelijke uitbreiding?
* U gaat maken gecentraliseerde virtuele netwerken of afzonderlijke virtuele netwerken voor elke resourcegroep maken?

Taken:

* Definieer de adresruimte voor de virtuele netwerken worden gemaakt.
* Definieer de set van subnetten en de adresruimte voor elk.
* Voor cross-premises instelt virtuele netwerken voor lokale netwerk adresruimten voor lokale locaties die de virtuele machines in het virtuele netwerk moeten bereiken.
* Werk met on-premises netwerken team om te controleren of de juiste routering is geconfigureerd bij het maken van cross-premises virtuele netwerken.
* Het virtueel netwerk maken met uw naamconventie.

## <a name="virtual-networks"></a>Virtuele netwerken
Virtuele netwerken zijn nodig voor de ondersteuning van communicatie tussen virtuele machines (VM's). U kunt definiëren subnetten, aangepaste IP-adres, DNS-instellingen, Beveiligingsfiltering en taakverdeling, net als bij de fysieke netwerken. Met behulp van een [VPN-gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md) of [Express Route-circuit](../../expressroute/expressroute-introduction.md), kunt u virtuele netwerken van Azure verbinden met uw on-premises netwerken. U kunt meer lezen over [virtuele netwerken en de bijbehorende onderdelen](../../virtual-network/virtual-networks-overview.md).

Met behulp van resourcegroepen, hebt u de flexibiliteit in het ontwerp van de onderdelen van uw virtuele netwerk. Virtuele machines kunnen verbinding maken met virtuele netwerken buiten hun eigen resourcegroep. Een algemene ontwerpbenadering zou zijn maken gecentraliseerde resourcegroepen die uw netwerkinfrastructuur core die kan worden beheerd door een algemene team, en vervolgens virtuele machines en hun geïmplementeerde toepassingen op afzonderlijke resourcegroepen bevatten. Deze aanpak kunt de eigenaren van toegang tot toepassingen aan de resourcegroep met de bijbehorende virtuele machines zonder toegang tot de configuratie van de grotere virtuele netwerkbronnen.

## <a name="site-connectivity"></a>Site-connectiviteit
### <a name="cloud-only-virtual-networks"></a>Alleen in de cloud virtuele netwerken
Als on-premises gebruikers en computers geen actieve verbinding met virtuele machines in een Azure-netwerk vereist, wordt het ontwerp van uw virtuele netwerk rechtstreeks doorsturen is:

![Alleen in de cloud virtuele Basisnetwerk-diagram](./media/infrastructure-networking-guidelines/vnet01.png)

Deze aanpak is doorgaans voor internetgerichte werkbelastingen, zoals een webserver met Internet. U kunt deze virtuele machines met RDP of punt-naar-site VPN-verbindingen kunt beheren.

Omdat ze geen verbinding met uw on-premises netwerk, kunnen virtuele netwerken die alleen Azure gebruiken een gedeelte van de persoonlijke IP-adresruimte, zelfs als dezelfde persoonlijke ruimte in de lokale gebruiken.

### <a name="cross-premises-virtual-networks"></a>Cross-premises virtuele netwerken
Als on-premises gebruikers en computers actieve verbinding met virtuele machines in een Azure-netwerk vereist, maakt u een virtueel netwerk met cross-premises.  Verbindt dit met uw on-premises netwerk met een ExpressRoute of site-naar-site VPN-verbinding.

![Cross-premises virtuele-netwerkdiagram](./media/infrastructure-networking-guidelines/vnet02.png)

In deze configuratie is het Azure-netwerk in wezen een cloud-gebaseerde uitbreiding van uw on-premises netwerk.

Omdat ze verbinding met uw on-premises netwerk maken, cross-premises virtuele netwerken moeten gebruiken een deel van de adresruimte die wordt gebruikt door uw organisatie die uniek is. Azure wordt een andere locatie op dezelfde manier die verschillende zakelijke locaties met een specifiek IP-subnet worden toegewezen, als u van uw netwerk uitbreiden.

Als wilt toestaan pakketten worden getransporteerd van het virtuele netwerk met cross-premises naar uw on-premises netwerk, moet u de set met relevante lokale adresvoorvoegsels configureren als onderdeel van de definitie van het lokale netwerk voor het virtuele netwerk. Afhankelijk van de adresruimte van het virtuele netwerk en de set met relevante lokale locaties, kunnen er veel adresvoorvoegsels in het lokale netwerk.

Kunt u een virtueel netwerk alleen in de cloud converteren naar een virtueel netwerk met cross-premises, maar het meest waarschijnlijke vereist dat u opnieuw IP uw adresruimte virtuele netwerk en Azure-resources. Daarom moet u zorgvuldig overwegen of een virtueel netwerk worden verbonden met uw on-premises netwerk moet wanneer u een IP-subnet toewijst.

## <a name="subnets"></a>Subnetten
Subnetten kunnen u delen van bronnen die zijn gerelateerd, ofwel logisch (bijvoorbeeld één subnet voor VM's die is gekoppeld aan dezelfde toepassing), of fysiek (bijvoorbeeld één subnet per resourcegroep). U kunt ook gebruikmaken van subnet-isolatietechnieken, voor extra beveiliging.

Voor cross-premises virtuele netwerken, moet u de subnetten met dezelfde conventies die u voor lokale bronnen gebruikt ontwerpen. **Azure gebruikt altijd de eerste drie IP-adressen van de adresruimte voor elk subnet**. Om te bepalen het aantal adressen dat nodig is voor het subnet, starten door het aantal virtuele machines die u nu moet te tellen. Schatten voor toekomstige groei en gebruik vervolgens de volgende tabel om te bepalen van de grootte van het subnet.

| Aantal virtuele machines nodig | Aantal hostbits nodig | Grootte van het subnet |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Voor een normale lokale subnetten, is het maximum aantal adressen van de host voor een subnet met hostbits n 2<sup> n </sup> : 2. Voor een Azure-subnet is het maximum aantal adressen van de host voor een subnet met hostbits n 2<sup> n </sup> – 5 (2 plus 3 voor de adressen die gebruikmaakt van Azure op elk subnet).
> 
> 

Als u een subnetgrootte die is te klein kiest, u hebt op re-IP-adres en implementeren van de virtuele machines in het subnet.

## <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
U kunt filterregels toepassen op het verkeer dat loopt via uw virtuele netwerken met behulp van Netwerkbeveiligingsgroepen. U kunt gedetailleerde filterregels voor het beveiligen van uw virtuele netwerkomgeving opbouwen voor het beheren van binnenkomende en uitgaande verkeer bron- en IP-adresbereiken, toegestaan poorten, enzovoort. Netwerkbeveiligingsgroepen kan worden toegepast op subnetten in een virtueel netwerk of rechtstreeks aan de opgegeven virtuele netwerkinterface. Het verdient aanbeveling om bepaalde mate van Netwerkbeveiligingsgroep voor het filteren van verkeer op uw virtuele netwerken. U kunt meer lezen over [Netwerkbeveiligingsgroepen](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Extra netwerkonderdelen
Azure virtuele netwerken kan net als bij een lokale fysieke netwerkinfrastructuur, meer dan subnetten en IP-adressen bevatten. Bij het ontwerpen van uw infrastructuur kunt u gebruikmaken van enkele van deze extra onderdelen:

* [VPN-gateways](../../vpn-gateway/vpn-gateway-about-vpngateways.md) - verbinding virtuele netwerken in Azure maken met andere virtuele netwerken in Azure of verbinding maken met on-premises netwerken via een Site-naar-Site VPN-verbinding. Express Route-verbindingen voor speciale, beveiligde verbindingen implementeert. U kunt ook rechtstreeks toegang voor gebruikers met punt-naar-Site VPN-verbindingen opgeven.
* [De load balancer](../../load-balancer/load-balancer-overview.md) -taakverdeling van verkeer voor de externe en interne verkeer naar wens biedt.
* [Toepassingsgateway](../../application-gateway/application-gateway-introduction.md) - HTTP-taakverdeling op de toepassingslaag, bieden een aantal extra voordelen voor webtoepassingen in plaats van de Azure load balancer implementeren.
* [Traffic Manager](../../traffic-manager/traffic-manager-overview.md) - DNS-gebaseerde verkeer distributie naar direct eindgebruikers aan de dichtstbijzijnde beschikbare toepassingsaanvragen-eindpunt, zodat u uw toepassing buiten het Azure-datacenters in verschillende regio's wordt gehost.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

