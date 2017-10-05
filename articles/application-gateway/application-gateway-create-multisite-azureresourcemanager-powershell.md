---
title: Een toepassingsgateway voor het hosten van meerdere sites maken | Microsoft Docs
description: Deze pagina vindt u instructies voor het maken, configureren van een toepassingsgateway voor het hosten van meerdere webtoepassingen op dezelfde gateway.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="acb70-103">Een toepassingsgateway voor het hosten van meerdere webtoepassingen maken</span><span class="sxs-lookup"><span data-stu-id="acb70-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="acb70-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="acb70-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="acb70-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="acb70-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="acb70-106">Meerdere hosting-site, kunt u meer dan een webtoepassing op dezelfde toepassingsgateway implementeren.</span><span class="sxs-lookup"><span data-stu-id="acb70-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="acb70-107">Is afhankelijk van de aanwezigheid van de host-header in de binnenkomende HTTP-aanvraag om te bepalen welke listener verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="acb70-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="acb70-108">De listener stuurt vervolgens verkeer naar de juiste back-endpool zoals geconfigureerd in de definitie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="acb70-109">In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van de Server de naam van vermelding (SNI)-extensie voor kiest u de juiste listener voor internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="acb70-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="acb70-110">Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over voor verschillende webdomeinen op verschillende back-endserver opslaggroepen.</span><span class="sxs-lookup"><span data-stu-id="acb70-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="acb70-111">Op dezelfde manier kunnen meerdere subdomeinen van het hoofddomein dezelfde ook worden gehost op dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="acb70-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="acb70-112">Scenario</span></span>

<span data-ttu-id="acb70-113">In het volgende voorbeeld toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep.</span><span class="sxs-lookup"><span data-stu-id="acb70-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="acb70-114">Vergelijkbare setup kan worden gebruikt voor de host subdomeinen zoals app.contoso.com en blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="acb70-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="acb70-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="acb70-116">Before you begin</span></span>

1. <span data-ttu-id="acb70-117">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="acb70-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="acb70-118">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="acb70-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="acb70-119">De servers toegevoegd aan de groep back-end gebruiken van de toepassingsgateway moeten bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk in een apart subnet of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="acb70-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="acb70-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="acb70-120">Requirements</span></span>

* <span data-ttu-id="acb70-121">**Back-endserverpool:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="acb70-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="acb70-122">De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="acb70-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="acb70-123">FQDN-naam kan ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="acb70-123">FQDN can also be used.</span></span>
* <span data-ttu-id="acb70-124">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="acb70-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="acb70-125">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="acb70-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="acb70-126">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="acb70-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="acb70-127">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="acb70-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="acb70-128">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="acb70-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="acb70-129">Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="acb70-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="acb70-130">**Regel:** de regel verbindt de listener met de back-end-servergroep, en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="acb70-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="acb70-131">Regels worden verwerkt in de volgorde die ze worden weergegeven en verkeer wordt doorgestuurd via de eerste regel die overeenkomt met ongeacht specifieke karakter.</span><span class="sxs-lookup"><span data-stu-id="acb70-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="acb70-132">Bijvoorbeeld, als u een regel met behulp van een basic-listener en een regel met meerdere sites listener beide op dezelfde poort hebt, kan de regel met de listener voor meerdere locaties moet worden vermeld voordat u de regel met de basic-listener in volgorde voor de regel voor meerdere locaties werken zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="acb70-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="acb70-133">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="acb70-133">Create an application gateway</span></span>

<span data-ttu-id="acb70-134">Hier volgen de stappen die nodig zijn om een toepassingsgateway te maken:</span><span class="sxs-lookup"><span data-stu-id="acb70-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="acb70-135">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acb70-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="acb70-136">Maak een virtueel netwerk, subnetten en openbare IP-adres voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="acb70-137">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="acb70-138">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="acb70-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="acb70-139">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acb70-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="acb70-140">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="acb70-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="acb70-141">Meer informatie vindt u op [Windows PowerShell gebruiken met Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="acb70-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="acb70-142">Stap 1</span><span class="sxs-lookup"><span data-stu-id="acb70-142">Step 1</span></span>

<span data-ttu-id="acb70-143">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="acb70-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="acb70-144">U wordt gevraagd om u te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="acb70-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="acb70-145">Stap 2</span><span class="sxs-lookup"><span data-stu-id="acb70-145">Step 2</span></span>

<span data-ttu-id="acb70-146">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="acb70-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="acb70-147">Stap 3</span><span class="sxs-lookup"><span data-stu-id="acb70-147">Step 3</span></span>

<span data-ttu-id="acb70-148">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="acb70-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="acb70-149">Stap 4</span><span class="sxs-lookup"><span data-stu-id="acb70-149">Step 4</span></span>

<span data-ttu-id="acb70-150">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="acb70-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="acb70-151">U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="acb70-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="acb70-152">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="acb70-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="acb70-153">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="acb70-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="acb70-154">Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="acb70-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="acb70-155">In het bovenstaande voorbeeld is er een resourcegroep aangeroepen hebt gemaakt **appgw-RG** met een locatie van **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="acb70-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="acb70-156">Als u voor uw toepassingsgateway een aangepaste test moet configureren, raadpleegt u [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md) (Met PowerShell een toepassingsgateway maken met aangepaste tests).</span><span class="sxs-lookup"><span data-stu-id="acb70-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="acb70-157">Ga naar [aangepaste tests en statuscontrole](application-gateway-probe-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="acb70-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="acb70-158">Een virtueel netwerk en subnetten maken</span><span class="sxs-lookup"><span data-stu-id="acb70-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="acb70-159">In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acb70-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="acb70-160">Twee subnetten worden gemaakt in deze stap.</span><span class="sxs-lookup"><span data-stu-id="acb70-160">Two subnets are created in this step.</span></span> <span data-ttu-id="acb70-161">Het eerste subnet is voor de toepassingsgateway zelf.</span><span class="sxs-lookup"><span data-stu-id="acb70-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="acb70-162">Toepassingsgateway vereist een eigen subnet voor het opslaan van de exemplaren.</span><span class="sxs-lookup"><span data-stu-id="acb70-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="acb70-163">Alleen andere toepassingsgateways kunnen worden geïmplementeerd in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="acb70-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="acb70-164">Het tweede subnet wordt gebruikt om de toepassing back-endservers.</span><span class="sxs-lookup"><span data-stu-id="acb70-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="acb70-165">Stap 1</span><span class="sxs-lookup"><span data-stu-id="acb70-165">Step 1</span></span>

<span data-ttu-id="acb70-166">Het adresbereik 10.0.0.0/24 toewijzen aan de variabele subnet moet worden gebruikt voor het opslaan van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="acb70-167">Stap 2</span><span class="sxs-lookup"><span data-stu-id="acb70-167">Step 2</span></span>

<span data-ttu-id="acb70-168">Het adresbereik 10.0.1.0/24 toewijzen aan de variabele subnet2 moet worden gebruikt voor de back-end-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="acb70-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="acb70-169">Stap 3</span><span class="sxs-lookup"><span data-stu-id="acb70-169">Step 3</span></span>

<span data-ttu-id="acb70-170">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West is met het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24 en 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="acb70-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="acb70-171">Stap 4</span><span class="sxs-lookup"><span data-stu-id="acb70-171">Step 4</span></span>

<span data-ttu-id="acb70-172">Wijs een subnetvariabele toe voor de volgende stappen, die een application gateway maakt.</span><span class="sxs-lookup"><span data-stu-id="acb70-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="acb70-173">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="acb70-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="acb70-174">Maak de openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS - west.</span><span class="sxs-lookup"><span data-stu-id="acb70-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="acb70-175">Er wordt een IP-adres toegewezen aan de toepassingsgateway wanneer de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="acb70-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="acb70-176">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="acb70-176">Create application gateway configuration</span></span>

<span data-ttu-id="acb70-177">U moet alle configuratie-items instellen voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="acb70-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="acb70-178">Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="acb70-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="acb70-179">Stap 1</span><span class="sxs-lookup"><span data-stu-id="acb70-179">Step 1</span></span>

<span data-ttu-id="acb70-180">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="acb70-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="acb70-181">Wanneer de toepassingsgateway wordt geopend, neemt over een IP-adres van het geconfigureerde subnet en netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="acb70-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="acb70-182">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="acb70-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="acb70-183">Stap 2</span><span class="sxs-lookup"><span data-stu-id="acb70-183">Step 2</span></span>

<span data-ttu-id="acb70-184">Configureer de backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50** voor **pool1** en **134.170.186.46**, **134.170.189.221**, **134.170.186.50** voor **pool2**.</span><span class="sxs-lookup"><span data-stu-id="acb70-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="acb70-185">In dit voorbeeld zijn er twee groepen van de back-end voor het doorsturen van netwerkverkeer op basis van de gevraagde website.</span><span class="sxs-lookup"><span data-stu-id="acb70-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="acb70-186">Één groep verkeer ontvangt van de site 'contoso.com' en andere toepassingen verkeer van site 'fabrikam.com' ontvangt.</span><span class="sxs-lookup"><span data-stu-id="acb70-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="acb70-187">U moet de voorgaande IP-adressen voor het toevoegen van uw eigen toepassing IP-adreseindpunten vervangen.</span><span class="sxs-lookup"><span data-stu-id="acb70-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="acb70-188">In plaats van interne IP-adressen kan u openbare IP-adressen, FQDN-naam of NIC van een virtuele machine ook gebruiken voor back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="acb70-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="acb70-189">FQDN-namen in plaats van IP-adressen opgeven in het gebruik van PowerShell '-BackendFQDNs ' parameter.</span><span class="sxs-lookup"><span data-stu-id="acb70-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="acb70-190">Stap 3</span><span class="sxs-lookup"><span data-stu-id="acb70-190">Step 3</span></span>

<span data-ttu-id="acb70-191">Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor het netwerkverkeer van taakverdeling in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="acb70-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="acb70-192">In dit voorbeeld configureert u de instellingen van de andere back-end-adresgroep voor de back-end-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="acb70-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="acb70-193">Elke back-endpool kan een eigen instelling van de back-endpool hebben.</span><span class="sxs-lookup"><span data-stu-id="acb70-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="acb70-194">Stap 4</span><span class="sxs-lookup"><span data-stu-id="acb70-194">Step 4</span></span>

<span data-ttu-id="acb70-195">Configureer het front-end-IP-adres met openbaar IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="acb70-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="acb70-196">Stap 5</span><span class="sxs-lookup"><span data-stu-id="acb70-196">Step 5</span></span>

<span data-ttu-id="acb70-197">Configureer de front-endpoort voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="acb70-198">Stap 6</span><span class="sxs-lookup"><span data-stu-id="acb70-198">Step 6</span></span>

<span data-ttu-id="acb70-199">Configureer twee SSL-certificaten voor de twee websites gaan we in dit voorbeeld wilt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="acb70-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="acb70-200">Er is één certificaat voor contoso.com verkeer en de andere is voor fabrikam.com verkeer.</span><span class="sxs-lookup"><span data-stu-id="acb70-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="acb70-201">Deze certificaten moeten een certificeringsinstantie uitgegeven certificaten voor uw websites.</span><span class="sxs-lookup"><span data-stu-id="acb70-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="acb70-202">Zelfondertekende certificaten worden ondersteund, maar niet aanbevolen voor productie-verkeer.</span><span class="sxs-lookup"><span data-stu-id="acb70-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="acb70-203">Stap 7</span><span class="sxs-lookup"><span data-stu-id="acb70-203">Step 7</span></span>

<span data-ttu-id="acb70-204">Configureer twee listeners voor de twee websites in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="acb70-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="acb70-205">Deze stap configureert u de listeners voor openbare IP-adres, poort en host die wordt gebruikt voor het ontvangen van binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="acb70-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="acb70-206">HostName-parameter is vereist voor ondersteuning voor meerdere site en moet worden ingesteld op de juiste website waarvan het verkeer wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="acb70-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="acb70-207">RequireServerNameIndication-parameter moet worden ingesteld op true voor websites die ondersteuning voor SSL in een scenario voor meerdere host nodig.</span><span class="sxs-lookup"><span data-stu-id="acb70-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="acb70-208">Als SSL-ondersteuning vereist is, moet u ook het SSL-certificaat dat wordt gebruikt voor de beveiliging van verkeer voor deze webtoepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="acb70-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="acb70-209">De combinatie van FrontendIPConfiguration, FrontendPort en host-naam moet uniek zijn voor een listener.</span><span class="sxs-lookup"><span data-stu-id="acb70-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="acb70-210">Elke listener kan één certificaat ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="acb70-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="acb70-211">Stap 8</span><span class="sxs-lookup"><span data-stu-id="acb70-211">Step 8</span></span>

<span data-ttu-id="acb70-212">Maak twee instelling van regel voor de twee webtoepassingen in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="acb70-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="acb70-213">Een regel verbindt samen listeners, back-endpools en HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="acb70-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="acb70-214">Deze stap configureert u de toepassingsgateway voor het gebruik van Basic routeringsregel, één voor elke website.</span><span class="sxs-lookup"><span data-stu-id="acb70-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="acb70-215">Verkeer naar elke website wordt ontvangen door de geconfigureerde listener en wordt vervolgens omgeleid naar de geconfigureerde back-endpool met behulp van de eigenschappen die zijn opgegeven in de BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="acb70-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="acb70-216">Stap 9</span><span class="sxs-lookup"><span data-stu-id="acb70-216">Step 9</span></span>

<span data-ttu-id="acb70-217">Configureer het aantal exemplaren en de grootte voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="acb70-218">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="acb70-218">Create application gateway</span></span>

<span data-ttu-id="acb70-219">Een toepassingsgateway maken met alle configuratie-objecten uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="acb70-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="acb70-220">Inrichting van Application Gateway is een langdurige bewerking en kan even duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="acb70-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="acb70-221">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="acb70-221">Get application gateway DNS name</span></span>

<span data-ttu-id="acb70-222">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="acb70-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="acb70-223">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="acb70-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="acb70-224">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="acb70-225">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="acb70-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="acb70-226">Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="acb70-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="acb70-227">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="acb70-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="acb70-228">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="acb70-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="acb70-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="acb70-229">Next steps</span></span>

<span data-ttu-id="acb70-230">Informatie over het beveiligen van uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="acb70-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

