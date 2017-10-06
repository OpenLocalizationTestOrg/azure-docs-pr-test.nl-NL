---
title: Azure Application Gateway met interne Load Balancer aaaUsing | Microsoft Docs
description: Deze pagina vindt u instructies tooconfigure een Azure-toepassingsgateway met een eindpunt interne met gelijke taakverdeling
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="17e07-103">Een Application Gateway maken met een Internal Load Balancer (ILB)</span><span class="sxs-lookup"><span data-stu-id="17e07-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17e07-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="17e07-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="17e07-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="17e07-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="17e07-106">Application Gateway kan worden geconfigureerd met een internetgericht virtueel IP-adres of met een interne eindpunt niet blootgesteld toohello internet, ook wel bekend als interne Load Balancer (ILB)-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="17e07-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="17e07-107">Hallo-gateway configureren met een ILB is nuttig voor toointernet interne line-of-business-toepassingen niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="17e07-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="17e07-108">Het is ook nuttig voor servicecategorieën binnen een toepassing met meerdere lagen, die bevindt zich in een grens niet blootgesteld beveiliging toointernet, maar er wel round-robin verdeling, sessiepersistentie of SSL-beëindiging.</span><span class="sxs-lookup"><span data-stu-id="17e07-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="17e07-109">Dit artikel begeleidt u bij Hallo stappen tooconfigure een toepassingsgateway met een ILB.</span><span class="sxs-lookup"><span data-stu-id="17e07-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17e07-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="17e07-110">Before you begin</span></span>

1. <span data-ttu-id="17e07-111">Installeer de nieuwste versie van Hallo Hallo Web Platform Installer met Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="17e07-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="17e07-112">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [downloadpagina](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="17e07-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="17e07-113">Controleer of u een werkend virtueel netwerk met een geldig subnetmasker.</span><span class="sxs-lookup"><span data-stu-id="17e07-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="17e07-114">Controleer of u back-endservers in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="17e07-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="17e07-115">een toepassingsgateway toocreate Hallo stappen te volgen in volgorde van Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="17e07-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="17e07-116">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="17e07-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="17e07-117">Hallo-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="17e07-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="17e07-118">De configuratie van een set Hallo-gateway</span><span class="sxs-lookup"><span data-stu-id="17e07-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="17e07-119">Hallo gateway starten</span><span class="sxs-lookup"><span data-stu-id="17e07-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="17e07-120">Controleer of de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="17e07-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="17e07-121">Een toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="17e07-121">Create an application gateway:</span></span>

<span data-ttu-id="17e07-122">**toocreate hello gateway**, gebruik Hallo `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="17e07-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="17e07-123">Houd er rekening mee dat facturering voor Hallo gateway niet op dit moment wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="17e07-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="17e07-124">Facturering begint met een latere stap Hallo gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="17e07-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="17e07-125">**toovalidate** dat Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="17e07-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="17e07-126">In voorbeeld Hallo *beschrijving*, *InstanceCount*, en *GatewaySize* zijn optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="17e07-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="17e07-127">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="17e07-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="17e07-128">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="17e07-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="17e07-129">Kleine en grote andere beschikbare waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="17e07-129">Small and Large are other available values.</span></span> <span data-ttu-id="17e07-130">*VIP* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="17e07-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="17e07-131">Deze worden nadat Hallo gateway Hallo uitvoeringsstatus is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="17e07-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="17e07-132">Hallo-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="17e07-132">Configure hello gateway</span></span>
<span data-ttu-id="17e07-133">Een toepassingsgateway configuratie bestaat uit meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="17e07-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="17e07-134">Hallo-waarden kunnen worden gekoppeld samen tooconstruct Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="17e07-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="17e07-135">Hallo-waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="17e07-135">hello values are:</span></span>

* <span data-ttu-id="17e07-136">**Back-end-servergroep:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="17e07-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="17e07-137">Hallo IP-adressen moeten ofwel deel uitmaken toohello VNet subnet, ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="17e07-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="17e07-138">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="17e07-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="17e07-139">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="17e07-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="17e07-140">**Front-Endpoort:** dit is de openbare poort Hallo in Hallo toepassingsgateway geopend.</span><span class="sxs-lookup"><span data-stu-id="17e07-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="17e07-141">Het verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="17e07-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="17e07-142">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="17e07-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="17e07-143">**Regel:** Hallo regel verbindt Hallo listener Hallo back-end-servergroep en bepaalt welke back-end server groep Hallo verkeer gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="17e07-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="17e07-144">Op dit moment alleen Hallo *basic* regel wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="17e07-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="17e07-145">Hallo *basic* regel is round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="17e07-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="17e07-146">U kunt de configuratie maken door het maken van een configuratieobject of met behulp van een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="17e07-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="17e07-147">tooconstruct uw configuratie met behulp van een XML-configuratiebestand, gebruik Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="17e07-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="17e07-148">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="17e07-148">Note hello following:</span></span>

* <span data-ttu-id="17e07-149">Hallo *FrontendIPConfigurations* element worden Hallo ILB details relevant zijn voor het configureren van Application Gateway met een ILB beschreven.</span><span class="sxs-lookup"><span data-stu-id="17e07-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="17e07-150">Hallo Frontend-IP- *Type* too'Private moet worden ingesteld '</span><span class="sxs-lookup"><span data-stu-id="17e07-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="17e07-151">Hallo *StaticIPAddress* toohello gewenst intern IP-adres op welke Hallo gateway verkeer ontvangt moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="17e07-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="17e07-152">Houd er rekening mee dat Hallo *StaticIPAddress* element is optioneel.</span><span class="sxs-lookup"><span data-stu-id="17e07-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="17e07-153">Als dat niet is ingesteld, een beschikbare interne IP-adres uit Hallo geïmplementeerd subnet is gekozen.</span><span class="sxs-lookup"><span data-stu-id="17e07-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="17e07-154">waarde van Hallo Hallo *naam* opgegeven element in *FrontendIPConfiguration* moet worden gebruikt in Hallo HTTPListener van *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="17e07-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="17e07-155">**Configuratie-XML-voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="17e07-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="17e07-156">De configuratie van een set Hallo-gateway</span><span class="sxs-lookup"><span data-stu-id="17e07-156">Set hello gateway configuration</span></span>
<span data-ttu-id="17e07-157">Vervolgens stelt u de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="17e07-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="17e07-158">U kunt Hallo `Set-AzureApplicationGatewayConfig` cmdlet met een configuratieobject of met een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="17e07-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="17e07-159">Hallo gateway starten</span><span class="sxs-lookup"><span data-stu-id="17e07-159">Start hello gateway</span></span>

<span data-ttu-id="17e07-160">Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="17e07-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="17e07-161">Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="17e07-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="17e07-162">Hallo `Start-AzureApplicationGateway` cmdlet toocomplete too15-20 minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="17e07-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="17e07-163">Controleer of de status van de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="17e07-163">Verify hello gateway status</span></span>

<span data-ttu-id="17e07-164">Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van gateway.</span><span class="sxs-lookup"><span data-stu-id="17e07-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="17e07-165">Als `Start-AzureApplicationGateway` is voltooid in de vorige stap hello, Hallo status moet worden *met*, en Hallo Vip en DnsName moet geldige vermeldingen hebben.</span><span class="sxs-lookup"><span data-stu-id="17e07-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="17e07-166">Dit voorbeeld toont Hallo cmdlet op de eerste regel hello, gevolgd door Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="17e07-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="17e07-167">In dit voorbeeld Hallo gateway wordt uitgevoerd en is klaar tootake verkeer.</span><span class="sxs-lookup"><span data-stu-id="17e07-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="17e07-168">Hallo application gateway is geconfigureerd tooaccept-verkeer bij Hallo ILB-eindpunt van de 10.0.0.10 geconfigureerd in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="17e07-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="17e07-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17e07-169">Next steps</span></span>
<span data-ttu-id="17e07-170">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="17e07-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="17e07-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="17e07-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="17e07-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="17e07-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

