---
title: aaaConfigure SSL-offload - Azure Application Gateway - PowerShell | Microsoft Docs
description: Deze pagina vindt u instructies toocreate een toepassingsgateway met SSL-offload met Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="a4bd7-103">Een toepassingsgateway configureren voor SSL-offload met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4bd7-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4bd7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a4bd7-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="a4bd7-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4bd7-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="a4bd7-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4bd7-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="a4bd7-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a4bd7-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="a4bd7-108">Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="a4bd7-109">SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a4bd7-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a4bd7-110">Before you begin</span></span>

1. <span data-ttu-id="a4bd7-111">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="a4bd7-112">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a4bd7-113">U maakt een virtueel netwerk en een subnet voor de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="a4bd7-114">Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="a4bd7-115">De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="a4bd7-116">Hallo-servers configureren van toouse Hallo toepassingsgateway moeten bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="a4bd7-117">Wat is vereist toocreate een application gateway?</span><span class="sxs-lookup"><span data-stu-id="a4bd7-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="a4bd7-118">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="a4bd7-119">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a4bd7-120">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a4bd7-121">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="a4bd7-122">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="a4bd7-123">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="a4bd7-124">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze instellingen zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a4bd7-125">**Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="a4bd7-126">Op dit moment alleen Hallo *basic* regel wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="a4bd7-127">Hallo *basic* regel is round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="a4bd7-128">**Aanvullende configuratieopmerkingen**</span><span class="sxs-lookup"><span data-stu-id="a4bd7-128">**Additional configuration notes**</span></span>

<span data-ttu-id="a4bd7-129">Hallo-protocol in voor de configuratie van SSL-certificaten, **HttpListener** moet ook wijzigen*Https* (hoofdlettergevoelig).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="a4bd7-130">Hallo **SslCertificate** element te toegevoegd**HttpListener** met Hallo variabele waarde die is geconfigureerd voor SSL-certificaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="a4bd7-131">Hallo front-endpoort moet bijgewerkte too443.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="a4bd7-132">**tooenable cookies gebaseerde affiniteit**: een application gateway kan worden geconfigureerd tooensure is een aanvraag van een clientsessie altijd gerichte toohello dezelfde virtuele machine in de webfarm Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="a4bd7-133">Dit scenario wordt gedaan door het injecteren van een sessiecookie waarmee Hallo gateway toodirect verkeer op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="a4bd7-134">tooenable cookies gebaseerde affiniteit ingesteld **CookieBasedAffinity** te*ingeschakeld* in Hallo **BackendHttpSettings** element.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="a4bd7-135">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-135">Create an application gateway</span></span>

<span data-ttu-id="a4bd7-136">Hallo verschil tussen het gebruik van de klassieke Azure-implementatiemodel Hallo en Azure Resource Manager is Hallo volgorde die u maakt een application gateway en Hallo de items die u moet toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="a4bd7-137">Met Resource Manager worden alle onderdelen van een toepassingsgateway worden afzonderlijk geconfigureerd en vervolgens samen toocreate een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="a4bd7-138">Hier volgen Hallo stappen die nodig zijn toocreate een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="a4bd7-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="a4bd7-139">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4bd7-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="a4bd7-140">Virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="a4bd7-141">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="a4bd7-142">Een toepassingsgatewayresource maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="a4bd7-143">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4bd7-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="a4bd7-144">Zorg ervoor dat u overschakelt naar PowerShell modus toouse hello Azure Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="a4bd7-145">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a4bd7-146">Stap 1</span><span class="sxs-lookup"><span data-stu-id="a4bd7-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="a4bd7-147">Stap 2</span><span class="sxs-lookup"><span data-stu-id="a4bd7-147">Step 2</span></span>

<span data-ttu-id="a4bd7-148">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a4bd7-149">Vraag tooauthenticate bent u met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="a4bd7-150">Stap 3</span><span class="sxs-lookup"><span data-stu-id="a4bd7-150">Step 3</span></span>

<span data-ttu-id="a4bd7-151">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="a4bd7-152">Stap 4</span><span class="sxs-lookup"><span data-stu-id="a4bd7-152">Step 4</span></span>

<span data-ttu-id="a4bd7-153">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="a4bd7-154">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a4bd7-155">Deze instelling wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="a4bd7-156">Zorg ervoor dat alle opdrachten toocreate maakt gebruik van een toepassingsgateway Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="a4bd7-157">In Hallo bovenstaande voorbeeld is er een resourcegroep aangeroepen gemaakt **appgw-RG** en locatie **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="a4bd7-158">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="a4bd7-159">Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="a4bd7-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="a4bd7-160">Stap 1</span><span class="sxs-lookup"><span data-stu-id="a4bd7-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="a4bd7-161">Dit voorbeeld wordt een virtueel netwerk toegewezen Hallo adres adresbereik 10.0.0.0/24 tooa subnet variabele toobe gebruikt toocreate.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="a4bd7-162">Stap 2</span><span class="sxs-lookup"><span data-stu-id="a4bd7-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="a4bd7-163">In dit voorbeeld wordt een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="a4bd7-164">Stap 3</span><span class="sxs-lookup"><span data-stu-id="a4bd7-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="a4bd7-165">Dit voorbeeld wordt Hallo subnet object toovariable $subnet voor de volgende stappen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="a4bd7-166">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="a4bd7-167">In dit voorbeeld wordt een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="a4bd7-168">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="a4bd7-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="a4bd7-169">Stap 1</span><span class="sxs-lookup"><span data-stu-id="a4bd7-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="a4bd7-170">In dit voorbeeld wordt een toepassingsgateway een IP-configuratie met de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="a4bd7-171">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="a4bd7-172">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="a4bd7-173">Stap 2</span><span class="sxs-lookup"><span data-stu-id="a4bd7-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="a4bd7-174">Dit voorbeeld configureert Hallo backend-IP-adresgroep met de naam **pool01** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="a4bd7-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="a4bd7-175">Deze waarden zijn Hallo IP-adressen die ontvangen netwerkverkeer op Hallo van Hallo front-end-IP-eindpunt binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="a4bd7-176">Hallo IP-adressen uit het voorgaande voorbeeld met Hallo IP-adressen van uw web-eindpunten toepassing hello vervangen.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="a4bd7-177">Stap 3</span><span class="sxs-lookup"><span data-stu-id="a4bd7-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="a4bd7-178">Dit voorbeeld configureert u de instelling voor application gateway **poolsetting01** tooload netwerkverkeer in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="a4bd7-179">Stap 4</span><span class="sxs-lookup"><span data-stu-id="a4bd7-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="a4bd7-180">Dit voorbeeld configureert u Hallo front-end-IP-poort met de naam **frontendport01** voor Hallo openbare IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="a4bd7-181">Stap 5</span><span class="sxs-lookup"><span data-stu-id="a4bd7-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="a4bd7-182">Dit voorbeeld configureert Hallo gebruikte certificaat voor SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="a4bd7-183">Hallo-certificaat moet toobe in PFX-indeling en Hallo wachtwoord moet tussen 4 too12 tekens.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="a4bd7-184">Stap 6</span><span class="sxs-lookup"><span data-stu-id="a4bd7-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="a4bd7-185">In dit voorbeeld wordt Hallo front-end-IP-configuratie met de naam **fipconfig01** en gekoppeld Hallo openbaar IP-adres met Hallo front-end-IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="a4bd7-186">Stap 7</span><span class="sxs-lookup"><span data-stu-id="a4bd7-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="a4bd7-187">In dit voorbeeld wordt de naam van de beschikbaarheidsgroeplistener hello **listener01** en gekoppeld Hallo front-endpoort toohello front-end-IP-configuratie en het certificaat.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="a4bd7-188">Stap 8</span><span class="sxs-lookup"><span data-stu-id="a4bd7-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="a4bd7-189">In dit voorbeeld wordt Hallo load balancer-routeringsregel met de naam **rule01** die het gedrag van Hallo load balancer configureert.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="a4bd7-190">Stap 9</span><span class="sxs-lookup"><span data-stu-id="a4bd7-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="a4bd7-191">Dit voorbeeld configureert Hallo exemplaargrootte van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="a4bd7-192">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a4bd7-193">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a4bd7-194">U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="a4bd7-195">Stap 10</span><span class="sxs-lookup"><span data-stu-id="a4bd7-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="a4bd7-196">Deze stap definieert Hallo SSL beleid toouse op Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="a4bd7-197">Ga naar [SSL configureren voor versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="a4bd7-198">Een toepassingsgateway maken met behulp van New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="a4bd7-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="a4bd7-199">Dit voorbeeld maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="a4bd7-200">In voorbeeld Hallo Hallo toepassingsgateway heet **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a4bd7-201">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="a4bd7-201">Get application gateway DNS name</span></span>

<span data-ttu-id="a4bd7-202">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="a4bd7-203">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a4bd7-204">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="a4bd7-205">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a4bd7-206">toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="a4bd7-207">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="a4bd7-208">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a4bd7-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="a4bd7-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4bd7-209">Next steps</span></span>

<span data-ttu-id="a4bd7-210">Als u wilt tooconfigure een toouse application gateway met een interne load balancer (ILB), Zie [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a4bd7-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a4bd7-211">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="a4bd7-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a4bd7-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a4bd7-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a4bd7-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a4bd7-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

