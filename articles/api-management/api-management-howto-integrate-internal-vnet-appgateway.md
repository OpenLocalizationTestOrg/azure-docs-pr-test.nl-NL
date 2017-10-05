---
title: Het gebruik van Azure API Management in virtueel netwerk met Application Gateway | Microsoft Docs
description: Meer informatie over het installeren en configureren van Azure API Management in een intern virtueel netwerk met Application Gateway (WAF) als FrontEnd
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
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="97909-103">API Management in een interne VNET integreren met Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97909-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="97909-104"><a name="overview"></a> Overzicht</span><span class="sxs-lookup"><span data-stu-id="97909-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="97909-105">De API Management-service kan worden geconfigureerd in een virtueel netwerk in de interne modus waardoor alleen toegankelijk vanuit het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="97909-106">Azure Application Gateway is een PAAS-Service die voorziet in een load balancer van laag 7.</span><span class="sxs-lookup"><span data-stu-id="97909-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="97909-107">Het fungeert als een reverse proxy-service en biedt tussen het aanbieden van een Web Application Firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="97909-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="97909-108">Combineren van API Management in een interne VNET met de toepassingsgateway frontend ingericht, kunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="97909-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="97909-109">Gebruik dezelfde API Management-resource voor verbruik door consumenten interne en externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97909-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="97909-110">Gebruik één API Management-resource en hebt u een subset van API's die zijn gedefinieerd in API Management beschikbaar voor externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97909-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="97909-111">Geef een directe manier toegang overschakelen naar de API Management via openbaar Internet, in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="97909-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="97909-112"><a name="scenario"></a> Scenario</span><span class="sxs-lookup"><span data-stu-id="97909-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="97909-113">Dit artikel wordt uitgelegd hoe u één API Management-service voor zowel interne als externe consumenten en maken het fungeren als een enkel frontend voor zowel on-premises en in de cloud-API's.</span><span class="sxs-lookup"><span data-stu-id="97909-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="97909-114">U ziet ook hoe om alleen een subset van uw API's (in het voorbeeld dat ze zijn gemarkeerd in het groen) voor extern verbruik PathBasedRouting functionaliteit die beschikbaar is in Application Gateway met weer te geven.</span><span class="sxs-lookup"><span data-stu-id="97909-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="97909-115">Uw API's worden in het eerste voorbeeld voor setup alleen via beheerd binnen het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="97909-116">Interne consumenten (gemarkeerd in oranje) hebben toegang tot alle uw interne en externe API's.</span><span class="sxs-lookup"><span data-stu-id="97909-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="97909-117">Verkeer wordt nooit gedeeld met Internet wordt geleverd met een hoge prestaties via Express Route-circuits.</span><span class="sxs-lookup"><span data-stu-id="97909-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![URL-route](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="97909-119"><a name="before-you-begin"></a> Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="97909-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="97909-120">Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="97909-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="97909-121">U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="97909-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="97909-122">Maak een virtueel netwerk en maak afzonderlijke subnetten voor API Management en Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="97909-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="97909-123">Als u van plan bent te maken van een aangepaste DNS-server voor het virtuele netwerk, doen voordat u de implementatie start.</span><span class="sxs-lookup"><span data-stu-id="97909-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="97909-124">Controleer die het werkt door te zorgen voor een virtuele machine gemaakt in een nieuw subnet in het virtuele netwerk kunt omzetten en toegang tot alle Azure-service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="97909-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="97909-125">Wat is vereist voor het maken van een integratie tussen API Management en Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="97909-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="97909-126">**Back-endserverpool:** dit is het interne virtuele IP-adres van de API Management-service.</span><span class="sxs-lookup"><span data-stu-id="97909-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="97909-127">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="97909-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="97909-128">Deze instellingen worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="97909-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="97909-129">**Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="97909-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="97909-130">Roept het verkeer wordt omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="97909-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="97909-131">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="97909-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="97909-132">**Regel:** de regel wordt een listener gebonden aan een back-end-servergroep.</span><span class="sxs-lookup"><span data-stu-id="97909-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="97909-133">**Aangepaste Health test:** Application Gateway gebruikt standaard IP-adres op basis van tests om te achterhalen welke servers in de BackendAddressPool actief zijn.</span><span class="sxs-lookup"><span data-stu-id="97909-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="97909-134">De API Management service alleen reageert op aanvragen met de juiste host-header, daarom de testpakketten standaard mislukken.</span><span class="sxs-lookup"><span data-stu-id="97909-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="97909-135">Een aangepaste health test moet worden gedefinieerd om te bepalen dat de service actief is en moet deze aanvragen worden doorgestuurd toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="97909-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="97909-136">**Aangepaste Domeincertificaat:** voor toegang tot API Management vanaf het internet moet u een CNAME-toewijzing van de hostnaam van de toepassingsgateway front-DNS-naam te maken.</span><span class="sxs-lookup"><span data-stu-id="97909-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="97909-137">Dit zorgt ervoor dat de hostnaam header en het certificaat verzonden naar Application Gateway die wordt doorgestuurd naar de API Management is een APIM als geldige kan herkennen.</span><span class="sxs-lookup"><span data-stu-id="97909-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="97909-138"><a name="overview-steps"></a> Stappen die nodig zijn voor het integreren van API Management en Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97909-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="97909-139">Maak een resourcegroep voor Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97909-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="97909-140">Maak een virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="97909-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="97909-141">Maak een ander subnet voor API Management.</span><span class="sxs-lookup"><span data-stu-id="97909-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="97909-142">Maak een API Management-service binnen het VNET subnet die eerder is gemaakt en zorg ervoor dat u de interne modus.</span><span class="sxs-lookup"><span data-stu-id="97909-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="97909-143">Het instellen van de aangepaste domeinnaam in de API Management-service.</span><span class="sxs-lookup"><span data-stu-id="97909-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="97909-144">Maak een configuratieobject voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="97909-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="97909-145">Een Application Gateway-resource maken.</span><span class="sxs-lookup"><span data-stu-id="97909-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="97909-146">Maak een CNAME van de openbare DNS-naam van de toepassingsgateway naar de hostnaam van de proxy API Management.</span><span class="sxs-lookup"><span data-stu-id="97909-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="97909-147">Een resourcegroep maken voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97909-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="97909-148">Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97909-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="97909-149">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97909-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="97909-150">Stap 1</span><span class="sxs-lookup"><span data-stu-id="97909-150">Step 1</span></span>

<span data-ttu-id="97909-151">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="97909-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="97909-152">Verifiëren met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="97909-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="97909-153">Stap 2</span><span class="sxs-lookup"><span data-stu-id="97909-153">Step 2</span></span>

<span data-ttu-id="97909-154">Controleer de abonnementen voor het account en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="97909-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="97909-155">Stap 3</span><span class="sxs-lookup"><span data-stu-id="97909-155">Step 3</span></span>

<span data-ttu-id="97909-156">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="97909-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="97909-157">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="97909-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="97909-158">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="97909-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="97909-159">Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97909-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="97909-160">Een virtueel netwerk en een subnet voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="97909-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="97909-161">Het volgende voorbeeld ziet hoe u een virtueel netwerk maken met de resource manager.</span><span class="sxs-lookup"><span data-stu-id="97909-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="97909-162">Stap 1</span><span class="sxs-lookup"><span data-stu-id="97909-162">Step 1</span></span>

<span data-ttu-id="97909-163">Het adresbereik 10.0.0.0/24 toewijzen aan de variabele subnet moet worden gebruikt voor toepassingsgateway tijdens het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="97909-164">Stap 2</span><span class="sxs-lookup"><span data-stu-id="97909-164">Step 2</span></span>

<span data-ttu-id="97909-165">Het adresbereik 10.0.1.0/24 toewijzen aan de variabele subnet moet worden gebruikt voor API Management tijdens het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="97909-166">Stap 3</span><span class="sxs-lookup"><span data-stu-id="97909-166">Step 3</span></span>

<span data-ttu-id="97909-167">Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **apim-appGw-RG** voor de regio VS-West is met het voorvoegsel 10.0.0.0/16 met subnetten 10.0.0.0/24 en 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="97909-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="97909-168">Stap 4</span><span class="sxs-lookup"><span data-stu-id="97909-168">Step 4</span></span>

<span data-ttu-id="97909-169">Wijs een subnetvariabele toe voor de volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97909-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="97909-170">Maak een API Management-service binnen een VNET dat is geconfigureerd in de interne modus</span><span class="sxs-lookup"><span data-stu-id="97909-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="97909-171">Het volgende voorbeeld laat zien hoe een API Management-service in een VNET dat is geconfigureerd voor interne toegang alleen maken.</span><span class="sxs-lookup"><span data-stu-id="97909-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="97909-172">Stap 1</span><span class="sxs-lookup"><span data-stu-id="97909-172">Step 1</span></span>
<span data-ttu-id="97909-173">Maak een virtueel netwerk van API Management-object met behulp van het subnet $apimsubnetdata die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97909-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="97909-174">Stap 2</span><span class="sxs-lookup"><span data-stu-id="97909-174">Step 2</span></span>
<span data-ttu-id="97909-175">Maak een API Management-service in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="97909-176">Nadat de bovenstaande opdracht is geslaagd verwijzen naar [DNS-configuratie vereist voor toegang tot interne VNET API Management-service](api-management-using-with-internal-vnet.md#apim-dns-configuration) om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="97909-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="97909-177">Installatie van een aangepaste domeinnaam in API Management</span><span class="sxs-lookup"><span data-stu-id="97909-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="97909-178">Stap 1</span><span class="sxs-lookup"><span data-stu-id="97909-178">Step 1</span></span>
<span data-ttu-id="97909-179">Upload het certificaat met persoonlijke sleutel voor het domein.</span><span class="sxs-lookup"><span data-stu-id="97909-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="97909-180">In dit voorbeeld worden `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="97909-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="97909-181">Stap 2</span><span class="sxs-lookup"><span data-stu-id="97909-181">Step 2</span></span>
<span data-ttu-id="97909-182">Zodra het certificaat is geüpload, maakt u een hostnaam configuration-object voor de proxy gebruikt met een hostnaam van `api.contoso.net`, zoals de voorbeeld-certificaat biedt autoriteit voor het `*.contoso.net` domein.</span><span class="sxs-lookup"><span data-stu-id="97909-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="97909-183">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="97909-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="97909-184">Maak een openbare IP-resource **publicIP01** in de resourcegroep **apim-appGw-RG** voor de regio VS-West.</span><span class="sxs-lookup"><span data-stu-id="97909-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="97909-185">Er wordt een IP-adres toegewezen aan de toepassingsgateway wanneer de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="97909-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="97909-186">De gatewayconfiguratie toepassing maken</span><span class="sxs-lookup"><span data-stu-id="97909-186">Create application gateway configuration</span></span>

<span data-ttu-id="97909-187">Alle configuratie-items moeten zijn ingesteld voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="97909-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="97909-188">Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="97909-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="97909-189">Stap 1</span><span class="sxs-lookup"><span data-stu-id="97909-189">Step 1</span></span>

<span data-ttu-id="97909-190">Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="97909-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="97909-191">Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool.</span><span class="sxs-lookup"><span data-stu-id="97909-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="97909-192">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97909-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="97909-193">Stap 2</span><span class="sxs-lookup"><span data-stu-id="97909-193">Step 2</span></span>

<span data-ttu-id="97909-194">Configureer de front-end-IP-poort voor het openbare IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97909-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="97909-195">Dit is de poort waarmee gebruikers verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="97909-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="97909-196">Stap 3</span><span class="sxs-lookup"><span data-stu-id="97909-196">Step 3</span></span>

<span data-ttu-id="97909-197">Configureer het front-end-IP-adres met openbaar IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97909-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="97909-198">Stap 4</span><span class="sxs-lookup"><span data-stu-id="97909-198">Step 4</span></span>

<span data-ttu-id="97909-199">Configureer het certificaat voor de toepassingsgateway opnieuw versleutelen van het verkeer te doorlopen en ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="97909-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="97909-200">Stap 5</span><span class="sxs-lookup"><span data-stu-id="97909-200">Step 5</span></span>

<span data-ttu-id="97909-201">De HTTP-listener voor de toepassingsgateway maken.</span><span class="sxs-lookup"><span data-stu-id="97909-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="97909-202">De front-end-IP-configuratie, poort en de ssl-certificaat aan toewijzen.</span><span class="sxs-lookup"><span data-stu-id="97909-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="97909-203">Stap 6</span><span class="sxs-lookup"><span data-stu-id="97909-203">Step 6</span></span>

<span data-ttu-id="97909-204">Maken van een aangepaste test naar de service Management API `ContosoApi` proxy domein eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97909-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="97909-205">Het pad `/status-0123456789abcdef` is een standaardeindpunt van de status voor alle API Management-services worden gehost.</span><span class="sxs-lookup"><span data-stu-id="97909-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="97909-206">Stel `api.contoso.net` als de hostnaam van een aangepaste test te beveiligen met SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="97909-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="97909-207">De hostnaam van de `contosoapi.azure-api.net` de hostnaam proxy is standaard geconfigureerd als een service met de naam `contosoapi` in openbare Azure is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97909-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="97909-208">Stap 7</span><span class="sxs-lookup"><span data-stu-id="97909-208">Step 7</span></span>

<span data-ttu-id="97909-209">Upload het certificaat moet worden gebruikt op de bronnen van de groep back-end SSL zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="97909-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="97909-210">Dit is hetzelfde certificaat dat u hebt opgegeven in stap 4 hierboven.</span><span class="sxs-lookup"><span data-stu-id="97909-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="97909-211">Stap 8</span><span class="sxs-lookup"><span data-stu-id="97909-211">Step 8</span></span>

<span data-ttu-id="97909-212">HTTP-back-end-instellingen voor de toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="97909-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="97909-213">Dit omvat het instellen van een time-out optreedt voor de back-end-aanvraag waarna ze worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="97909-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="97909-214">Deze waarde verschilt van de time-out voor de test.</span><span class="sxs-lookup"><span data-stu-id="97909-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="97909-215">Stap 9</span><span class="sxs-lookup"><span data-stu-id="97909-215">Step 9</span></span>

<span data-ttu-id="97909-216">Configureer een backend-IP-adresgroep met de naam **apimbackend** met het interne virtuele IP-adres van de API Management-service die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97909-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="97909-217">Stap 10</span><span class="sxs-lookup"><span data-stu-id="97909-217">Step 10</span></span>

<span data-ttu-id="97909-218">Instellingen maken voor een dummy (niet-bestaand) back-end.</span><span class="sxs-lookup"><span data-stu-id="97909-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="97909-219">Aanvragen voor API-paden die we niet wilt weergeven van API Management via Application Gateway wordt bereikt deze back-end en 404 retourneren.</span><span class="sxs-lookup"><span data-stu-id="97909-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="97909-220">HTTP-instellingen configureren voor de dummy back-end.</span><span class="sxs-lookup"><span data-stu-id="97909-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="97909-221">Configureer een dummy back-end **dummyBackendPool**, die verwijzen naar een FQDN-adres **dummybackend.com**. Dit adres FQDN bestaat niet in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="97909-222">Maken van de instelling van een regel voor de toepassingsgateway gebruikt standaard die naar de niet-bestaande back-end wijst **dummybackend.com** in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="97909-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="97909-223">Stap 11</span><span class="sxs-lookup"><span data-stu-id="97909-223">Step 11</span></span>

<span data-ttu-id="97909-224">URL-paden regel voor de back-end-adresgroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="97909-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="97909-225">Hierdoor is slechts een deel van de API's te selecteren in API Management voor blootgesteld aan het publiek.</span><span class="sxs-lookup"><span data-stu-id="97909-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="97909-226">Bijvoorbeeld, als er `Echo API` (/ echo /), `Calculator API` (/calc/) enz. Controleer alleen `Echo API` toegankelijk is vanaf Internet).</span><span class="sxs-lookup"><span data-stu-id="97909-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="97909-227">Het volgende voorbeeld wordt een eenvoudige regel voor het '/ echo /' pad routering verkeer naar de back-end 'apimProxyBackendPool'.</span><span class="sxs-lookup"><span data-stu-id="97909-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="97909-228">Als het pad komt niet overeen met de padregels wilt inschakelen via de API Management, de regelconfiguratie pad-kaart, configureert u een standaard-back-end-adresgroep met de naam **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="97909-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="97909-229">Bijvoorbeeld: http://api.contoso.net/calc/ * overschakelt naar de **dummyBackendPool** zoals deze is gedefinieerd als de standaardgroep voor niet-overeenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="97909-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="97909-230">Deze stap zorgt ervoor dat alleen aanvragen voor het pad '/ echo' door de toepassingsgateway zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="97909-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="97909-231">Aanvragen tot andere geconfigureerd in API Management-API's genereert 404-fouten van Application Gateway wanneer deze vanuit het Internet.</span><span class="sxs-lookup"><span data-stu-id="97909-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="97909-232">Stap 12</span><span class="sxs-lookup"><span data-stu-id="97909-232">Step 12</span></span>

<span data-ttu-id="97909-233">Maak een instelling voor de toepassingsgateway te gebruiken URL-pad gebaseerde routering.</span><span class="sxs-lookup"><span data-stu-id="97909-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="97909-234">Stap 13</span><span class="sxs-lookup"><span data-stu-id="97909-234">Step 13</span></span>

<span data-ttu-id="97909-235">Het aantal exemplaren en de grootte voor de toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="97909-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="97909-236">Hier gebruiken we de [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) voor een betere beveiliging van de API Management-resource.</span><span class="sxs-lookup"><span data-stu-id="97909-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="97909-237">Stap 14</span><span class="sxs-lookup"><span data-stu-id="97909-237">Step 14</span></span>

<span data-ttu-id="97909-238">Configureer WAF 'Preventie'-modus.</span><span class="sxs-lookup"><span data-stu-id="97909-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="97909-239">Toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="97909-239">Create Application Gateway</span></span>

<span data-ttu-id="97909-240">Een toepassingsgateway maken met de configuratieobjecten uit de bovenstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="97909-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="97909-241">De hostnaam van de API Management-proxy aan de openbare DNS-naam van de resource Application Gateway CNAME</span><span class="sxs-lookup"><span data-stu-id="97909-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="97909-242">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="97909-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="97909-243">Wanneer u een openbaar IP-adres, vereist de toepassingsgateway een dynamisch toegewezen DNS-naam die niet eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97909-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="97909-244">De toepassingsgateway DNS-naam moet worden gebruikt voor het maken van een CNAME-record die de APIM proxy-hostnaam wijst (bv. `api.contoso.net` in de bovenstaande voorbeelden) aan deze DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="97909-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="97909-245">Voor het configureren van de frontend-IP-CNAME-record ophalen van de gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element.</span><span class="sxs-lookup"><span data-stu-id="97909-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="97909-246">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan worden gewijzigd bij opnieuw opstarten van de gateway.</span><span class="sxs-lookup"><span data-stu-id="97909-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="97909-247"><a name="summary"></a> Samenvatting</span><span class="sxs-lookup"><span data-stu-id="97909-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="97909-248">Azure API Management geconfigureerd in een VNET biedt een interface één gateway voor alle geconfigureerde API's, ongeacht of deze gehoste on-premises of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="97909-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="97909-249">Integratie van Application Gateway met API Management biedt de flexibiliteit van selectief inschakelen van bepaalde API's voor het toegankelijk is op het Internet, evenals biedt u een Web Application Firewall als een frontend naar uw API Management-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="97909-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="97909-250"><a name="next-steps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97909-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="97909-251">Meer informatie over Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97909-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="97909-252">Overzicht van Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97909-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="97909-253">Application Gateway Web Application Firewall</span><span class="sxs-lookup"><span data-stu-id="97909-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="97909-254">Application Gateway met behulp van Routing op basis van het pad</span><span class="sxs-lookup"><span data-stu-id="97909-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="97909-255">Meer informatie over API Management en VNETs</span><span class="sxs-lookup"><span data-stu-id="97909-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="97909-256">Met behulp van API Management is alleen beschikbaar in het VNET</span><span class="sxs-lookup"><span data-stu-id="97909-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="97909-257">Met behulp van API Management in VNET</span><span class="sxs-lookup"><span data-stu-id="97909-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
