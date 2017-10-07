---
title: aaaCreate en beheren van een Azure Application Gateway - PowerShell | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, configureren, starten en verwijderen van een toepassingsgateway met Azure Resource Manager
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
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="2c61a-103">Een toepassingsgateway maken, openen of verwijderen met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c61a-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c61a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2c61a-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="2c61a-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c61a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="2c61a-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c61a-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="2c61a-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="2c61a-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="2c61a-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2c61a-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="2c61a-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="2c61a-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="2c61a-110">Het biedt de failover- en HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="2c61a-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="2c61a-111">Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="2c61a-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="2c61a-112">toofind een volledige lijst van ondersteunde functies, gaat u naar [Application Gateway overzicht](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2c61a-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="2c61a-113">Dit artikel begeleidt u bij Hallo stappen toocreate, configureren en start een toepassingsgateway verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2c61a-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c61a-114">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Resource Manager en classic.</span><span class="sxs-lookup"><span data-stu-id="2c61a-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="2c61a-115">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="2c61a-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="2c61a-116">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2c61a-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="2c61a-117">In dit document leest u meer over het maken van een toepassingsgateway met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c61a-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="2c61a-118">toouse hello klassieke versie, gaat u te[een klassieke implementatie van een toepassing-gateway maken met behulp van PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="2c61a-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2c61a-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2c61a-119">Before you begin</span></span>

1. <span data-ttu-id="2c61a-120">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="2c61a-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="2c61a-121">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2c61a-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="2c61a-122">Als u een bestaand virtueel netwerk hebt, selecteer een bestaande lege subnet of een subnet maken in uw bestaande virtuele netwerk uitsluitend voor gebruik door Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="2c61a-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="2c61a-123">U kunt geen Hallo application gateway tooa ander virtueel netwerk implementeren dan Hallo resources u van plan bent toodeploy achter Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="2c61a-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="2c61a-124">Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="2c61a-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="2c61a-125">Wat is vereist toocreate een application gateway?</span><span class="sxs-lookup"><span data-stu-id="2c61a-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="2c61a-126">**Back-end-servergroep:** Hallo lijst met IP-adressen, FQDN's of NIC's van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="2c61a-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="2c61a-127">Als u IP-adressen gebruikt, worden ze moeten ofwel deel uitmaken toohello virtueel netwerksubnet of moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="2c61a-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="2c61a-128">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="2c61a-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="2c61a-129">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="2c61a-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="2c61a-130">**front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="2c61a-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="2c61a-131">Het verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="2c61a-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="2c61a-132">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="2c61a-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="2c61a-133">**Regel:** Hallo regel verbindt Hallo listener, Hallo back-end-servergroep en definieert naar welke back-end server groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="2c61a-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="2c61a-134">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c61a-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="2c61a-135">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="2c61a-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="2c61a-136">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c61a-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="2c61a-137">Meld u bij tooAzure en voer uw referenties.</span><span class="sxs-lookup"><span data-stu-id="2c61a-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="2c61a-138">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="2c61a-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="2c61a-139">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="2c61a-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="2c61a-140">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="2c61a-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="2c61a-141">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2c61a-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2c61a-142">Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2c61a-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="2c61a-143">Zorg ervoor dat alle opdrachten toocreate maakt gebruik van een toepassingsgateway Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2c61a-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="2c61a-144">In Hallo bovenstaande voorbeeld is er een resourcegroep aangeroepen gemaakt **ContosoRG** en locatie **VS-Oost**.</span><span class="sxs-lookup"><span data-stu-id="2c61a-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="2c61a-145">Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, gaat u naar: [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2c61a-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="2c61a-146">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c61a-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="2c61a-147">Hallo-toepassingsgateway configuratie-objecten maken</span><span class="sxs-lookup"><span data-stu-id="2c61a-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="2c61a-148">Alle configuratie-items moeten worden ingesteld voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="2c61a-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="2c61a-149">Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="2c61a-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="2c61a-150">Als u klaar ophalen met details van DNS- en VIP van de toepassingsgateway Hallo Hallo openbare IP-resource gekoppelde toohello toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="2c61a-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="2c61a-151">Hallo toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="2c61a-151">Delete hello application gateway</span></span>

<span data-ttu-id="2c61a-152">Hallo wordt volgende voorbeeld de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c61a-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="2c61a-153">Hallo **-force** switch kan worden gebruikt toosuppress Hallo bevestigingsbericht voor verwijdering.</span><span class="sxs-lookup"><span data-stu-id="2c61a-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="2c61a-154">tooverify die Hallo service is verwijderd, kunt u Hallo `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c61a-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="2c61a-155">Deze stap is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="2c61a-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2c61a-156">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="2c61a-156">Get application gateway DNS name</span></span>

<span data-ttu-id="2c61a-157">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="2c61a-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="2c61a-158">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="2c61a-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2c61a-159">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c61a-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="2c61a-160">toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="2c61a-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="2c61a-161">Dit kunt u doen met Azure DNS- of andere providers DNS-door een CNAME-record maken die wijst toohello [openbaar IP-adres](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="2c61a-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="2c61a-162">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2c61a-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="2c61a-163">Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2c61a-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="2c61a-164">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="2c61a-164">Delete all resources</span></span>

<span data-ttu-id="2c61a-165">toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="2c61a-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="2c61a-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c61a-166">Next steps</span></span>

<span data-ttu-id="2c61a-167">Als u wilt dat tooconfigure SSL-offload, gaat u naar: [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="2c61a-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="2c61a-168">Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, gaat u naar: [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="2c61a-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="2c61a-169">Als u meer informatie wilt over de algemene opties voor taakverdeling, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="2c61a-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="2c61a-170">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="2c61a-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="2c61a-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2c61a-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
