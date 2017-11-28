---
title: een Azure internetgerichte aaaCreate de load balancer - PowerShell | Microsoft Docs
description: Meer informatie over hoe een internetgerichte toocreate netwerktaakverdeler in Resource Manager met behulp van PowerShell
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
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="39b43-103"><a name="get-started"></a>Een internetgerichte load balancer maken in Resource Manager met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b43-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39b43-104">Portal</span><span class="sxs-lookup"><span data-stu-id="39b43-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="39b43-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b43-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="39b43-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39b43-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="39b43-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="39b43-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="39b43-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="39b43-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="39b43-109">U kunt ook [meer informatie over hoe een internetgerichte toocreate netwerktaakverdeler met het klassieke implementatiemodel Hallo](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="39b43-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="39b43-110">Hallo-oplossing implementeren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b43-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="39b43-111">Hallo volgen procedures wordt uitgelegd hoe toocreate een internetgerichte netwerktaakverdeler met behulp van Azure Resource Manager met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39b43-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="39b43-112">Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een load balancer.</span><span class="sxs-lookup"><span data-stu-id="39b43-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="39b43-113">U moet maken en configureren van Hallo objecten toodeploy een load balancer te volgen:</span><span class="sxs-lookup"><span data-stu-id="39b43-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="39b43-114">Front-end-IP-configuratie: bevat openbare IP-adressen (PIP) voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="39b43-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="39b43-115">Back-end-adresgroep: netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer bevat.</span><span class="sxs-lookup"><span data-stu-id="39b43-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="39b43-116">Regels voor taakverdeling: bevat regels die een openbare poort op Hallo load balancer tooa poort in Hallo back-end-adresgroep toewijzen.</span><span class="sxs-lookup"><span data-stu-id="39b43-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="39b43-117">Binnenkomende NAT-regels: bevat regels die een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in Hallo back-end-adresgroep toewijzen.</span><span class="sxs-lookup"><span data-stu-id="39b43-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="39b43-118">Tests: bevat de beschikbaarheid van health-tests gebruikt toocheck exemplaren van virtuele machines in Hallo back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="39b43-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="39b43-119">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="39b43-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="39b43-120">PowerShell toouse Resource Manager instellen</span><span class="sxs-lookup"><span data-stu-id="39b43-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="39b43-121">Controleer of er Hallo nieuwste productieversie van hello Azure Resource Manager-module voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="39b43-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="39b43-122">Meld u aan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="39b43-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="39b43-123">Voer uw referenties in wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="39b43-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="39b43-124">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="39b43-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="39b43-125">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="39b43-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="39b43-126">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="39b43-126">Create a resource group.</span></span> <span data-ttu-id="39b43-127">(Sla deze stap over als u een bestaande resourcegroep gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="39b43-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="39b43-128">Een virtueel netwerk en een openbare IP-adres voor Hallo front-end-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="39b43-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="39b43-129">Maak een subnet en een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="39b43-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="39b43-130">Een Azure openbare IP-adres-resource maken, met de naam **PublicIP**, die wordt gebruikt door een front-end-IP-adresgroep met Hallo DNS-naam toobe **loadbalancernrp.westus.cloudapp.azure.com**. Hallo volgende opdracht maakt gebruik van Hallo statische toewijzingstype.</span><span class="sxs-lookup"><span data-stu-id="39b43-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="39b43-131">Hallo load balancer gebruikmaakt Hallo domeinlabel van Hallo openbare IP-adres als een voorvoegsel voor de FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="39b43-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="39b43-132">Dit wijkt af van Hallo klassieke implementatiemodel, dit maakt gebruik van cloudservice Hallo Hallo load balancer FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="39b43-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="39b43-133">In dit voorbeeld Hallo FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="39b43-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="39b43-134">Een front-end-IP-adresgroep en back-endadresgroep maken</span><span class="sxs-lookup"><span data-stu-id="39b43-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="39b43-135">Maak een front-end-IP-adresgroep met de naam **LB-Frontend** die gebruikmaakt van Hallo **PublicIp** resource.</span><span class="sxs-lookup"><span data-stu-id="39b43-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="39b43-136">Maak een back-endadresgroep met de naam **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="39b43-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="39b43-137">NAT-regels, een load balancer-regel, een test en een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="39b43-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="39b43-138">In dit voorbeeld maakt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="39b43-138">This example creates hello following items:</span></span>

* <span data-ttu-id="39b43-139">Een NAT-regel tootranslate alle binnenkomend verkeer op poort 3441 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="39b43-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="39b43-140">Een NAT-regel tootranslate alle binnenkomend verkeer op poort 3442 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="39b43-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="39b43-141">Een test regel toocheck Hallo gezondheidsstatus op een pagina met de naam **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="39b43-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="39b43-142">Een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool</span><span class="sxs-lookup"><span data-stu-id="39b43-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="39b43-143">Een load balancer die gebruikmaakt van al deze objecten</span><span class="sxs-lookup"><span data-stu-id="39b43-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="39b43-144">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="39b43-144">Use these steps:</span></span>

1. <span data-ttu-id="39b43-145">Hallo NAT-regels maken.</span><span class="sxs-lookup"><span data-stu-id="39b43-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="39b43-146">Maak een statustest.</span><span class="sxs-lookup"><span data-stu-id="39b43-146">Create a health probe.</span></span> <span data-ttu-id="39b43-147">Er zijn twee manieren tooconfigure een test:</span><span class="sxs-lookup"><span data-stu-id="39b43-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="39b43-148">HTTP-test</span><span class="sxs-lookup"><span data-stu-id="39b43-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="39b43-149">TPC-test</span><span class="sxs-lookup"><span data-stu-id="39b43-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="39b43-150">Maak een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="39b43-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="39b43-151">Hallo load balancer maken met behulp van de objecten Hallo eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39b43-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="39b43-152">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="39b43-152">Create NICs</span></span>

<span data-ttu-id="39b43-153">Netwerkinterfaces te maken (of bestaande wijzigen) en vervolgens koppelen tooNAT regels, load balancer-regels en -tests:</span><span class="sxs-lookup"><span data-stu-id="39b43-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="39b43-154">Haal Hallo virtueel netwerk en een virtueel netwerksubnet waar Hallo NIC's moeten toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39b43-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="39b43-155">Maak een NIC met de naam **lb nic1 worden**, en deze koppelen aan de eerste NAT-regel Hallo en Hallo eerste (en alleen) back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="39b43-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="39b43-156">Maak een NIC met de naam **lb nic2 worden**, en deze koppelen aan de tweede NAT-regel Hallo en Hallo eerste (en alleen) back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="39b43-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="39b43-157">Controleer Hallo NIC's.</span><span class="sxs-lookup"><span data-stu-id="39b43-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="39b43-158">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="39b43-158">Expected output:</span></span>

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

5. <span data-ttu-id="39b43-159">Gebruik Hallo `Add-AzureRmVMNetworkInterface` cmdlet tooassign Hallo NIC's toodifferent virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="39b43-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="39b43-160">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="39b43-160">Create a virtual machine</span></span>

<span data-ttu-id="39b43-161">Zie voor instructies voor het maken van een virtuele machine en het toewijzen van een NIC [Een Azure-VM maken met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39b43-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="39b43-162">Hallo network interface toohello load balancer toevoegen</span><span class="sxs-lookup"><span data-stu-id="39b43-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="39b43-163">Hallo load balancer ophalen uit Azure.</span><span class="sxs-lookup"><span data-stu-id="39b43-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="39b43-164">Hallo load balancerresource in een variabele laden (als u die nog niet hebt gedaan).</span><span class="sxs-lookup"><span data-stu-id="39b43-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="39b43-165">Hallo variabele heet **$lb**. Gebruik hello dezelfde namen van Hallo load balancerresource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39b43-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="39b43-166">Hallo-back-end configuratie tooa variabele worden geladen.</span><span class="sxs-lookup"><span data-stu-id="39b43-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="39b43-167">Netwerkinterface Hallo al gemaakt in een variabele laden.</span><span class="sxs-lookup"><span data-stu-id="39b43-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="39b43-168">Hallo variabelenaam is **$nic**.</span><span class="sxs-lookup"><span data-stu-id="39b43-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="39b43-169">Hallo naam voor de netwerkinterface is Hallo dezelfde is als die van Hallo eerdere voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="39b43-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="39b43-170">Hallo back-end-configuratie wijzigen op Hallo-netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="39b43-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="39b43-171">Sla Hallo netwerkinterface-object.</span><span class="sxs-lookup"><span data-stu-id="39b43-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="39b43-172">Na een netwerkinterface is toohello load balancer back-end-adresgroep hebt toegevoegd, start het netwerkverkeer op basis van Hallo-taakverdeling regels voor de load balancerresource ontvangen.</span><span class="sxs-lookup"><span data-stu-id="39b43-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="39b43-173">Een bestaande load balancer bijwerken</span><span class="sxs-lookup"><span data-stu-id="39b43-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="39b43-174">Met behulp van Hallo netwerktaakverdeler uit eerdere voorbeeld Hallo, een load balancer-toohello objectvariabele toewijzen **$slb** met behulp van `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="39b43-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="39b43-175">In de Hallo voorbeeld te volgen, voegt u een binnenkomende NAT-regel--met behulp van poort 81 in Hallo front-toepassingen en -poort 8181 voor Hallo back-end-pool--tooan bestaande load balancer.</span><span class="sxs-lookup"><span data-stu-id="39b43-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="39b43-176">Hallo nieuwe configuratie op te slaan met behulp van `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="39b43-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="39b43-177">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="39b43-177">Remove a load balancer</span></span>

<span data-ttu-id="39b43-178">Gebruik de opdracht Hallo `Remove-AzureLoadBalancer` toodelete een eerder gemaakte load balancer met de naam **NRP LB** aangeroepen in een resourcegroep **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="39b43-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="39b43-179">U kunt een optionele schakeloptie Hallo **-Force** tooavoid Hallo prompt voor verwijdering.</span><span class="sxs-lookup"><span data-stu-id="39b43-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39b43-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39b43-180">Next steps</span></span>

[<span data-ttu-id="39b43-181">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="39b43-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="39b43-182">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="39b43-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="39b43-183">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="39b43-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
