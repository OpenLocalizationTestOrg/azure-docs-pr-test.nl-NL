---
title: Een internetgerichte load balancer maken - PowerShell | Microsoft Docs
description: Meer informatie over hoe u met behulp van PowerShell een internetgerichte load balancer maakt in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="c68d9-103"><a name="get-started"></a>Een internetgerichte load balancer maken in Resource Manager met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c68d9-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c68d9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c68d9-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="c68d9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c68d9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="c68d9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c68d9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="c68d9-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="c68d9-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c68d9-108">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c68d9-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c68d9-109">Hier vindt u [meer informatie over hoe u een internetgerichte load balancer maakt met het klassieke implementatiemodel](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c68d9-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="c68d9-110">De oplossing implementeren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c68d9-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="c68d9-111">De volgende procedures laten zien hoe u Azure Resource Manager gebruikt om een internetgerichte load balancer te maken met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c68d9-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="c68d9-112">Met Azure Resource Manager wordt elke resource afzonderlijk gemaakt en geconfigureerd, en vervolgens samengevoegd om een load balancer te maken.</span><span class="sxs-lookup"><span data-stu-id="c68d9-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="c68d9-113">U moet de volgende objecten maken en configureren om een load balancer te implementeren:</span><span class="sxs-lookup"><span data-stu-id="c68d9-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="c68d9-114">Front-end-IP-configuratie: bevat openbare IP-adressen (PIP) voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="c68d9-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="c68d9-115">Back-endadresgroep: bevat netwerkinterfaces (NIC's) waardoor de virtuele machines netwerkverkeer kunnen ontvangen van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="c68d9-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="c68d9-116">Regels voor taakverdeling: bevat regels die een openbare poort op de load balancer toewijst aan een poort in de back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="c68d9-117">Inkomende NAT-regels: bevat regels die een openbare poort op de load balancer toewijst aan een poort voor een specifieke virtuele machine in de back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="c68d9-118">Tests: bevat statustests die worden gebruikt om de beschikbaarheid van exemplaren van virtuele machines in de back-endadresgroep te controleren.</span><span class="sxs-lookup"><span data-stu-id="c68d9-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="c68d9-119">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c68d9-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="c68d9-120">PowerShell instellen voor het gebruik van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c68d9-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="c68d9-121">Zorg ervoor dat u de nieuwste productieversie van de Azure Resource Manager-module voor PowerShell hebt:</span><span class="sxs-lookup"><span data-stu-id="c68d9-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="c68d9-122">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="c68d9-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="c68d9-123">Voer uw referenties in wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="c68d9-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="c68d9-124">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="c68d9-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="c68d9-125">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c68d9-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="c68d9-126">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-126">Create a resource group.</span></span> <span data-ttu-id="c68d9-127">(Sla deze stap over als u een bestaande resourcegroep gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="c68d9-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="c68d9-128">Een virtueel netwerk en een openbaar IP-adres voor de front-end-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="c68d9-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="c68d9-129">Maak een subnet en een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c68d9-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="c68d9-130">Maak een openbare IP-adresresource voor Azure met de naam **PublicIP** dat moet worden gebruikt door een front-end-IP-adresgroep met de DNS-naam **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="c68d9-131">De volgende opdracht maakt gebruik van het statische toewijzingstype.</span><span class="sxs-lookup"><span data-stu-id="c68d9-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="c68d9-132">De load balancer gebruikt het domeinlabel van het openbare IP als voorvoegsel voor de FQDN.</span><span class="sxs-lookup"><span data-stu-id="c68d9-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="c68d9-133">Dit wijkt af van het klassieke implementatiemodel, waarbij de cloudservice wordt gebruikt als de FQDN voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="c68d9-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="c68d9-134">In dit voorbeeld is de FQDN **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="c68d9-135">Een front-end-IP-adresgroep en back-endadresgroep maken</span><span class="sxs-lookup"><span data-stu-id="c68d9-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="c68d9-136">Maak een front-end-IP-adresgroep met de naam **LB-Frontend** die gebruikmaakt van de resource **PublicIp**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="c68d9-137">Maak een back-endadresgroep met de naam **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="c68d9-138">NAT-regels, een load balancer-regel, een test en een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="c68d9-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="c68d9-139">In dit voorbeeld worden de volgende items gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c68d9-139">This example creates the following items:</span></span>

* <span data-ttu-id="c68d9-140">Een NAT-regel om al het verkeer dat binnenkomt op poort 3441, om te zetten naar poort 3389</span><span class="sxs-lookup"><span data-stu-id="c68d9-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="c68d9-141">Een NAT-regel om al het verkeer dat binnenkomt op poort 3442, om te zetten naar poort 3389</span><span class="sxs-lookup"><span data-stu-id="c68d9-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="c68d9-142">Een testregel om de integriteitsstatus te testen op een pagina met de naam **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="c68d9-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="c68d9-143">Een load balancer-regel om al het verkeer dat binnenkomt op poort 80, gelijk te verdelen naar poort 80 op de adressen in de back-endgroep</span><span class="sxs-lookup"><span data-stu-id="c68d9-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="c68d9-144">Een load balancer die gebruikmaakt van al deze objecten</span><span class="sxs-lookup"><span data-stu-id="c68d9-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="c68d9-145">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="c68d9-145">Use these steps:</span></span>

1. <span data-ttu-id="c68d9-146">Maak de NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="c68d9-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="c68d9-147">Maak een statustest.</span><span class="sxs-lookup"><span data-stu-id="c68d9-147">Create a health probe.</span></span> <span data-ttu-id="c68d9-148">Er zijn twee manieren om een steekproef te configureren:</span><span class="sxs-lookup"><span data-stu-id="c68d9-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="c68d9-149">HTTP-test</span><span class="sxs-lookup"><span data-stu-id="c68d9-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="c68d9-150">TPC-test</span><span class="sxs-lookup"><span data-stu-id="c68d9-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="c68d9-151">Maak een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="c68d9-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="c68d9-152">Maak de load balancer met behulp van de eerder gemaakte objecten.</span><span class="sxs-lookup"><span data-stu-id="c68d9-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="c68d9-153">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="c68d9-153">Create NICs</span></span>

<span data-ttu-id="c68d9-154">Maak netwerkinterfaces (of wijzig bestaande interfaces) en koppel deze aan NAT-regels, load balancer-regels en tests:</span><span class="sxs-lookup"><span data-stu-id="c68d9-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="c68d9-155">Ga naar het virtuele netwerk en een subnet van een virtueel netwerk waarop de NIC's moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c68d9-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="c68d9-156">Maak een NIC met de naam **lb-nic1-be**, en koppel deze aan de eerste NAT-regel en de eerste (en enige) back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="c68d9-157">Maak een NIC met de naam **lb-nic2-be**, en koppel deze aan de tweede NAT-regel en de eerste (en enige) back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="c68d9-158">Controleer de NIC's.</span><span class="sxs-lookup"><span data-stu-id="c68d9-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="c68d9-159">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c68d9-159">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="c68d9-160">Gebruik de cmdlet `Add-AzureRmVMNetworkInterface` om de NIC's toe te wijzen aan verschillende VM’s.</span><span class="sxs-lookup"><span data-stu-id="c68d9-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c68d9-161">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c68d9-161">Create a virtual machine</span></span>

<span data-ttu-id="c68d9-162">Zie voor instructies voor het maken van een virtuele machine en het toewijzen van een NIC [Een Azure-VM maken met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c68d9-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="c68d9-163">De netwerkinterface toevoegen aan de load balancer</span><span class="sxs-lookup"><span data-stu-id="c68d9-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="c68d9-164">Haal de load balancer op uit Azure.</span><span class="sxs-lookup"><span data-stu-id="c68d9-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="c68d9-165">Laad de load balancer-resource in een variabele (als u dat nog niet hebt gedaan).</span><span class="sxs-lookup"><span data-stu-id="c68d9-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="c68d9-166">De variabele heet **$lb**. Gebruik de namen van de load balancer-resource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c68d9-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="c68d9-167">Laad de back-endconfiguratie in een variabele.</span><span class="sxs-lookup"><span data-stu-id="c68d9-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="c68d9-168">Laad de gemaakte netwerkinterface in een variabele.</span><span class="sxs-lookup"><span data-stu-id="c68d9-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="c68d9-169">De variabele heet **$nic**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-169">The variable name is **$nic**.</span></span> <span data-ttu-id="c68d9-170">De netwerkinterfacenaam is hetzelfde als in bovenstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c68d9-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="c68d9-171">Wijzig de back-endconfiguratie op de netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="c68d9-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="c68d9-172">Sla het netwerkinterfaceobject op.</span><span class="sxs-lookup"><span data-stu-id="c68d9-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="c68d9-173">Zodra er een netwerkinterface is toegevoegd aan de back-endgroep van de load balancer, begint deze netwerkverkeer te ontvangen op basis van de taakverdelingsregels voor die load balancer-resource.</span><span class="sxs-lookup"><span data-stu-id="c68d9-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="c68d9-174">Een bestaande load balancer bijwerken</span><span class="sxs-lookup"><span data-stu-id="c68d9-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="c68d9-175">Met behulp van de load balancer uit het bovenstaande voorbeeld wijst u load balancer-object toe aan de variabele **$slb** met `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="c68d9-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="c68d9-176">In het volgende voorbeeld voegt u aan een bestaande load balancer een NAT-regel voor binnenkomende verbindingen toe met poort 81 in de front-end en poort 8181 voor de back-endgroep.</span><span class="sxs-lookup"><span data-stu-id="c68d9-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="c68d9-177">Sla de nieuwe configuratie op met behulp van `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="c68d9-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="c68d9-178">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="c68d9-178">Remove a load balancer</span></span>

<span data-ttu-id="c68d9-179">Gebruik de opdracht `Remove-AzureLoadBalancer` om een eerder gemaakte load balancer met de naam **NRP-LB** te verwijderen uit de resourcegroep **NRP RG**.</span><span class="sxs-lookup"><span data-stu-id="c68d9-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="c68d9-180">Met de optionele schakeloptie **-Force** kunt u de prompt voor verwijdering uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c68d9-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c68d9-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c68d9-181">Next steps</span></span>

[<span data-ttu-id="c68d9-182">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="c68d9-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c68d9-183">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="c68d9-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c68d9-184">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="c68d9-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
