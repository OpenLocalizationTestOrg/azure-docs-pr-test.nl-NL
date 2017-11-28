---
title: aaaConfigure web application firewall - Azure Application Gateway | Microsoft Docs
description: In dit artikel biedt richtlijnen voor hoe toostart met behulp van web application firewall op een bestaande of nieuwe Application Gateway.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="b755e-103">Web application firewall configureren op een nieuwe of bestaande Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b755e-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b755e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b755e-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="b755e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b755e-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="b755e-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="b755e-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="b755e-107">Meer informatie over hoe toocreate web application firewall ingeschakeld voor Application Gateway of web application firewall tooan bestaande toepassingsgateway toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b755e-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="b755e-108">Hallo web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.</span><span class="sxs-lookup"><span data-stu-id="b755e-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="b755e-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="b755e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b755e-110">Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="b755e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b755e-111">Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere.</span><span class="sxs-lookup"><span data-stu-id="b755e-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b755e-112">toofind een volledige lijst van ondersteunde functies, gaat u naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b755e-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="b755e-113">Hallo volgende artikel laat zien hoe te[web application firewall tooan bestaande toepassingsgateway toevoegen](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="b755e-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![afbeelding van scenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="b755e-115">WAF configuratie verschillen</span><span class="sxs-lookup"><span data-stu-id="b755e-115">WAF configuration differences</span></span>

<span data-ttu-id="b755e-116">Als u hebt gelezen [een toepassingsgateway maken met PowerShell](application-gateway-create-gateway-arm.md), u begrijpt Hallo SKU instellingen tooconfigure bij het maken van een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="b755e-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="b755e-117">WAF biedt extra instellingen toodefine bij het configureren van Hallo SKU voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="b755e-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="b755e-118">Er zijn geen aanvullende wijzigingen die u op Hallo Application Gateway zelf aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="b755e-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="b755e-119">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="b755e-119">**Setting**</span></span> | <span data-ttu-id="b755e-120">**Details**</span><span class="sxs-lookup"><span data-stu-id="b755e-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="b755e-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="b755e-121">**SKU**</span></span> |<span data-ttu-id="b755e-122">Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote** grootten.</span><span class="sxs-lookup"><span data-stu-id="b755e-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="b755e-123">Dankzij de introductie van de Hallo van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**.</span><span class="sxs-lookup"><span data-stu-id="b755e-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="b755e-124">WAF wordt niet ondersteund op kleine Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="b755e-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="b755e-125">**Laag**</span><span class="sxs-lookup"><span data-stu-id="b755e-125">**Tier**</span></span> | <span data-ttu-id="b755e-126">Hallo beschikbare waarden zijn **standaard** of **WAF**.</span><span class="sxs-lookup"><span data-stu-id="b755e-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="b755e-127">Bij gebruik van web application firewall, **WAF** moeten worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="b755e-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="b755e-128">**Modus**</span><span class="sxs-lookup"><span data-stu-id="b755e-128">**Mode**</span></span> | <span data-ttu-id="b755e-129">Deze instelling is Hallo-modus van WAF.</span><span class="sxs-lookup"><span data-stu-id="b755e-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="b755e-130">toegestane waarden zijn **detectie** en **preventie**.</span><span class="sxs-lookup"><span data-stu-id="b755e-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="b755e-131">Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="b755e-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="b755e-132">Gebeurtenissen worden nog wel geregistreerd in '-modus, maar Hallo aanvaller 403 onbevoegde-antwoord van Hallo Application Gateway ontvangt.</span><span class="sxs-lookup"><span data-stu-id="b755e-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="b755e-133">Web application firewall tooan bestaande toepassingsgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="b755e-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="b755e-134">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="b755e-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b755e-135">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b755e-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="b755e-136">Meld u bij tooyour Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="b755e-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="b755e-137">Selecteer Hallo abonnement toouse voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="b755e-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="b755e-138">Hallo-gateway die u web application firewall om te toevoegen wilt worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b755e-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="b755e-139">Hallo web application firewall sku configureren.</span><span class="sxs-lookup"><span data-stu-id="b755e-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="b755e-140">Hallo beschikbare grootten zijn **WAF\_grote** en **WAF\_gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="b755e-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="b755e-141">Bij gebruik van web application firewall Hallo laag moet **WAF**, Hallo capaciteit moet worden bevestigd bij het instellen van Hallo sku.</span><span class="sxs-lookup"><span data-stu-id="b755e-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="b755e-142">Hallo WAF instellingen te configureren zoals gedefinieerd in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="b755e-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="b755e-143">Voor **FirewallMode**, Hallo beschikbare waarden zijn preventie en detectie.</span><span class="sxs-lookup"><span data-stu-id="b755e-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="b755e-144">Hallo Application Gateway met Hallo-instellingen die zijn gedefinieerd in de voorgaande stap Hallo bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b755e-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="b755e-145">Met deze opdracht werkt Hallo Application Gateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="b755e-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="b755e-146">Ga naar [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand hoe tooview voor uw toepassingsgateway registreert.</span><span class="sxs-lookup"><span data-stu-id="b755e-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="b755e-147">Vervaldatum toohello aard van de beveiliging van WAF beoordeeld logboeken moeten toobe regelmatig toounderstand Hallo-beveiligingsstatus van uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="b755e-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="b755e-148">Een toepassingsgateway maken met web application firewall</span><span class="sxs-lookup"><span data-stu-id="b755e-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="b755e-149">Hallo gaat volgende stappen u door de hele proces Hallo van begin tooend voor het maken van een toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="b755e-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="b755e-150">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="b755e-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b755e-151">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b755e-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="b755e-152">Meld u bij tooAzure door het uitvoeren van `Login-AzureRmAccount`, u tooauthenticate na vragen aan gebruiker zich met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="b755e-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="b755e-153">Hallo-abonnementen voor Hallo account controleren door te voeren`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="b755e-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="b755e-154">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="b755e-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="b755e-155">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="b755e-155">Create a resource group</span></span>

<span data-ttu-id="b755e-156">Maak een resourcegroep voor Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b755e-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="b755e-157">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b755e-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b755e-158">Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b755e-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b755e-159">Zorg ervoor dat alle opdrachten die gebruikmaakt van toocreate een toepassingsgateway dezelfde resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="b755e-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="b755e-160">In Hallo voorgaande voorbeeld, er gemaakt met een resourcegroep genaamd "Appgw-RG' en de locatie 'VS-West."</span><span class="sxs-lookup"><span data-stu-id="b755e-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="b755e-161">Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b755e-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="b755e-162">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b755e-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="b755e-163">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="b755e-163">Configure virtual network</span></span>

<span data-ttu-id="b755e-164">Toepassingsgateway vereist een subnet van een eigen.</span><span class="sxs-lookup"><span data-stu-id="b755e-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="b755e-165">In deze stap maakt u een virtueel netwerk met een adresruimte van 10.0.0.0/16 en twee subnetten, één voor Application Gateway Hallo en één voor de back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="b755e-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="b755e-166">Openbare IP-adres configureren</span><span class="sxs-lookup"><span data-stu-id="b755e-166">Configure public IP address</span></span>

<span data-ttu-id="b755e-167">Application Gateway vereist in volgorde toohandle externe aanvragen, een openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b755e-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="b755e-168">Dit openbare IP-adres mag niet hebben een `DomainNameLabel` toobe die wordt gebruikt door Hallo Application Gateway gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b755e-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="b755e-169">Hallo Application Gateway configureren</span><span class="sxs-lookup"><span data-stu-id="b755e-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="b755e-170">Toepassingsgateways gemaakt met de Hallo basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="b755e-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b755e-171">Ophalen van Application Gateway DNS-naam</span><span class="sxs-lookup"><span data-stu-id="b755e-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="b755e-172">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="b755e-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b755e-173">Wanneer u een openbaar IP-adres, vereist de toepassingsgateway een dynamisch toegewezen DNS-naam, geen beschrijvende is.</span><span class="sxs-lookup"><span data-stu-id="b755e-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b755e-174">tooensure eindgebruikers Hallo Application Gateway kan worden bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b755e-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="b755e-175">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b755e-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="b755e-176">een alias tooconfigure ophalen van gegevens van Hallo Application Gateway en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppeld toohello Application Gateway met.</span><span class="sxs-lookup"><span data-stu-id="b755e-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="b755e-177">Hallo Application Gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="b755e-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="b755e-178">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b755e-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b755e-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b755e-179">Next steps</span></span>

<span data-ttu-id="b755e-180">Meer informatie over hoe tooconfigure Diagnostische logboekregistratie, toolog Hallo gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="b755e-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
