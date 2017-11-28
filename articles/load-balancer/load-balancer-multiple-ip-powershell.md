---
title: De Load Balancer op meerdere IP-configuraties in Azure | Microsoft Docs
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
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="0c7d1-103">De Load Balancer op meerdere IP-configuraties met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c7d1-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c7d1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0c7d1-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="0c7d1-105">CLI</span><span class="sxs-lookup"><span data-stu-id="0c7d1-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="0c7d1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c7d1-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="0c7d1-107">Dit artikel wordt beschreven hoe u Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="0c7d1-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="0c7d1-108">In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="0c7d1-109">Elk van de secundaire NIC's twee IP-configuraties hebben.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="0c7d1-110">Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden aan een van de IP-configuraties voor de secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="0c7d1-111">We Azure Load Balancer gebruiken om twee IP-adressen voor frontend, één voor elke website, voor het distribueren van het verkeer naar de respectieve IP-configuratie voor de website weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="0c7d1-112">Dit scenario gebruikt hetzelfde poortnummer op zowel frontends, evenals het IP-adressen van zowel back-end-groep.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="0c7d1-114">Stappen om taken te verdelen over meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="0c7d1-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="0c7d1-115">Volg onderstaande stappen voor het bereiken van het scenario in dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="0c7d1-116">Installeer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-116">Install Azure PowerShell.</span></span> <span data-ttu-id="0c7d1-117">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor informatie over het installeren van de nieuwste versie van Azure PowerShell, het selecteren van het abonnement en het aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="0c7d1-118">Maak een resourcegroep met de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="0c7d1-119">Zie voor meer informatie stap 2 van [een resourcegroep maken](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c7d1-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="0c7d1-120">[Maken van een Beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) uw virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="0c7d1-121">In dit scenario moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="0c7d1-122">Volg de instructies stappen 3 tot en met 5 in [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artikel voor het voorbereiden van het maken van een virtuele machine met een enkele netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="0c7d1-123">6.1 stap uit te voeren en de volgende opdracht gebruiken in plaats van stap 6.2:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="0c7d1-124">Voltooi [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6.3 via 6,8 stappen.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="0c7d1-125">Een tweede IP-configuratie toevoegen aan elk van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="0c7d1-126">Volg de instructies in [meerdere IP-adressen toewijzen aan virtuele machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artikel.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="0c7d1-127">Gebruik de volgende configuratieinstellingen:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="0c7d1-128">U hoeft niet te koppelen van de secundaire IP-configuraties met openbare IP-adressen voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="0c7d1-129">Bewerk de opdracht voor het verwijderen van het openbare deel van de IP-koppeling.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="0c7d1-130">Voltooi de stappen 4 tot en met 6 van dit artikel opnieuw voor VM2.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="0c7d1-131">Zorg ervoor dat de naam van de VM naar VM2 vervangen wanneer dit te doen.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="0c7d1-132">Houd er rekening mee dat u niet wilt maken van een virtueel netwerk voor de tweede VM.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="0c7d1-133">U kunt of kan een nieuw subnet op basis van uw gebruiksvoorbeeld niet maken.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="0c7d1-134">Twee openbare IP-adressen maken en deze opslaan op de juiste variabelen, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="0c7d1-135">Maak twee frontend-IP-configuraties:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="0c7d1-136">Uw back-end-adresgroepen, een test en de load-balancingregels maken:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="0c7d1-137">Zodra u deze resources die zijn gemaakt hebt, maakt u de load balancer:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="0c7d1-138">De tweede back-end-pool en frontend IP-adresconfiguratie toevoegen aan de zojuist gemaakte load balancer:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="0c7d1-139">De onderstaande opdrachten de NIC's ophalen en vervolgens beide IP-configuraties van elke secundaire NIC toe te voegen aan de back-end-adresgroep van de load balancer:</span><span class="sxs-lookup"><span data-stu-id="0c7d1-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

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

13. <span data-ttu-id="0c7d1-140">Tot slot moet u DNS-bronrecords om te verwijzen naar de respectieve frontend-IP-adres van de Load Balancer configureren.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="0c7d1-141">U kunt uw domeinen in Azure DNS hosten.</span><span class="sxs-lookup"><span data-stu-id="0c7d1-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="0c7d1-142">Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0c7d1-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c7d1-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c7d1-143">Next steps</span></span>
- <span data-ttu-id="0c7d1-144">Meer informatie over het combineren van de load balancer-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0c7d1-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="0c7d1-145">Meer informatie over hoe u verschillende typen logboeken kunt gebruiken in Azure te beheren en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="0c7d1-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
