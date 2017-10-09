---
title: richtlijnen voor infrastructuur - Linux networking aaaAzure | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van virtuele netwerken in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Azure-infrastructuur richtlijnen netwerken voor virtuele Linux-machines

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op wat Hallo plannen van stappen voor virtuele netwerken in Azure en verbindingen tussen bestaande on-premises omgevingen vereist.

## <a name="implementation-guidelines-for-virtual-networks"></a>Richtlijnen voor de implementatie voor virtuele netwerken
Beslissingen te nemen:

* Welk type van het virtuele netwerk moet u toohost infrastructuur of uw IT-werkbelasting (alleen in de cloud of cross-premises)?
* Voor cross-premises virtuele netwerken, hoeveel adresruimte moet u toohost Hallo subnetten en virtuele machines nu en redelijke uitbreiding in Hallo toekomstige?
* Weet u toocreate gecentraliseerde virtuele netwerken of afzonderlijke virtuele netwerken voor elke resourcegroep maken?

Taken:

* Definieer Hallo adresruimte voor Hallo virtuele netwerken toobe gemaakt.
* Hallo set van subnetten en Hallo-adresruimte voor elk definiëren.
* Voor cross-premises virtuele netwerken, Hallo set LAN-adresruimtes voor Hallo lokale locaties die virtuele machines in Hallo virtueel netwerk nodig tooreach Hallo te definiëren.
* Werk met on-premises netwerken team tooensure Hallo juiste routering is geconfigureerd bij het maken van cross-premises virtuele netwerken.
* Hallo virtueel netwerk maken met uw naamconventie.

## <a name="virtual-networks"></a>Virtuele netwerken
Virtuele netwerken zijn nodig toosupport communicatie tussen virtuele machines (VM's). U kunt definiëren subnetten, aangepaste IP-adres, DNS-instellingen, Beveiligingsfiltering en taakverdeling, net als bij de fysieke netwerken. Met behulp van een [VPN-Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md) of [Express Route-circuit](../../expressroute/expressroute-introduction.md), kunt u virtuele netwerken van Azure tooyour on-premises netwerken. U kunt meer lezen over [virtuele netwerken en de bijbehorende onderdelen](../../virtual-network/virtual-networks-overview.md).

Met behulp van resourcegroepen, hebt u de flexibiliteit in het ontwerp van de onderdelen van uw virtuele netwerk. Virtuele machines verbinding kunnen maken voor netwerken toovirtual buiten hun eigen resourcegroep. Een algemene ontwerpbenadering zijn toocreate gecentraliseerde resourcegroepen die uw netwerkinfrastructuur core die kan worden beheerd door een algemene team bevatten. Virtuele machines en hun toepassingen geïmplementeerd tooseparate resourcegroepen. Deze aanpak kunt u toepassingseigenaars toegang toohello resourcegroep met hun virtuele machines zonder te openen van toegang toohello configuratie van Hallo grotere virtuele netwerken bronnen.

## <a name="site-connectivity"></a>Site-connectiviteit
### <a name="cloud-only-virtual-networks"></a>Alleen in de cloud virtuele netwerken
Als on-premises gebruikers en computers niet lopende connectiviteit tooVMs in een Azure-netwerk hoeven, is het ontwerp van uw virtuele netwerk rechtstreeks doorsturen:

![Alleen in de cloud virtuele Basisnetwerk-diagram](./media/infrastructure-networking-guidelines/vnet01.png)

Deze aanpak is doorgaans voor internetgerichte werkbelastingen, zoals een webserver met Internet. U kunt deze virtuele machines met behulp van SSH of een punt-naar-site VPN-verbindingen kunt beheren.

Omdat ze geen verbinding tooyour on-premises netwerk maken, kunnen een gedeelte van Hallo persoonlijke IP-adresruimte in virtuele netwerken die alleen Azure gebruiken. Hallo-adresruimte mag Hallo dezelfde persoonlijke ruimte in lokale gebruiken.

### <a name="cross-premises-virtual-networks"></a>Cross-premises virtuele netwerken
Als on-premises gebruikers en computers lopende connectiviteit tooVMs in een Azure-netwerk is vereist, maakt u een virtueel netwerk met cross-premises. Hallo virtueel netwerk tooyour on-premises netwerk verbinden met een ExpressRoute of site-naar-site VPN-verbinding.

![Cross-premises virtuele-netwerkdiagram](./media/infrastructure-networking-guidelines/vnet02.png)

In deze configuratie is Hallo virtuele Azure-netwerk in wezen een cloud-gebaseerde uitbreiding van uw on-premises netwerk.

Omdat ze verbinding maken met tooyour lokaal netwerk, cross-premises virtuele netwerken moeten gebruiken een deel van het Hallo-adresruimte die wordt gebruikt door uw organisatie die uniek is. In hello dezelfde manier die verschillende zakelijke locaties zijn toegewezen met een specifiek IP-subnet, Azure, wordt een andere locatie als u van uw netwerk uitbreiden.

tooallow pakketten tootravel van uw cross-premises virtuele netwerk tooyour on-premises netwerk, moet u relevante lokale adresvoorvoegsels Hallo set configureren als onderdeel van de lokale netwerkdefinitie Hallo voor Hallo virtuele netwerk. Afhankelijk van Hallo adres ruimte van Hallo virtuele netwerk en Hallo set relevante on-premises locaties, kunnen er veel adresvoorvoegsels in Hallo lokale netwerk.

U kunt een virtueel netwerk voor alleen in de cloud virtueel netwerk tooa cross-premises omzetten, maar het meest waarschijnlijke toore-IP vereist uw adresruimte virtuele netwerk en Azure-resources. Daarom moet u zorgvuldig overwegen of een virtueel netwerk toobe verbonden tooyour on-premises netwerk moet bij het toewijzen van een IP-subnet.

## <a name="subnets"></a>Subnetten
Subnetten kunnen u tooorganize resources die zijn gerelateerd, ofwel logisch (bijvoorbeeld één subnet voor VM's van de gekoppelde toohello dezelfde toepassing), of fysiek (bijvoorbeeld één subnet per resourcegroep). U kunt ook gebruikmaken van subnet-isolatietechnieken, voor extra beveiliging.

Voor cross-premises virtuele netwerken, moet u subnetten met Hallo ontwerpen dezelfde conventies die u voor lokale bronnen gebruikt. **Azure altijd gebruikt de eerste drie IP-adressen van de adresruimte Hallo voor elk subnet Hallo**. toodetermine hello nummer van de adressen die nodig zijn voor het Hallo-subnet, starten door het aantal virtuele machines die u nu moet hello te tellen. Schatten voor toekomstige groei en gebruik vervolgens Hallo tabel toodetermine Hallo grootte van Hallo subnet te volgen.

| Aantal virtuele machines nodig | Aantal hostbits nodig | Grootte van het Hallo-subnet |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Voor een normale lokale subnetten, maximum aantal adressen van de host voor een subnet met n hostbits Hallo is 2<sup> n </sup> : 2. Voor een Azure-subnet is Hallo kunt u het maximum aantal adressen van de host voor een subnet met hostbits n 2<sup> n </sup> – 5 (2 plus 3 voor Hallo-adressen die gebruikmaakt van Azure op elk subnet).
> 
> 

Als u een subnetgrootte die is te klein kiest, u hebt toore-IP- en opnieuw implementeren Hallo VM's in Hallo subnet.

## <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
U kunt filteren regels toohello van het verkeer dat loopt via uw virtuele netwerken toepassen met behulp van Netwerkbeveiligingsgroepen. U kunt opbouwen gedetailleerde filteren regels toosecure uw virtuele netwerkomgeving beheren binnenkomend en uitgaand verkeer bron- en IP-adresbereiken, toegestaan poorten, enzovoort. Netwerkbeveiligingsgroepen mag toegepaste toosubnets binnen een virtueel netwerk of rechtstreeks tooa virtuele netwerkinterface gegeven. Het is aanbevolen toohave een zekere mate van Netwerkbeveiligingsgroep voor het filteren van verkeer op uw virtuele netwerken. U kunt meer lezen over [Netwerkbeveiligingsgroepen](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Extra netwerkonderdelen
Net als bij een lokale fysieke netwerkinfrastructuur, bevatten Azure virtuele netwerken meer dan alleen subnetten en IP-adressen. Bij het ontwerpen van uw infrastructuur, kunt u tooincorporate enkele van deze extra onderdelen:

* [VPN-gateways](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -verbinding maken met virtuele netwerken van Azure tooother Azure virtuele netwerken of tooon-premises netwerken via een Site-naar-Site VPN-verbinding verbinding te maken. Express Route-verbindingen voor speciale, beveiligde verbindingen implementeert. U kunt ook rechtstreeks toegang voor gebruikers met punt-naar-Site VPN-verbindingen opgeven.
* [De load balancer](../../load-balancer/load-balancer-overview.md) -taakverdeling van verkeer voor de externe en interne verkeer naar wens biedt.
* [Toepassingsgateway](../../application-gateway/application-gateway-introduction.md) - HTTP-taakverdeling op de toepassingslaag hello, bieden een aantal extra voordelen voor webtoepassingen in plaats van hello Azure load balancer implementeren.
* [Traffic Manager](../../traffic-manager/traffic-manager-overview.md) - DNS-gebaseerde verkeer distributie toodirect eindgebruikers toohello dichtstbijzijnde beschikbare toepassingsaanvragen eindpunt, waardoor toohost u uw toepassing buiten het Azure-datacenters in verschillende regio's.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

