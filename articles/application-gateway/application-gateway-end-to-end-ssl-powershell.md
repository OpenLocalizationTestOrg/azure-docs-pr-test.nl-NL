---
title: aaaConfigure end tooend SSL met Azure Application Gateway | Microsoft Docs
description: "Dit artikel wordt beschreven hoe tooconfigure tooend SSL met Application Gateway met Azure Resource Manager PowerShell beëindigen"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="d1eb2-103">Einde tooend SSL configureren met Application Gateway met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1eb2-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="d1eb2-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d1eb2-104">Overview</span></span>

<span data-ttu-id="d1eb2-105">Een toepassing Gateway ondersteunt eindigen tooend codering van verkeer.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="d1eb2-106">Toepassingsgateway doet dit door het Hallo-SSL-verbinding op Hallo application gateway wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="d1eb2-107">Hallo gateway geldt routeringsregels Hallo toohello verkeer, opnieuw versleutelt hello-pakket en stuurt Hallo pakket toohello juiste back-end op basis van Hallo routeringsregels gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="d1eb2-108">Geen antwoord van de webserver Hallo Hallo doorloopt dezelfde back toohello eindgebruiker verwerken.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="d1eb2-109">Een andere functie die toepassingsgateway ondersteunt aangepaste SSL opties definiëren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="d1eb2-110">Toepassingsgateway ondersteunt uitschakelen Hallo na protocolversie; **TLSv1.0**, **TLSv1.1**, en **TLSv1.2** ook definiëren Hallo die cipher suites toouse en Hallo volgorde van voorkeur.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="d1eb2-111">toolearn meer informatie over de configureerbare opties voor SSL, gaat u naar [SSL overzicht](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb2-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d1eb2-112">SSL 2.0 en SSL 3.0 zijn standaard uitgeschakeld en kan niet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="d1eb2-113">Ze worden als onveilig beschouwd en zijn niet kunnen toobe gebruikt met Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![afbeelding van scenario][scenario]

## <a name="scenario"></a><span data-ttu-id="d1eb2-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="d1eb2-115">Scenario</span></span>

<span data-ttu-id="d1eb2-116">In dit scenario, leert u hoe een application gateway met toocreate tooend SSL eindigen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="d1eb2-117">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="d1eb2-117">This scenario will:</span></span>

* <span data-ttu-id="d1eb2-118">Maak een resourcegroep met de naam **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="d1eb2-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="d1eb2-119">Maak een virtueel netwerk met de naam **appgwvnet** met een adresruimte van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="d1eb2-120">Maken van twee subnetten aangeroepen **appgwsubnet** en **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="d1eb2-121">Maak een kleine toepassing gateway ondersteunende end tooend SSL-versleuteling die limieten SSL-protocollen versies en coderingssuites.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d1eb2-122">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d1eb2-122">Before you begin</span></span>

<span data-ttu-id="d1eb2-123">tooconfigure end tooend SSL met een application gateway, een certificaat is vereist voor het Hallo-gateway en certificaten zijn vereist voor Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="d1eb2-124">Hallo gatewaycertificaat is gebruikte tooencrypt en ontsleutelen Hallo verkeer dat wordt verzonden tooit met SSL.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="d1eb2-125">Hallo gatewaycertificaat moet toobe Personal Information Exchange (pfx)-indeling.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="d1eb2-126">Deze bestandsindeling kunt Hallo persoonlijke sleutel toobe geëxporteerd die vereist wordt door Hallo application gateway tooperform Hallo versleuteling en ontsleuteling van verkeer.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="d1eb2-127">Voor end moet tooend SSL-versleuteling Hallo back-end goedgekeurde lijst met toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="d1eb2-128">Dit wordt gedaan door het openbare certificaat van Hallo back-ends toohello toepassingsgateway Hallo uploadt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="d1eb2-129">Dit zorgt ervoor dat toepassingsgateway Hallo communiceert alleen met bekende back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="d1eb2-130">Dit verdere beveiligt Hallo end tooend communicatie.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="d1eb2-131">Dit proces wordt beschreven in Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1eb2-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="d1eb2-132">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-132">Create hello Resource Group</span></span>

<span data-ttu-id="d1eb2-133">Deze sectie helpt u bij het maken van een resourcegroep met Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="d1eb2-134">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d1eb2-134">Step 1</span></span>

<span data-ttu-id="d1eb2-135">Meld u bij tooyour Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d1eb2-136">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d1eb2-136">Step 2</span></span>

<span data-ttu-id="d1eb2-137">Selecteer Hallo abonnement toouse voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="d1eb2-138">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d1eb2-138">Step 3</span></span>

<span data-ttu-id="d1eb2-139">Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).</span><span class="sxs-lookup"><span data-stu-id="d1eb2-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="d1eb2-140">Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="d1eb2-141">Hallo volgende voorbeeld wordt een virtueel netwerk en twee subnets.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="d1eb2-142">Eén subnet is gebruikte toohold Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="d1eb2-143">Hallo wordt andere subnet gebruikt voor Hallo back-ends hosting Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="d1eb2-144">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d1eb2-144">Step 1</span></span>

<span data-ttu-id="d1eb2-145">Een adresbereik toewijzen voor Hallo subnet voor Application Gateway zelf hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="d1eb2-146">Subnetten geconfigureerd voor application gateway moeten correct worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="d1eb2-147">Een application gateway kan worden geconfigureerd voor up too10 exemplaren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="d1eb2-148">Elk exemplaar duurt één IP-adres van Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="d1eb2-149">Te klein van een subnet, kan de uitbreiden van een toepassingsgateway nadelig beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="d1eb2-150">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d1eb2-150">Step 2</span></span>

<span data-ttu-id="d1eb2-151">Een adresbereik toobe gebruikt voor back-endadresgroep Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="d1eb2-152">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d1eb2-152">Step 3</span></span>

<span data-ttu-id="d1eb2-153">Een virtueel netwerk maken met gedefinieerd in de vorige stappen Hallo Hallo-subnetten.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="d1eb2-154">Stap 4</span><span class="sxs-lookup"><span data-stu-id="d1eb2-154">Step 4</span></span>

<span data-ttu-id="d1eb2-155">Hallo virtueel netwerk resource en subnet resources toobe gebruikt in de volgende stappen uit Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="d1eb2-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="d1eb2-156">Een openbaar IP-adres voor de front-endconfiguratie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="d1eb2-157">Maak een openbare IP-resource toobe gebruikt voor toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="d1eb2-158">Dit openbare IP-adres wordt gebruikt een volgende stap.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="d1eb2-159">Toepassingsgateway biedt geen ondersteuning voor Hallo gebruik van een openbaar IP-adres dat is gemaakt met een domein etiket is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="d1eb2-160">Alleen een openbaar IP-adres met een domeinlabel dynamisch gemaakte wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="d1eb2-161">Als u een beschrijvende DNS-naam voor de toepassingsgateway Hallo vereist, is het raadzaam toouse een CNAME-record als een alias.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="d1eb2-162">Een configuratieobject voor de toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="d1eb2-163">Alle configuratie-items worden ingesteld voordat u de toepassingsgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="d1eb2-164">Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="d1eb2-165">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d1eb2-165">Step 1</span></span>

<span data-ttu-id="d1eb2-166">Toepassingsgateway een IP-configuratie maken, deze instelling configureert welke subnet Hallo application gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="d1eb2-167">Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en netwerkverkeer toohello IP-adressen van routes in Hallo backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="d1eb2-168">Onthoud dat elk exemplaar één IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="d1eb2-169">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d1eb2-169">Step 2</span></span>

<span data-ttu-id="d1eb2-170">Maak een front-end-IP-configuratie, deze instelling wordt een persoonlijke of openbare IP-adres toohello front-end van de toepassingsgateway Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="d1eb2-171">Hallo stap koppelt Hallo openbaar IP-adres in de voorgaande stap met het front-end-IP-configuratie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="d1eb2-172">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d1eb2-172">Step 3</span></span>

<span data-ttu-id="d1eb2-173">Hallo backend-IP-adresgroep configureren met Hallo IP-adressen van Hallo back-end-webservers.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="d1eb2-174">Deze IP-adressen zijn Hallo IP-adressen die ontvangen netwerkverkeer op Hallo van Hallo front-end-IP-eindpunt binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="d1eb2-175">U vervangen Hallo IP-adressen tooadd na uw eigen toepassing IP-adreseindpunten.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="d1eb2-176">Een volledig gekwalificeerde domeinnaam (FQDN) is ook een geldige waarde in plaats van een IP-adres voor de back-endservers Hallo door middel van Hallo - BackendFqdns switch.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="d1eb2-177">Stap 4</span><span class="sxs-lookup"><span data-stu-id="d1eb2-177">Step 4</span></span>

<span data-ttu-id="d1eb2-178">Hallo front-end-IP-poort voor het openbare IP-eindpunt Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="d1eb2-179">Dit is Hallo-poort waarmee gebruikers verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="d1eb2-180">Stap 5</span><span class="sxs-lookup"><span data-stu-id="d1eb2-180">Step 5</span></span>

<span data-ttu-id="d1eb2-181">Hallo-certificaat voor de toepassingsgateway Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="d1eb2-182">Dit certificaat wordt gebruikt toodecrypt en Hallo-verkeer in de toepassingsgateway Hallo opnieuw versleutelen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="d1eb2-183">Dit voorbeeld configureert Hallo gebruikte certificaat voor SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="d1eb2-184">Hallo-certificaat moet toobe in PFX-indeling en Hallo wachtwoord moet tussen 4 too12 tekens.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="d1eb2-185">Stap 6</span><span class="sxs-lookup"><span data-stu-id="d1eb2-185">Step 6</span></span>

<span data-ttu-id="d1eb2-186">Hallo HTTP-listener voor de toepassingsgateway Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="d1eb2-187">Hallo front-end-IP-configuratie, poort en SSL-certificaat toouse toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="d1eb2-188">Stap 7</span><span class="sxs-lookup"><span data-stu-id="d1eb2-188">Step 7</span></span>

<span data-ttu-id="d1eb2-189">Upload het Hallo-certificaat toobe gebruikt op Hallo SSL ingeschakeld resources in de back-end.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="d1eb2-190">Hallo standaard test krijgt Hallo openbare sleutel van Hallo **standaard** SSL-binding op Hallo back-end van IP-adres en vergelijkt Hallo waarde de openbare sleutel toohello waarde de openbare sleutel u hier opgeeft, wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="d1eb2-191">Hallo opgehaalde openbare sleutel mag niet per se zijn bedoeld Hallo site toowhich verkeersstromen **als** u hostheaders en SNI op Hallo back-end gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="d1eb2-192">Als u twijfelt, gaat u naar https://127.0.0.1/ op Hallo back-ends van tooconfirm welk certificaat wordt gebruikt voor Hallo **standaard** SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="d1eb2-193">Hallo openbare sleutel van deze aanvraag gebruikt in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="d1eb2-194">Als u van hostheaders en SNI op HTTPS-bindingen gebruikmaakt en niet u een antwoord en het certificaat van een handmatige browser aanvraag toohttps://127.0.0.1/ op Hallo back-ends ontvangt, moet u een standaard SSL-binding op back-ends van Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="d1eb2-195">Als u niet doet dit, mislukt de tests en Hallo back-end is niet wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="d1eb2-196">Hallo certificaat dat is opgegeven in deze stap moet Hallo openbare sleutel van het Hallo pfx-certificaat aanwezig is op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="d1eb2-197">Exporteer Hallo certificaat (geen basiscertificaat Hallo) op Hallo back-endserver in. CER indeling en deze gebruiken in deze stap.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="d1eb2-198">Deze stap whitelists Hallo backend met Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="d1eb2-199">Stap 8</span><span class="sxs-lookup"><span data-stu-id="d1eb2-199">Step 8</span></span>

<span data-ttu-id="d1eb2-200">Hallo application gateway back-end-HTTP-instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="d1eb2-201">Hallo-certificaat geüpload in de voorgaande stap toohello HTTP-instellingen Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="d1eb2-202">Stap 9</span><span class="sxs-lookup"><span data-stu-id="d1eb2-202">Step 9</span></span>

<span data-ttu-id="d1eb2-203">Maak een load balancer-routeringsregel waarmee het gedrag van Hallo load balancer worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="d1eb2-204">In dit voorbeeld wordt wordt een eenvoudige round robinregel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="d1eb2-205">Stap 10</span><span class="sxs-lookup"><span data-stu-id="d1eb2-205">Step 10</span></span>

<span data-ttu-id="d1eb2-206">Hallo exemplaargrootte van de toepassingsgateway Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="d1eb2-207">Hallo beschikbare grootten zijn **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="d1eb2-208">Hallo beschikbare waarden zijn, de capaciteit van 1 t/m 10.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="d1eb2-209">Een aantal exemplaren van 1 worden gekozen voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="d1eb2-210">Het is belangrijk dat elke instantie onder twee exemplaren tellen tooknow niet wordt gedekt door Hallo SLA en worden daarom niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="d1eb2-211">Kleine gateways worden gebruikt voor het ontwikkelen testen en niet voor productiedoeleinden toobe.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="d1eb2-212">Stap 11</span><span class="sxs-lookup"><span data-stu-id="d1eb2-212">Step 11</span></span>

<span data-ttu-id="d1eb2-213">Hallo SSL beleid toobe gebruikt op Hallo toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="d1eb2-214">Hallo mogelijkheid tooset minimaal versie biedt ondersteuning voor toepassingsgateway voor SSL-protocol versie.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="d1eb2-215">Hallo zijn volgende waarden een lijst met protocolversies die kunnen worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="d1eb2-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="d1eb2-216">**TLSv1_0**</span></span>
* <span data-ttu-id="d1eb2-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="d1eb2-217">**TLSv1_1**</span></span>
* <span data-ttu-id="d1eb2-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="d1eb2-218">**TLSv1_2**</span></span>

<span data-ttu-id="d1eb2-219">Sets Hallo minimale protocolversie te**TLSv1_2** en schakelt **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** alleen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="d1eb2-220">Hallo toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-220">Create hello Application Gateway</span></span>

<span data-ttu-id="d1eb2-221">Maak met alle Hallo vorige stappen Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="d1eb2-222">Hallo maken van Hallo gateway is een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="d1eb2-223">SSL-protocol versie op een bestaande toepassingsgateway beperken</span><span class="sxs-lookup"><span data-stu-id="d1eb2-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="d1eb2-224">Hallo voorgaande stappen nemen u bij het maken van een toepassing met einde tooend SSL- en uitschakelen van bepaalde versies van SSL-protocol.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="d1eb2-225">Hallo volgende voorbeeld wordt uitgeschakeld bepaalde beleidsregels SSL op een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="d1eb2-226">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d1eb2-226">Step 1</span></span>

<span data-ttu-id="d1eb2-227">Hallo application gateway tooupdate ophalen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="d1eb2-228">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d1eb2-228">Step 2</span></span>

<span data-ttu-id="d1eb2-229">Definieer een SSL-beleid.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-229">Define an SSL policy.</span></span> <span data-ttu-id="d1eb2-230">In Hallo voorbeeld te volgen, TLSv1.0 TLSv1.1 zijn uitgeschakeld en de coderingssuites Hallo **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** Hallo enigen toegestaan zijn.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="d1eb2-231">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d1eb2-231">Step 3</span></span>

<span data-ttu-id="d1eb2-232">Tot slot werkt Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-232">Finally, update hello gateway.</span></span> <span data-ttu-id="d1eb2-233">Het is belangrijk toonote dat deze laatste stap een langlopende taak is.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="d1eb2-234">Wanneer dit wordt gedaan, eindigen tooend die SSL op Hallo application gateway is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d1eb2-235">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="d1eb2-235">Get application gateway DNS name</span></span>

<span data-ttu-id="d1eb2-236">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="d1eb2-237">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d1eb2-238">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="d1eb2-239">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb2-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d1eb2-240">toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="d1eb2-241">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="d1eb2-242">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d1eb2-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d1eb2-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1eb2-243">Next steps</span></span>

<span data-ttu-id="d1eb2-244">Meer informatie over het beperken van Hallo beveiliging van uw webtoepassingen met Web Application Firewall via Application Gateway in via [Web Application Firewall-overzicht](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d1eb2-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
