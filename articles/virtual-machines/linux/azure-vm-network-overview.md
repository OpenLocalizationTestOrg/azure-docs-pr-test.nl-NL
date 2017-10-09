---
title: aaaAzure en Linux VM-netwerk overzicht | Microsoft Docs
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
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure- en Linux-VM Network-overzicht
## <a name="virtual-networks"></a>Virtuele netwerken
Een Azure-netwerk (VNet) is een weergave van uw eigen netwerk in Hallo cloud. Het is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement. U kunt volledig Hallo IP-adresblokken, DNS-instellingen, beveiligingsbeleidsregels en routetabellen binnen dit netwerk beheren. U kunt ook verder segmenteren van uw VNet in subnetten en Azure IaaS virtuele machines (VM's) en/of cloudservices (PaaS-rolexemplaren) starten. Bovendien kunt u Hallo virtueel netwerk tooyour on-premises netwerk via een van de opties voor netwerkconnectiviteit Hallo beschikbaar in Azure. U kunt uw netwerk tooAzure, met volledige controle over IP-adresblokken met Hallo voordeel van het enterprise scale die Azure biedt in wezen kunt uitbreiden.

* [Overzicht van Virtual Network](../../virtual-network/virtual-networks-overview.md)

een VNet met behulp van toocreate hello Azure CLI, gaat u hier toofollow Hallo doorlopen.

* [Hoe een VNet met toocreate hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
Netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer tooyour VM-exemplaren in een virtueel netwerk. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet. Bovendien verkeer tooan afzonderlijke VM kan worden beperkt door een NSG koppelen verdere rechtstreeks toothat VM.

* [Wat is een netwerkbeveiligingsgroep (NSG)?](../../virtual-network/virtual-networks-nsg.md)
* [Hoe toocreate nsg's in Azure CLI Hallo](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Door de gebruiker gedefinieerde routes
Als u virtuele machines (VM's) tooa virtueel netwerk (VNet) in Azure toevoegt, ziet u dat Hallo virtuele machines kunnen toocommunicate met elkaar via Hallo netwerk, automatisch worden. U hoeft niet toospecify een gateway, ondanks het feit Hallo virtuele machines in verschillende subnetten. Hallo geldt ook voor communicatie vanaf Hallo VMs toohello Internet en zelfs tooyour on-premises netwerk wanneer u een hybride verbinding is tussen Azure tooyour eigenaar datacenter aanwezig is.

* [Wat zijn door de gebruiker gedefinieerde routes en Doorsturen via IP?](../../virtual-network/virtual-networks-udr-overview.md)
* [Maken van een UDR in hello Azure CLI](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Koppelen van een FQDN-naam tooyour Linux VM
Wanneer u een virtuele machine (VM) in hello Azure-portal maakt wordt met behulp van Hallo Resource Manager-implementatiemodel, een openbare IP-bron voor Hallo virtuele machine automatisch gemaakt. U gebruikt dit IP-adres tooremotely toegang Hallo VM. Hoewel het Hallo-portal maakt geen een FQDN-naam of FQDN-naam, standaard, kunt u een toevoegen wanneer Hallo VM is gemaakt.

* [Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Netwerkinterfaces
Een netwerkinterface (NIC) is een koppeling tussen een virtuele Machine (VM) en de onderliggende software netwerk Hallo Hallo. Dit artikel wordt uitgelegd wat een netwerkinterface is en hoe deze wordt gebruikt in hello Azure Resource Manager-implementatiemodel.

* [Virtuele netwerkinterfaces](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Virtuele NIC's en DNS-labels
Als u een server die u moet toobe permanente, maar die server wordt behandeld als runderen en is verwijderd en vaak geïmplementeerd, zult u toouse DNS-labels op de naam van uw NIC toopersist Hallo op Hallo VNET.  U wordt een permanent benoemde NIC met een statisch IP-adres instellen Hello te volgen procedure.

* [Een volledige Linux-omgeving maken met behulp van hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Virtuele netwerkgateways
Een virtuele netwerkgateway wordt gebruikt toosend netwerkverkeer tussen virtuele netwerken van Azure en de locaties van de lokale en ook tussen virtuele netwerken in Azure (VNet-naar-VNet). Wanneer u een VPN-gateway configureert, moet u een virtuele netwerkgateway en een virtuele netwerkgatewayverbinding maken en configureren.

* [Over VPN Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Interne Load Balancing
Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer. Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set. Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.

* [Maken van een interne load balancer hello Azure CLI gebruiken](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

