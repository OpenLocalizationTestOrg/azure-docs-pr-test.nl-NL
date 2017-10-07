---
title: aaaHow toouse Azure API Management in virtueel netwerk met Application Gateway | Microsoft Docs
description: Meer informatie over hoe toosetup en Azure API Management in een intern virtueel netwerk met Application Gateway (WAF) als FrontEnd configureren
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="c1cf0-103">API Management in een interne VNET integreren met Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1cf0-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="c1cf0-104"><a name="overview"></a> Overzicht</span><span class="sxs-lookup"><span data-stu-id="c1cf0-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="c1cf0-105">Hallo API Management-service kan worden geconfigureerd in een virtueel netwerk in de interne modus waardoor alleen toegankelijk vanuit Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="c1cf0-106">Azure Application Gateway is een PAAS-Service die voorziet in een load balancer van laag 7.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="c1cf0-107">Het fungeert als een reverse proxy-service en biedt tussen het aanbieden van een Web Application Firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="c1cf0-108">Combineren van API Management ingericht in een interne VNET met Hallo Application Gateway frontend kunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="c1cf0-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="c1cf0-109">Gebruik dezelfde Hallo API Management-resource voor verbruik door consumenten interne en externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="c1cf0-110">Gebruik één API Management-resource en hebt u een subset van API's die zijn gedefinieerd in API Management beschikbaar voor externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="c1cf0-111">Bieden een directe manier tooswitch toegang tooAPI Management van Hallo openbare Internet in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="c1cf0-112"><a name="scenario"></a> Scenario</span><span class="sxs-lookup"><span data-stu-id="c1cf0-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="c1cf0-113">In dit artikel wordt uitgelegd hoe toouse één API-Management-service voor zowel interne als externe consumenten en fungeren als een enkel frontend voor zowel on-premises en in de cloud-API's.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="c1cf0-114">U ziet ook hoe tooexpose slechts een subset van uw API's (per Hallo zoals ze zijn gemarkeerd in het groen) voor extern verbruik met Hallo PathBasedRouting functionaliteit beschikbaar zijn in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="c1cf0-115">Uw API's worden in de eerste installatie voorbeeld Hallo beheerd alleen vanuit binnen het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="c1cf0-116">Interne consumenten (gemarkeerd in oranje) hebben toegang tot alle uw interne en externe API's.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="c1cf0-117">Verkeer wordt nooit wordt gedeeld tooInternet die wordt geleverd met een hoge prestaties via Express Route-circuits.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![URL-route](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="c1cf0-119"><a name="before-you-begin"></a> Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c1cf0-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="c1cf0-120">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="c1cf0-121">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c1cf0-122">Maak een virtueel netwerk en maak afzonderlijke subnetten voor API Management en Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="c1cf0-123">Als u van plan een aangepaste DNS-server voor het virtuele netwerk Hallo toocreate bent, doen voordat u Hallo implementatie start.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="c1cf0-124">Controleer die het werkt door te zorgen voor een virtuele machine gemaakt in een nieuw subnet in Hallo virtueel netwerk kunt omzetten en toegang tot alle Azure-service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="c1cf0-125">Wat is vereist toocreate een integratie tussen API Management en Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="c1cf0-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="c1cf0-126">**Back-endserverpool:** dit Hallo interne virtuele IP-adres van Hallo API Management-service is.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="c1cf0-127">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c1cf0-128">Deze instellingen zijn toegepast tooall servers binnen Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="c1cf0-129">**Front-endpoort:** dit Hallo openbare poort die in Hallo toepassingsgateway wordt geopend is.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="c1cf0-130">Roept het verkeer opgehaald omgeleide tooone Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="c1cf0-131">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="c1cf0-132">**Regel:** Hallo regel een listener tooa back-endserverpool wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="c1cf0-133">**Aangepaste Health test:** Application Gateway maakt standaard gebruik van IP-adres op basis van tests toofigure uit welke servers in Hallo BackendAddressPool actief zijn.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="c1cf0-134">Hallo API Management-service reageert alleen toorequests waarvoor de juiste host-header hello, daarom Hallo standaard tests is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="c1cf0-135">Een aangepaste health test moet toobe gedefinieerd toohelp toepassingsgateway bepalen dat Hallo-service actief is en moet deze aanvragen worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="c1cf0-136">**Aangepaste Domeincertificaat:** tooaccess API Management van Hallo internet, moet u een CNAME-toewijzing van de hostnaam toohello Application Gateway front-DNS-naam toocreate.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="c1cf0-137">Dit zorgt ervoor dat Hallo hostname-header en het certificaat dat is verzonden tooApplication Gateway die wordt doorgestuurd tooAPI Management is een die APIM als geldige herkennen kan.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="c1cf0-138"><a name="overview-steps"></a> Stappen die nodig zijn voor het integreren van API Management en Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1cf0-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="c1cf0-139">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="c1cf0-140">Maak een virtueel netwerk, subnet en openbaar IP-adres voor Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="c1cf0-141">Maak een ander subnet voor API Management.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="c1cf0-142">Maak een API Management-service binnen Hallo VNET subnet die eerder is gemaakt en zorg ervoor dat u interne Hallo-modus.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="c1cf0-143">Het instellen van de aangepaste domeinnaam Hallo in Hallo API Management-service.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="c1cf0-144">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="c1cf0-145">Een Application Gateway-resource maken.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="c1cf0-146">Maak een CNAME van Hallo openbare DNS-naam van Hallo Application Gateway toohello API Management proxy hostnaam.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="c1cf0-147">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1cf0-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="c1cf0-148">Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="c1cf0-149">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="c1cf0-150">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c1cf0-150">Step 1</span></span>

<span data-ttu-id="c1cf0-151">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="c1cf0-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c1cf0-152">Verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="c1cf0-153">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c1cf0-153">Step 2</span></span>

<span data-ttu-id="c1cf0-154">Controleer de abonnementen Hallo voor Hallo-account en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="c1cf0-155">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c1cf0-155">Step 3</span></span>

<span data-ttu-id="c1cf0-156">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="c1cf0-157">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="c1cf0-158">Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="c1cf0-159">Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="c1cf0-160">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="c1cf0-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="c1cf0-161">Hallo volgende voorbeeld ziet u hoe een virtueel netwerk met toocreate Hallo resourcemanager.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="c1cf0-162">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c1cf0-162">Step 1</span></span>

<span data-ttu-id="c1cf0-163">Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikt voor toepassingsgateway tijdens het maken van een virtueel netwerk toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="c1cf0-164">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c1cf0-164">Step 2</span></span>

<span data-ttu-id="c1cf0-165">Hallo adresbereik 10.0.1.0/24 toohello subnet variabele toobe gebruikt voor API Management tijdens het maken van een virtueel netwerk toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="c1cf0-166">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c1cf0-166">Step 3</span></span>

<span data-ttu-id="c1cf0-167">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **apim-appGw-RG** voor de regio VS-West Hallo Hallo voorvoegsel 10.0.0.0/16 met met subnetten 10.0.0.0/24 en 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="c1cf0-168">Stap 4</span><span class="sxs-lookup"><span data-stu-id="c1cf0-168">Step 4</span></span>

<span data-ttu-id="c1cf0-169">Wijs een subnetvariabele toe voor de volgende stappen Hallo</span><span class="sxs-lookup"><span data-stu-id="c1cf0-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="c1cf0-170">Maak een API Management-service binnen een VNET dat is geconfigureerd in de interne modus</span><span class="sxs-lookup"><span data-stu-id="c1cf0-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="c1cf0-171">Hallo volgende voorbeeld ziet u hoe toocreate een API Management-service in een VNET geconfigureerd voor interne toegang alleen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="c1cf0-172">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c1cf0-172">Step 1</span></span>
<span data-ttu-id="c1cf0-173">Maakt een virtueel netwerk van API Management-object met behulp van Hallo subnet $apimsubnetdata die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="c1cf0-174">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c1cf0-174">Step 2</span></span>
<span data-ttu-id="c1cf0-175">Maak een API Management-service binnen Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="c1cf0-176">Raadpleeg nadat Hallo hierboven opdracht is geslaagd te[DNS-configuratie vereist tooaccess interne VNET API Management-service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess deze.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="c1cf0-177">Installatie van een aangepaste domeinnaam in API Management</span><span class="sxs-lookup"><span data-stu-id="c1cf0-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="c1cf0-178">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c1cf0-178">Step 1</span></span>
<span data-ttu-id="c1cf0-179">Upload het Hallo-certificaat met persoonlijke sleutel voor Hallo domein.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="c1cf0-180">In dit voorbeeld worden `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="c1cf0-181">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c1cf0-181">Step 2</span></span>
<span data-ttu-id="c1cf0-182">Zodra het Hallo-certificaat is geüpload, een configuratieobject voor de hostnaam voor Hallo proxy maken met een hostnaam van `api.contoso.net`, zoals Hallo voorbeeld certificaat autoriteit voor Hallo biedt `*.contoso.net` domein.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="c1cf0-183">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="c1cf0-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="c1cf0-184">Maak een openbare IP-resource **publicIP01** in de resourcegroep **apim-appGw-RG** voor de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="c1cf0-185">Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="c1cf0-186">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="c1cf0-186">Create application gateway configuration</span></span>

<span data-ttu-id="c1cf0-187">Alle configuratie-items moeten worden ingesteld voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="c1cf0-188">Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="c1cf0-189">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c1cf0-189">Step 1</span></span>

<span data-ttu-id="c1cf0-190">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="c1cf0-191">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="c1cf0-192">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="c1cf0-193">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c1cf0-193">Step 2</span></span>

<span data-ttu-id="c1cf0-194">Hallo front-end-IP-poort voor het openbare IP-eindpunt Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="c1cf0-195">Dit is Hallo-poort waarmee gebruikers verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="c1cf0-196">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c1cf0-196">Step 3</span></span>

<span data-ttu-id="c1cf0-197">Hallo front-end-IP-met openbare IP-eindpunt configureren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="c1cf0-198">Stap 4</span><span class="sxs-lookup"><span data-stu-id="c1cf0-198">Step 4</span></span>

<span data-ttu-id="c1cf0-199">Hallo-certificaat configureren voor hello Application Gateway gebruikt toodecrypt en Hallo-verkeer te doorlopen opnieuw versleutelen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="c1cf0-200">Stap 5</span><span class="sxs-lookup"><span data-stu-id="c1cf0-200">Step 5</span></span>

<span data-ttu-id="c1cf0-201">Hallo HTTP-listener voor Hallo toepassingsgateway maken.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="c1cf0-202">Hallo front-end-IP-configuratie, poort en ssl-certificaat tooit toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="c1cf0-203">Stap 6</span><span class="sxs-lookup"><span data-stu-id="c1cf0-203">Step 6</span></span>

<span data-ttu-id="c1cf0-204">Maken van een aangepaste test toohello API Management-service `ContosoApi` proxy domein eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="c1cf0-205">Hallo pad `/status-0123456789abcdef` is een standaardeindpunt health gehost op alle Hallo API Management-services.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="c1cf0-206">Stel `api.contoso.net` als een aangepaste test hostnaam toosecure met SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="c1cf0-207">hostname Hallo `contosoapi.azure-api.net` is Hallo standaard proxy hostnaam geconfigureerd als een service met de naam `contosoapi` in openbare Azure is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="c1cf0-208">Stap 7</span><span class="sxs-lookup"><span data-stu-id="c1cf0-208">Step 7</span></span>

<span data-ttu-id="c1cf0-209">Upload het Hallo-certificaat toobe gebruikt op Hallo resources in de back-end SSL zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="c1cf0-210">Dit is Hallo hetzelfde certificaat dat u hebt opgegeven in stap 4 hierboven.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="c1cf0-211">Stap 8</span><span class="sxs-lookup"><span data-stu-id="c1cf0-211">Step 8</span></span>

<span data-ttu-id="c1cf0-212">HTTP-back-end-instellingen voor Application Gateway Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="c1cf0-213">Dit omvat het instellen van een time-out optreedt voor de back-end-aanvraag waarna ze worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="c1cf0-214">Deze waarde verschilt van Hallo test time.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="c1cf0-215">Stap 9</span><span class="sxs-lookup"><span data-stu-id="c1cf0-215">Step 9</span></span>

<span data-ttu-id="c1cf0-216">Configureer een backend-IP-adresgroep met de naam **apimbackend** met Hallo interne virtuele IP-adres van Hallo API Management-service die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="c1cf0-217">Stap 10</span><span class="sxs-lookup"><span data-stu-id="c1cf0-217">Step 10</span></span>

<span data-ttu-id="c1cf0-218">Instellingen maken voor een dummy (niet-bestaand) back-end.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="c1cf0-219">Aanvragen tooAPI paden die we niet wilt tooexpose van API Management via Application Gateway wordt bereikt deze back-end en 404 retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="c1cf0-220">HTTP-instellingen configureren voor Hallo dummy back-end.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="c1cf0-221">Configureer een dummy back-end **dummyBackendPool**, die tooa FQDN-adres wijst **dummybackend.com**. Dit adres FQDN bestaat niet in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="c1cf0-222">Maak een regel instellen die Hallo Application Gateway gebruikt standaard die toohello niet-bestaande back-end wijst **dummybackend.com** in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="c1cf0-223">Stap 11</span><span class="sxs-lookup"><span data-stu-id="c1cf0-223">Step 11</span></span>

<span data-ttu-id="c1cf0-224">URL-regel paden voor back-end-adresgroepen Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="c1cf0-225">Hierdoor kunnen alleen enkele Hallo-API's van API Management voor wordt blootgesteld toohello openbaar.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="c1cf0-226">Bijvoorbeeld, als er `Echo API` (/ echo /), `Calculator API` (/calc/) enz. Controleer alleen `Echo API` toegankelijk is vanaf Internet).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="c1cf0-227">Hallo wordt volgende voorbeeld een eenvoudige regel voor Hallo '/ echo /' pad routering verkeer toohello back-end 'apimProxyBackendPool'.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="c1cf0-228">Als Hallo pad komt niet overeen met de Hallo pad regels willen we tooenable van API Management, Hallo regel pad kaart configuratie configureert ook een standaard-back-end-adresgroep met de naam **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="c1cf0-229">Bijvoorbeeld: http://api.contoso.net/calc/ * gaat te**dummyBackendPool** zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="c1cf0-230">Hallo hierboven stap zorgt ervoor dat alleen aanvragen voor Hallo pad '/ echo' via Hallo Application Gateway zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="c1cf0-231">Aanvragen tooother API's die zijn geconfigureerd in API Management genereert 404-fouten van Application Gateway wanneer deze vanuit Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="c1cf0-232">Stap 12</span><span class="sxs-lookup"><span data-stu-id="c1cf0-232">Step 12</span></span>

<span data-ttu-id="c1cf0-233">Maak een instelling voor Hallo Application Gateway toouse URL-pad gebaseerde routering.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="c1cf0-234">Stap 13</span><span class="sxs-lookup"><span data-stu-id="c1cf0-234">Step 13</span></span>

<span data-ttu-id="c1cf0-235">Hallo aantal exemplaren en de grootte voor Hallo Application Gateway configureren.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="c1cf0-236">We gebruiken hier Hallo [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) voor een betere beveiliging Hallo API Management-resource.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="c1cf0-237">Stap 14</span><span class="sxs-lookup"><span data-stu-id="c1cf0-237">Step 14</span></span>

<span data-ttu-id="c1cf0-238">WAF toobe configureren in de modus 'Preventie'.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="c1cf0-239">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="c1cf0-239">Create Application Gateway</span></span>

<span data-ttu-id="c1cf0-240">Een toepassingsgateway met alle Hallo configuratie-objecten uit de vorige stappen Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="c1cf0-241">CNAME Hallo API Management proxy hostnaam toohello openbare DNS-naam van Hallo Application Gateway resource</span><span class="sxs-lookup"><span data-stu-id="c1cf0-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="c1cf0-242">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="c1cf0-243">Wanneer u een openbaar IP-adres, vereist Application Gateway een dynamisch toegewezen DNS-naam die gemakkelijk toouse niet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="c1cf0-244">Hallo toepassingsgateway van DNS-naam moet gebruikte toocreate een CNAME-record die Hallo APIM proxyhostnaam wijst (bijvoorbeeld `api.contoso.net` in bovenstaande Hallo voorbeelden) toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="c1cf0-245">Hallo-details van Hallo Application Gateway en de bijbehorende IP-en DNS-naam met behulp van Hallo PublicIPAddress element tooconfigure Hallo frontend IP CNAME-record, worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="c1cf0-246">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP kan worden gewijzigd bij opnieuw opstarten van de gateway.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="c1cf0-247"><a name="summary"></a> Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c1cf0-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="c1cf0-248">Azure API Management geconfigureerd in een VNET biedt een interface één gateway voor alle geconfigureerde API's, ongeacht of deze gehoste on-premises of in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="c1cf0-249">Integratie van Application Gateway met API Management flexibel Hallo van bepaalde API's toobe toegankelijk is op Internet Hallo selectief inschakelen, evenals bieden een Web Application Firewall als een frontend tooyour API Management-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="c1cf0-250"><a name="next-steps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1cf0-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="c1cf0-251">Meer informatie over Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1cf0-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="c1cf0-252">Overzicht van Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1cf0-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="c1cf0-253">Application Gateway Web Application Firewall</span><span class="sxs-lookup"><span data-stu-id="c1cf0-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="c1cf0-254">Application Gateway met behulp van Routing op basis van het pad</span><span class="sxs-lookup"><span data-stu-id="c1cf0-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="c1cf0-255">Meer informatie over API Management en VNETs</span><span class="sxs-lookup"><span data-stu-id="c1cf0-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="c1cf0-256">Met behulp van API Management is alleen beschikbaar in Hallo VNET</span><span class="sxs-lookup"><span data-stu-id="c1cf0-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="c1cf0-257">Met behulp van API Management in VNET</span><span class="sxs-lookup"><span data-stu-id="c1cf0-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
