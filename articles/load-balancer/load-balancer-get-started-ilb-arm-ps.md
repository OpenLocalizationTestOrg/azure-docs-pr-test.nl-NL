---
title: een Azure-interne aaaCreate de load balancer - PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer met behulp van PowerShell in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="d3243-103">Een interne load balancer maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3243-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3243-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d3243-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="d3243-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3243-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="d3243-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d3243-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="d3243-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="d3243-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d3243-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3243-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d3243-109">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d3243-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="d3243-110">Hallo stappen wordt uitgelegd hoe toocreate een interne load balancer met Azure Resource Manager met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3243-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="d3243-111">Met Azure Resource Manager Hallo items toocreate een interne load balancer worden afzonderlijk geconfigureerd en vervolgens gecombineerd toocreate een load balancer.</span><span class="sxs-lookup"><span data-stu-id="d3243-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="d3243-112">U moet toocreate en configureer Hallo objecten toodeploy een load balancer te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3243-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="d3243-113">Front-end-IP-configuratie - Hallo privé IP-adres voor binnenkomend netwerkverkeer wilt configureren</span><span class="sxs-lookup"><span data-stu-id="d3243-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="d3243-114">Back-endadresgroep - wilt Hallo netwerkinterfaces die ontvangt Hallo taakverdelingsverkeer afkomstig is van de front-end-IP-adresgroep configureren</span><span class="sxs-lookup"><span data-stu-id="d3243-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="d3243-115">Taakverdelingsregels - bron- en configuratie van de lokale poort voor Hallo de load balancer.</span><span class="sxs-lookup"><span data-stu-id="d3243-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="d3243-116">Tests - Hallo health statustest voor de virtuele Machine-exemplaren Hallo configureert.</span><span class="sxs-lookup"><span data-stu-id="d3243-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="d3243-117">NAT-regels voor binnenkomende verbindingen-configureert u de Hallo poort regels toodirectly toegang een Hallo exemplaren van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d3243-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="d3243-118">Meer informatie over de load balancer-onderdelen in Azure Resource Manager vindt u op [Ondersteuning van Azure Resource Manager voor Azure Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d3243-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="d3243-119">Hallo volgende stappen wordt uitgelegd hoe tooconfigure een load balancer tussen twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d3243-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="d3243-120">Setup PowerShell toouse Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3243-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="d3243-121">Zorg ervoor dat u Hallo nieuwste productieversie van hello Azure-module voor PowerShell en PowerShell instellen correct tooaccess uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d3243-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-122">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d3243-123">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-123">Step 2</span></span>

<span data-ttu-id="d3243-124">Controleer de abonnementen Hallo voor Hallo-account</span><span class="sxs-lookup"><span data-stu-id="d3243-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d3243-125">U zult na vragen aan gebruiker tooAuthenticate met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="d3243-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="d3243-126">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d3243-126">Step 3</span></span>

<span data-ttu-id="d3243-127">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="d3243-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="d3243-128">Resourcegroep voor load balancer maken</span><span class="sxs-lookup"><span data-stu-id="d3243-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="d3243-129">Een nieuwe resourcegroep maken (sla deze stap over als u een bestaande resourcegroep gebruikt)</span><span class="sxs-lookup"><span data-stu-id="d3243-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="d3243-130">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d3243-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d3243-131">Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d3243-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d3243-132">Zorg ervoor dat alle opdrachten toocreate een load balancer gebruiken Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d3243-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="d3243-133">In Hallo voorbeeld hierboven wordt gemaakt met een resourcegroep 'NRP-RG' en de locatie ' West ' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d3243-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="d3243-134">Virtueel netwerk en een particulier IP-adres voor front-end-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="d3243-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="d3243-135">Maakt een subnet voor het virtuele netwerk Hallo en wijst toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="d3243-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="d3243-136">Een virtueel netwerk maken:</span><span class="sxs-lookup"><span data-stu-id="d3243-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="d3243-137">Hallo virtueel netwerk maakt en voegt Hallo subnet toohello lb-subnet niet virtueel netwerk NRPVNet toe en wijst toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="d3243-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="d3243-138">Front-end-IP-adresgroep en back-endadresgroep maken</span><span class="sxs-lookup"><span data-stu-id="d3243-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="d3243-139">Instellen van een front-end-IP-adresgroep voor inkomende hello load balancer-netwerkverkeer en de back-end adresgroep tooreceive hello taakverdelingsverkeer.</span><span class="sxs-lookup"><span data-stu-id="d3243-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-140">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-140">Step 1</span></span>

<span data-ttu-id="d3243-141">Maak een front-end-IP-adresgroep met Hallo privé IP-adres 10.0.2.5 voor Hallo subnet 10.0.2.0/24 Hallo binnenkomende verkeer netwerkeindpunt worden.</span><span class="sxs-lookup"><span data-stu-id="d3243-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="d3243-142">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-142">Step 2</span></span>

<span data-ttu-id="d3243-143">Instellen van een back-end-adresgroep gebruikt tooreceive inkomend verkeer van de front-end-IP-adresgroep:</span><span class="sxs-lookup"><span data-stu-id="d3243-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="d3243-144">LB-regels, NAT-regels, test en load balancer maken</span><span class="sxs-lookup"><span data-stu-id="d3243-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="d3243-145">Na het Hallo-front-end-IP-adresgroep en Hallo back-end-adresgroep maken, moet u toocreate Hallo regels die deel van toohello load balancerresource uitmaakt:</span><span class="sxs-lookup"><span data-stu-id="d3243-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-146">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="d3243-147">Hallo in bovenstaand voorbeeld met het maken van de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="d3243-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="d3243-148">NAT-regel waarmee alle binnenkomende verkeer tooport 3441 gaat tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="d3243-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="d3243-149">een tweede NAT-regel waarmee alle binnenkomende verkeer tooport 3442 gaat tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="d3243-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="d3243-150">alle binnenkomend verkeer op poort 80 van de openbare poort 80 in Hallo back-end-adresgroep toolocal het saldo van een regel voor load balancer die wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="d3243-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="d3243-151">een test-regel die de gezondheidsstatus Hallo voor pad 'HealthProbe.aspx' wordt gecontroleerd</span><span class="sxs-lookup"><span data-stu-id="d3243-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="d3243-152">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-152">Step 2</span></span>

<span data-ttu-id="d3243-153">Hallo load balancer samen met het toevoegen van alle objecten (NAT-regels, Load balancerregels, test-configuraties) maken:</span><span class="sxs-lookup"><span data-stu-id="d3243-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="d3243-154">Netwerkinterfaces maken</span><span class="sxs-lookup"><span data-stu-id="d3243-154">Create network interfaces</span></span>

<span data-ttu-id="d3243-155">Na het maken van Hallo interne load balancer, moet u definiëren welke netwerkinterfaces ontvangt Hallo binnenkomende taakverdeling netwerkverkeer, NAT-regels en test.</span><span class="sxs-lookup"><span data-stu-id="d3243-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="d3243-156">Hallo-netwerkinterface in dit geval afzonderlijk geconfigureerd en kan worden toegewezen tooa virtuele machine later op.</span><span class="sxs-lookup"><span data-stu-id="d3243-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-157">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-157">Step 1</span></span>

<span data-ttu-id="d3243-158">Hallo resource virtuele netwerk en subnet toocreate netwerkinterfaces ophalen:</span><span class="sxs-lookup"><span data-stu-id="d3243-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="d3243-159">Deze stap maakt u een netwerkinterface die wordt behoren toohello load balancer back-end-pool en Hallo eerste NAT-regel voor RDP voor deze netwerkinterface koppelen:</span><span class="sxs-lookup"><span data-stu-id="d3243-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="d3243-160">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-160">Step 2</span></span>

<span data-ttu-id="d3243-161">Maak als volgt een tweede netwerkinterface met de naam LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="d3243-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="d3243-162">Deze stap maakt u een tweede netwerkinterface, toohello toewijzen dezelfde load balancer terug pool beëindigen en koppelen van Hallo tweede NAT-regel gemaakt voor RDP:</span><span class="sxs-lookup"><span data-stu-id="d3243-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="d3243-163">het eindresultaat Hello wordt Hallo volgende weergeven:</span><span class="sxs-lookup"><span data-stu-id="d3243-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="d3243-164">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d3243-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="d3243-165">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d3243-165">Step 3</span></span>

<span data-ttu-id="d3243-166">Hallo opdracht toevoegen AzureRmVMNetworkInterface tooassign Hallo NIC tooa virtuele Machine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3243-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="d3243-167">Vindt u stapsgewijze instructies toocreate een virtuele machine Hallo en tooa NIC toewijzen Hallo documentatie te volgen: [maken van een virtuele machine in Azure met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3243-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="d3243-168">Hallo-netwerkinterface toevoegen</span><span class="sxs-lookup"><span data-stu-id="d3243-168">Add hello network interface</span></span>

<span data-ttu-id="d3243-169">Als er al een virtuele machine gemaakt, kunt u Hallo netwerkinterface toevoegen Hello stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3243-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-170">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-170">Step 1</span></span>

<span data-ttu-id="d3243-171">Hallo load balancerresource in een variabele laden (als u die nog niet hebt gedaan).</span><span class="sxs-lookup"><span data-stu-id="d3243-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="d3243-172">Hallo-variabele die wordt gebruikt is aangeroepen $lb en gebruik Hallo Hallo load balancerresource dezelfde namen die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3243-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="d3243-173">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-173">Step 2</span></span>

<span data-ttu-id="d3243-174">Hallo back-end configuratie tooa variabele worden geladen.</span><span class="sxs-lookup"><span data-stu-id="d3243-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="d3243-175">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d3243-175">Step 3</span></span>

<span data-ttu-id="d3243-176">Netwerkinterface Hallo al gemaakt in een variabele laden.</span><span class="sxs-lookup"><span data-stu-id="d3243-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="d3243-177">Hallo variabelenaam gebruikt is $nic.</span><span class="sxs-lookup"><span data-stu-id="d3243-177">hello variable name used is $nic.</span></span> <span data-ttu-id="d3243-178">Hallo naam voor de netwerkinterface gebruikt Hallo dezelfde van Hallo in bovenstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d3243-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="d3243-179">Stap 4</span><span class="sxs-lookup"><span data-stu-id="d3243-179">Step 4</span></span>

<span data-ttu-id="d3243-180">Hallo back-end-configuratie wijzigen op Hallo-netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="d3243-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="d3243-181">Stap 5</span><span class="sxs-lookup"><span data-stu-id="d3243-181">Step 5</span></span>

<span data-ttu-id="d3243-182">Sla Hallo netwerkinterface-object.</span><span class="sxs-lookup"><span data-stu-id="d3243-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="d3243-183">Nadat een netwerkinterface kan back-endpool van toohello load balancer is toegevoegd, wordt gestart op basis van regels voor de load balancerresource voor taakverdeling Hallo netwerkverkeer ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d3243-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="d3243-184">Een bestaande load balancer bijwerken</span><span class="sxs-lookup"><span data-stu-id="d3243-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="d3243-185">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d3243-185">Step 1</span></span>
<span data-ttu-id="d3243-186">Load balancer-object toovariable $slb met Get-AzureRmLoadBalancer met Hallo load balancer van Hallo in bovenstaand voorbeeld, toewijzen</span><span class="sxs-lookup"><span data-stu-id="d3243-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="d3243-187">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d3243-187">Step 2</span></span>

<span data-ttu-id="d3243-188">In Hallo voorbeeld te volgen, wordt u een nieuwe inkomende NAT-regel met behulp van poort 81 in de front-end Hallo toevoegen en poort 8181 Hallo terug eindigen groep tooan bestaande load balancer</span><span class="sxs-lookup"><span data-stu-id="d3243-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="d3243-189">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d3243-189">Step 3</span></span>

<span data-ttu-id="d3243-190">Sla de nieuwe configuratie Hallo met Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="d3243-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="d3243-191">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3243-191">Remove a load balancer</span></span>

<span data-ttu-id="d3243-192">Hallo opdracht Remove-AzureRmLoadBalancer toodelete een eerder gemaakte taakverdeler met de naam 'NRP-LB' in een resourcegroep genaamd 'NRP-RG' gebruiken</span><span class="sxs-lookup"><span data-stu-id="d3243-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="d3243-193">U kunt optioneel Hallo switch - Force tooavoid Hallo prompt voor verwijdering.</span><span class="sxs-lookup"><span data-stu-id="d3243-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3243-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3243-194">Next steps</span></span>

[<span data-ttu-id="d3243-195">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d3243-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d3243-196">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d3243-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
