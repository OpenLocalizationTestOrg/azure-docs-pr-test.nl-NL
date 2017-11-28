---
title: End-to-end SSL configureren met Azure Application Gateway | Microsoft Docs
description: Dit artikel wordt beschreven hoe u complete SSL configureren met een toepassingsgateway met Azure Resource Manager PowerShell
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="3cfad-103">End-to-end SSL configureren met Application Gateway met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cfad-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="3cfad-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3cfad-104">Overview</span></span>

<span data-ttu-id="3cfad-105">Application Gateway biedt ondersteuning voor end-to-end-versleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="3cfad-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="3cfad-106">Application Gateway doet dit door de SSL-verbinding bij de toepassingsgateway te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="3cfad-107">De gateway past vervolgens de routeringsregels op het verkeer toe, versleutelt het pakket opnieuw en stuurt het pakket naar de juiste back-end op basis van de gedefinieerde routeringsregels.</span><span class="sxs-lookup"><span data-stu-id="3cfad-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="3cfad-108">Reacties van de webserver ondergaan hetzelfde proces terug naar de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="3cfad-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="3cfad-109">Een andere functie die toepassingsgateway ondersteunt aangepaste SSL opties definiëren.</span><span class="sxs-lookup"><span data-stu-id="3cfad-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="3cfad-110">Application Gateway biedt ondersteuning voor het uitschakelen van de volgende protocolversie; **TLSv1.0**, **TLSv1.1**, en **TLSv1.2** als goed definiëren de die coderingssuites moet gebruiken en de volgorde van voorkeur.</span><span class="sxs-lookup"><span data-stu-id="3cfad-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="3cfad-111">Voor meer informatie over de configureerbare opties voor SSL, gaat u naar [SSL overzicht](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3cfad-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3cfad-112">SSL 2.0 en SSL 3.0 zijn standaard uitgeschakeld en kan niet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3cfad-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="3cfad-113">Deze worden beschouwd als niet-beveiligd en niet kunnen worden gebruikt met Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![afbeelding van scenario][scenario]

## <a name="scenario"></a><span data-ttu-id="3cfad-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="3cfad-115">Scenario</span></span>

<span data-ttu-id="3cfad-116">In dit scenario wordt informatie over het maken van een toepassingsgateway met end-to-end SSL met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cfad-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="3cfad-117">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="3cfad-117">This scenario will:</span></span>

* <span data-ttu-id="3cfad-118">Maak een resourcegroep met de naam **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="3cfad-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="3cfad-119">Maak een virtueel netwerk met de naam **appgwvnet** met een adresruimte van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="3cfad-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="3cfad-120">Maken van twee subnetten aangeroepen **appgwsubnet** en **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="3cfad-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="3cfad-121">Maak een kleine toepassingsgateway complete SSL-versleuteling ondersteunen die limieten SSL-protocollen versies en coderingssuites.</span><span class="sxs-lookup"><span data-stu-id="3cfad-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3cfad-122">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3cfad-122">Before you begin</span></span>

<span data-ttu-id="3cfad-123">Voor end-to-end SSL met een application gateway configureert, is een certificaat vereist voor de gateway en certificaten zijn vereist voor de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="3cfad-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="3cfad-124">Het gatewaycertificaat wordt gebruikt voor het versleutelen en ontsleutelen van het verkeer dat wordt verzonden via SSL.</span><span class="sxs-lookup"><span data-stu-id="3cfad-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="3cfad-125">Het gatewaycertificaat moet zich in de indeling Personal Information Exchange (pfx).</span><span class="sxs-lookup"><span data-stu-id="3cfad-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="3cfad-126">Deze bestandsindeling kunt u de persoonlijke sleutel exporteerbaar die voor de toepassingsgateway vereist is om uit te voeren voor de versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="3cfad-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="3cfad-127">Voor end-to-end-SSL-codering moet de back-end goedgekeurde lijst met toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="3cfad-128">Dit wordt gedaan door het openbare certificaat van de back-ends uploaden naar de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="3cfad-129">Dit zorgt ervoor dat de toepassingsgateway alleen met bekende back-end-exemplaren communiceert.</span><span class="sxs-lookup"><span data-stu-id="3cfad-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="3cfad-130">Dit verdere beveiligt de end-to-end communicatie.</span><span class="sxs-lookup"><span data-stu-id="3cfad-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="3cfad-131">Dit proces wordt beschreven in de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3cfad-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="3cfad-132">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="3cfad-132">Create the Resource Group</span></span>

<span data-ttu-id="3cfad-133">Deze sectie helpt u bij het maken van een resourcegroep met de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="3cfad-134">Stap 1</span><span class="sxs-lookup"><span data-stu-id="3cfad-134">Step 1</span></span>

<span data-ttu-id="3cfad-135">Aanmelden bij uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="3cfad-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="3cfad-136">Stap 2</span><span class="sxs-lookup"><span data-stu-id="3cfad-136">Step 2</span></span>

<span data-ttu-id="3cfad-137">Selecteer het abonnement moet worden gebruikt voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="3cfad-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="3cfad-138">Stap 3</span><span class="sxs-lookup"><span data-stu-id="3cfad-138">Step 3</span></span>

<span data-ttu-id="3cfad-139">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="3cfad-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="3cfad-140">Een virtueel netwerk en een subnet maken voor de toepassingsgateway</span><span class="sxs-lookup"><span data-stu-id="3cfad-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="3cfad-141">Het volgende voorbeeld wordt een virtueel netwerk en twee subnets.</span><span class="sxs-lookup"><span data-stu-id="3cfad-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="3cfad-142">Eén subnet wordt gebruikt om de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="3cfad-143">Het andere subnet wordt gebruikt voor de back-ends die als host fungeert voor de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3cfad-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="3cfad-144">Stap 1</span><span class="sxs-lookup"><span data-stu-id="3cfad-144">Step 1</span></span>

<span data-ttu-id="3cfad-145">Een adresbereik toewijzen voor het subnet voor de toepassingsgateway zelf worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="3cfad-146">Subnetten geconfigureerd voor application gateway moeten correct worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="3cfad-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="3cfad-147">Een application gateway kan worden geconfigureerd voor maximaal 10 exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3cfad-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="3cfad-148">Elk exemplaar duurt één IP-adres van het subnet.</span><span class="sxs-lookup"><span data-stu-id="3cfad-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="3cfad-149">Te klein van een subnet, kan de uitbreiden van een toepassingsgateway nadelig beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="3cfad-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="3cfad-150">Stap 2</span><span class="sxs-lookup"><span data-stu-id="3cfad-150">Step 2</span></span>

<span data-ttu-id="3cfad-151">Een adresbereik moet worden gebruikt voor de back-end-adresgroep toewijzen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="3cfad-152">Stap 3</span><span class="sxs-lookup"><span data-stu-id="3cfad-152">Step 3</span></span>

<span data-ttu-id="3cfad-153">Een virtueel netwerk maken met de subnetten die is gedefinieerd in de voorgaande stappen hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3cfad-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="3cfad-154">Stap 4</span><span class="sxs-lookup"><span data-stu-id="3cfad-154">Step 4</span></span>

<span data-ttu-id="3cfad-155">Ophalen van de resource van virtueel netwerk en bronnen van het subnet moet worden gebruikt in de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3cfad-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="3cfad-156">Een openbaar IP-adres maken voor de front-endconfiguratie</span><span class="sxs-lookup"><span data-stu-id="3cfad-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="3cfad-157">Een openbaar IP-bron moet worden gebruikt voor de toepassingsgateway maken.</span><span class="sxs-lookup"><span data-stu-id="3cfad-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="3cfad-158">Dit openbare IP-adres wordt gebruikt een volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3cfad-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="3cfad-159">Toepassingsgateway biedt geen ondersteuning voor het gebruik van een openbaar IP-adres dat is gemaakt met een domein etiket is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3cfad-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="3cfad-160">Alleen een openbaar IP-adres met een domeinlabel dynamisch gemaakte wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3cfad-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="3cfad-161">Als u een beschrijvende DNS-naam voor de toepassingsgateway vereist, wordt het aanbevolen een CNAME-record gebruiken als een alias.</span><span class="sxs-lookup"><span data-stu-id="3cfad-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="3cfad-162">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="3cfad-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="3cfad-163">Alle configuratie-items zijn ingesteld voordat u de toepassingsgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="3cfad-164">Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="3cfad-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="3cfad-165">Stap 1</span><span class="sxs-lookup"><span data-stu-id="3cfad-165">Step 1</span></span>

<span data-ttu-id="3cfad-166">Toepassingsgateway een IP-configuratie maken, deze instelling configureert welke subnet maakt gebruik van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="3cfad-167">Wanneer de toepassingsgateway wordt geopend, neemt over een IP-adres van het geconfigureerde subnet en routeert netwerkverkeer naar de IP-adressen in de back-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="3cfad-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="3cfad-168">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="3cfad-169">Stap 2</span><span class="sxs-lookup"><span data-stu-id="3cfad-169">Step 2</span></span>

<span data-ttu-id="3cfad-170">Maak een front-end-IP-configuratie, deze instelling wordt een persoonlijke of openbare IP-adres toegewezen aan de front-end van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="3cfad-171">De volgende stap koppelt het openbare IP-adres in de vorige stap aan de front-end-IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="3cfad-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="3cfad-172">Stap 3</span><span class="sxs-lookup"><span data-stu-id="3cfad-172">Step 3</span></span>

<span data-ttu-id="3cfad-173">De backend-IP-adresgroep configureren met de IP-adressen van de back-end-webservers.</span><span class="sxs-lookup"><span data-stu-id="3cfad-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="3cfad-174">Deze IP-adressen zijn de IP-adressen die het netwerkverkeer ontvangen dat afkomstig is van het front-end-IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="3cfad-175">U vervangen de volgende IP-adressen voor het toevoegen van uw eigen toepassing IP-adreseindpunten.</span><span class="sxs-lookup"><span data-stu-id="3cfad-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="3cfad-176">Een volledig gekwalificeerde domeinnaam (FQDN) is ook een geldige waarde in plaats van een IP-adres voor de back-endservers met de schakeloptie - BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="3cfad-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="3cfad-177">Stap 4</span><span class="sxs-lookup"><span data-stu-id="3cfad-177">Step 4</span></span>

<span data-ttu-id="3cfad-178">Configureer de front-end-IP-poort voor het openbare IP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="3cfad-179">Dit is de poort waarmee gebruikers verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="3cfad-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="3cfad-180">Stap 5</span><span class="sxs-lookup"><span data-stu-id="3cfad-180">Step 5</span></span>

<span data-ttu-id="3cfad-181">Configureer het certificaat voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="3cfad-182">Dit certificaat wordt gebruikt om te ontsleutelen en opnieuw versleutelen van het verkeer in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="3cfad-183">Hiermee configureert u het certificaat dat wordt gebruikt voor de SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="3cfad-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="3cfad-184">Het certificaat moet de indeling .pfx hebben en het wachtwoord moet uit 4-12 tekens bestaan.</span><span class="sxs-lookup"><span data-stu-id="3cfad-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="3cfad-185">Stap 6</span><span class="sxs-lookup"><span data-stu-id="3cfad-185">Step 6</span></span>

<span data-ttu-id="3cfad-186">De HTTP-listener voor de toepassingsgateway maken.</span><span class="sxs-lookup"><span data-stu-id="3cfad-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="3cfad-187">Toewijzen aan de front-end-IP-configuratie, de poort en de SSL-certificaat te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cfad-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="3cfad-188">Stap 7</span><span class="sxs-lookup"><span data-stu-id="3cfad-188">Step 7</span></span>

<span data-ttu-id="3cfad-189">Het uploaden van het certificaat moet worden gebruikt op het SSL-resources in de back-end ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3cfad-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="3cfad-190">De standaard-test haalt de openbare sleutel van de **standaard** SSL-binding op de back-end-IP-adres en vergelijkt de waarde voor openbare sleutel wordt ontvangen aan de waarde van de openbare sleutel u hier opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3cfad-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="3cfad-191">De opgehaalde openbare sleutel kan niet de gewenste site naar welke verkeersstromen **als** u hostheaders en SNI gebruikt op de back-end.</span><span class="sxs-lookup"><span data-stu-id="3cfad-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="3cfad-192">Als u twijfelt, gaat u naar https://127.0.0.1/ op de back-ends om te controleren welk certificaat wordt gebruikt voor de **standaard** SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="3cfad-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="3cfad-193">Gebruik de openbare sleutel van de aanvraag die in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3cfad-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="3cfad-194">Als u van hostheaders en SNI op HTTPS-bindingen gebruikmaakt en niet u een antwoord en het certificaat van een aanvraag voor een handmatige browser naar https://127.0.0.1/ op de back-ends ontvangt, moet u een standaard SSL-binding op de back-ends instellen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="3cfad-195">Als u niet doet dit, mislukt de tests en de back-end is niet wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="3cfad-196">Het certificaat dat is opgegeven in deze stap moet de openbare sleutel van het pfx-certificaat dat aanwezig is op de back-end.</span><span class="sxs-lookup"><span data-stu-id="3cfad-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="3cfad-197">Exporteer het certificaat (niet het basiscertificaat) geïnstalleerd op de back-endserver in. CER indeling en deze gebruiken in deze stap.</span><span class="sxs-lookup"><span data-stu-id="3cfad-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="3cfad-198">Deze stap whitelists de back-end met de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="3cfad-199">Stap 8</span><span class="sxs-lookup"><span data-stu-id="3cfad-199">Step 8</span></span>

<span data-ttu-id="3cfad-200">De back-end-HTTP-instellingen voor de toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="3cfad-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="3cfad-201">Toewijzen van het certificaat dat is geüpload in de vorige stap in de http-instellingen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="3cfad-202">Stap 9</span><span class="sxs-lookup"><span data-stu-id="3cfad-202">Step 9</span></span>

<span data-ttu-id="3cfad-203">Maak een load balancer-routeringsregel waarmee het gedrag van de load balancer worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3cfad-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="3cfad-204">In dit voorbeeld wordt wordt een eenvoudige round robinregel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3cfad-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="3cfad-205">Stap 10</span><span class="sxs-lookup"><span data-stu-id="3cfad-205">Step 10</span></span>

<span data-ttu-id="3cfad-206">Configureer de exemplaargrootte van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="3cfad-207">De beschikbare grootten zijn **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**.</span><span class="sxs-lookup"><span data-stu-id="3cfad-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="3cfad-208">De capaciteit zijn de beschikbare waarden 1 tot en met 10.</span><span class="sxs-lookup"><span data-stu-id="3cfad-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="3cfad-209">Een aantal exemplaren van 1 worden gekozen voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3cfad-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="3cfad-210">Het is belangrijk te weten dat alle exemplaren onder twee exemplaren niet wordt gedekt door de SLA en worden daarom niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="3cfad-211">Er zijn kleine gateways moet worden gebruikt voor het ontwikkelen testen en niet voor productiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3cfad-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="3cfad-212">Stap 11</span><span class="sxs-lookup"><span data-stu-id="3cfad-212">Step 11</span></span>

<span data-ttu-id="3cfad-213">Configureer het SSL-beleid moet worden gebruikt in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="3cfad-214">Application Gateway ondersteunt de mogelijkheid om in te stellen de minimumversie voor SSL-protocol versie.</span><span class="sxs-lookup"><span data-stu-id="3cfad-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="3cfad-215">De volgende waarden zijn een lijst met protocolversies die kunnen worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3cfad-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="3cfad-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="3cfad-216">**TLSv1_0**</span></span>
* <span data-ttu-id="3cfad-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="3cfad-217">**TLSv1_1**</span></span>
* <span data-ttu-id="3cfad-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="3cfad-218">**TLSv1_2**</span></span>

<span data-ttu-id="3cfad-219">De minimale protocolversie stelt op **TLSv1_2** en schakelt **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** alleen.</span><span class="sxs-lookup"><span data-stu-id="3cfad-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="3cfad-220">De toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="3cfad-220">Create the Application Gateway</span></span>

<span data-ttu-id="3cfad-221">Met de bovenstaande stappen maakt u de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="3cfad-222">Het maken van de gateway is een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="3cfad-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="3cfad-223">SSL-protocol versie op een bestaande toepassingsgateway beperken</span><span class="sxs-lookup"><span data-stu-id="3cfad-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="3cfad-224">De voorgaande stappen gaat u door het maken van een toepassing met end-to-end-SSL- en uitschakelen van bepaalde versies van SSL-protocol.</span><span class="sxs-lookup"><span data-stu-id="3cfad-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="3cfad-225">Bepaalde beleidsregels SSL op een bestaande toepassingsgateway Hiermee schakelt u het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3cfad-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="3cfad-226">Stap 1</span><span class="sxs-lookup"><span data-stu-id="3cfad-226">Step 1</span></span>

<span data-ttu-id="3cfad-227">Ophalen van de toepassingsgateway om bij te werken.</span><span class="sxs-lookup"><span data-stu-id="3cfad-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="3cfad-228">Stap 2</span><span class="sxs-lookup"><span data-stu-id="3cfad-228">Step 2</span></span>

<span data-ttu-id="3cfad-229">Definieer een SSL-beleid.</span><span class="sxs-lookup"><span data-stu-id="3cfad-229">Define an SSL policy.</span></span> <span data-ttu-id="3cfad-230">In het volgende voorbeeld TLSv1.0 en TLSv1.1 zijn uitgeschakeld en de coderingssuites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** zijn de enigen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3cfad-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="3cfad-231">Stap 3</span><span class="sxs-lookup"><span data-stu-id="3cfad-231">Step 3</span></span>

<span data-ttu-id="3cfad-232">Tot slot werkt de gateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-232">Finally, update the gateway.</span></span> <span data-ttu-id="3cfad-233">Het is belangrijk te weten dat deze laatste stap een langlopende taak is.</span><span class="sxs-lookup"><span data-stu-id="3cfad-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="3cfad-234">Wanneer deze is voltooid, wordt end-to-end-SSL geconfigureerd in de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="3cfad-235">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="3cfad-235">Get application gateway DNS name</span></span>

<span data-ttu-id="3cfad-236">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="3cfad-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="3cfad-237">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="3cfad-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="3cfad-238">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="3cfad-239">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3cfad-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="3cfad-240">Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="3cfad-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="3cfad-241">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="3cfad-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="3cfad-242">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3cfad-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3cfad-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cfad-243">Next steps</span></span>

<span data-ttu-id="3cfad-244">Meer informatie over het beperken van de beveiliging van uw webtoepassingen met Web Application Firewall via Application Gateway in via [Web Application Firewall-overzicht](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3cfad-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
