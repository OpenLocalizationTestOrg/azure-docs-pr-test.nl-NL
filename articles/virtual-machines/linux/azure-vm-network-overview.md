---
title: Overzicht van Azure- en Linux-VM-netwerk | Microsoft Docs
description: Een overzicht van Azure- en Linux-VM-netwerken.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 1ff4a0482d6dc6ec0eceaa89ca4b87ba1e2f89a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure- en Linux-VM Network-overzicht
## <a name="virtual-networks"></a>Virtuele netwerken
Een virtueel Azure-netwerk (VNet) is een weergave van uw eigen netwerk in de cloud. Het is een logische isolatie van de Azure-cloud die is toegewezen aan uw abonnement. U kunt de IP-adresblokken, DNS-instellingen, beveiligingsbeleidsregels en routetabellen binnen dit netwerk volledig beheren. U kunt ook verder segmenteren van uw VNet in subnetten en Azure IaaS virtuele machines (VM's) en/of cloudservices (PaaS-rolexemplaren) starten. Bovendien kunt u het virtuele netwerk verbinding maken met uw on-premises netwerk via een van de opties voor netwerkconnectiviteit die beschikbaar zijn in Azure. In wezen kunt u uw netwerk uitbreiden naar Azure met behoud van de volledige controle over IP-adresblokken en de schaalvoordelen van Azure voor ondernemingen.

* [Overzicht van Virtual Network](../../virtual-network/virtual-networks-overview.md)

Ga voor het maken van een VNet met behulp van de Azure CLI, Hier volgen de walk via.

* [Het maken van een VNet met de Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
Een netwerkbeveiligingsgroep (NSG) bevat een lijst met ACL-regels (Access Control List, toegangsbeheerlijst) waarmee netwerkverkeer voor uw VM-exemplaren in een virtueel netwerk wordt toegestaan of geweigerd. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Als een NSG is gekoppeld aan een subnet, zijn de ACL-regels van toepassing op alle VM-exemplaren in dat subnet. U kunt het verkeer naar een afzonderlijke VM nog verder beperken door een NSG rechtstreeks aan die VM te koppelen.

* [Wat is een netwerkbeveiligingsgroep (NSG)?](../../virtual-network/virtual-networks-nsg.md)
* [NSG's maken in Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Door de gebruiker gedefinieerde routes
Als u virtuele machines (VM's) aan een virtueel netwerk (VNet) in Azure toevoegt, ziet u dat de virtuele machines automatisch met elkaar kunnen communiceren via het netwerk. U hoeft geen gateway op te geven, ook niet als de virtuele machines tot verschillende subnetten behoren. Hetzelfde geldt voor de communicatie tussen VM's en internet. Als er een hybride verbinding is tussen Azure en uw eigen datacentrum, is er zelfs communicatie met uw on-premises netwerk mogelijk.

* [Wat zijn door de gebruiker gedefinieerde routes en Doorsturen via IP?](../../virtual-network/virtual-networks-udr-overview.md)
* [Een UDR maken in de Azure CLI](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-to-your-linux-vm"></a>Een FQDN-naam van uw virtuele Linux-machine koppelen
Wanneer u een virtuele machine (VM) in de Azure portal met het implementatiemodel van Resource Manager maakt, wordt er automatisch een openbare IP-resource voor de virtuele machine gemaakt. U kunt dit IP-adres gebruiken voor externe toegang tot de virtuele machine. Hoewel de portal een FQDN-naam of FQDN standaard niet maken biedt, kunt u een toevoegen wanneer de virtuele machine is gemaakt.

* [Maken van een volledig gekwalificeerde domeinnaam in de Azure portal](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Netwerkinterfaces
Een netwerkinterface (NIC) is de onderlinge verbinding tussen een virtuele machine (VM) en het onderliggende softwarenetwerk. In dit artikel wordt uitgelegd wat een netwerkinterface is en hoe deze wordt gebruikt in het Azure Resource Manager-implementatiemodel.

* [Virtuele netwerkinterfaces](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Virtuele NIC's en DNS-labels
Als u een server die u moet persistent hebt, maar dat server wordt behandeld als runderen en is verwijderd en vaak geïmplementeerd, wilt u DNS-labels op uw NIC gebruiken om vast te leggen van de naam in het VNET.  Met de volgende procedure stelt u een permanent benoemde NIC met een statisch IP-adres.

* [Een volledige Linux-omgeving maken met behulp van de Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Virtuele netwerkgateways
Een virtuele netwerkgateway wordt gebruikt voor het verzenden van netwerkverkeer tussen virtuele netwerken van Azure en on-premises locaties, evenals tussen virtuele netwerken in Azure (VNet-naar-VNet). Wanneer u een VPN-gateway configureert, moet u een virtuele netwerkgateway en een virtuele netwerkgatewayverbinding maken en configureren.

* [Over VPN Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Interne Load Balancing
Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer. De load balancer biedt hoge beschikbaarheid bij het verdelen van inkomend verkeer over gezonde service-exemplaren in cloudservices of virtuele machines in een load balancer-set. Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.

* [Maken van een interne load balancer met de Azure CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

