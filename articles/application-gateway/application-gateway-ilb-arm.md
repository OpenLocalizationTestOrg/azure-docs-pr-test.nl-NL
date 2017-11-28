---
title: Azure Application Gateway met interne Load Balancer - PowerShell aaaUsing | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, configureren, starten en verwijderen van een toepassingsgateway met interne load balancer (ILB) voor Azure Resource Manager
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
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="c27dd-103">Een toepassingsgateway met een interne load balancer (ILB) maken met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c27dd-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c27dd-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="c27dd-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="c27dd-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="c27dd-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="c27dd-106">Azure Application Gateway kan worden geconfigureerd met een internetgerichte VIP of met een intern eindpunt dat geen zichtbare toohello Internet, ook wel bekend als een interne load balancer (ILB)-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c27dd-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="c27dd-107">Hallo-gateway configureren met een ILB is nuttig voor interne line-of-business-toepassingen die niet blootgestelde toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="c27dd-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="c27dd-108">Het is ook handig voor services en lagen gebruikt in een toepassing met meerdere lagen die zich bevinden in een beveiligingsgrens die geen zichtbare toohello Internet maar er wel round robin laden distributie, sessiepersistentie of beëindiging van Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="c27dd-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="c27dd-109">Dit artikel begeleidt u bij Hallo stappen tooconfigure een toepassingsgateway met een ILB.</span><span class="sxs-lookup"><span data-stu-id="c27dd-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c27dd-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c27dd-110">Before you begin</span></span>

1. <span data-ttu-id="c27dd-111">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c27dd-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="c27dd-112">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c27dd-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c27dd-113">U maakt een virtueel netwerk en een subnet voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c27dd-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="c27dd-114">Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn.</span><span class="sxs-lookup"><span data-stu-id="c27dd-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="c27dd-115">De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.</span><span class="sxs-lookup"><span data-stu-id="c27dd-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="c27dd-116">Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="c27dd-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="c27dd-117">Wat is vereist toocreate een application gateway?</span><span class="sxs-lookup"><span data-stu-id="c27dd-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="c27dd-118">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="c27dd-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="c27dd-119">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerk, maar in een ander subnet voor de toepassingsgateway hello of een openbare IP-/ VIP moet zijn.</span><span class="sxs-lookup"><span data-stu-id="c27dd-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="c27dd-120">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="c27dd-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c27dd-121">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="c27dd-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="c27dd-122">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c27dd-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="c27dd-123">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="c27dd-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="c27dd-124">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="c27dd-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="c27dd-125">**Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="c27dd-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="c27dd-126">Op dit moment alleen Hallo *basic* regel wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c27dd-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="c27dd-127">Hallo *basic* regel is round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="c27dd-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="c27dd-128">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-128">Create an application gateway</span></span>

<span data-ttu-id="c27dd-129">Hallo verschil tussen het gebruik van Azure Classic en Azure Resource Manager is Hallo volgorde waarin u de toepassingsgateway Hallo en Hallo-items die u toobe geconfigureerd moet maken.</span><span class="sxs-lookup"><span data-stu-id="c27dd-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="c27dd-130">Met Resource Manager worden alle items waaruit een toepassingsgateway afzonderlijk geconfigureerd en deze vervolgens samen toocreate hello toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="c27dd-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="c27dd-131">Hier volgen Hallo stappen nodig toocreate een toepassingsgateway zijn:</span><span class="sxs-lookup"><span data-stu-id="c27dd-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="c27dd-132">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c27dd-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="c27dd-133">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="c27dd-134">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="c27dd-135">Een toepassingsgatewayresource maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="c27dd-136">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c27dd-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="c27dd-137">Zorg ervoor dat u overschakelt naar PowerShell modus toouse hello Azure Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c27dd-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="c27dd-138">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c27dd-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="c27dd-139">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c27dd-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="c27dd-140">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c27dd-140">Step 2</span></span>

<span data-ttu-id="c27dd-141">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="c27dd-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="c27dd-142">Vraag tooauthenticate bent u met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="c27dd-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="c27dd-143">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c27dd-143">Step 3</span></span>

<span data-ttu-id="c27dd-144">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="c27dd-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="c27dd-145">Stap 4</span><span class="sxs-lookup"><span data-stu-id="c27dd-145">Step 4</span></span>

<span data-ttu-id="c27dd-146">Maak een nieuwe resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="c27dd-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="c27dd-147">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c27dd-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="c27dd-148">Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c27dd-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="c27dd-149">Zorg ervoor dat alle opdrachten toocreate maakt gebruik van een toepassingsgateway Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c27dd-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="c27dd-150">In Hallo voorgaande voorbeeld, wij een resourcegroep 'Appgw-rg' en de locatie 'VS-West' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c27dd-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="c27dd-151">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="c27dd-152">Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c27dd-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="c27dd-153">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c27dd-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="c27dd-154">Deze stap wijst Hallo adres adresbereik 10.0.0.0/24 tooa subnet variabele toobe gebruikt toocreate een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c27dd-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="c27dd-155">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c27dd-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="c27dd-156">Deze stap maakt een virtueel netwerk met de naam 'appgwvnet' in de resourcegroep 'appgw-rg' voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="c27dd-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="c27dd-157">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c27dd-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="c27dd-158">Deze stap wijst Hallo subnet object toovariable $subnet voor de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27dd-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="c27dd-159">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="c27dd-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="c27dd-160">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c27dd-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="c27dd-161">Deze stap maakt toepassingsgateway een IP-configuratie met de naam 'gatewayIP01'.</span><span class="sxs-lookup"><span data-stu-id="c27dd-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="c27dd-162">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="c27dd-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="c27dd-163">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c27dd-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="c27dd-164">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c27dd-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="c27dd-165">Deze stap configureert u Hallo backend-IP-adresgroep met de naam 'pool01' met IP-adressen '10.1.1.8, 10.1.1.9, 10.1.1.10'.</span><span class="sxs-lookup"><span data-stu-id="c27dd-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="c27dd-166">Hallo IP-adressen die Hallo netwerkverkeer ontvangen dat afkomstig van de front-end-IP-eindpunt Hallo is zijn.</span><span class="sxs-lookup"><span data-stu-id="c27dd-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="c27dd-167">U vervangen Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adreseindpunten.</span><span class="sxs-lookup"><span data-stu-id="c27dd-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="c27dd-168">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c27dd-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="c27dd-169">Deze stap configureert application gateway-instelling 'poolsetting01' voor Hallo load balanced netwerkverkeer op Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="c27dd-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="c27dd-170">Stap 4</span><span class="sxs-lookup"><span data-stu-id="c27dd-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="c27dd-171">Deze stap configureert u Hallo front-end-IP-poort is met de naam 'frontendport01' hello ILB.</span><span class="sxs-lookup"><span data-stu-id="c27dd-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="c27dd-172">Stap 5</span><span class="sxs-lookup"><span data-stu-id="c27dd-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="c27dd-173">Deze stap Hallo front-end-IP-configuratie met de naam 'fipconfig01' maakt en koppelt u deze aan een particuliere IP-adres van de huidige virtuele netwerksubnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27dd-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="c27dd-174">Stap 6</span><span class="sxs-lookup"><span data-stu-id="c27dd-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="c27dd-175">Deze stap Hallo listener met de naam 'listener01' maakt en koppelt u Hallo front-endpoort toohello front-end-IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c27dd-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="c27dd-176">Stap 7</span><span class="sxs-lookup"><span data-stu-id="c27dd-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="c27dd-177">Deze stap maakt Hallo load balancer-routeringsregel genaamd 'rule01' hello load balancer-gedrag te configureren.</span><span class="sxs-lookup"><span data-stu-id="c27dd-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="c27dd-178">Stap 8</span><span class="sxs-lookup"><span data-stu-id="c27dd-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="c27dd-179">Deze stap configureert u Hallo exemplaargrootte van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27dd-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="c27dd-180">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="c27dd-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c27dd-181">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="c27dd-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c27dd-182">U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="c27dd-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="c27dd-183">Een toepassingsgateway maken met behulp van New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="c27dd-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="c27dd-184">Hiermee maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27dd-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="c27dd-185">In dit voorbeeld wordt de toepassingsgateway Hallo 'appgwtest' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c27dd-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="c27dd-186">Deze stap maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27dd-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="c27dd-187">In voorbeeld Hallo Hallo toepassingsgateway 'appgwtest' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c27dd-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="c27dd-188">Een toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="c27dd-188">Delete an application gateway</span></span>

<span data-ttu-id="c27dd-189">een toepassingsgateway toodelete, moet u toodo Hallo stappen te volgen in de volgorde:</span><span class="sxs-lookup"><span data-stu-id="c27dd-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="c27dd-190">Gebruik Hallo `Stop-AzureRmApplicationGateway` cmdlet toostop Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="c27dd-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="c27dd-191">Gebruik Hallo `Remove-AzureRmApplicationGateway` cmdlet tooremove Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="c27dd-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="c27dd-192">Controleer of deze Hallo-gateway is verwijderd met behulp van Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c27dd-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="c27dd-193">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c27dd-193">Step 1</span></span>

<span data-ttu-id="c27dd-194">Hallo application gateway-object ophalen en koppelt u deze variabele tooa '$getgw'.</span><span class="sxs-lookup"><span data-stu-id="c27dd-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="c27dd-195">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c27dd-195">Step 2</span></span>

<span data-ttu-id="c27dd-196">Gebruik `Stop-AzureRmApplicationGateway` toostop Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c27dd-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="c27dd-197">Dit voorbeeld wordt Hallo `Stop-AzureRmApplicationGateway` cmdlet uit op de eerste regel hello, gevolgd door Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c27dd-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="c27dd-198">Nadat de toepassingsgateway Hallo gestopt is, gebruikt u Hallo `Remove-AzureRmApplicationGateway` cmdlet tooremove Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c27dd-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

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
> <span data-ttu-id="c27dd-199">Hallo **-force** switch kan worden gebruikt toosuppress Hallo bevestigingsbericht voor verwijdering.</span><span class="sxs-lookup"><span data-stu-id="c27dd-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="c27dd-200">tooverify die Hallo service is verwijderd, kunt u Hallo `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c27dd-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="c27dd-201">Deze stap is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="c27dd-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="c27dd-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c27dd-202">Next steps</span></span>

<span data-ttu-id="c27dd-203">Als u tooconfigure SSL-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="c27dd-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="c27dd-204">Als u wilt dat tooconfigure een toouse application gateway met een ILB, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="c27dd-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="c27dd-205">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="c27dd-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="c27dd-206">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c27dd-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="c27dd-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c27dd-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

