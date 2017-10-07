---
title: aaaOverview van IPv6 voor Azure Load Balancer | Microsoft Docs
description: Understanding IPv6-ondersteuning voor Azure Load Balancer en taakverdeling virtuele machines.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Overzicht van IPv6 voor Azure Load Balancer

Internet gerichte load balancers kunnen worden geïmplementeerd met een IPv6-adres. Bovendien tooIPv4 connectiviteit, hierdoor Hallo volgende mogelijkheden:

* Oorspronkelijke end-to-end IPv6-connectiviteit tussen het openbare Internet-clients en Azure Virtual Machines (VM's) via Hallo load balancer.
* Systeemeigen end-to-end IPv6 uitgaande connectiviteit tussen virtuele machines en openbare clients voor Internet IPv6 is ingeschakeld.

Hallo volgende afbeelding ziet u Hallo IPv6-functionaliteit voor Azure Load Balancer.

![Azure Load Balancer met IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Zodra geïmplementeerd, wordt een IPv4- of IPv6-functionaliteit Internet-client kan communiceren met de Hallo openbare IPv4- of IPv6-adressen of hostnamen van hello Azure Internet gerichte Load Balancer. Hallo load balancer routes Hallo IPv6-pakketten toohello persoonlijke IPv6-adressen van Hallo VM's met network address translation (NAT). Hallo IPv6-Internet client kan niet communiceren rechtstreeks met de Hallo IPv6-adres van Hallo virtuele machines.

## <a name="features"></a>Functies

Systeemeigen IPv6-ondersteuning voor virtuele machines die zijn geïmplementeerd via Azure Resource Manager biedt:

1. IPv6-services voor IPv6-clients op Internet Hallo Netwerktaakverdeling
2. Systeemeigen IPv6- en IPv4-eindpunten op virtuele machines ('dual gestapelde')
3. Binnenkomende en uitgaande geïnitieerde systeemeigen IPv6-verbindingen
4. Ondersteunde protocollen zoals TCP, UDP- en HTTP (S) inschakelen een volledige reeks architecturen service

## <a name="benefits"></a>Voordelen

Deze functionaliteit kunnen Hallo volgende belangrijke voordelen:

* Voldoen aan wettelijke voorschriften vereisen dat nieuwe toepassingen toegankelijk clients met alleen tooIPv6 zijn
* Schakel mobiele en Internet der dingen (IOT) ontwikkelaars toouse dual gestapelde (IPv4 + IPv6) Azure Virtual Machines tooaddress Hallo groeiende mobile en IOT markten

## <a name="details-and-limitations"></a>Meer informatie en beperkingen

Details

* Hello Azure DNS-service bevat zowel IPv4 A en AAAA IPv6-records van naam en reageert met beide records voor Hallo load balancer. Hallo client kiezen welke adres (IPv4 of IPv6) toocommunicate met.
* Wanneer een virtuele machine een verbinding tooa openbaar Internet IPv6 verbonden apparaat initieert, is bron Hallo van de virtuele machine IPv6-adres netwerkadres vertaald (NAT) toohello openbare IPv6-adres van Hallo load balancer.
* Virtuele machines met Linux-besturingssysteem Hallo moet geconfigureerde tooreceive een IPv6-IP-adres via DHCP. Veel van Hallo Linux afbeeldingen in Hallo galerie van Azure zijn al geconfigureerd toosupport IPv6 zonder aanpassing. Zie voor meer informatie [DHCPv6 configureren voor virtuele Linux-machines](load-balancer-ipv6-for-linux.md)
* Als u ervoor kiest wordt toouse een health test met de load balancer een IPv4-test maken en deze gebruiken met zowel Hallo IPv4 en IPv6-eindpunten. Als het Hallo-service op de virtuele machine wordt uitgeschakeld, worden zowel Hallo IPv4 en IPv6-eindpunten buiten rotatie genomen.

Beperkingen

* U kunt geen regels voor taakverdeling IPv6 toevoegen in hello Azure-portal. Hallo-regels kunnen alleen worden gemaakt via Hallo sjabloon, CLI, PowerShell.
* U kunt geen upgrade van bestaande toouse IPv6-adressen van virtuele machines. U kunt nieuwe virtuele machines moet implementeren.
* Één IPv6-adres kan één netwerkinterface tooa in elke virtuele machine worden toegewezen.
* Hallo openbare IPv6-adressen kunnen niet worden toegewezen als tooa VM. Ze kunnen alleen worden toegewezen tooa load balancer.
* U kunt Hallo achterwaartse DNS-zoekopdracht niet configureren voor uw openbare IPv6-adressen.
* Hallo virtuele machines met Hallo IPv6-adressen kan niet lid zijn van een Azure Cloud Service. Ze kunnen worden verbonden tooan Azure Virtual Network (VNet) en communiceren met elkaar via hun IPv4-adressen.
* Persoonlijke IPv6-adressen kunnen worden geïmplementeerd op afzonderlijke virtuele machines in een resourcegroep, maar kunnen niet worden geïmplementeerd in een resourcegroep via-Schaalsets.
* Virtuele machines in Azure kunnen geen verbinding maken via IPv6 tooother virtuele machines, andere Azure-services of on-premises apparaten. Ze kunnen alleen hello Azure load balancer communiceren via IPv6. Ze kunnen echter communiceren met deze andere resources met behulp van IPv4.
* Beveiliging van de Netwerkbeveiligingsgroep (NSG) voor IPv4 wordt ondersteund in implementaties van dual stack (IPv4 + IPv6). Nsg's toohello IPv6-eindpunten niet van toepassing.
* Hallo IPv6-eindpunt op Hallo VM niet is rechtstreeks blootgesteld toohello internet. Het is achter een load balancer. Alleen Hallo poorten die zijn opgegeven in de regels voor load balancer Hallo zijn toegankelijk via IPv6.
* Het wijzigen van Hallo IdleTimeout parameter voor IPv6 is **momenteel niet ondersteund**. Hallo standaardwaarde is vier minuten.
* Het wijzigen van Hallo loadDistributionMethod parameter voor IPv6 is **momenteel niet ondersteund**.
* Gereserveerd IP-IPv6-adressen (waarbij IPAllocationMethod = statisch) zijn **momenteel niet ondersteund**.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toodeploy een load balancer met IPv6.

* [Beschikbaarheid van IPv6 per regio](https://go.microsoft.com/fwlink/?linkid=828357)
* [Een load balancer met IPv6 met een sjabloon implementeren](load-balancer-ipv6-internet-template.md)
* [Implementeren van een load balancer met IPv6 met Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Implementeren van een load balancer met IPv6 met Azure CLI](load-balancer-ipv6-internet-cli.md)
