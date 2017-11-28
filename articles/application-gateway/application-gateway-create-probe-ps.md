---
title: een aangepaste aaaCreate probe - Azure Application Gateway - PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste test voor Application Gateway met behulp van PowerShell in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="82d50-103">Maken van een aangepaste test voor Azure Application Gateway met behulp van PowerShell voor Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82d50-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82d50-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="82d50-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="82d50-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="82d50-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="82d50-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="82d50-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="82d50-107">In dit artikel voegt u een aangepaste test tooan bestaande application gateway met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82d50-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="82d50-108">Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op Hallo standaardwebtoepassing geen bieden.</span><span class="sxs-lookup"><span data-stu-id="82d50-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="82d50-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82d50-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="82d50-110">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="82d50-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="82d50-111">Een toepassingsgateway maken met een aangepaste test</span><span class="sxs-lookup"><span data-stu-id="82d50-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="82d50-112">Aanmelden en resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="82d50-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="82d50-113">Gebruik `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="82d50-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="82d50-114">Hallo-abonnementen voor Hallo account krijgen.</span><span class="sxs-lookup"><span data-stu-id="82d50-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="82d50-115">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="82d50-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="82d50-116">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="82d50-116">Create a resource group.</span></span> <span data-ttu-id="82d50-117">Als u een bestaande resourcegroep hebt, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="82d50-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="82d50-118">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="82d50-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="82d50-119">Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="82d50-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="82d50-120">Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="82d50-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="82d50-121">In Hallo voorgaande voorbeeld, is er een resourcegroep aangeroepen gemaakt **appgw-RG** op locatie **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="82d50-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="82d50-122">Een virtueel netwerk en een subnet maken</span><span class="sxs-lookup"><span data-stu-id="82d50-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="82d50-123">Hallo volgende voorbeeld wordt een virtueel netwerk en een subnet voor de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="82d50-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="82d50-124">Toepassingsgateway vereist een eigen subnet voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="82d50-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="82d50-125">Om deze reden moet Hallo subnet gemaakt voor de toepassingsgateway Hallo kleiner zijn dan de adresruimte Hallo van Hallo VNET tooallow voor andere subnetten toobe gemaakt en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="82d50-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="82d50-126">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="82d50-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="82d50-127">Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="82d50-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="82d50-128">Dit voorbeeld wordt een openbaar IP-adres voor front-end-IP-adres van de toepassingsgateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="82d50-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="82d50-129">Toepassingsgateway Hallo openbare IP-adres toohave een dynamisch gemaakte DNS-naam Hallo daarom vereist `-DomainNameLabel` tijdens het maken van Hallo Hallo openbare IP-adres kan niet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="82d50-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="82d50-130">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="82d50-130">Create an application gateway</span></span>

<span data-ttu-id="82d50-131">U instellen alle configuratie-items voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="82d50-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="82d50-132">Hallo maakt volgende voorbeeld Hallo configuratie-items die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="82d50-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="82d50-133">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="82d50-133">**Component**</span></span> | <span data-ttu-id="82d50-134">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="82d50-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="82d50-135">**Toepassingsgateway IP-configuratie**</span><span class="sxs-lookup"><span data-stu-id="82d50-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="82d50-136">Een IP-configuratie voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="82d50-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="82d50-137">**Back-endpool**</span><span class="sxs-lookup"><span data-stu-id="82d50-137">**Backend pool**</span></span> | <span data-ttu-id="82d50-138">Een pool van IP-adressen, FQDN's of NIC's die zijn toohello toepassingsservers die als host Hallo-webtoepassing fungeren</span><span class="sxs-lookup"><span data-stu-id="82d50-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="82d50-139">**De statuscontrole**</span><span class="sxs-lookup"><span data-stu-id="82d50-139">**Health probe**</span></span> | <span data-ttu-id="82d50-140">Een aangepaste test toomonitor Hallo status van de back-end-groepsleden Hallo gebruikt</span><span class="sxs-lookup"><span data-stu-id="82d50-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="82d50-141">**HTTP-instellingen**</span><span class="sxs-lookup"><span data-stu-id="82d50-141">**HTTP settings**</span></span> | <span data-ttu-id="82d50-142">Een verzameling met inbegrip van instellingen, poort, protocol, cookies gebaseerde affiniteit, test en time-out.</span><span class="sxs-lookup"><span data-stu-id="82d50-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="82d50-143">Deze instellingen bepalen hoe verkeer wordt gerouteerd toohello back-end-groepsleden</span><span class="sxs-lookup"><span data-stu-id="82d50-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="82d50-144">**Front-endpoort**</span><span class="sxs-lookup"><span data-stu-id="82d50-144">**Frontend port**</span></span> | <span data-ttu-id="82d50-145">Hallo-poort die Hallo toepassingsgateway luistert voor verkeer op</span><span class="sxs-lookup"><span data-stu-id="82d50-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="82d50-146">**Listener**</span><span class="sxs-lookup"><span data-stu-id="82d50-146">**Listener**</span></span> | <span data-ttu-id="82d50-147">Een combinatie van een protocol, de frontend-IP-configuratie en de frontend-poort.</span><span class="sxs-lookup"><span data-stu-id="82d50-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="82d50-148">Dit is wat luistert naar binnenkomende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="82d50-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="82d50-149">**Regel**</span><span class="sxs-lookup"><span data-stu-id="82d50-149">**Rule**</span></span>| <span data-ttu-id="82d50-150">Routes Hallo verkeer toohello juiste back-end op basis van HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="82d50-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="82d50-151">Een test tooan bestaande toepassingsgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="82d50-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="82d50-152">Hallo voegt volgende codefragment een test tooan bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="82d50-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="82d50-153">Een test uit een bestaande toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="82d50-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="82d50-154">Hallo volgende codefragment verwijdert een test van een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="82d50-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="82d50-155">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="82d50-155">Get application gateway DNS name</span></span>

<span data-ttu-id="82d50-156">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="82d50-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="82d50-157">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="82d50-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="82d50-158">tooensure eindgebruikers Hallo toepassingsgateway een CNAME-record kan worden gebruikt. Druk toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="82d50-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="82d50-159">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82d50-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="82d50-160">toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="82d50-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="82d50-161">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="82d50-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="82d50-162">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="82d50-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="82d50-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82d50-163">Next steps</span></span>

<span data-ttu-id="82d50-164">Meer informatie over tooconfigure SSL-offloading in via: [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="82d50-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

