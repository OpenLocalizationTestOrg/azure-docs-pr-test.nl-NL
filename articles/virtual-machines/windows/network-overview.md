---
title: aaaVirtual netwerken en Windows virtuele machines in Azure | Microsoft Docs
description: Meer informatie over het netwerk als deze zich toohello basisbeginselen verhoudt van het maken van virtuele Windows-machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Virtuele netwerken en virtuele Windows-machines in Azure 

Wanneer u een virtuele Azure-machine maakt, moet u een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md) (VNet) maken of een bestaand VNet gebruiken. U moet ook toodecide hoe uw virtuele machines beoogde toobe geopend op Hallo VNet worden. Het is belangrijk te[-abonnement gebruikt voordat het maken van resources](../../virtual-network/virtual-network-vnet-plan-design-arm.md) en zorg ervoor dat u Hallo begrijpt [grenzen van netwerkresources](../../azure-subscription-service-limits.md#networking-limits).

Virtuele machines worden in Hallo volgende afbeelding, weergegeven als webservers en databaseservers. Elke set van virtuele machines zijn tooseparate subnetten in VNet Hallo toegewezen.

![Azure Virtual Network](./media/network-overview/vnetoverview.png)

U kunt een VNet maken voordat u een virtuele machine maken of u Hallo VNet maken kunt bij het maken van een virtuele machine. U moet ofwel zelf een VNet maken of er moet er een voor u worden gemaakt wanneer u een virtuele machine maakt.

U maakt deze resources toosupport communicatie met een virtuele machine:

- Netwerkinterfaces
- IP-adressen
- Virtueel netwerk en subnetten

Bovendien toothose basic resources, moet u ook overwegen deze optionele resources:

- Netwerkbeveiligingsgroepen
- Load balancers 

## <a name="network-interfaces"></a>Netwerkinterfaces

Een [netwerkinterface (NIC)](../../virtual-network/virtual-network-network-interface.md) Hallo koppeling tussen een virtuele machine en een virtueel netwerk (VNet) is. Een virtuele machine moet ten minste één NIC hebt, maar u kunt meer dan één hebben, afhankelijk van de grootte Hallo Hallo VM die u maakt. Meer informatie over het aantal NIC's dat elke VM-grootte ondersteunt, vindt u in [Grootten voor virtuele machines in Azure](sizes.md). 

Als u een virtuele machine met meer dan één NIC toocreate wilt, moet u Hallo VM maken met ten minste twee.  Na het maken kunt u extra netwerkinterfacekaarten up toohello dat wordt ondersteund door de VM-grootte hello, toevoegen, maar u kunt geen extra NIC's tooa alleen gemaakt met een virtuele machine toevoegen, ongeacht hoeveel NIC's Hallo VM-grootte ondersteunt. 

Als Hallo VM wordt tooan beschikbaarheidsset toegevoegd, moeten alle virtuele machines binnen de beschikbaarheidsset Hallo een of meerdere NIC's hebben. Virtuele machines met meer dan één NIC zijn niet vereist toohave Hallo hetzelfde aantal NIC's, maar deze moeten alle hebben ten minste twee.

Elke NIC die is gekoppeld tooa VM moet aanwezig zijn in Hallo dezelfde locatie en abonnement zoals Hallo VM. Elke NIC moet worden verbonden tooa VNet dat in Hallo dezelfde bestaat Azure-locatie en het abonnement, zoals Hallo NIC. Nadat een NIC is gemaakt, kunt u Hallo-subnet die is verbonden met, maar u kunt Hallo VNet verbonden met niet wijzigen.  Elke NIC gekoppeld tooa die VM is toegewezen MAC-adres dat niet verandert tot Hallo VM worden verwijderd.

Deze tabel bevat Hallo methoden waarmee u toocreate een netwerkinterface kunt.

| Methode | Beschrijving |
| ------ | ----------- |
| Azure Portal | Wanneer u een virtuele machine in hello Azure-portal maakt, wordt een netwerkinterface automatisch voor u (u kunt een NIC die u maakt u een afzonderlijk niet gebruiken) gemaakt. Hallo-portal maakt u een virtuele machine met slechts één NIC Als u een virtuele machine met meer dan één NIC toocreate wilt, moet u deze maken met een andere methode. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Gebruik [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) Hello **- PublicIpAddressId** parameter tooprovide Hallo-id van het openbare IP-adres hello, die u eerder hebt gemaakt. |
| [Azure-CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | tooprovide Hallo-id van Hallo openbare IP-adres dat u eerder gemaakte gebruik [az netwerk nic maken](https://docs.microsoft.com/cli/azure/network/nic#create) Hello **--openbare-ip-adres** parameter. |
| [Sjabloon](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Gebruik [Netwerkinterface in een virtueel netwerk met openbaar IP-adres](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) als richtlijn voor het implementeren van een netwerkinterface met behulp van een sjabloon. |

## <a name="ip-addresses"></a>IP-adressen 

U kunt deze typen [IP-adressen](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa NIC in Azure:

- **Openbare IP-adressen** -toocommunicate binnenkomende en uitgaande (zonder NAT (Netwerkadresomzetting)) gebruikt met Hallo Internet en andere Azure-resources niet tooa VNet verbonden. Het toewijzen van een openbare IP-adres tooa is NIC optioneel. Openbare IP-adressen hebben geringe kosten en er is een maximum aantal dat per abonnement kan worden gebruikt.
- **Privé IP-adressen** : wordt gebruikt voor communicatie binnen een VNet, uw on-premises netwerk en Hallo Internet (met NAT). U moet ten minste één persoonlijke IP-adres tooa VM toewijzen. toolearn meer informatie over NAT in Azure, lezen [inzicht in uitgaande verbindingen in Azure](../../load-balancer/load-balancer-outbound-connections.md).

U kunt openbare IP-adressen tooVMs of netwerktaakverdelers internetgerichte toewijzen. U kunt privé IP-adressen tooVMs en interne load balancers kunt toewijzen. U toewijzen IP-adressen tooa VM die gebruikmaakt van een netwerkinterface.

Er zijn twee manieren waarop een IP-adres tooa resource - dynamische of statische is toegewezen. Hallo standaard toewijzingsmethode is dynamisch, wanneer een IP-adres niet toegewezen is wanneer deze wordt gemaakt. Hallo IP-adres is in plaats daarvan toegewezen wanneer u een virtuele machine maken of een gestopte VM start. Hallo IP-adres is uitgebracht als u Hallo VM verwijderen of stoppen. 

tooensure hello IP-adres voor de virtuele machine blijft Hallo Hallo dezelfde, kunt u de toewijzingsmethode Hallo expliciet instellen toostatic. In dat geval wordt er onmiddellijk een IP-adres toegewezen. Wanneer u Hallo VM verwijderen of wijzigen van de toewijzing van methode toodynamic wordt vrijgegeven.
    
Deze tabel bevat Hallo methoden waarmee u toocreate een IP-adres kunt.

| Methode | Beschrijving |
| ------ | ----------- |
| [Azure Portal](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Standaard openbare IP-adressen dynamisch zijn en Hallo-adres is gekoppeld toothem kan veranderen wanneer Hallo VM is gestopt of verwijderd. maakt gebruik van tooguarantee die VM altijd Hallo Hallo hetzelfde openbare IP-adres, een statische openbare IP-adres maken. Standaard wijst Hallo portal een dynamische particuliere IP-adres tooa NIC bij het maken van een virtuele machine. U kunt deze toostatic wijzigen na Hallo die virtuele machine wordt gemaakt.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | U gebruikt [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) Hello **- AllocationMethod** parameter als dynamische of statische. |
| [Azure-CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | U gebruikt [az netwerk openbare ip-maken](https://docs.microsoft.com/cli/azure/network/public-ip#create) Hello **--toewijzingsmethode** parameter als dynamische of statische. |
| [Sjabloon](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Gebruik [Netwerkinterface in een virtueel netwerk met openbaar IP-adres](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) als richtlijn voor het implementeren van een openbaar IP-adres met behulp van een sjabloon. |

Nadat u een openbaar IP-adres hebt gemaakt, kunt u deze met een VM koppelen toe te wijzen tooa NIC.

## <a name="virtual-network-and-subnets"></a>Virtueel netwerk en subnetten

Een subnet is een bereik met IP-adressen in Hallo VNet. U kunt u een VNET onderverdelen in meerdere subnetten voor organisatie- en beveiligingsdoeleinden. Elke NIC in een VM is verbonden tooone subnet in een VNet. NIC's aangesloten toosubnets (dezelfde of verschillende) binnen een VNet kunnen met elkaar communiceren zonder extra configuratie.

Wanneer u een VNet hebt ingesteld, geeft u Hallo-topologie, met inbegrip van Hallo beschikbaar adresruimten en subnetten. Als Hallo VNet toobe verbonden tooother VNets of on-premises netwerken, moet u adresbereiken die elkaar niet overlappen. Hallo IP-adressen privé zijn en niet toegankelijk vanuit Hallo Internet; dit geldt alleen voor niet-routeable IP-adressen zoals 10.0.0.0/8, 172.16.0.0/12 of 192.168.0.0/16 Hallo is. Azure wordt nu een adresbereik beschouwd als onderdeel van Hallo persoonlijke VNet IP-adresruimte die alleen bereikbaar binnen Hallo VNet, binnen VNets met elkaar verbonden en naar uw on-premises locatie. 

Als u binnen een organisatie waarin iemand anders verantwoordelijk voor interne netwerken Hallo is werkt, moet u contact opnemen toothat persoon voordat u uw adresruimte selecteert. Zorg ervoor dat er is geen overlapping en laat ze weten Hallo ruimte toouse zodat ze niet proberen toouse Hallo hetzelfde bereik van IP-adressen. 

Er is standaard geen beveiligingsgrens tussen subnetten, zodat virtuele machines in elk van deze subnetten tooone praten kunnen een andere. U kunt echter Netwerkbeveiligingsgroepen (nsg's), waarmee u toocontrol Hallo verkeer stroom tooand van subnetten en tooand van VM's instellen. 

Deze tabel bevat Hallo methoden waarmee u toocreate een VNet en subnetten kunt.   

| Methode | Beschrijving |
| ------ | ----------- |
| [Azure Portal](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Als u toestaat dat Azure een VNet maken wanneer u een virtuele machine maakt, Hallo-naam is een combinatie van Hallo Resourcegroepnaam met Hallo VNet en **- vnet**. Hallo-adresruimte is 10.0.0.0/24, Hallo vereist subnetnaam **standaard**, en Hallo subnet-adresbereik 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | U gebruikt [nieuw AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) en [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate een subnet en een VNet. U kunt ook [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd een subnet tooan bestaande VNet. |
| [Azure-CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hallo subnet en Hallo VNet worden gemaakt op Hallo dezelfde tijd. Geef een **--subnet naam** parameter te[az network vnet maken](https://docs.microsoft.com/cli/azure/network/vnet#create) met Hallo subnetnaam. |
| [Sjabloon](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Hallo gemakkelijkste manier toocreate een VNet en subnetten is een bestaande sjabloon toodownload zoals [virtueel netwerk met twee subnetten](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets), en voor uw behoeften te wijzigen. |

## <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen

Een [netwerkbeveiligingsgroep (NSG)](../../virtual-network/virtual-networks-nsg.md) bevat een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer toosubnets of NIC's. Nsg's kunnen worden gekoppeld aan subnetten of afzonderlijke NIC's aangesloten tooa subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall hello, virtuele machines in dat subnet. Afzonderlijke NIC kan worden beperkt door een NSG koppelen tooan bovendien het verkeer rechtstreeks tooa NIC.

NSG's bevatten twee sets met regels: een set met regels voor binnenkomend verkeer en een set met regels voor uitgaand verkeer. Hallo-prioriteit voor een regel moet uniek zijn binnen elke set. Elke regel heeft eigenschappen voor protocol, bron- en doelpoortbereik, adresvoorvoegsels, richting van verkeer, prioriteit en toegangstype. 

Alle NSG's bevatten een set met standaardregels. Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze de laagste prioriteit Hallo zijn toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt. 

Als u een NSG tooa NIC koppelt, zijn Hallo netwerktoegangsregels in Hallo NSG toegepaste alleen toothat NIC. Als u een NSG wordt toegepast tooa enkel NIC op een VM meerdere NIC's deze heeft geen invloed op verkeer toohello andere NIC's. U kunt verschillende nsg's tooa NIC (of virtuele machine, afhankelijk van het implementatiemodel Hallo) koppelen en Hallo subnet dat een NIC of VM is gebonden aan. Prioriteit krijgt op basis van de Hallo richting van verkeer.

Zorg ervoor dat te[plan](../../virtual-network/virtual-networks-nsg.md#planning) uw nsg's wanneer u van plan uw VM's en VNet bent.

Deze tabel bevat Hallo methoden waarmee u een netwerkbeveiligingsgroep toocreate kunt.

| Methode | Beschrijving |
| ------ | ----------- |
| [Azure Portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Wanneer u een virtuele machine in hello Azure-portal maakt, een NSG wordt automatisch gemaakt en gekoppeld toohello NIC Hallo portal maakt. de naam van de Hallo Hallo NSG is een combinatie van naam Hallo Hallo VM en **- nsg**. Deze NSG bevat één binnenkomende regel met een prioriteit 1000, service set tooRDP, Hallo protocol set tooTCP, poort ingesteld too3389 en tooAllow ingesteld. Als u op elk andere binnenkomend verkeer toohello VM tooallow wilt, moet u extra regels toohello NSG toevoegen. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Gebruik [nieuw AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) en Hallo vereist regel informatie te bieden. Gebruik [nieuw AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG. Gebruik [Set AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello NSG voor subnet Hallo. Gebruik [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello VNet. |
| [Azure-CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Gebruik [az netwerk nsg maken](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially hello NSG maken. Gebruik [az netwerk nsg regel maken](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd toohello NSG regels. Gebruik [az network vnet subnet update](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) tooadd hello NSG toohello subnet. |
| [Sjabloon](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Gebruik [Een netwerkbeveiligingsgroep maken](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) als richtlijn voor het implementeren van een netwerkbeveiligingsgroep met behulp van een sjabloon. |

## <a name="load-balancers"></a>Load balancers

[Azure Load Balancer](../../load-balancer/load-balancer-overview.md) tooyour toepassingen voor hoge beschikbaarheid en netwerk prestaties levert. Een load balancer te kan worden geconfigureerd[saldo Binnenkomend internetverkeer](../../load-balancer/load-balancer-internet-overview.md) tooVMs of [verkeer tussen VM's in een VNet in evenwicht](../../load-balancer/load-balancer-internal-overview.md). Een load balancer kan ook worden verdeeld verkeer tussen lokale computers en virtuele machines in een cross-premises netwerk of doorsturen externe verkeer tooa specifieke virtuele machine.

Hallo load balancer maps binnenkomende en uitgaande verkeer tussen Hallo openbare IP-adres en poort op Hallo load balancer en Hallo privé IP-adres en poort van Hallo VM.

Wanneer u een load balancer maakt, moet u ook rekening houden met deze configuratie-elementen:

- **Front-end IP-adresconfiguratie**: een load balancer kan een of meer front-end IP-adressen bevatten, ook wel bekend als virtuele IP-adressen (VIP's). Deze IP-adressen fungeren als inkomend voor Hallo-verkeer.
- **Back-end-adresgroep** – IP-adressen die zijn gekoppeld aan Hallo NIC toowhich load wordt gedistribueerd.
- **NAT-regels** -definieert hoe binnenkomend verkeer stroomt via Hallo front-end-IP-adres en gedistribueerde toohello backend-IP.
- **Taakverdelingsregels** -toewijzingen van een opgegeven front-end-IP en een poort combinatie tooa backend-IP-adressen en poort. Een enkele load balancer kan meerdere regels voor taakverdeling bevatten. Elke regel is een combinatie van een front-end IP en poort en back-end IP en poort die is gekoppeld aan virtuele machines.
- **[Tests](../../load-balancer/load-balancer-custom-probe-overview.md)**  -Monitors Hallo status van virtuele machines. Wanneer een test toorespond mislukt Hallo load balancer stopt het verzenden van nieuwe verbindingen toohello slecht VM. Hallo bestaande verbindingen worden niet beïnvloed en nieuwe verbindingen toohealthy virtuele machines worden verzonden.

Deze tabel bevat Hallo methoden waarmee u toocreate een internetgerichte load balancer kunt.

| Methode | Beschrijving |
| ------ | ----------- |
| Azure Portal | U een internet gerichte load balancer hello Azure-portal met kan momenteel niet maken. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | tooprovide Hallo-id van Hallo openbare IP-adres dat u eerder gemaakte gebruik [nieuw AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) Hello **- PublicIpAddress** parameter. Gebruik [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate Hallo configuratie van Hallo back-end-adresgroep. Gebruik [nieuw AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate binnenkomende NAT-regels die zijn gekoppeld aan het front-end-IP-configuratie hello, die u hebt gemaakt. Gebruik [nieuw AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Hallo-tests dat u nodig hebt. Gebruik [nieuw AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate Hallo load balancer-configuratie. Gebruik [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate Hallo load balancer.|
| [Azure-CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Gebruik [az network Load Balancer maken](https://docs.microsoft.com/cli/azure/network/lb#create) toocreate Hallo initiële load balancer-configuratie. Gebruik [az netwerk lb frontend-ip maken](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd Hallo openbare IP-adres dat u eerder hebt gemaakt. Gebruik [az netwerk lb-adresgroep maken](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd Hallo configuratie van Hallo back-end-adresgroep. Gebruik [az netwerk lb-nat-regel voor binnenkomende verbindingen maken](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT-regels. Gebruik [az network Load Balancer-regel maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd Hallo load balancer-regels. Gebruik [az network Load Balancer-test maken](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Hallo tests. |
| [Sjabloon](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Gebruik [2 virtuele machines in een Load Balancer en NAT-regels configureren op Hallo LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) als richtlijn voor het implementeren van een load balancer met een sjabloon. |
    
Deze tabel bevat Hallo methoden waarmee u een interne load balancer toocreate kunt.

| Methode | Beschrijving |
| ------ | ----------- |
| Azure Portal | U kunt geen momenteel een interne load balancer met hello Azure-portal maken. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | een persoonlijke IP-adres in netwerksubnet hello, gebruik tooprovide [nieuw AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) Hello **- PrivateIpAddress** parameter. Gebruik [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate Hallo configuratie van Hallo back-end-adresgroep. Gebruik [nieuw AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate binnenkomende NAT-regels die zijn gekoppeld aan het front-end-IP-configuratie hello, die u hebt gemaakt. Gebruik [nieuw AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Hallo-tests dat u nodig hebt. Gebruik [nieuw AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate Hallo load balancer-configuratie. Gebruik [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate Hallo load balancer.|
| [Azure-CLI](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Gebruik Hallo [az network Load Balancer maken](https://docs.microsoft.com/cli/azure/network/lb#create) opdracht toocreate Hallo initiële load balancer-configuratie. toodefine hello privé IP-adres, gebruik [az netwerk lb frontend-ip maken](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) Hello **--privé-ip-adres** parameter. Gebruik [az netwerk lb-adresgroep maken](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd Hallo configuratie van Hallo back-end-adresgroep. Gebruik [az netwerk lb-nat-regel voor binnenkomende verbindingen maken](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT-regels. Gebruik [az network Load Balancer-regel maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd Hallo load balancer-regels. Gebruik [az network Load Balancer-test maken](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Hallo tests.|
| [Sjabloon](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Gebruik [2 virtuele machines in een Load Balancer en NAT-regels configureren op Hallo LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) als richtlijn voor het implementeren van een load balancer met een sjabloon. |

## <a name="vms"></a>VM's

Virtuele machines kunnen worden gemaakt in Hallo hetzelfde VNet en ze verbinding kunnen maken van andere tooeach met particuliere IP-adressen. Ze verbinding kunnen maken zelfs als ze zich in verschillende subnetten zonder Hallo nodig tooconfigure een gateway of openbare IP-adressen gebruiken. virtuele machines in een VNet tooput, u Hallo VNet maken en vervolgens bij het maken van elke VM, wijst u deze toohello VNet en het subnet. VM's verkrijgen hun netwerkinstellingen tijdens de implementatie of tijdens het opstarten.  

Aan virtuele machines wordt een IP-adres toegewezen wanneer deze worden geïmplementeerd. Als u meerdere virtuele machines in een VNet of subnet implementeert, worden er IP-adressen aan toegewezen als ze opstarten. Dynamische IP-adressen (DIP) is Hallo interne IP-adres die zijn gekoppeld aan een virtuele machine. U kunt een statische DIP tooa VM toewijzen. Als u een statisch DIP toewijst, moet u rekening houden met behulp van een specifiek subnet tooavoid per ongeluk een statische DIP opnieuw te gebruiken voor een andere virtuele machine.  

Als u een virtuele machine maken en later toomigrate wilt deze in een VNet, het is niet een eenvoudige configuratiewijziging. U moet Hallo VM in Hallo VNet opnieuw implementeren. Hallo gemakkelijkste manier tooredeploy is toodelete Hallo VM, maar niet alle schijven gekoppeld tooit en vervolgens opnieuw maken Hallo virtuele machine met behulp van Hallo oorspronkelijke schijven in Hallo VNet. 

Deze tabel bevat Hallo-methoden die u kunt toocreate een virtuele machine in een VNet gebruiken.

| Methode | Beschrijving |
| ------ | ----------- |
| [Azure Portal](../virtual-machines-windows-hero-tutorial.md) | Hallo netwerk de standaardinstellingen gebruikt die eerder werden vermeld toocreate een virtuele machine met een enkele netwerkinterfacekaart. toocreate met meerdere NIC's een virtuele machine, moet u een andere methode gebruiken. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Gebruik van Hallo bevat [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd Hallo NIC dat u eerder hebt gemaakt toohello VM-configuratie. |
| [Sjabloon](ps-template.md) | Gebruik [Zeer eenvoudige implementatie van een virtuele Windows-machine](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) als richtlijn voor het implementeren van een virtuele machine met behulp van een sjabloon. |

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe tooconfigure [gebruiker gedefinieerde routes en doorsturen via IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Meer informatie over hoe tooconfigure [tooVNet-VNet-verbindingen](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Meer informatie over hoe te[routes oplossen](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
