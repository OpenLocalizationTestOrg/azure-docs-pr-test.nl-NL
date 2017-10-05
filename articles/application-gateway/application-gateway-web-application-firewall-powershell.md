---
title: Web application firewall - Azure Application Gateway configureren | Microsoft Docs
description: In dit artikel biedt richtlijnen voor het gebruik van web application firewall op een bestaande of nieuwe Application Gateway.
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="6c4a2-103">Web application firewall configureren op een nieuwe of bestaande Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6c4a2-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c4a2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6c4a2-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="6c4a2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c4a2-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="6c4a2-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="6c4a2-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="6c4a2-107">Informatie over het maken van een webtoepassing firewall ingeschakeld Application Gateway of web application firewall toevoegen aan een bestaande Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="6c4a2-108">De web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="6c4a2-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="6c4a2-110">De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud).</span><span class="sxs-lookup"><span data-stu-id="6c4a2-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="6c4a2-111">Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="6c4a2-112">Ga voor een volledige lijst met ondersteunde functies naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c4a2-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="6c4a2-113">Het volgende artikel toont hoe [web application firewall toevoegen aan een bestaande toepassingsgateway](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="6c4a2-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![afbeelding van scenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="6c4a2-115">WAF configuratie verschillen</span><span class="sxs-lookup"><span data-stu-id="6c4a2-115">WAF configuration differences</span></span>

<span data-ttu-id="6c4a2-116">Als u hebt gelezen [een toepassingsgateway maken met PowerShell](application-gateway-create-gateway-arm.md), u inzicht in de SKU-instellingen bij het maken van een toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="6c4a2-117">WAF biedt aanvullende instellingen op te geven bij het configureren van de SKU voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="6c4a2-118">Er zijn geen aanvullende wijzigingen die u in de toepassingsgateway zelf aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="6c4a2-119">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="6c4a2-119">**Setting**</span></span> | <span data-ttu-id="6c4a2-120">**Details**</span><span class="sxs-lookup"><span data-stu-id="6c4a2-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="6c4a2-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="6c4a2-121">**SKU**</span></span> |<span data-ttu-id="6c4a2-122">Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote** grootten.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="6c4a2-123">Dankzij de introductie van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="6c4a2-124">WAF wordt niet ondersteund op kleine Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="6c4a2-125">**Laag**</span><span class="sxs-lookup"><span data-stu-id="6c4a2-125">**Tier**</span></span> | <span data-ttu-id="6c4a2-126">De beschikbare waarden zijn **standaard** of **WAF**.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="6c4a2-127">Bij gebruik van web application firewall, **WAF** moeten worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="6c4a2-128">**Modus**</span><span class="sxs-lookup"><span data-stu-id="6c4a2-128">**Mode**</span></span> | <span data-ttu-id="6c4a2-129">Deze instelling wordt de modus van WAF.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="6c4a2-130">toegestane waarden zijn **detectie** en **preventie**.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="6c4a2-131">Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="6c4a2-132">Gebeurtenissen worden nog wel geregistreerd in de modus te voorkomen, maar de aanvaller ontvangt een niet-geautoriseerde 403-antwoord van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="6c4a2-133">Web application firewall toevoegen aan een bestaande Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6c4a2-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="6c4a2-134">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6c4a2-135">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="6c4a2-136">Aanmelden bij uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="6c4a2-137">Selecteer het abonnement moet worden gebruikt voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="6c4a2-138">De gateway die u web application firewall om te toevoegen wilt worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="6c4a2-139">De sku van web application firewall configureren.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="6c4a2-140">De beschikbare grootten zijn **WAF\_grote** en **WAF\_gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="6c4a2-141">Als u web application firewall gebruikt de laag moet **WAF**, de capaciteit moet worden bevestigd bij het instellen van de sku.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="6c4a2-142">Configureer de instellingen WAF zoals gedefinieerd in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6c4a2-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="6c4a2-143">Voor **FirewallMode**, de beschikbare waarden zijn preventie en detectie.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="6c4a2-144">De toepassingsgateway bijwerken met de instellingen die zijn gedefinieerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="6c4a2-145">Deze opdracht werkt u de toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="6c4a2-146">Ga naar [Application Gateway diagnostics](application-gateway-diagnostics.md) om te begrijpen hoe logboeken bekijken voor uw toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="6c4a2-147">Vanwege de aard van de beveiliging van WAF moeten Logboeken regelmatig worden gecontroleerd om te begrijpen van de beveiligingsstatus van uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="6c4a2-148">Een toepassingsgateway maken met web application firewall</span><span class="sxs-lookup"><span data-stu-id="6c4a2-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="6c4a2-149">De volgende stappen gaat u door het hele proces van begin tot eind voor het maken van een toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="6c4a2-150">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6c4a2-151">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="6c4a2-152">Meld u aan bij Azure door het uitvoeren van `Login-AzureRmAccount`, u wordt gevraagd te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="6c4a2-153">Controleer de abonnementen voor het account door te voeren`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="6c4a2-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="6c4a2-154">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="6c4a2-155">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6c4a2-155">Create a resource group</span></span>

<span data-ttu-id="6c4a2-156">Een resourcegroep maken voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="6c4a2-157">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6c4a2-158">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6c4a2-159">Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="6c4a2-160">In het voorgaande voorbeeld is er een resourcegroep met de naam 'appgw-RG' en de locatie 'VS-West.' gemaakt</span><span class="sxs-lookup"><span data-stu-id="6c4a2-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="6c4a2-161">Als u een aangepaste test voor uw toepassingsgateway configureren moet, Zie [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6c4a2-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="6c4a2-162">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="6c4a2-163">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="6c4a2-163">Configure virtual network</span></span>

<span data-ttu-id="6c4a2-164">Toepassingsgateway vereist een subnet van een eigen.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="6c4a2-165">In deze stap maakt u een virtueel netwerk met een adresruimte van 10.0.0.0/16 en twee subnetten, één voor de toepassingsgateway en één voor de back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="6c4a2-166">Openbare IP-adres configureren</span><span class="sxs-lookup"><span data-stu-id="6c4a2-166">Configure public IP address</span></span>

<span data-ttu-id="6c4a2-167">Application Gateway vereist om te kunnen verwerken van externe aanvragen, een openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="6c4a2-168">Dit openbare IP-adres mag niet hebben een `DomainNameLabel` gedefinieerd die worden gebruikt door de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="6c4a2-169">De toepassingsgateway configureren</span><span class="sxs-lookup"><span data-stu-id="6c4a2-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="6c4a2-170">Toepassingsgateways gemaakt met de basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6c4a2-171">Ophalen van Application Gateway DNS-naam</span><span class="sxs-lookup"><span data-stu-id="6c4a2-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="6c4a2-172">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="6c4a2-173">Wanneer u een openbaar IP-adres, vereist de toepassingsgateway een dynamisch toegewezen DNS-naam, geen beschrijvende is.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6c4a2-174">Om ervoor te zorgen eindgebruikers kunnen de toepassingsgateway bereikt, kan een CNAME-record worden gebruikt om te verwijzen naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="6c4a2-175">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c4a2-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6c4a2-176">Voor het configureren van een alias ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="6c4a2-177">De toepassingsgateway DNS-naam moet worden gebruikt voor het maken van een CNAME-record die de twee webtoepassingen aan deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="6c4a2-178">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6c4a2-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6c4a2-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c4a2-179">Next steps</span></span>

<span data-ttu-id="6c4a2-180">Informatie over het configureren van diagnostische gegevens vastleggen voor de gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall logboekregistratie in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="6c4a2-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
