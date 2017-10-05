---
title: Met behulp van Azure-toepassingsgateway met interne Load Balancer - PowerShell | Microsoft Docs
description: Op deze pagina vindt u instructies voor het maken, configureren, openen en verwijderen van een Azure-toepassingsgateway met een interne load balancer (ILB) voor Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="62e80-103">Een toepassingsgateway met een interne load balancer (ILB) maken met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62e80-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="62e80-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="62e80-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="62e80-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="62e80-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="62e80-106">Azure Application Gateway kan worden geconfigureerd met een internetgerichte VIP of met een intern eindpunt dat geen toegang heeft tot het internet. Dit heet ook wel een ILB-eindpunt (interne load balancer).</span><span class="sxs-lookup"><span data-stu-id="62e80-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="62e80-107">Het is een goed idee om de gateway te configureren met een ILB als u interne line-of-business-toepassingen gebruikt die geen toegang hebben tot het internet.</span><span class="sxs-lookup"><span data-stu-id="62e80-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="62e80-108">Ook is dit handig als u services en lagen gebruikt in een toepassing met meerdere lagen die zich binnen een beveiligingsgrens bevinden, en als deze toepassing geen toegang heeft tot het internet, maar er wel round-robinbelastingverdeling, sessiepersistentie of SSL-beëindiging (Secure Sockets Layer) vereist is.</span><span class="sxs-lookup"><span data-stu-id="62e80-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="62e80-109">In dit artikel worden de stappen beschreven voor het configureren van een toepassingsgateway met een ILB.</span><span class="sxs-lookup"><span data-stu-id="62e80-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62e80-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="62e80-110">Before you begin</span></span>

1. <span data-ttu-id="62e80-111">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="62e80-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="62e80-112">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="62e80-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="62e80-113">U maakt een virtueel netwerk en een subnet voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="62e80-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="62e80-114">Zorg ervoor dat er geen virtuele machines en cloudimplementaties zijn die gebruikmaken van het subnet.</span><span class="sxs-lookup"><span data-stu-id="62e80-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="62e80-115">De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.</span><span class="sxs-lookup"><span data-stu-id="62e80-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="62e80-116">De servers die u voor gebruik van de toepassingsgateway configureert, moeten al bestaan in het virtuele netwerk of hier hun eindpunten hebben. Een andere optie is om er een openbaar IP- of VIP-adres aan toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="62e80-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="62e80-117">Wat is er vereist om een toepassingsgateway te maken?</span><span class="sxs-lookup"><span data-stu-id="62e80-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="62e80-118">**Back-endserverpool:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="62e80-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="62e80-119">De IP-adressen moeten ofwel deel uitmaken van het virtueel netwerk, maar zich bevinden in een ander subnet voor de toepassingsgateway, ofwel openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="62e80-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="62e80-120">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="62e80-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="62e80-121">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="62e80-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="62e80-122">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="62e80-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="62e80-123">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="62e80-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="62e80-124">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="62e80-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="62e80-125">**Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="62e80-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="62e80-126">Momenteel wordt alleen de regel *basic* ondersteund.</span><span class="sxs-lookup"><span data-stu-id="62e80-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="62e80-127">De regel *basic* is een vorm van round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="62e80-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="62e80-128">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="62e80-128">Create an application gateway</span></span>

<span data-ttu-id="62e80-129">Het verschil tussen het gebruik van Azure Classic en Azure Resource Manager zit hem in de volgorde waarin u de toepassingsgateway maakt en in de items die u moet configureren.</span><span class="sxs-lookup"><span data-stu-id="62e80-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="62e80-130">Met Resource Manager worden alle items waaruit een toepassingsgateway bestaat afzonderlijk geconfigureerd en vervolgens samengesteld om de toepassingsgatewayresource te maken.</span><span class="sxs-lookup"><span data-stu-id="62e80-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="62e80-131">Dit zijn de stappen voor het maken van een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="62e80-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="62e80-132">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62e80-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="62e80-133">Een virtueel netwerk en een subnet maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="62e80-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="62e80-134">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="62e80-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="62e80-135">Een toepassingsgatewayresource maken</span><span class="sxs-lookup"><span data-stu-id="62e80-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="62e80-136">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62e80-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="62e80-137">Zorg ervoor dat u overschakelt naar de PowerShell-modus om de Azure Resource Manager-cmdlets te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="62e80-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="62e80-138">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="62e80-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="62e80-139">Stap 1</span><span class="sxs-lookup"><span data-stu-id="62e80-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="62e80-140">Stap 2</span><span class="sxs-lookup"><span data-stu-id="62e80-140">Step 2</span></span>

<span data-ttu-id="62e80-141">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="62e80-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="62e80-142">U wordt gevraagd om u te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="62e80-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="62e80-143">Stap 3</span><span class="sxs-lookup"><span data-stu-id="62e80-143">Step 3</span></span>

<span data-ttu-id="62e80-144">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="62e80-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="62e80-145">Stap 4</span><span class="sxs-lookup"><span data-stu-id="62e80-145">Step 4</span></span>

<span data-ttu-id="62e80-146">Maak een nieuwe resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="62e80-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="62e80-147">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="62e80-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="62e80-148">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="62e80-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="62e80-149">Zorg ervoor dat bij alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62e80-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="62e80-150">In het vorige voorbeeld gemaakt we een resourcegroep 'appgw-rg' en de locatie ' West ' genoemd.</span><span class="sxs-lookup"><span data-stu-id="62e80-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="62e80-151">Een virtueel netwerk en een subnet maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="62e80-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="62e80-152">In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="62e80-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="62e80-153">Stap 1</span><span class="sxs-lookup"><span data-stu-id="62e80-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="62e80-154">Deze stap wijst het adresbereik 10.0.0.0/24 toe aan een variabele subnet dat wordt gebruikt om een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="62e80-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="62e80-155">Stap 2</span><span class="sxs-lookup"><span data-stu-id="62e80-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="62e80-156">Deze stap maakt een virtueel netwerk met de naam 'appgwvnet' in de resourcegroep 'appgw-rg' voor de regio VS-West is met het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="62e80-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="62e80-157">Stap 3</span><span class="sxs-lookup"><span data-stu-id="62e80-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="62e80-158">Deze stap wijst u het subnetobject toe aan de variabele $subnet voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="62e80-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="62e80-159">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="62e80-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="62e80-160">Stap 1</span><span class="sxs-lookup"><span data-stu-id="62e80-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="62e80-161">Deze stap maakt toepassingsgateway een IP-configuratie met de naam 'gatewayIP01'.</span><span class="sxs-lookup"><span data-stu-id="62e80-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="62e80-162">Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool.</span><span class="sxs-lookup"><span data-stu-id="62e80-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="62e80-163">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62e80-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="62e80-164">Stap 2</span><span class="sxs-lookup"><span data-stu-id="62e80-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="62e80-165">Deze stap configureert u de backend-IP-adresgroep met de naam 'pool01' met IP-adressen '10.1.1.8, 10.1.1.9, 10.1.1.10'.</span><span class="sxs-lookup"><span data-stu-id="62e80-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="62e80-166">Dit zijn de IP-adressen waardoor het netwerkverkeer van het front-end-IP-eindpunt binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="62e80-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="62e80-167">U vervangt de bovenstaande IP-adressen met de IP-adreseindpunten van uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="62e80-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="62e80-168">Stap 3</span><span class="sxs-lookup"><span data-stu-id="62e80-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="62e80-169">Deze stap configureert u application gateway-instelling 'poolsetting01' voor de load balanced netwerkverkeer in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="62e80-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="62e80-170">Stap 4</span><span class="sxs-lookup"><span data-stu-id="62e80-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="62e80-171">Deze stap configureert u de front-end-IP-poort met de naam 'frontendport01' voor de ILB.</span><span class="sxs-lookup"><span data-stu-id="62e80-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="62e80-172">Stap 5</span><span class="sxs-lookup"><span data-stu-id="62e80-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="62e80-173">Deze stap maakt u de front-end-IP-configuratie 'fipconfig01' genoemd en koppelt u deze aan een particuliere IP-adres van het subnet van de huidige virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="62e80-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="62e80-174">Stap 6</span><span class="sxs-lookup"><span data-stu-id="62e80-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="62e80-175">Deze stap maakt de listener met de naam 'listener01' en koppelt u de front-endpoort aan de front-end-IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="62e80-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="62e80-176">Stap 7</span><span class="sxs-lookup"><span data-stu-id="62e80-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="62e80-177">Deze stap maakt de load balancer-routeringsregel genaamd 'rule01', waarmee het gedrag van de load balancer worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="62e80-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="62e80-178">Stap 8</span><span class="sxs-lookup"><span data-stu-id="62e80-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="62e80-179">Deze stap configureert u de exemplaargrootte van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="62e80-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="62e80-180">De standaardwaarde voor *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="62e80-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="62e80-181">De standaardwaarde voor *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="62e80-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="62e80-182">U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="62e80-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="62e80-183">Een toepassingsgateway maken met behulp van New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="62e80-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="62e80-184">Hiermee maakt een toepassingsgateway met alle configuratie-items uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="62e80-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="62e80-185">In dit voorbeeld heeft de toepassingsgateway de naam appgwtest.</span><span class="sxs-lookup"><span data-stu-id="62e80-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="62e80-186">Deze stap maakt een toepassingsgateway met alle configuratie-items uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="62e80-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="62e80-187">In dit voorbeeld heeft de toepassingsgateway de naam appgwtest.</span><span class="sxs-lookup"><span data-stu-id="62e80-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="62e80-188">Een toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="62e80-188">Delete an application gateway</span></span>

<span data-ttu-id="62e80-189">Om een toepassingsgateway verwijderen, moet u de volgende stappen in volgorde uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="62e80-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="62e80-190">Gebruik de cmdlet `Stop-AzureRmApplicationGateway` om de gateway te stoppen.</span><span class="sxs-lookup"><span data-stu-id="62e80-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="62e80-191">Gebruik de cmdlet `Remove-AzureRmApplicationGateway` om de gateway te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="62e80-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="62e80-192">Gebruik de cmdlet `Get-AzureApplicationGateway` om te controleren of de gateway is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="62e80-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="62e80-193">Stap 1</span><span class="sxs-lookup"><span data-stu-id="62e80-193">Step 1</span></span>

<span data-ttu-id="62e80-194">Haal het toepassingsgatewayobject op en koppel dit aan de variabele $getgw.</span><span class="sxs-lookup"><span data-stu-id="62e80-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="62e80-195">Stap 2</span><span class="sxs-lookup"><span data-stu-id="62e80-195">Step 2</span></span>

<span data-ttu-id="62e80-196">Gebruik `Stop-AzureRmApplicationGateway` om de toepassingsgateway te stoppen.</span><span class="sxs-lookup"><span data-stu-id="62e80-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="62e80-197">Dit voorbeeld wordt de `Stop-AzureRmApplicationGateway` cmdlet uit op de eerste regel weergegeven, gevolgd door de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="62e80-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="62e80-198">Nadat de toepassingsgateway is gestopt, gebruikt u de cmdlet `Remove-AzureRmApplicationGateway` om de service te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="62e80-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="62e80-199">U kunt de switch **-force** gebruiken om het bevestigingsbericht voor de verwijdering niet te laten weergeven.</span><span class="sxs-lookup"><span data-stu-id="62e80-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="62e80-200">Gebruik de cmdlet `Get-AzureRmApplicationGateway` als u wilt controleren of de service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="62e80-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="62e80-201">Deze stap is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="62e80-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="62e80-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62e80-202">Next steps</span></span>

<span data-ttu-id="62e80-203">Als u SSL-offload wilt configureren, raadpleegt u [Configure an application gateway for SSL offload](application-gateway-ssl.md) (Een toepassingsgateway voor SSL-offload configureren).</span><span class="sxs-lookup"><span data-stu-id="62e80-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="62e80-204">Als u een Application Gateway wilt configureren voor gebruik met een ILB, raadpleegt u [Een Application Gateway met een interne Load Balancer (ILB) maken](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="62e80-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="62e80-205">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="62e80-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="62e80-206">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="62e80-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="62e80-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="62e80-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

