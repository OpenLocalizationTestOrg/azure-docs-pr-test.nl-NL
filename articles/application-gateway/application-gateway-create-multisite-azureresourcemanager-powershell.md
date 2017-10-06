---
title: een toepassingsgateway voor het hosten van meerdere sites aaaCreate | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, het configureren van een toepassingsgateway voor het hosten van meerdere webtoepassingen op Hallo dezelfde gateway.
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="438b1-103">Een toepassingsgateway voor het hosten van meerdere webtoepassingen maken</span><span class="sxs-lookup"><span data-stu-id="438b1-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="438b1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="438b1-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="438b1-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="438b1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="438b1-106">Meerdere hosting-site kunt u toodeploy meer dan één webtoepassing op Hallo dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="438b1-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="438b1-107">Is afhankelijk van de aanwezigheid van de host-header in Hallo inkomende HTTP-aanvraag, toodetermine welke listener verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="438b1-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="438b1-108">Hallo-listener stuurt vervolgens verkeer tooappropriate back-endpool zoals geconfigureerd in de definitie van de gateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="438b1-109">In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van Hallo indicatie voor Server-naam (SNI) extensie toochoose Hallo juist listener voor internetverkeer Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="438b1-110">Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over tooload voor verschillende web domeinen toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="438b1-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="438b1-111">Op dezelfde manier Hallo meerdere subdomeinen Hallo dezelfde hoofddomein kan ook worden gehost op dezelfde toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="438b1-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="438b1-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="438b1-112">Scenario</span></span>

<span data-ttu-id="438b1-113">In de Hallo voorbeeld te volgen, toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep.</span><span class="sxs-lookup"><span data-stu-id="438b1-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="438b1-114">Vergelijkbare installatie wordt mogelijk gebruikt toohost subdomeinen zoals app.contoso.com en blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="438b1-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="438b1-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="438b1-116">Before you begin</span></span>

1. <span data-ttu-id="438b1-117">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="438b1-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="438b1-118">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="438b1-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="438b1-119">Hallo-servers toegevoegd toohello back-end-pool toouse Hallo application gateway moet al bestaan of hebt gemaakt hun eindpunten in Hallo virtueel netwerk in een apart subnet of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="438b1-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="438b1-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="438b1-120">Requirements</span></span>

* <span data-ttu-id="438b1-121">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="438b1-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="438b1-122">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="438b1-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="438b1-123">FQDN-naam kan ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="438b1-123">FQDN can also be used.</span></span>
* <span data-ttu-id="438b1-124">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="438b1-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="438b1-125">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="438b1-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="438b1-126">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="438b1-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="438b1-127">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="438b1-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="438b1-128">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="438b1-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="438b1-129">Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="438b1-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="438b1-130">**Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool, en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="438b1-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="438b1-131">Regels worden verwerkt op Hallo volgorde die ze worden weergegeven en verkeer wordt omgeleid via Hallo eerste regel die overeenkomt met ongeacht specifieke karakter.</span><span class="sxs-lookup"><span data-stu-id="438b1-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="438b1-132">Bijvoorbeeld, als u een regel met een basic-listener en een regel met meerdere sites listener beide op dezelfde poort, regel met Hallo Hallo hebt moet Hallo multi-site-listener worden weergegeven voordat Hallo regel met Hallo basic listener om Hallo multi-site regel toofunction als Er werd verwacht.</span><span class="sxs-lookup"><span data-stu-id="438b1-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="438b1-133">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="438b1-133">Create an application gateway</span></span>

<span data-ttu-id="438b1-134">Hallo hieronder vindt u Hallo stappen nodig toocreate een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="438b1-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="438b1-135">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="438b1-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="438b1-136">Maak een virtueel netwerk, subnetten en openbare IP-adres voor de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="438b1-137">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="438b1-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="438b1-138">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="438b1-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="438b1-139">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="438b1-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="438b1-140">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="438b1-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="438b1-141">Meer informatie vindt u op [Windows PowerShell gebruiken met Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="438b1-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="438b1-142">Stap 1</span><span class="sxs-lookup"><span data-stu-id="438b1-142">Step 1</span></span>

<span data-ttu-id="438b1-143">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="438b1-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="438b1-144">Vraag tooauthenticate bent u met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="438b1-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="438b1-145">Stap 2</span><span class="sxs-lookup"><span data-stu-id="438b1-145">Step 2</span></span>

<span data-ttu-id="438b1-146">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="438b1-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="438b1-147">Stap 3</span><span class="sxs-lookup"><span data-stu-id="438b1-147">Step 3</span></span>

<span data-ttu-id="438b1-148">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="438b1-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="438b1-149">Stap 4</span><span class="sxs-lookup"><span data-stu-id="438b1-149">Step 4</span></span>

<span data-ttu-id="438b1-150">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="438b1-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="438b1-151">U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="438b1-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="438b1-152">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="438b1-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="438b1-153">Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="438b1-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="438b1-154">Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="438b1-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="438b1-155">In Hallo bovenstaande voorbeeld is er een resourcegroep aangeroepen gemaakt **appgw-RG** met een locatie van **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="438b1-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="438b1-156">Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="438b1-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="438b1-157">Ga naar [aangepaste tests en statuscontrole](application-gateway-probe-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="438b1-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="438b1-158">Een virtueel netwerk en subnetten maken</span><span class="sxs-lookup"><span data-stu-id="438b1-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="438b1-159">Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="438b1-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="438b1-160">Twee subnetten worden gemaakt in deze stap.</span><span class="sxs-lookup"><span data-stu-id="438b1-160">Two subnets are created in this step.</span></span> <span data-ttu-id="438b1-161">het eerste subnet Hallo is voor de toepassingsgateway Hallo zelf.</span><span class="sxs-lookup"><span data-stu-id="438b1-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="438b1-162">Toepassingsgateway vereist een eigen subnet toohold de exemplaren.</span><span class="sxs-lookup"><span data-stu-id="438b1-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="438b1-163">Alleen andere toepassingsgateways kunnen worden geïmplementeerd in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="438b1-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="438b1-164">het tweede subnet Hallo is gebruikte toohold Hallo toepassing back-endservers.</span><span class="sxs-lookup"><span data-stu-id="438b1-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="438b1-165">Stap 1</span><span class="sxs-lookup"><span data-stu-id="438b1-165">Step 1</span></span>

<span data-ttu-id="438b1-166">Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikte toohold Hallo toepassingsgateway toewijzen.</span><span class="sxs-lookup"><span data-stu-id="438b1-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="438b1-167">Stap 2</span><span class="sxs-lookup"><span data-stu-id="438b1-167">Step 2</span></span>

<span data-ttu-id="438b1-168">Hallo adresbereik 10.0.1.0/24 toohello subnet2 variabele toobe gebruikt voor back-endpools Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="438b1-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="438b1-169">Stap 3</span><span class="sxs-lookup"><span data-stu-id="438b1-169">Step 3</span></span>

<span data-ttu-id="438b1-170">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24 met en 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="438b1-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="438b1-171">Stap 4</span><span class="sxs-lookup"><span data-stu-id="438b1-171">Step 4</span></span>

<span data-ttu-id="438b1-172">Wijs een subnetvariabele toe voor de volgende stappen hello, waarmee u een toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="438b1-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="438b1-173">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="438b1-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="438b1-174">Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="438b1-175">Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="438b1-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="438b1-176">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="438b1-176">Create application gateway configuration</span></span>

<span data-ttu-id="438b1-177">U hebt tooset van alle configuratie-items voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="438b1-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="438b1-178">Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="438b1-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="438b1-179">Stap 1</span><span class="sxs-lookup"><span data-stu-id="438b1-179">Step 1</span></span>

<span data-ttu-id="438b1-180">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="438b1-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="438b1-181">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="438b1-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="438b1-182">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="438b1-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="438b1-183">Stap 2</span><span class="sxs-lookup"><span data-stu-id="438b1-183">Step 2</span></span>

<span data-ttu-id="438b1-184">Configureer Hallo backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50** voor **pool1** en **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  voor **pool2**.</span><span class="sxs-lookup"><span data-stu-id="438b1-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="438b1-185">In dit voorbeeld zijn er twee back-end-adresgroepen tooroute-netwerkverkeer op basis van de gevraagde website Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="438b1-186">Één groep verkeer ontvangt van de site 'contoso.com' en andere toepassingen verkeer van site 'fabrikam.com' ontvangt.</span><span class="sxs-lookup"><span data-stu-id="438b1-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="438b1-187">U hebt tooreplace Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adres-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="438b1-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="438b1-188">In plaats van interne IP-adressen kan u openbare IP-adressen, FQDN-naam of NIC van een virtuele machine ook gebruiken voor back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="438b1-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="438b1-189">toospecify FQDN-namen in plaats van IP-adressen in het gebruik van PowerShell '-BackendFQDNs ' parameter.</span><span class="sxs-lookup"><span data-stu-id="438b1-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="438b1-190">Stap 3</span><span class="sxs-lookup"><span data-stu-id="438b1-190">Step 3</span></span>

<span data-ttu-id="438b1-191">Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="438b1-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="438b1-192">In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor Hallo back-end-adresgroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="438b1-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="438b1-193">Elke back-endpool kan een eigen instelling van de back-endpool hebben.</span><span class="sxs-lookup"><span data-stu-id="438b1-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="438b1-194">Stap 4</span><span class="sxs-lookup"><span data-stu-id="438b1-194">Step 4</span></span>

<span data-ttu-id="438b1-195">Hallo front-end-IP-met openbare IP-eindpunt configureren.</span><span class="sxs-lookup"><span data-stu-id="438b1-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="438b1-196">Stap 5</span><span class="sxs-lookup"><span data-stu-id="438b1-196">Step 5</span></span>

<span data-ttu-id="438b1-197">Hallo front-endpoort voor een toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="438b1-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="438b1-198">Stap 6</span><span class="sxs-lookup"><span data-stu-id="438b1-198">Step 6</span></span>

<span data-ttu-id="438b1-199">Configureer twee SSL-certificaten voor Hallo twee websites gaan we toosupport in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="438b1-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="438b1-200">Er is één certificaat voor contoso.com verkeer en Hallo andere voor fabrikam.com verkeer.</span><span class="sxs-lookup"><span data-stu-id="438b1-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="438b1-201">Deze certificaten moeten een certificeringsinstantie uitgegeven certificaten voor uw websites.</span><span class="sxs-lookup"><span data-stu-id="438b1-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="438b1-202">Zelfondertekende certificaten worden ondersteund, maar niet aanbevolen voor productie-verkeer.</span><span class="sxs-lookup"><span data-stu-id="438b1-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="438b1-203">Stap 7</span><span class="sxs-lookup"><span data-stu-id="438b1-203">Step 7</span></span>

<span data-ttu-id="438b1-204">Configureer twee listeners voor twee websites Hallo in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="438b1-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="438b1-205">Deze stap configureert Hallo listeners voor openbare IP-adres, poort en host tooreceive binnenkomend verkeer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="438b1-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="438b1-206">HostName-parameter is vereist voor ondersteuning voor meerdere site en moet toohello juiste website instellen voor welke Hallo verkeer wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="438b1-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="438b1-207">RequireServerNameIndication-parameter moet worden ingesteld als tootrue voor websites die ondersteuning voor SSL in een scenario voor meerdere host nodig.</span><span class="sxs-lookup"><span data-stu-id="438b1-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="438b1-208">Als u ondersteuning voor SSL is vereist, moet u ook toospecify Hallo SSL certificaat namelijk gebruikte toosecure verkeer voor deze webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="438b1-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="438b1-209">Hallo combinatie van FrontendIPConfiguration FrontendPort en HostName moet unieke tooa listener.</span><span class="sxs-lookup"><span data-stu-id="438b1-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="438b1-210">Elke listener kan één certificaat ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="438b1-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="438b1-211">Stap 8</span><span class="sxs-lookup"><span data-stu-id="438b1-211">Step 8</span></span>

<span data-ttu-id="438b1-212">Maak twee regel instellen voor Hallo twee webtoepassingen in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="438b1-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="438b1-213">Een regel verbindt samen listeners, back-endpools en HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="438b1-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="438b1-214">Deze stap configureert u Hallo application gateway toouse Basic routeringsregel, één voor elke website.</span><span class="sxs-lookup"><span data-stu-id="438b1-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="438b1-215">Verkeer tooeach website wordt ontvangen door de geconfigureerde listener en wordt vervolgens omgeleid tooits back-endpool met behulp van Hallo-eigenschappen die zijn opgegeven in Hallo BackendHttpSettings geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="438b1-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="438b1-216">Stap 9</span><span class="sxs-lookup"><span data-stu-id="438b1-216">Step 9</span></span>

<span data-ttu-id="438b1-217">Hallo aantal exemplaren en de grootte voor de toepassingsgateway Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="438b1-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="438b1-218">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="438b1-218">Create application gateway</span></span>

<span data-ttu-id="438b1-219">Een toepassingsgateway met alle configuratie-objecten uit de vorige stappen Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="438b1-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="438b1-220">Inrichting van Application Gateway is een langdurige bewerking en sommige toocomplete tijd kan duren.</span><span class="sxs-lookup"><span data-stu-id="438b1-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="438b1-221">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="438b1-221">Get application gateway DNS name</span></span>

<span data-ttu-id="438b1-222">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="438b1-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="438b1-223">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="438b1-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="438b1-224">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="438b1-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="438b1-225">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="438b1-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="438b1-226">toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="438b1-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="438b1-227">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="438b1-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="438b1-228">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="438b1-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="438b1-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="438b1-229">Next steps</span></span>

<span data-ttu-id="438b1-230">Meer informatie over hoe tooprotect uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="438b1-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

