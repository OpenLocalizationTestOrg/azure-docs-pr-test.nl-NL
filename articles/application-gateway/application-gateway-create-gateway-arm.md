---
title: Een Azure Application Gateway maken en beheren - PowerShell | Microsoft Docs
description: Op deze pagina vindt u instructies voor het maken, configureren, openen en verwijderen van een Azure-toepassingsgateway met Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="02105-103">Een toepassingsgateway maken, openen of verwijderen met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02105-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02105-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02105-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="02105-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="02105-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="02105-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="02105-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="02105-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="02105-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="02105-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02105-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="02105-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="02105-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="02105-110">De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud).</span><span class="sxs-lookup"><span data-stu-id="02105-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="02105-111">Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="02105-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="02105-112">Een volledige lijst met ondersteunde functies vindt u in [Overzicht van Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02105-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="02105-113">In dit artikel vindt u meer informatie over de stappen voor het maken, configureren, openen en verwijderen van een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="02105-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02105-114">Voordat u met Azure-resources gaat werken, is het belangrijk om te weten dat Azure momenteel twee implementatiemodellen heeft: Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="02105-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="02105-115">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="02105-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="02105-116">U kunt de documentatie voor verschillende hulpprogramma's bekijken door op de tabbladen boven aan dit artikel te klikken.</span><span class="sxs-lookup"><span data-stu-id="02105-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="02105-117">In dit document leest u meer over het maken van een toepassingsgateway met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02105-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="02105-118">Als u de klassieke versie wilt gebruiken, gaat u naar [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md) (Een klassieke toepassingsgatewayimplementatie maken met PowerShell).</span><span class="sxs-lookup"><span data-stu-id="02105-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="02105-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="02105-119">Before you begin</span></span>

1. <span data-ttu-id="02105-120">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="02105-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="02105-121">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="02105-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="02105-122">Als u een bestaand virtueel netwerk hebt, selecteert u een bestaand leeg subnet of maakt u een subnet in uw bestaande virtuele netwerk, uitsluitend voor gebruik door de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="02105-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="02105-123">U kunt de toepassingsgateway niet implementeren op een ander virtueel netwerk dan de resources die u wilt implementeren achter de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="02105-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="02105-124">De servers die u voor gebruik van de toepassingsgateway configureert, moeten al bestaan in het virtuele netwerk of hier hun eindpunten hebben. Een andere optie is om er een openbaar IP- of VIP-adres aan toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="02105-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="02105-125">Wat is er vereist om een toepassingsgateway te maken?</span><span class="sxs-lookup"><span data-stu-id="02105-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="02105-126">**Back-endserverpool:** de lijst met IP-adressen, FQDN's of NIC's van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="02105-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="02105-127">Als er IP-adressen worden gebruikt, moeten deze deel uitmaken van het subnet van het virtuele netwerk of moeten dit openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="02105-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="02105-128">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="02105-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="02105-129">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="02105-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="02105-130">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="02105-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="02105-131">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="02105-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="02105-132">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="02105-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="02105-133">**Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="02105-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="02105-134">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02105-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="02105-135">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02105-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="02105-136">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02105-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="02105-137">Meld u aan bij Azure en voer uw referenties in.</span><span class="sxs-lookup"><span data-stu-id="02105-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="02105-138">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="02105-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="02105-139">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02105-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="02105-140">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="02105-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="02105-141">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="02105-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="02105-142">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="02105-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="02105-143">Zorg ervoor dat bij alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02105-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="02105-144">In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam **ContosoRG** en de locatie **VS - oost**.</span><span class="sxs-lookup"><span data-stu-id="02105-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="02105-145">Ga naar [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md) (Met PowerShell een toepassingsgateway maken met aangepaste tests) als u voor uw toepassingsgateway een aangepaste test moet configureren.</span><span class="sxs-lookup"><span data-stu-id="02105-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="02105-146">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02105-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="02105-147">Het configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="02105-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="02105-148">Alle configuratie-items moeten zijn ingesteld voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="02105-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="02105-149">Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="02105-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="02105-150">Haal als u klaar bent DNS- en VIP-details van de toepassingsgateway op van de openbare IP-resource die aan de toepassingsgateway is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="02105-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="02105-151">De toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="02105-151">Delete the application gateway</span></span>

<span data-ttu-id="02105-152">In het volgende voorbeeld wordt de toepassingsgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="02105-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="02105-153">U kunt de switch **-force** gebruiken om het bevestigingsbericht voor de verwijdering niet te laten weergeven.</span><span class="sxs-lookup"><span data-stu-id="02105-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="02105-154">Gebruik de cmdlet `Get-AzureRmApplicationGateway` als u wilt controleren of de service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="02105-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="02105-155">Deze stap is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="02105-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="02105-156">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="02105-156">Get application gateway DNS name</span></span>

<span data-ttu-id="02105-157">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="02105-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="02105-158">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="02105-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="02105-159">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="02105-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="02105-160">Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="02105-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="02105-161">Dit kunt u doen met Azure DNS of andere DNS-providers door een CNAME-record te maken dat verwijst naar het [openbare IP-adres](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="02105-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="02105-162">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02105-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="02105-163">Er wordt een IP-adres toegewezen aan de toepassingsgateway wanneer de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02105-163">An IP address is assigned to the application gateway when the service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="02105-164">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="02105-164">Delete all resources</span></span>

<span data-ttu-id="02105-165">Als u alle resources wilt verwijderen die u in dit artikel hebt gemaakt, voert u de volgende stap uit:</span><span class="sxs-lookup"><span data-stu-id="02105-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="02105-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02105-166">Next steps</span></span>

<span data-ttu-id="02105-167">Ga naar: [Configure an application gateway for SSL offload](application-gateway-ssl.md) (Een toepassingsgateway voor SSL-offload configureren) als u SSL-offload wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="02105-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="02105-168">Ga naar: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Een toepassingsgateway met een interne load balancer (ILB) maken) als u een toepassingsgateway wilt configureren voor gebruik met een interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="02105-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="02105-169">Als u meer informatie wilt over de algemene opties voor taakverdeling, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="02105-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="02105-170">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="02105-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="02105-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="02105-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
