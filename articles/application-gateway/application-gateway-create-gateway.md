---
title: aaaCreate, openen of verwijderen van een toepassingsgateway | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, configureren, start en een Azure-toepassingsgateway verwijderen
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="718c9-103">Een toepassingsgateway maken, openen of verwijderen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="718c9-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="718c9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="718c9-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="718c9-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="718c9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="718c9-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="718c9-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="718c9-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="718c9-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="718c9-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="718c9-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="718c9-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="718c9-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="718c9-110">Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="718c9-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="718c9-111">Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="718c9-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="718c9-112">toofind een volledige lijst van ondersteunde functies, gaat u naar [Application Gateway-overzicht](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="718c9-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="718c9-113">Dit artikel begeleidt u bij Hallo stappen toocreate, configureren en start een toepassingsgateway verwijderen.</span><span class="sxs-lookup"><span data-stu-id="718c9-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="718c9-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="718c9-114">Before you begin</span></span>

1. <span data-ttu-id="718c9-115">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="718c9-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="718c9-116">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="718c9-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="718c9-117">Als u een bestaand virtueel netwerk hebt, selecteert u een bestaande lege subnet of een nieuw subnet maken in uw bestaande virtuele netwerk uitsluitend voor gebruik met Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="718c9-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="718c9-118">U kunt geen Hallo application gateway tooa ander virtueel netwerk implementeren dan Hallo resources u van plan bent toodeploy achter Hallo toepassingsgateway tenzij vnet-peering wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="718c9-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="718c9-119">Ga meer toolearn naar [Vnet-Peering](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="718c9-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="718c9-120">Controleer of u een werkend virtueel netwerk hebt met een geldig subnet.</span><span class="sxs-lookup"><span data-stu-id="718c9-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="718c9-121">Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn.</span><span class="sxs-lookup"><span data-stu-id="718c9-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="718c9-122">Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.</span><span class="sxs-lookup"><span data-stu-id="718c9-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="718c9-123">Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="718c9-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="718c9-124">Wat is vereist toocreate een application gateway?</span><span class="sxs-lookup"><span data-stu-id="718c9-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="718c9-125">Wanneer u Hallo gebruikt `New-AzureApplicationGateway` opdracht toocreate Hallo toepassingsgateway geen configuratie ingesteld op dit moment en resource Hallo nieuw gemaakt zijn geconfigureerd met XML of een configuratieobject.</span><span class="sxs-lookup"><span data-stu-id="718c9-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="718c9-126">Hallo-waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="718c9-126">hello values are:</span></span>

* <span data-ttu-id="718c9-127">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="718c9-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="718c9-128">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="718c9-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="718c9-129">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="718c9-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="718c9-130">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="718c9-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="718c9-131">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="718c9-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="718c9-132">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="718c9-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="718c9-133">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="718c9-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="718c9-134">**Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="718c9-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="718c9-135">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="718c9-135">Create an application gateway</span></span>

<span data-ttu-id="718c9-136">toocreate een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="718c9-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="718c9-137">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="718c9-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="718c9-138">Maak een XML-configuratiebestand of een configuratieobject.</span><span class="sxs-lookup"><span data-stu-id="718c9-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="718c9-139">Doorvoeren Hallo configuratie toohello nieuw gemaakte toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="718c9-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="718c9-140">Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="718c9-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="718c9-141">Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="718c9-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Voorbeeldscenario][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="718c9-143">Een toepassingsgatewayresource maken</span><span class="sxs-lookup"><span data-stu-id="718c9-143">Create an application gateway resource</span></span>

<span data-ttu-id="718c9-144">Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="718c9-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="718c9-145">Facturering voor Hallo-gateway op dit moment niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="718c9-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="718c9-146">Facturering begint met een latere stap Hallo gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="718c9-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="718c9-147">Hallo volgende voorbeeld maakt u een toepassingsgateway met behulp van een virtueel netwerk met de naam 'testvnet1' en een subnet met de naam 'subnet 1':</span><span class="sxs-lookup"><span data-stu-id="718c9-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="718c9-148">*Description*, *InstanceCount* en *GatewaySize* zijn optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="718c9-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="718c9-149">toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="718c9-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="718c9-150">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="718c9-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="718c9-151">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="718c9-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="718c9-152">U kunt kiezen tussen Small, Medium en Large.</span><span class="sxs-lookup"><span data-stu-id="718c9-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="718c9-153">*VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="718c9-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="718c9-154">Deze worden nadat Hallo gateway Hallo uitvoeringsstatus is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="718c9-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="718c9-155">Hallo toepassingsgateway configureren</span><span class="sxs-lookup"><span data-stu-id="718c9-155">Configure hello application gateway</span></span>

<span data-ttu-id="718c9-156">U kunt Hallo toepassingsgateway configureren met XML of een configuratieobject.</span><span class="sxs-lookup"><span data-stu-id="718c9-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="718c9-157">Hallo toepassingsgateway configureren met XML</span><span class="sxs-lookup"><span data-stu-id="718c9-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="718c9-158">In Hallo voorbeeld te volgen, gebruiken een XML-bestand tooconfigure alle instellingen voor de toepassingsgateway en ze toohello toepassingsgatewayresource doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="718c9-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="718c9-159">Stap 1</span><span class="sxs-lookup"><span data-stu-id="718c9-159">Step 1</span></span>

<span data-ttu-id="718c9-160">Kopieer Hallo tekst tooNotepad te volgen.</span><span class="sxs-lookup"><span data-stu-id="718c9-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="718c9-161">Hallo waarden tussen haakjes Hallo voor Hallo configuratie-items bewerken.</span><span class="sxs-lookup"><span data-stu-id="718c9-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="718c9-162">Hallo-bestand opslaan met de bestandsextensie .xml.</span><span class="sxs-lookup"><span data-stu-id="718c9-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="718c9-163">Hallo protocolitem Http of Https is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="718c9-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="718c9-164">Hallo volgende voorbeeld ziet u hoe een configuratie toouse tooset up Hallo toepassingsgateway bestand.</span><span class="sxs-lookup"><span data-stu-id="718c9-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="718c9-165">Hallo voorbeeld load compromis tussen de HTTP-verkeer via de openbare poort 80 en stuurt netwerkverkeer tooback-endpoort 80 tussen twee IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="718c9-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="718c9-166">Stap 2</span><span class="sxs-lookup"><span data-stu-id="718c9-166">Step 2</span></span>

<span data-ttu-id="718c9-167">Vervolgens stelt u de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="718c9-167">Next, set hello application gateway.</span></span> <span data-ttu-id="718c9-168">Gebruik Hallo `Set-AzureApplicationGatewayConfig` cmdlet uit met een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="718c9-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="718c9-169">Hallo toepassingsgateway configureren met behulp van een configuration-object</span><span class="sxs-lookup"><span data-stu-id="718c9-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="718c9-170">Hallo volgende voorbeeld ziet u hoe tooconfigure toepassingsgateway Hallo met behulp van configuratie-objecten.</span><span class="sxs-lookup"><span data-stu-id="718c9-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="718c9-171">Alle configuratie-items moeten afzonderlijk worden geconfigureerd en vervolgens toegevoegd tooan application gateway configuration-object.</span><span class="sxs-lookup"><span data-stu-id="718c9-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="718c9-172">Nadat Hallo configuration-object is gemaakt, gebruikt u Hallo `Set-AzureApplicationGateway` opdracht toocommit Hallo configuratie toohello eerder gemaakte toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="718c9-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="718c9-173">Voordat u een waarde tooeach configuration-object toewijst, moet u toodeclare wat voor soort object PowerShell voor opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="718c9-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="718c9-174">Hallo eerste regel toocreate Hallo afzonderlijke items definieert wat `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="718c9-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="718c9-175">Stap 1</span><span class="sxs-lookup"><span data-stu-id="718c9-175">Step 1</span></span>

<span data-ttu-id="718c9-176">Maak alle afzonderlijke configuratie-items.</span><span class="sxs-lookup"><span data-stu-id="718c9-176">Create all individual configuration items.</span></span>

<span data-ttu-id="718c9-177">Maak Hallo front-end-IP zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="718c9-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="718c9-178">Maak Hallo front-endpoort zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="718c9-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="718c9-179">Hallo back-endserverpool maken.</span><span class="sxs-lookup"><span data-stu-id="718c9-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="718c9-180">Hallo IP-adressen die zijn toegevoegd toohello back-endserverpool zoals weergegeven in het volgende voorbeeld Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="718c9-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="718c9-181">Gebruik Hallo $server object tooadd Hallo waarden toohello back-end-pool object ($pool).</span><span class="sxs-lookup"><span data-stu-id="718c9-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="718c9-182">Hallo back-endserverpoolinstelling maken.</span><span class="sxs-lookup"><span data-stu-id="718c9-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="718c9-183">Hallo-listener maken.</span><span class="sxs-lookup"><span data-stu-id="718c9-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="718c9-184">Hallo-regel maken.</span><span class="sxs-lookup"><span data-stu-id="718c9-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="718c9-185">Stap 2</span><span class="sxs-lookup"><span data-stu-id="718c9-185">Step 2</span></span>

<span data-ttu-id="718c9-186">Wijs alle afzonderlijke configuratie-items tooan application gateway configuration-object ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="718c9-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="718c9-187">Hallo front-end-IP-toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="718c9-188">Hallo front-endpoort toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="718c9-189">Hallo back-endserver groep toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="718c9-190">Hallo back-end-pool instelling toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="718c9-191">Hallo-listener toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="718c9-192">Hallo regel toohello configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="718c9-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="718c9-193">Stap 3</span><span class="sxs-lookup"><span data-stu-id="718c9-193">Step 3</span></span>
<span data-ttu-id="718c9-194">Toepassingsgatewayresource van Hallo configuration-object toohello doorvoeren met behulp van `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="718c9-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="718c9-195">Hallo gateway starten</span><span class="sxs-lookup"><span data-stu-id="718c9-195">Start hello gateway</span></span>

<span data-ttu-id="718c9-196">Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="718c9-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="718c9-197">Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="718c9-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="718c9-198">Hallo `Start-AzureApplicationGateway` cmdlet toofinish too15-20 minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="718c9-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="718c9-199">Controleer of de status van de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="718c9-199">Verify hello gateway status</span></span>

<span data-ttu-id="718c9-200">Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="718c9-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="718c9-201">Als `Start-AzureApplicationGateway` is voltooid in de vorige stap Hallo *status* moet worden uitgevoerd, en *Vip* en *DnsName* geldige waarden.</span><span class="sxs-lookup"><span data-stu-id="718c9-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="718c9-202">Hallo volgende voorbeeld wordt een toepassingsgateway weergegeven die actief is en gereed tootake verkeer dat is bestemd voor `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="718c9-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="718c9-203">Hallo toepassingsgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="718c9-203">Delete hello application gateway</span></span>

<span data-ttu-id="718c9-204">toodelete hello toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="718c9-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="718c9-205">Gebruik Hallo `Stop-AzureApplicationGateway` cmdlet toostop Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="718c9-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="718c9-206">Gebruik Hallo `Remove-AzureApplicationGateway` cmdlet tooremove Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="718c9-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="718c9-207">Controleer of deze Hallo-gateway is verwijderd met behulp van Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="718c9-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="718c9-208">Hallo volgende voorbeeld ziet u Hallo `Stop-AzureApplicationGateway` cmdlet uit op de eerste regel hello, gevolgd door Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="718c9-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="718c9-209">Nadat de toepassingsgateway Hallo gestopt is, gebruikt u Hallo `Remove-AzureApplicationGateway` cmdlet tooremove Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="718c9-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="718c9-210">tooverify die Hallo service is verwijderd, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="718c9-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="718c9-211">Deze stap is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="718c9-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="718c9-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="718c9-212">Next steps</span></span>

<span data-ttu-id="718c9-213">Als u tooconfigure SSL-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="718c9-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="718c9-214">Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="718c9-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="718c9-215">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="718c9-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="718c9-216">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="718c9-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="718c9-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="718c9-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
