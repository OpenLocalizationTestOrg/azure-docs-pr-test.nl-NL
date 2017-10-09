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
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="85ef6-103">De Load Balancer op meerdere IP-configuraties met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="85ef6-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="85ef6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="85ef6-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="85ef6-105">CLI</span><span class="sxs-lookup"><span data-stu-id="85ef6-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="85ef6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85ef6-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="85ef6-107">Dit artikel wordt beschreven hoe toouse Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="85ef6-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="85ef6-108">In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="85ef6-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="85ef6-109">Elk van de secundaire Hallo NIC's, hebben twee IP-configuraties.</span><span class="sxs-lookup"><span data-stu-id="85ef6-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="85ef6-110">Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden tooone Hallo IP-configuraties op Hallo secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="85ef6-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="85ef6-111">We gebruiken Azure Load Balancer tooexpose twee frontend IP-adressen, één voor elke website, toodistribute verkeer toohello respectieve IP-configuratie voor Hallo-website.</span><span class="sxs-lookup"><span data-stu-id="85ef6-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="85ef6-112">Dit scenario maakt gebruik van hetzelfde poortnummer Hallo over zowel frontends, evenals het IP-adressen van zowel back-end-groep.</span><span class="sxs-lookup"><span data-stu-id="85ef6-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="85ef6-114">Stappen tooload verdelen over meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="85ef6-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="85ef6-115">Hallo stappen hieronder tooachieve Hallo scenario in dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="85ef6-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="85ef6-116">Installeer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85ef6-116">Install Azure PowerShell.</span></span> <span data-ttu-id="85ef6-117">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.</span><span class="sxs-lookup"><span data-stu-id="85ef6-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="85ef6-118">Maak een resourcegroep met Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="85ef6-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="85ef6-119">Zie voor meer informatie stap 2 van [een resourcegroep maken](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85ef6-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="85ef6-120">[Maken van een Beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85ef6-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="85ef6-121">Gebruik voor dit scenario Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="85ef6-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="85ef6-122">Volg de instructies stappen 3 tot en met 5 in [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artikel tooprepare Hallo maken van een virtuele machine met een enkele netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="85ef6-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="85ef6-123">Stap 6.1 uit te voeren en de volgende hello gebruiken in plaats van stap 6.2:</span><span class="sxs-lookup"><span data-stu-id="85ef6-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="85ef6-124">Voltooi [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6.3 via 6,8 stappen.</span><span class="sxs-lookup"><span data-stu-id="85ef6-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="85ef6-125">Voeg een tweede IP-configuratie tooeach Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85ef6-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="85ef6-126">Volg de instructies in Hallo [meerdere IP-adressen toewijzen toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artikel.</span><span class="sxs-lookup"><span data-stu-id="85ef6-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="85ef6-127">Hallo na configuratie-instellingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="85ef6-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="85ef6-128">U hoeft niet tooassociate Hallo secundaire IP-configuraties met openbare IP-adressen voor Hallo doel van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="85ef6-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="85ef6-129">Hallo opdracht tooremove Hallo openbare IP-koppeling onderdeel bewerken.</span><span class="sxs-lookup"><span data-stu-id="85ef6-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="85ef6-130">Voltooi de stappen 4 tot en met 6 van dit artikel opnieuw voor VM2.</span><span class="sxs-lookup"><span data-stu-id="85ef6-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="85ef6-131">Niet zeker tooreplace Hallo VM naam tooVM2 wanneer dit te doen.</span><span class="sxs-lookup"><span data-stu-id="85ef6-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="85ef6-132">Opmerking dat u niet toocreate een virtueel netwerk voor Hallo hoeft tweede VM.</span><span class="sxs-lookup"><span data-stu-id="85ef6-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="85ef6-133">U kunt of kan een nieuw subnet op basis van uw gebruiksvoorbeeld niet maken.</span><span class="sxs-lookup"><span data-stu-id="85ef6-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="85ef6-134">Twee openbare IP-adressen maken en deze opslaan op Hallo betreffende variabelen, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="85ef6-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="85ef6-135">Maak twee frontend-IP-configuraties:</span><span class="sxs-lookup"><span data-stu-id="85ef6-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="85ef6-136">Uw back-end-adresgroepen, een test en de load-balancingregels maken:</span><span class="sxs-lookup"><span data-stu-id="85ef6-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="85ef6-137">Zodra u deze resources die zijn gemaakt hebt, maakt u de load balancer:</span><span class="sxs-lookup"><span data-stu-id="85ef6-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="85ef6-138">Hallo tweede back-end adres pool en frontend IP-configuratie tooyour nieuwe load balancer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="85ef6-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="85ef6-139">Hallo onderstaande opdrachten Hallo NIC's ophalen en voegt u dat beide IP-configuraties van elke secundaire NIC toohello back-end-adresgroep Hallo de load balancer:</span><span class="sxs-lookup"><span data-stu-id="85ef6-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

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

13. <span data-ttu-id="85ef6-140">Tot slot moet u DNS-resource records toopoint toohello respectieve frontend IP-adres van de Load Balancer Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="85ef6-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="85ef6-141">U kunt uw domeinen in Azure DNS hosten.</span><span class="sxs-lookup"><span data-stu-id="85ef6-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="85ef6-142">Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="85ef6-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85ef6-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85ef6-143">Next steps</span></span>
- <span data-ttu-id="85ef6-144">Meer informatie over hoe toocombine load balancing-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="85ef6-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="85ef6-145">Meer informatie over hoe u verschillende typen Logboeken gebruiken in Azure toomanage en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="85ef6-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
