---
title: een toepassingsgateway met URL-routering regels aaaCreate | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, een Azure-toepassingsgateway met behulp van regels voor URL-routering configureren
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="bcf2b-103">Een toepassingsgateway met pad gebaseerde routering maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcf2b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bcf2b-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="bcf2b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcf2b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="bcf2b-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bcf2b-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="bcf2b-107">URL-pad gebaseerde routering, kunt u tooassociate routes op basis van Hallo URL-pad van een Http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="bcf2b-108">Het controleren of er een route tooa back-end-adresgroep geconfigureerd voor Hallo-URL die zijn gepresenteerd in Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="bcf2b-109">Vervolgens stuurt Hallo netwerkverkeer toohello gedefinieerd back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="bcf2b-110">Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="bcf2b-111">URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="bcf2b-112">Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="bcf2b-113">Basic regeltype biedt round robin-service voor Hallo back-end opslaggroepen tijdens PathBasedRouting bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="bcf2b-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="bcf2b-114">Scenario</span></span>

<span data-ttu-id="bcf2b-115">In de Hallo voorbeeld te volgen, Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: video servergroep en image-servergroep.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="bcf2b-116">Aanvragen voor http://contoso.com/image * worden gerouteerd servergroep tooimage (pool1) en http://contoso.com/video * worden gerouteerd servergroep toovideo (pool2).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="bcf2b-117">Als geen van Hallo pad patronen overeenkomen, kan een standaardgroep server (pool1) is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![URL-route](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="bcf2b-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bcf2b-119">Before you begin</span></span>

1. <span data-ttu-id="bcf2b-120">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="bcf2b-121">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="bcf2b-122">Maakt u een virtueel netwerk en subnet voor Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="bcf2b-123">Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="bcf2b-124">Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="bcf2b-125">Hallo-servers toegevoegd toohello back-end-pool toouse Hallo application gateway moet al bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="bcf2b-126">Wat is vereist toocreate een application gateway?</span><span class="sxs-lookup"><span data-stu-id="bcf2b-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="bcf2b-127">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="bcf2b-128">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="bcf2b-129">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="bcf2b-130">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="bcf2b-131">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="bcf2b-132">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="bcf2b-133">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="bcf2b-134">**Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="bcf2b-135">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-135">Create an application gateway</span></span>

<span data-ttu-id="bcf2b-136">Hallo verschil tussen het gebruik van Azure Classic en Azure Resource Manager is Hallo volgorde waarin u de toepassingsgateway Hallo en Hallo-items die u toobe geconfigureerd moet maken.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="bcf2b-137">Met Resource Manager worden alle items waaruit een toepassingsgateway worden afzonderlijk geconfigureerd en deze vervolgens samen toocreate hello toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="bcf2b-138">Hier volgen Hallo stappen nodig toocreate een toepassingsgateway zijn:</span><span class="sxs-lookup"><span data-stu-id="bcf2b-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="bcf2b-139">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="bcf2b-140">Maak een virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="bcf2b-141">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="bcf2b-142">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="bcf2b-143">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcf2b-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="bcf2b-144">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="bcf2b-145">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="bcf2b-146">Stap 1</span><span class="sxs-lookup"><span data-stu-id="bcf2b-146">Step 1</span></span>

<span data-ttu-id="bcf2b-147">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="bcf2b-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="bcf2b-148">Vraag tooauthenticate bent u met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="bcf2b-149">Stap 2</span><span class="sxs-lookup"><span data-stu-id="bcf2b-149">Step 2</span></span>

<span data-ttu-id="bcf2b-150">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="bcf2b-151">Stap 3</span><span class="sxs-lookup"><span data-stu-id="bcf2b-151">Step 3</span></span>

<span data-ttu-id="bcf2b-152">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="bcf2b-153">Stap 4</span><span class="sxs-lookup"><span data-stu-id="bcf2b-153">Step 4</span></span>

<span data-ttu-id="bcf2b-154">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="bcf2b-155">U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="bcf2b-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="bcf2b-156">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="bcf2b-157">Deze resourcegroep wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="bcf2b-158">Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="bcf2b-159">Wij gemaakt een resourcegroep met de naam 'appgw-RG' en de locatie 'West ons' hello bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="bcf2b-160">Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="bcf2b-161">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="bcf2b-162">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="bcf2b-163">Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="bcf2b-164">In dit voorbeeld maakt een VNET voor Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="bcf2b-165">Toepassingsgateway vereist een eigen subnet, om deze reden Hallo-subnet voor Application Gateway Hallo gemaakt kleiner dan VNET-adresruimte Hallo is.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="bcf2b-166">Hiermee kunt u andere resources, met inbegrip van maar niet beperkt tooweb servers toobe dat is geconfigureerd in Hallo hetzelfde VNET.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="bcf2b-167">Stap 1</span><span class="sxs-lookup"><span data-stu-id="bcf2b-167">Step 1</span></span>

<span data-ttu-id="bcf2b-168">Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikt toocreate een virtueel netwerk toewijzen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="bcf2b-169">Hiermee maakt u Hallo subnet configuration-object voor Application Gateway die wordt gebruikt in het volgende voorbeeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="bcf2b-170">Stap 2</span><span class="sxs-lookup"><span data-stu-id="bcf2b-170">Step 2</span></span>

<span data-ttu-id="bcf2b-171">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="bcf2b-172">Deze configuratie Hallo Hallo VNET met één subnet voor Hallo Application Gateway tooreside is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="bcf2b-173">Stap 3</span><span class="sxs-lookup"><span data-stu-id="bcf2b-173">Step 3</span></span>

<span data-ttu-id="bcf2b-174">Toewijzen Hallo subnetvariabele toe voor Hallo Vervolgstappen, dit wordt doorgegeven toohello `New-AzureRMApplicationGateway` cmdlet in een toekomstige stap.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="bcf2b-175">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="bcf2b-176">Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="bcf2b-177">Toepassingsgateway kunt een openbaar IP-adres, interne IP-adres of beide aanvragen tooreceive gebruiken voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="bcf2b-178">In dit voorbeeld wordt er alleen een openbaar IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-178">This example only uses a public IP address.</span></span> <span data-ttu-id="bcf2b-179">Hallo voorbeeld te volgen, wordt geen DNS-naam voor het maken van Hallo openbare IP-adres geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="bcf2b-180">Application Gateway biedt geen ondersteuning voor aangepaste DNS-namen voor openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="bcf2b-181">Als u een aangepaste naam is vereist voor Hallo openbaar eindpunt, moet een CNAME-record toopoint toohello automatisch gegenereerd DNS-naam voor het openbare IP-adres Hallo worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="bcf2b-182">Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="bcf2b-183">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-183">Create application gateway configuration</span></span>

<span data-ttu-id="bcf2b-184">Alle configuratie-items moeten worden ingesteld voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="bcf2b-185">Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="bcf2b-186">Stap 1</span><span class="sxs-lookup"><span data-stu-id="bcf2b-186">Step 1</span></span>

<span data-ttu-id="bcf2b-187">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="bcf2b-188">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="bcf2b-189">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="bcf2b-190">Stap 2</span><span class="sxs-lookup"><span data-stu-id="bcf2b-190">Step 2</span></span>

<span data-ttu-id="bcf2b-191">Configureer Hallo backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen voor **pool1** en **pool2**.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="bcf2b-192">Deze IP-adressen zijn IP-adressen Hallo Hallo-resources die als Hallo web application toobe beveiligd door Hallo toepassingsgateway host.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="bcf2b-193">Deze back-end-groepsleden zijn alle gevalideerde toobe orde door de tests, ongeacht of deze eenvoudige tests of aangepaste tests.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="bcf2b-194">Verkeer wordt vervolgens omgeleid toothem wanneer aanvragen Hallo toepassingsgateway binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="bcf2b-195">Back-endpools kunnen worden gebruikt door meerdere regels, binnen de toepassingsgateway hello, wat betekent dat één back endadresgroep kan worden gebruikt voor meerdere webtoepassingen die zich op Hallo dezelfde bevinden host.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="bcf2b-196">In dit voorbeeld zijn er twee back-end-adresgroepen tooroute-netwerkverkeer op basis van Hallo URL-pad.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="bcf2b-197">Een pool ontvangt verkeer vanuit het URL-pad '/video' en andere pool ontvangt verkeer vanuit het pad '/image'.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="bcf2b-198">Vervang Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adres-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="bcf2b-199">Stap 3</span><span class="sxs-lookup"><span data-stu-id="bcf2b-199">Step 3</span></span>

<span data-ttu-id="bcf2b-200">Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="bcf2b-201">In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor Hallo back-end-adresgroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="bcf2b-202">Elke back-endpool kan een eigen instelling van de back-endpool hebben.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="bcf2b-203">Back-end-HTTP-instellingen worden gebruikt door regels tooroute verkeer toohello juiste back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="bcf2b-204">Hiermee bepaalt u het Hallo-protocol en poort die wordt gebruikt bij het verzenden van verkeer toohello back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="bcf2b-205">Op basis van het cookie sessies worden ook bepaald door Hallo back-end-HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="bcf2b-206">Bij inschakeling sessie cookies gebaseerde affiniteit verkeer toohello verzendt dezelfde back-end als de vorige aanvragen voor elk pakket.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="bcf2b-207">Stap 4</span><span class="sxs-lookup"><span data-stu-id="bcf2b-207">Step 4</span></span>

<span data-ttu-id="bcf2b-208">Hallo front-end-IP-met openbare IP-eindpunt configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="bcf2b-209">Hallo front-end-IP-configuratie van object wordt gebruikt door een listener toorelate Hallo passieve internetgerichte IP-adres met Hallo listener.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="bcf2b-210">Stap 5</span><span class="sxs-lookup"><span data-stu-id="bcf2b-210">Step 5</span></span>

<span data-ttu-id="bcf2b-211">Hallo front-endpoort voor een toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="bcf2b-212">Hallo front-endpoort configuration-object wordt gebruikt door een listener toodefine wat Hallo Application Gateway luistert naar verkeer op Hallo listener-poort.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="bcf2b-213">Stap 6</span><span class="sxs-lookup"><span data-stu-id="bcf2b-213">Step 6</span></span>

<span data-ttu-id="bcf2b-214">Hallo-listener configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-214">Configure hello listener.</span></span> <span data-ttu-id="bcf2b-215">Deze stap configureert u Hallo-listener voor Hallo openbaar IP-adres en poort gebruikt tooreceive binnenkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="bcf2b-216">Hallo volgt duurt Hallo eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en Hallo listener configureert.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="bcf2b-217">Hallo-listener luistert in dit voorbeeld tooHTTP verkeer op poort 80 voor het openbare IP-adres hello, dat eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="bcf2b-218">Stap 7</span><span class="sxs-lookup"><span data-stu-id="bcf2b-218">Step 7</span></span>

<span data-ttu-id="bcf2b-219">URL-regel paden voor back-end-adresgroepen Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="bcf2b-220">Deze stap Hallo relatief pad gebruikt door de toepassingsgateway configureert en definieert Hallo toewijzing tussen Hallo URL-pad en Hallo back-end-pool toohandle Hallo binnenkomend verkeer is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf2b-221">Elk pad moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan, Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="bcf2b-222">Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="bcf2b-223">Hallo tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst '? ' of '#' en deze tekens zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="bcf2b-224">Hallo volgende voorbeeld maakt u twee regels: één voor het '/ afbeelding /' pad routering verkeer tooback-end 'pool1' en een andere voor '/ video /' pad routering verkeer tooback-end 'pool2'.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="bcf2b-225">Deze regels ervoor dat verkeer voor elke set van URL's gerouteerde toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="bcf2b-226">Bijvoorbeeld: http://contoso.com/image/figure1.jpg gaat toopool1 en http://contoso.com/video/example.mp4 toopool2 gaat.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="bcf2b-227">Als het pad Hallo komt niet overeen met de vooraf gedefinieerde padregels hello, configureert pad Hallo-kaart regelconfiguratie ook een standaard back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="bcf2b-228">Http://contoso.com/shoppingcart/test.html geldt bijvoorbeeld toopool1 zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="bcf2b-229">Stap 8</span><span class="sxs-lookup"><span data-stu-id="bcf2b-229">Step 8</span></span>

<span data-ttu-id="bcf2b-230">De instelling van een regel maken.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-230">Create a rule setting.</span></span> <span data-ttu-id="bcf2b-231">Deze stap configureert u Hallo application gateway toouse URL-pad gebaseerde routering.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="bcf2b-232">Hallo `$urlPathMap` variabele gedefinieerd in Hallo eerdere stap is nu gebruikte toocreate Hallo pad op basis van een regel.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="bcf2b-233">In deze stap koppelen we Hallo regel met een listener en Hallo url-padtoewijzing eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="bcf2b-234">Stap 9</span><span class="sxs-lookup"><span data-stu-id="bcf2b-234">Step 9</span></span>

<span data-ttu-id="bcf2b-235">Hallo aantal exemplaren en de grootte voor de toepassingsgateway Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="bcf2b-236">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="bcf2b-236">Create Application Gateway</span></span>

<span data-ttu-id="bcf2b-237">Een toepassingsgateway met alle configuratie-objecten uit de vorige stappen Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="bcf2b-238">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="bcf2b-238">Get application gateway DNS name</span></span>

<span data-ttu-id="bcf2b-239">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="bcf2b-240">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="bcf2b-241">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="bcf2b-242">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="bcf2b-243">tooconfigure hello frontend IP CNAME-record, ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="bcf2b-244">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="bcf2b-245">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bcf2b-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bcf2b-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bcf2b-246">Next steps</span></span>

<span data-ttu-id="bcf2b-247">Als u toolearn Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bcf2b-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

