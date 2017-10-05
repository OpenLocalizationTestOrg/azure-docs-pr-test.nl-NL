---
title: Maak een aangepaste test - Azure Application Gateway - PowerShell | Microsoft Docs
description: Informatie over het maken van een aangepaste test voor Application Gateway met behulp van PowerShell in Resource Manager
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
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="22325-103">Maken van een aangepaste test voor Azure Application Gateway met behulp van PowerShell voor Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22325-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="22325-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="22325-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="22325-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="22325-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="22325-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="22325-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="22325-107">In dit artikel kunt u een aangepaste test toevoegen aan een bestaande application gateway met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22325-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="22325-108">Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op de standaardwebtoepassing geen bieden.</span><span class="sxs-lookup"><span data-stu-id="22325-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="22325-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="22325-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="22325-110">Dit artikel bevat informatie over het Resource Manager-implementatiemodel, dat door Microsoft wordt aanbevolen voor de meeste nieuwe implementaties in plaats van het [klassieke implementatiemodel](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="22325-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="22325-111">Een toepassingsgateway maken met een aangepaste test</span><span class="sxs-lookup"><span data-stu-id="22325-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="22325-112">Aanmelden en resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="22325-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="22325-113">Gebruik `Login-AzureRmAccount` om te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="22325-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="22325-114">De abonnementen voor het account worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="22325-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="22325-115">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22325-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="22325-116">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="22325-116">Create a resource group.</span></span> <span data-ttu-id="22325-117">Als u een bestaande resourcegroep hebt, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="22325-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="22325-118">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="22325-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="22325-119">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="22325-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="22325-120">Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="22325-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="22325-121">In het voorgaande voorbeeld wordt er een resourcegroep aangeroepen hebt gemaakt **appgw-RG** op locatie **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="22325-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="22325-122">Een virtueel netwerk en een subnet maken</span><span class="sxs-lookup"><span data-stu-id="22325-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="22325-123">Het volgende voorbeeld wordt een virtueel netwerk en een subnet voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="22325-124">Toepassingsgateway vereist een eigen subnet voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="22325-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="22325-125">Daarom moet moet het subnet dat is gemaakt voor de toepassingsgateway kleiner zijn dan de adresruimte van het VNET om toe te staan voor andere subnetten worden gemaakt en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="22325-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="22325-126">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="22325-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="22325-127">Maak de openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS - west.</span><span class="sxs-lookup"><span data-stu-id="22325-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="22325-128">Dit voorbeeld wordt een openbaar IP-adres voor de front-end-IP-adres van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="22325-129">Toepassingsgateway het openbare IP-adres in een dynamisch gemaakte DNS-naam daarom vereist de `-DomainNameLabel` tijdens het maken van het openbare IP-adres kan niet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="22325-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="22325-130">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="22325-130">Create an application gateway</span></span>

<span data-ttu-id="22325-131">U instellen alle configuratie-items voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="22325-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="22325-132">Het volgende voorbeeld wordt de configuratie-items die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="22325-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="22325-133">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="22325-133">**Component**</span></span> | <span data-ttu-id="22325-134">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="22325-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="22325-135">**Toepassingsgateway IP-configuratie**</span><span class="sxs-lookup"><span data-stu-id="22325-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="22325-136">Een IP-configuratie voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="22325-137">**Back-endpool**</span><span class="sxs-lookup"><span data-stu-id="22325-137">**Backend pool**</span></span> | <span data-ttu-id="22325-138">Een pool van IP-adressen, FQDN's of NIC's die naar de toepassingsservers die als host fungeren van de webtoepassing zijn</span><span class="sxs-lookup"><span data-stu-id="22325-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="22325-139">**De statuscontrole**</span><span class="sxs-lookup"><span data-stu-id="22325-139">**Health probe**</span></span> | <span data-ttu-id="22325-140">Een aangepaste test gebruikt voor het bewaken van de status van de leden van de groep back-end</span><span class="sxs-lookup"><span data-stu-id="22325-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="22325-141">**HTTP-instellingen**</span><span class="sxs-lookup"><span data-stu-id="22325-141">**HTTP settings**</span></span> | <span data-ttu-id="22325-142">Een verzameling met inbegrip van instellingen, poort, protocol, cookies gebaseerde affiniteit, test en time-out.</span><span class="sxs-lookup"><span data-stu-id="22325-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="22325-143">Deze instellingen bepalen hoe verkeer wordt doorgestuurd naar de leden van de groep back-end</span><span class="sxs-lookup"><span data-stu-id="22325-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="22325-144">**Front-endpoort**</span><span class="sxs-lookup"><span data-stu-id="22325-144">**Frontend port**</span></span> | <span data-ttu-id="22325-145">De poort die de toepassingsgateway luistert voor verkeer op</span><span class="sxs-lookup"><span data-stu-id="22325-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="22325-146">**Listener**</span><span class="sxs-lookup"><span data-stu-id="22325-146">**Listener**</span></span> | <span data-ttu-id="22325-147">Een combinatie van een protocol, de frontend-IP-configuratie en de frontend-poort.</span><span class="sxs-lookup"><span data-stu-id="22325-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="22325-148">Dit is wat luistert naar binnenkomende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="22325-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="22325-149">**Regel**</span><span class="sxs-lookup"><span data-stu-id="22325-149">**Rule**</span></span>| <span data-ttu-id="22325-150">Routes die het verkeer naar de juiste back-end op basis van HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="22325-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="22325-151">Een test toevoegen aan een bestaande application gateway</span><span class="sxs-lookup"><span data-stu-id="22325-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="22325-152">Het volgende codefragment wordt een test aan een bestaande toepassingsgateway toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="22325-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="22325-153">Een test uit een bestaande toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="22325-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="22325-154">Het volgende codefragment verwijdert een test van een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="22325-155">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="22325-155">Get application gateway DNS name</span></span>

<span data-ttu-id="22325-156">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="22325-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="22325-157">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="22325-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="22325-158">Opdat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt om te wijzen naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="22325-159">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="22325-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="22325-160">Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="22325-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="22325-161">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="22325-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="22325-162">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="22325-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22325-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22325-163">Next steps</span></span>

<span data-ttu-id="22325-164">Informatie over het configureren van SSL-offloading in via: [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="22325-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

