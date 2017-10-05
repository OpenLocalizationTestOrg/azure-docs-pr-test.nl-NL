---
title: Een application gateway met behulp van regels voor het doorsturen van URL | Microsoft Docs
description: Deze pagina vindt u instructies voor het maken, configureren van een toepassingsgateway met behulp van regels voor het doorsturen van URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="dce3e-103">Een toepassingsgateway met pad gebaseerde routering maken</span><span class="sxs-lookup"><span data-stu-id="dce3e-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dce3e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dce3e-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="dce3e-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="dce3e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="dce3e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dce3e-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="dce3e-107">URL-pad gebaseerde routering, kunt u de routes op basis van het URL-pad van een Http-aanvraag koppelen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="dce3e-108">Het controleren of er een route naar een back-end-adresgroep geconfigureerd voor de URL die zijn gepresenteerd in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="dce3e-109">Deze stuurt vervolgens het netwerkverkeer naar de gedefinieerde back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="dce3e-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="dce3e-110">Vaak gebruikt voor het doorsturen van op basis van een URL is voor andere typen inhoud aan andere back-endserver groepen van aanvragen verdelen over.</span><span class="sxs-lookup"><span data-stu-id="dce3e-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="dce3e-111">URL gebaseerde routering introduceert een nieuwe regel-type dat aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="dce3e-112">Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="dce3e-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="dce3e-113">Basic regeltype biedt een round robin-service voor de back-end-adresgroepen tijdens PathBasedRouting naast round robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL tijdens de back-endpool te kiezen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="dce3e-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="dce3e-114">Scenario</span></span>

<span data-ttu-id="dce3e-115">In het volgende voorbeeld Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: video servergroep en image-servergroep.</span><span class="sxs-lookup"><span data-stu-id="dce3e-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="dce3e-116">Aanvragen voor http://contoso.com/image * worden doorgestuurd naar de installatiekopie servergroep (pool1) en http://contoso.com/video * worden doorgestuurd naar video servergroep (pool2).</span><span class="sxs-lookup"><span data-stu-id="dce3e-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="dce3e-117">Als geen van de pad-patronen overeenkomen, kan een standaardgroep server (pool1) is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="dce3e-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![URL-route](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="dce3e-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="dce3e-119">Before you begin</span></span>

1. <span data-ttu-id="dce3e-120">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="dce3e-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="dce3e-121">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dce3e-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dce3e-122">Maakt u een virtueel netwerk en subnet voor Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="dce3e-123">Zorg ervoor dat er geen virtuele machines en cloudimplementaties zijn die gebruikmaken van het subnet.</span><span class="sxs-lookup"><span data-stu-id="dce3e-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="dce3e-124">De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.</span><span class="sxs-lookup"><span data-stu-id="dce3e-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="dce3e-125">De servers toegevoegd aan de groep back-end gebruiken van de toepassingsgateway moeten bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="dce3e-126">Wat is er vereist om een toepassingsgateway te maken?</span><span class="sxs-lookup"><span data-stu-id="dce3e-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="dce3e-127">**Back-endserverpool:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="dce3e-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="dce3e-128">De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="dce3e-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dce3e-129">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="dce3e-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dce3e-130">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="dce3e-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="dce3e-131">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="dce3e-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="dce3e-132">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="dce3e-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="dce3e-133">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="dce3e-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dce3e-134">**Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="dce3e-135">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="dce3e-135">Create an application gateway</span></span>

<span data-ttu-id="dce3e-136">Het verschil tussen het gebruik van Azure Classic en Azure Resource Manager zit hem in de volgorde waarin u de toepassingsgateway maakt en in de items die u moet configureren.</span><span class="sxs-lookup"><span data-stu-id="dce3e-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="dce3e-137">Met Resource Manager worden alle items waaruit een toepassingsgateway bestaat, afzonderlijk geconfigureerd en vervolgens samengesteld om de toepassingsgatewayresource te maken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="dce3e-138">Dit zijn de stappen voor het maken van een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="dce3e-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="dce3e-139">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dce3e-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="dce3e-140">Maak een virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="dce3e-141">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="dce3e-142">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="dce3e-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="dce3e-143">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dce3e-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="dce3e-144">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="dce3e-145">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dce3e-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="dce3e-146">Stap 1</span><span class="sxs-lookup"><span data-stu-id="dce3e-146">Step 1</span></span>

<span data-ttu-id="dce3e-147">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3e-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="dce3e-148">U wordt gevraagd om u te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="dce3e-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="dce3e-149">Stap 2</span><span class="sxs-lookup"><span data-stu-id="dce3e-149">Step 2</span></span>

<span data-ttu-id="dce3e-150">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="dce3e-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="dce3e-151">Stap 3</span><span class="sxs-lookup"><span data-stu-id="dce3e-151">Step 3</span></span>

<span data-ttu-id="dce3e-152">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="dce3e-153">Stap 4</span><span class="sxs-lookup"><span data-stu-id="dce3e-153">Step 4</span></span>

<span data-ttu-id="dce3e-154">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="dce3e-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="dce3e-155">U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="dce3e-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="dce3e-156">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dce3e-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="dce3e-157">Deze resourcegroep wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="dce3e-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="dce3e-158">Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="dce3e-159">In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam appgw-RG en de locatie VS - west.</span><span class="sxs-lookup"><span data-stu-id="dce3e-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="dce3e-160">Als u voor uw toepassingsgateway een aangepaste test moet configureren, raadpleegt u [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md) (Met PowerShell een toepassingsgateway maken met aangepaste tests).</span><span class="sxs-lookup"><span data-stu-id="dce3e-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="dce3e-161">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dce3e-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="dce3e-162">Een virtueel netwerk en een subnet maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="dce3e-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="dce3e-163">In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dce3e-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="dce3e-164">In dit voorbeeld wordt er een VNET gemaakt voor Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="dce3e-165">Toepassingsgateway vereist een eigen subnet, om deze reden het subnet dat is gemaakt voor de toepassingsgateway kleiner dan de VNET-adresruimte is.</span><span class="sxs-lookup"><span data-stu-id="dce3e-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="dce3e-166">Hierdoor kunnen andere resources, inclusief maar niet beperkt tot webservers moet worden geconfigureerd in hetzelfde VNET.</span><span class="sxs-lookup"><span data-stu-id="dce3e-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="dce3e-167">Stap 1</span><span class="sxs-lookup"><span data-stu-id="dce3e-167">Step 1</span></span>

<span data-ttu-id="dce3e-168">Wijs het adresbereik 10.0.0.0/24 toe aan de subnetvariabele die u gaat gebruiken om een virtueel netwerk te maken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="dce3e-169">Hiermee maakt u het configuratieobject subnet voor de toepassingsgateway, die wordt gebruikt in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="dce3e-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="dce3e-170">Stap 2</span><span class="sxs-lookup"><span data-stu-id="dce3e-170">Step 2</span></span>

<span data-ttu-id="dce3e-171">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg**. Doe dit voor de regio VS - west. Gebruik het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="dce3e-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="dce3e-172">Hiermee wordt de configuratie van het VNET met één subnet voor de toepassingsgateway zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="dce3e-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="dce3e-173">Stap 3</span><span class="sxs-lookup"><span data-stu-id="dce3e-173">Step 3</span></span>

<span data-ttu-id="dce3e-174">Toewijzen van de variabele subnet voor de volgende stappen, dit wordt doorgegeven aan de `New-AzureRMApplicationGateway` cmdlet in een toekomstige stap.</span><span class="sxs-lookup"><span data-stu-id="dce3e-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="dce3e-175">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="dce3e-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="dce3e-176">Maak de openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS - west.</span><span class="sxs-lookup"><span data-stu-id="dce3e-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="dce3e-177">Voor Application Gateway kan een openbaar IP-adres, een intern IP-adres of beide worden gebruikt om aanvragen voor de taakverdeling te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="dce3e-178">In dit voorbeeld wordt er alleen een openbaar IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-178">This example only uses a public IP address.</span></span> <span data-ttu-id="dce3e-179">In het volgende voorbeeld is er geen DNS-naam geconfigureerd voor het maken van het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="dce3e-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="dce3e-180">Application Gateway biedt geen ondersteuning voor aangepaste DNS-namen voor openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="dce3e-181">Als er een aangepaste naam is vereist voor het openbare eindpunt, moet er een CNAME-record worden gemaakt die verwijst naar de automatisch gegenereerde DNS-naam voor het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="dce3e-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="dce3e-182">Er wordt een IP-adres toegewezen aan de toepassingsgateway wanneer de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="dce3e-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="dce3e-183">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="dce3e-183">Create application gateway configuration</span></span>

<span data-ttu-id="dce3e-184">Alle configuratie-items moeten zijn ingesteld voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="dce3e-185">Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="dce3e-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="dce3e-186">Stap 1</span><span class="sxs-lookup"><span data-stu-id="dce3e-186">Step 1</span></span>

<span data-ttu-id="dce3e-187">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="dce3e-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="dce3e-188">Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool.</span><span class="sxs-lookup"><span data-stu-id="dce3e-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="dce3e-189">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="dce3e-190">Stap 2</span><span class="sxs-lookup"><span data-stu-id="dce3e-190">Step 2</span></span>

<span data-ttu-id="dce3e-191">Configureer de backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen voor **pool1** en **pool2**.</span><span class="sxs-lookup"><span data-stu-id="dce3e-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="dce3e-192">Deze IP-adressen zijn de IP-adressen van de resources waarop de webtoepassing wordt gehost die moet worden beveiligd door de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="dce3e-193">Aan de hand van basistests of aangepaste tests wordt gecontroleerd of alle back-endpoolleden in orde zijn.</span><span class="sxs-lookup"><span data-stu-id="dce3e-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="dce3e-194">Vervolgens wordt verkeer hiernaartoe doorgestuurd wanneer er aanvragen binnenkomen in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="dce3e-195">Back-endpools kunnen worden gebruikt door meerdere regels in de toepassingsgateway. Dit betekent dat een back-endpool kan worden gebruikt voor meerdere webtoepassingen die zich op dezelfde host bevinden.</span><span class="sxs-lookup"><span data-stu-id="dce3e-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="dce3e-196">In dit voorbeeld zijn er twee back-endpools voor het verzenden van netwerkverkeer op basis van het URL-pad.</span><span class="sxs-lookup"><span data-stu-id="dce3e-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="dce3e-197">Een pool ontvangt verkeer vanuit het URL-pad '/video' en andere pool ontvangt verkeer vanuit het pad '/image'.</span><span class="sxs-lookup"><span data-stu-id="dce3e-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="dce3e-198">Vervang de bovenstaande IP-adressen door de IP-adreseindpunten van uw eigen toepassing.</span><span class="sxs-lookup"><span data-stu-id="dce3e-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="dce3e-199">Stap 3</span><span class="sxs-lookup"><span data-stu-id="dce3e-199">Step 3</span></span>

<span data-ttu-id="dce3e-200">Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor het netwerkverkeer van taakverdeling in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="dce3e-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="dce3e-201">In dit voorbeeld configureert u de instellingen van de andere back-end-adresgroep voor de back-end-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="dce3e-202">Elke back-endpool kan een eigen instelling van de back-endpool hebben.</span><span class="sxs-lookup"><span data-stu-id="dce3e-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="dce3e-203">Back-end-HTTP-instellingen worden gebruikt door regels om verkeer te verzenden naar de juiste back-endpoolleden.</span><span class="sxs-lookup"><span data-stu-id="dce3e-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="dce3e-204">Hiermee bepaalt u het protocol en de poort die wordt gebruikt bij het verzenden van verkeer op de leden van de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="dce3e-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="dce3e-205">Sessies op basis van cookies worden ook bepaald door de back-end-HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="dce3e-206">Als sessieaffiniteit op basis van cookies is ingeschakeld, wordt verkeer verzonden naar dezelfde back-end als bij de vorige aanvragen voor elk pakket.</span><span class="sxs-lookup"><span data-stu-id="dce3e-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="dce3e-207">Stap 4</span><span class="sxs-lookup"><span data-stu-id="dce3e-207">Step 4</span></span>

<span data-ttu-id="dce3e-208">Configureer het front-end-IP-adres met openbaar IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="dce3e-209">Het configuratie-object front-end-IP-adres wordt gebruikt door een listener om het uitgaande IP-adres te koppelen aan de listener.</span><span class="sxs-lookup"><span data-stu-id="dce3e-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="dce3e-210">Stap 5</span><span class="sxs-lookup"><span data-stu-id="dce3e-210">Step 5</span></span>

<span data-ttu-id="dce3e-211">Configureer de front-endpoort voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="dce3e-212">Het configuratieobject front-endpoort wordt gebruikt door een listener om te definiëren via welke poort Application Gateway naar verkeer op de listener luistert.</span><span class="sxs-lookup"><span data-stu-id="dce3e-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="dce3e-213">Stap 6</span><span class="sxs-lookup"><span data-stu-id="dce3e-213">Step 6</span></span>

<span data-ttu-id="dce3e-214">Configureer de listener.</span><span class="sxs-lookup"><span data-stu-id="dce3e-214">Configure the listener.</span></span> <span data-ttu-id="dce3e-215">In deze stap wordt de listener voor het openbare IP-adres en de poort voor het ontvangen van binnenkomend netwerkverkeer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="dce3e-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="dce3e-216">Het volgende voorbeeld wordt de eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en configureert de listener.</span><span class="sxs-lookup"><span data-stu-id="dce3e-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="dce3e-217">In dit voorbeeld luistert de listener luistert naar HTTP-verkeer op poort 80 voor het openbare IP-adres dat eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="dce3e-218">Stap 7</span><span class="sxs-lookup"><span data-stu-id="dce3e-218">Step 7</span></span>

<span data-ttu-id="dce3e-219">URL-paden regel voor de back-end-adresgroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="dce3e-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="dce3e-220">Deze stap configureert u het relatieve pad gebruikt door de toepassingsgateway en definieert de toewijzing tussen het URL-pad en de back-end-pool die is toegewezen aan de binnenkomend verkeer verwerken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dce3e-221">Elk pad moet beginnen met / en de enige plaats waar een '\*' is toegestaan, wordt aan het einde.</span><span class="sxs-lookup"><span data-stu-id="dce3e-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="dce3e-222">Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *.</span><span class="sxs-lookup"><span data-stu-id="dce3e-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="dce3e-223">De tekenreeks die is ingevoerd in het pad matcher geen tekst bevatten na de eerste '? ' of '#' en deze tekens zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dce3e-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="dce3e-224">Het volgende voorbeeld maakt u twee regels: één voor '/ afbeelding /' pad routeren van verkeer naar de back-end 'pool1' en een andere voor '/ video /' pad routeren van verkeer naar de back-end 'pool2'.</span><span class="sxs-lookup"><span data-stu-id="dce3e-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="dce3e-225">Deze regels ervoor zorgen dat verkeer voor elke set van URL's wordt doorgestuurd naar de back-end.</span><span class="sxs-lookup"><span data-stu-id="dce3e-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="dce3e-226">Bijvoorbeeld: http://contoso.com/image/figure1.jpg gaat naar pool1 en http://contoso.com/video/example.mp4 gaat dan naar pool2.</span><span class="sxs-lookup"><span data-stu-id="dce3e-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="dce3e-227">Als het pad komt niet met de vooraf gedefinieerde padregels overeen, configureert de regel pad kaart configuratie ook een standaard back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="dce3e-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="dce3e-228">Bijvoorbeeld: http://contoso.com/shoppingcart/test.html gaat u naar pool1 zoals deze is gedefinieerd als de standaardgroep voor niet-overeenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="dce3e-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="dce3e-229">Stap 8</span><span class="sxs-lookup"><span data-stu-id="dce3e-229">Step 8</span></span>

<span data-ttu-id="dce3e-230">De instelling van een regel maken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-230">Create a rule setting.</span></span> <span data-ttu-id="dce3e-231">Deze stap configureert u de toepassingsgateway als URL-pad gebaseerde routering wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dce3e-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="dce3e-232">De `$urlPathMap` variabele gedefinieerd in de vorige stap nu gebruikt voor het maken van de regel op basis van het pad.</span><span class="sxs-lookup"><span data-stu-id="dce3e-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="dce3e-233">In deze stap wordt de regel koppelen aan een listener en de toewijzing van de url-pad eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dce3e-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="dce3e-234">Stap 9</span><span class="sxs-lookup"><span data-stu-id="dce3e-234">Step 9</span></span>

<span data-ttu-id="dce3e-235">Configureer het aantal exemplaren en de grootte voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="dce3e-236">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="dce3e-236">Create Application Gateway</span></span>

<span data-ttu-id="dce3e-237">Een toepassingsgateway maken met alle configuratie-objecten uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="dce3e-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="dce3e-238">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="dce3e-238">Get application gateway DNS name</span></span>

<span data-ttu-id="dce3e-239">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="dce3e-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="dce3e-240">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="dce3e-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="dce3e-241">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="dce3e-242">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dce3e-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="dce3e-243">Voor het configureren van de frontend-IP-CNAME-record ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="dce3e-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="dce3e-244">De toepassingsgateway DNS-naam moet worden gebruikt voor het maken van een CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="dce3e-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="dce3e-245">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="dce3e-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dce3e-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dce3e-246">Next steps</span></span>

<span data-ttu-id="dce3e-247">Als u weten van Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="dce3e-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

