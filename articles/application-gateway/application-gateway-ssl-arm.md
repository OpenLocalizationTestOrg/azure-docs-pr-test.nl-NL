---
title: Configureren van SSL-offload - Azure Application Gateway - PowerShell | Microsoft Docs
description: Op deze pagina vindt u instructies voor het maken van een toepassingsgateway met SSL-offload met behulp van Azure Resource Manager
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
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="73b0b-103">Een toepassingsgateway configureren voor SSL-offload met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73b0b-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="73b0b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="73b0b-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="73b0b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="73b0b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="73b0b-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="73b0b-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="73b0b-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="73b0b-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="73b0b-108">Azure Application Gateway kan zodanig worden geconfigureerd dat de Secure Sockets Layer-sessie (SSL) wordt beëindigd bij de gateway om kostbare SSL-ontsleutelingstaken te voorkomen die worden uitgevoerd in de webfarm.</span><span class="sxs-lookup"><span data-stu-id="73b0b-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="73b0b-109">Met SSL-offload worden ook het instellen van de front-endserver en het beheer van de webtoepassing eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="73b0b-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="73b0b-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="73b0b-110">Before you begin</span></span>

1. <span data-ttu-id="73b0b-111">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="73b0b-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="73b0b-112">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="73b0b-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="73b0b-113">Maak een virtueel netwerk en een subnet voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="73b0b-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="73b0b-114">Zorg ervoor dat er geen virtuele machines en cloudimplementaties zijn die gebruikmaken van het subnet.</span><span class="sxs-lookup"><span data-stu-id="73b0b-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="73b0b-115">De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.</span><span class="sxs-lookup"><span data-stu-id="73b0b-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="73b0b-116">De servers die u voor gebruik van de toepassingsgateway configureert, moeten al bestaan in het virtuele netwerk of hier hun eindpunten hebben. Een andere optie is om er een openbaar IP- of VIP-adres aan toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="73b0b-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="73b0b-117">Wat is er vereist om een toepassingsgateway te maken?</span><span class="sxs-lookup"><span data-stu-id="73b0b-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="73b0b-118">**Back-endserverpool:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="73b0b-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="73b0b-119">De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="73b0b-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="73b0b-120">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="73b0b-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="73b0b-121">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="73b0b-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="73b0b-122">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="73b0b-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="73b0b-123">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="73b0b-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="73b0b-124">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze instellingen zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="73b0b-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="73b0b-125">**Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="73b0b-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="73b0b-126">Momenteel wordt alleen de regel *basic* ondersteund.</span><span class="sxs-lookup"><span data-stu-id="73b0b-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="73b0b-127">De regel *basic* is een vorm van round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="73b0b-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="73b0b-128">**Aanvullende configuratieopmerkingen**</span><span class="sxs-lookup"><span data-stu-id="73b0b-128">**Additional configuration notes**</span></span>

<span data-ttu-id="73b0b-129">Voor het configureren van SSL-certificaten moet het protocol in **HttpListener** worden gewijzigd in *Https* (hoofdlettergevoelig).</span><span class="sxs-lookup"><span data-stu-id="73b0b-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="73b0b-130">Het element **SslCertificate** wordt toegevoegd aan **HttpListener**, waarbij de waarde van de variabele moet worden geconfigureerd voor het SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="73b0b-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="73b0b-131">De front-endpoort moet worden bijgewerkt naar 443.</span><span class="sxs-lookup"><span data-stu-id="73b0b-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="73b0b-132">**Op cookies gebaseerde affiniteit inschakelen**: u kunt een toepassingsgateway zodanig configureren dat u zeker weet dat aanvragen vanuit clientsessies altijd worden omgeleid naar dezelfde virtuele machine in de webfarm.</span><span class="sxs-lookup"><span data-stu-id="73b0b-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="73b0b-133">Dit wordt gedaan door het injecteren van een sessiecookie waarmee de gateway het verkeer correct kan omleiden.</span><span class="sxs-lookup"><span data-stu-id="73b0b-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="73b0b-134">Als u op cookies gebaseerde affiniteit wilt inschakelen, stelt u **CookieBasedAffinity** in op *Enabled* in het element **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="73b0b-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="73b0b-135">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="73b0b-135">Create an application gateway</span></span>

<span data-ttu-id="73b0b-136">Het verschil tussen het gebruik van het klassieke Azure-implementatiemodel en Azure Resource Manager zit hem in de volgorde waarin u een toepassingsgateway maakt en in de items die u moet configureren.</span><span class="sxs-lookup"><span data-stu-id="73b0b-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="73b0b-137">Met Resource Manager worden alle componenten van een toepassingsgateway afzonderlijk geconfigureerd en vervolgens samengesteld om een toepassingsgatewayresource te maken.</span><span class="sxs-lookup"><span data-stu-id="73b0b-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="73b0b-138">Dit zijn de stappen voor het maken van een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="73b0b-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="73b0b-139">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73b0b-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="73b0b-140">Een virtueel netwerk, subnet en openbaar IP-adres maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="73b0b-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="73b0b-141">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="73b0b-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="73b0b-142">Een toepassingsgatewayresource maken</span><span class="sxs-lookup"><span data-stu-id="73b0b-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="73b0b-143">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73b0b-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="73b0b-144">Zorg ervoor dat u overschakelt naar de PowerShell-modus om de Azure Resource Manager-cmdlets te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="73b0b-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="73b0b-145">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="73b0b-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="73b0b-146">Stap 1</span><span class="sxs-lookup"><span data-stu-id="73b0b-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="73b0b-147">Stap 2</span><span class="sxs-lookup"><span data-stu-id="73b0b-147">Step 2</span></span>

<span data-ttu-id="73b0b-148">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="73b0b-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="73b0b-149">U wordt gevraagd om u te verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="73b0b-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="73b0b-150">Stap 3</span><span class="sxs-lookup"><span data-stu-id="73b0b-150">Step 3</span></span>

<span data-ttu-id="73b0b-151">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="73b0b-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="73b0b-152">Stap 4</span><span class="sxs-lookup"><span data-stu-id="73b0b-152">Step 4</span></span>

<span data-ttu-id="73b0b-153">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="73b0b-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="73b0b-154">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="73b0b-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="73b0b-155">Deze instelling wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="73b0b-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="73b0b-156">Zorg ervoor dat bij alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="73b0b-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="73b0b-157">In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam **appgw-RG** en de locatie **VS - west**.</span><span class="sxs-lookup"><span data-stu-id="73b0b-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="73b0b-158">Een virtueel netwerk en een subnet maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="73b0b-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="73b0b-159">In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="73b0b-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="73b0b-160">Stap 1</span><span class="sxs-lookup"><span data-stu-id="73b0b-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="73b0b-161">Hiermee wijst u het adresbereik 10.0.0.0/24 toe aan de subnetvariabele die u gaat gebruiken om een virtueel netwerk te maken.</span><span class="sxs-lookup"><span data-stu-id="73b0b-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="73b0b-162">Stap 2</span><span class="sxs-lookup"><span data-stu-id="73b0b-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="73b0b-163">In dit voorbeeld wordt een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West is met het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="73b0b-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="73b0b-164">Stap 3</span><span class="sxs-lookup"><span data-stu-id="73b0b-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="73b0b-165">Hiermee wijst u het subnetobject toe aan de variabele $subnet voor gebruik in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="73b0b-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="73b0b-166">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="73b0b-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="73b0b-167">In dit voorbeeld wordt een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West.</span><span class="sxs-lookup"><span data-stu-id="73b0b-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="73b0b-168">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="73b0b-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="73b0b-169">Stap 1</span><span class="sxs-lookup"><span data-stu-id="73b0b-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="73b0b-170">In dit voorbeeld wordt een toepassingsgateway een IP-configuratie met de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="73b0b-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="73b0b-171">Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool.</span><span class="sxs-lookup"><span data-stu-id="73b0b-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="73b0b-172">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="73b0b-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="73b0b-173">Stap 2</span><span class="sxs-lookup"><span data-stu-id="73b0b-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="73b0b-174">Dit voorbeeld configureert de backend-IP-adresgroep met de naam **pool01** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="73b0b-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="73b0b-175">Deze waarden zijn de IP-adressen waardoor het netwerkverkeer van het front-end-IP-eindpunt binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="73b0b-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="73b0b-176">Vervang de IP-adressen uit het voorbeeld hierboven door de IP-adressen van de eindpunten van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="73b0b-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="73b0b-177">Stap 3</span><span class="sxs-lookup"><span data-stu-id="73b0b-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="73b0b-178">Dit voorbeeld configureert u de instelling voor application gateway **poolsetting01** voor taakverdeling van netwerkverkeer in de groep back-end.</span><span class="sxs-lookup"><span data-stu-id="73b0b-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="73b0b-179">Stap 4</span><span class="sxs-lookup"><span data-stu-id="73b0b-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="73b0b-180">Dit voorbeeld configureert u de front-end-IP-poort met de naam **frontendport01** voor het openbare IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="73b0b-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="73b0b-181">Stap 5</span><span class="sxs-lookup"><span data-stu-id="73b0b-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="73b0b-182">Hiermee configureert u het certificaat dat wordt gebruikt voor de SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="73b0b-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="73b0b-183">Het certificaat moet de indeling .pfx hebben en het wachtwoord moet uit 4-12 tekens bestaan.</span><span class="sxs-lookup"><span data-stu-id="73b0b-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="73b0b-184">Stap 6</span><span class="sxs-lookup"><span data-stu-id="73b0b-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="73b0b-185">In dit voorbeeld wordt de front-end-IP-configuratie met de naam **fipconfig01** en koppelt u het openbare IP-adres aan de front-end-IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="73b0b-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="73b0b-186">Stap 7</span><span class="sxs-lookup"><span data-stu-id="73b0b-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="73b0b-187">In dit voorbeeld wordt de naam van de listener **listener01** en koppelt u de front-endpoort aan de front-end-IP-configuratie en het certificaat.</span><span class="sxs-lookup"><span data-stu-id="73b0b-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="73b0b-188">Stap 8</span><span class="sxs-lookup"><span data-stu-id="73b0b-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="73b0b-189">In dit voorbeeld wordt de load balancer-routeringsregel met de naam **rule01** die het gedrag van de load balancer configureert.</span><span class="sxs-lookup"><span data-stu-id="73b0b-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="73b0b-190">Stap 9</span><span class="sxs-lookup"><span data-stu-id="73b0b-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="73b0b-191">Hiermee configureert u de exemplaargrootte van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="73b0b-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="73b0b-192">De standaardwaarde voor *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="73b0b-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="73b0b-193">De standaardwaarde voor *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="73b0b-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="73b0b-194">U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="73b0b-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="73b0b-195">Stap 10</span><span class="sxs-lookup"><span data-stu-id="73b0b-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="73b0b-196">Deze stap definieert de SSL-beleid gebruiken in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="73b0b-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="73b0b-197">Ga naar [SSL configureren voor versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="73b0b-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="73b0b-198">Een toepassingsgateway maken met behulp van New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="73b0b-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="73b0b-199">In dit voorbeeld wordt een toepassingsgateway gemaakt met alle configuratie-items uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="73b0b-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="73b0b-200">In het voorbeeld wordt de toepassingsgateway wordt aangeroepen **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="73b0b-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="73b0b-201">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="73b0b-201">Get application gateway DNS name</span></span>

<span data-ttu-id="73b0b-202">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="73b0b-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="73b0b-203">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="73b0b-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="73b0b-204">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="73b0b-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="73b0b-205">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73b0b-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="73b0b-206">Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="73b0b-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="73b0b-207">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="73b0b-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="73b0b-208">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="73b0b-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="73b0b-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73b0b-209">Next steps</span></span>

<span data-ttu-id="73b0b-210">Als u een toepassingsgateway wilt configureren voor gebruik met een interne load balancer, raadpleegt u [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Een toepassingsgateway met een interne load balancer (ILB) maken).</span><span class="sxs-lookup"><span data-stu-id="73b0b-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="73b0b-211">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="73b0b-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="73b0b-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="73b0b-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="73b0b-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="73b0b-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

