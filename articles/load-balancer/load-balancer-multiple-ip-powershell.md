---
title: aaaLoad balancing op meerdere IP-configuraties in Azure | Microsoft Docs
description: Taakverdeling over de primaire en secundaire IP-configuraties.
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>De Load Balancer op meerdere IP-configuraties met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Dit artikel wordt beschreven hoe toouse Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC). In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC. Elk van de secundaire Hallo NIC's, hebben twee IP-configuraties. Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden tooone Hallo IP-configuraties op Hallo secundaire NIC. We gebruiken Azure Load Balancer tooexpose twee frontend IP-adressen, één voor elke website, toodistribute verkeer toohello respectieve IP-configuratie voor Hallo-website. Dit scenario maakt gebruik van hetzelfde poortnummer Hallo over zowel frontends, evenals het IP-adressen van zowel back-end-groep.

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Stappen tooload verdelen over meerdere IP-configuraties

Hallo stappen hieronder tooachieve Hallo scenario in dit artikel wordt beschreven:

1. Installeer Azure PowerShell. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.
2. Maak een resourcegroep met Hallo volgende instellingen:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Zie voor meer informatie stap 2 van [een resourcegroep maken](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Maken van een Beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain uw virtuele machines. Gebruik voor dit scenario Hallo volgende opdracht:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Volg de instructies stappen 3 tot en met 5 in [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artikel tooprepare Hallo maken van een virtuele machine met een enkele netwerkinterfacekaart. Stap 6.1 uit te voeren en de volgende hello gebruiken in plaats van stap 6.2:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Voltooi [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6.3 via 6,8 stappen.

5. Voeg een tweede IP-configuratie tooeach Hallo virtuele machines. Volg de instructies in Hallo [meerdere IP-adressen toewijzen toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artikel. Hallo na configuratie-instellingen gebruiken:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    U hoeft niet tooassociate Hallo secundaire IP-configuraties met openbare IP-adressen voor Hallo doel van deze zelfstudie. Hallo opdracht tooremove Hallo openbare IP-koppeling onderdeel bewerken.

6. Voltooi de stappen 4 tot en met 6 van dit artikel opnieuw voor VM2. Niet zeker tooreplace Hallo VM naam tooVM2 wanneer dit te doen. Opmerking dat u niet toocreate een virtueel netwerk voor Hallo hoeft tweede VM. U kunt of kan een nieuw subnet op basis van uw gebruiksvoorbeeld niet maken.

7. Twee openbare IP-adressen maken en deze opslaan op Hallo betreffende variabelen, zoals wordt weergegeven:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Maak twee frontend-IP-configuraties:

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Uw back-end-adresgroepen, een test en de load-balancingregels maken:

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Zodra u deze resources die zijn gemaakt hebt, maakt u de load balancer:

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Hallo tweede back-end adres pool en frontend IP-configuratie tooyour nieuwe load balancer toevoegen:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. Hallo onderstaande opdrachten Hallo NIC's ophalen en voegt u dat beide IP-configuraties van elke secundaire NIC toohello back-end-adresgroep Hallo de load balancer:

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Tot slot moet u DNS-resource records toopoint toohello respectieve frontend IP-adres van de Load Balancer Hallo configureren. U kunt uw domeinen in Azure DNS hosten. Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hoe toocombine load balancing-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Meer informatie over hoe u verschillende typen Logboeken gebruiken in Azure toomanage en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).
