---
title: aaaCommon PowerShell-opdrachten voor Azure Virtual Networks | Microsoft Docs
description: Algemene PowerShell-opdrachten tooget die u beginnen met het opstellen van een virtueel netwerk en de bijbehorende bronnen voor virtuele machines.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Algemene PowerShell-opdrachten voor virtuele netwerken van Azure

Als u wilt dat toocreate een virtuele machine, moet u toocreate een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md) of weten over een bestaand virtueel netwerk in welke Hallo VM kan worden toegevoegd. Wanneer u een virtuele machine maakt, moet u doorgaans ook tooconsider maken Hallo resources in dit artikel wordt beschreven.

Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.

Sommige variabelen kunnen handig zijn voor u als meer dan één Hallo opdrachten in dit artikel wordt uitgevoerd:

- $location - locatie Hallo Hallo netwerkbronnen. U kunt [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind een [geografische regio](https://azure.microsoft.com/regions/) die voor u geschikt.
- $myResourceGroup - Hallo-naam van resourcegroep Hallo waarin Hallo netwerkbronnen bevinden.

## <a name="create-network-resources"></a>Maken van netwerkbronnen

| Taak | Opdracht |
| ---- | ------- |
| Subnetconfiguraties maken |$subnet1 = [nieuwe AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -naam 'mySubnet1' - AddressPrefix XX. X.X.X/XX<BR>$subnet2 = nieuwe AzureRmVirtualNetworkSubnetConfig-naam 'mySubnet2' - AddressPrefix XX. X.X.X/XX<BR><BR>Een typische netwerk wellicht een subnet voor een [internet gerichte load balancer](../../load-balancer/load-balancer-internet-overview.md) en een apart subnet voor een [interne load balancer](../../load-balancer/load-balancer-internal-overview.md). |
| Een virtueel netwerk maken |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -naam 'myVNet' - ResourceGroupName $myResourceGroup-locatie $location - AddressPrefix XX. X.X.X/XX-Subnet $subnet1, $subnet2 |
| Test voor een unieke domeinnaam |[Test AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) - DomainNameLabel 'myDNS'-locatie $location<BR><BR>U kunt opgeven dat een DNS-domeinnaam voor een [openbare IP-resource](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), die een toewijzing maakt voor voor domainname.location.cloudapp.azure.com toohello openbare IP-adres in hello Azure beheerde DNS-servers. Hallo-naam mag alleen letters, cijfers en afbreekstreepjes. Hallo eerste en laatste teken moet een letter of cijfer en Hallo-domeinnaam moet uniek zijn binnen de Azure-locatie. Als **waar** wordt geretourneerd, is de voorgestelde naam uniek. |
| Een openbaar IP-adres maken |$pip = [nieuw AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -naam 'myPublicIp' - ResourceGroupName $myResourceGroup - DomainNameLabel 'myDNS'-locatie $location - AllocationMethod dynamische<BR><BR>Hallo openbaar IP-adres gebruikt Hallo-domeinnaam die u eerder hebt getest en wordt gebruikt door Hallo frontend configuratie Hallo load balancer. |
| Maken van een frontend-IP-configuratie |$frontendIP = [nieuw AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -naam 'myFrontendIP' - PublicIpAddress $pip<BR><BR>Hallo frontend configuratie omvat het openbare IP-adres hello, die u eerder hebt gemaakt voor binnenkomend netwerkverkeer. |
| Een back-end-adresgroep maken |$beAddressPool = [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -naam 'myBackendAddressPool'<BR><BR>Biedt interne adressen voor back-end Hallo Hallo load balancer die toegankelijk zijn via een netwerkinterface. |
| Een test maken |$healthProbe = [nieuw AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -naam 'myProbe' - RequestPath 'HealthProbe.aspx'-Protocol http-poort 80 - IntervalInSeconds 15 - ProbeCount 2<BR><BR>Bevat de beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in Hallo back-end-adresgroep. |
| Een taakverdelingsregel maken |$lbRule = [nieuw AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -naam HTTP - FrontendIpConfiguration $frontendIP - BackendAddressPool $beAddressPool-$healthProbe Probe-Protocol Tcp - FrontendPort 80 - BackendPort 80<BR><BR>Bevat de regels die een openbare poort op Hallo load balancer tooa poort in Hallo back-end-adresgroep toewijzen. |
| Een binnenkomende NAT-regel maken |$inboundNATRule = [nieuw AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -naam 'myInboundRule1' - FrontendIpConfiguration $frontendIP-Protocol TCP - FrontendPort 3441 - BackendPort 3389<BR><BR>Bevat de regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in Hallo back-end-adresgroep. |
| Een load balancer maken |$loadBalancer = [nieuw AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) - ResourceGroupName $myResourceGroup-naam 'myLoadBalancer'-locatie $location - FrontendIpConfiguration $frontendIP - InboundNatRule $inboundNATRule - LoadBalancingRule $lbRule - BackendAddressPool $beAddressPool-$healthProbe-test |
| Een netwerkinterface maken |$nic1 = [nieuw AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) - ResourceGroupName $myResourceGroup-naam 'myNIC' - locatie $location - PrivateIpAddress XX. X.X.X-Subnet $subnet2 - LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] - loadbalancerinboundnatrule gebruikt $loadBalancer.InboundNatRules[0]<BR><BR>Maak een netwerkinterface Hallo openbare IP-adres en subnet van het virtuele netwerk dat u eerder hebt gemaakt. |

## <a name="get-information-about-network-resources"></a>Informatie over netwerkbronnen ophalen

| Taak | Opdracht |
| ---- | ------- |
| Lijst met virtuele netwerken |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) - ResourceGroupName $myResourceGroup<BR><BR>Geeft een lijst van alle Hallo virtuele netwerken in de resourcegroep Hallo. |
| Informatie ophalen over een virtueel netwerk |Get-AzureRmVirtualNetwork-naam 'myVNet' - ResourceGroupName $myResourceGroup |
| Lijst met subnetten in een virtueel netwerk |Get-AzureRmVirtualNetwork-naam 'myVNet' - ResourceGroupName $myResourceGroup &#124; Selecteer subnetten |
| Informatie ophalen over een subnet |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -naam 'mySubnet1' - VirtualNetwork $vnet<BR><BR>Hiermee haalt informatie over het Hallo-subnet in de opgegeven virtuele netwerk Hallo. Hallo $vnet waarde vertegenwoordigt Hallo-object geretourneerd door Get-AzureRmVirtualNetwork. |
| Lijst met IP-adressen |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) - ResourceGroupName $myResourceGroup<BR><BR>Openbare IP-adressen in de resourcegroep Hallo Hallo bevat. |
| Lijst met load balancers |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) - ResourceGroupName $myResourceGroup<BR><BR>Geeft een lijst van alle Hallo load balancers in de resourcegroep Hallo. |
| Lijst met netwerkinterfaces |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) - ResourceGroupName $myResourceGroup<BR><BR>Geeft een lijst van alle netwerkinterfaces Hallo in Hallo resourcegroep. |
| Informatie ophalen over een netwerkinterface |Get-AzureRmNetworkInterface-naam 'myNIC' - ResourceGroupName $myResourceGroup<BR><BR>Hiermee haalt u informatie over een specifieke netwerkinterface. |
| Hallo-IP-configuratie van een netwerkinterface ophalen |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -naam 'myNICIP' - NetworkInterface $nic<BR><BR>Hiermee haalt u informatie over Hallo IP-configuratie van opgegeven Hallo-netwerkinterface. Hallo $nic waarde vertegenwoordigt Hallo-object geretourneerd door Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Netwerkresources beheren

| Taak | Opdracht |
| ---- | ------- |
| Een subnet tooa virtueel netwerk toevoegen |[Voeg AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) - AddressPrefix XX. X.X.X/XX-naam 'mySubnet1' - VirtualNetwork $vnet<BR><BR>Voegt een subnet tooan bestaand virtueel netwerk. Hallo $vnet waarde vertegenwoordigt Hallo-object geretourneerd door Get-AzureRmVirtualNetwork. |
| Een virtueel netwerk verwijderen |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -naam 'myVNet' - ResourceGroupName $myResourceGroup<BR><BR>De opgegeven virtuele netwerk Hallo verwijdert uit Hallo resourcegroep. |
| Verwijderen van een netwerkinterface |[Verwijder AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -naam 'myNIC' - ResourceGroupName $myResourceGroup<BR><BR>Hallo opgegeven netwerkinterface verwijdert uit de resourcegroep Hallo. |
| Een load balancer verwijderen |[Verwijder AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -naam 'myLoadBalancer' - ResourceGroupName $myResourceGroup<BR><BR>Hiermee verwijdert u Hallo opgegeven load balancer van Hallo resourcegroep. |
| Een openbaar IP-adres verwijderen |[Verwijder AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-naam 'myIPAddress' - ResourceGroupName $myResourceGroup<BR><BR>Hiermee verwijdert u Hallo opgegeven openbare IP-adres van de resourcegroep Hallo. |

## <a name="next-steps"></a>Volgende stappen
* Gebruik Hallo netwerkinterface die u zojuist hebt gemaakt wanneer u [een virtuele machine maken](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Meer informatie over hoe u kunt [een virtuele machine maken met meerdere netwerkinterfaces](../../virtual-network/virtual-networks-multiple-nics.md).

