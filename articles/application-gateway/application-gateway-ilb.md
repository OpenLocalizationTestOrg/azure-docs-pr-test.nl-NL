---
title: Met behulp van Azure-toepassingsgateway met interne Load Balancer | Microsoft Docs
description: Deze pagina vindt u instructies voor het configureren van een Azure-toepassingsgateway met een eindpunt interne met gelijke taakverdeling
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
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="95360-103">Een Application Gateway maken met een Internal Load Balancer (ILB)</span><span class="sxs-lookup"><span data-stu-id="95360-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="95360-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="95360-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="95360-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="95360-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="95360-106">Application Gateway kan worden geconfigureerd met een internetgericht virtueel IP-adres of met een interne eindpunt niet blootgesteld aan internet, ook wel bekend als interne Load Balancer (ILB)-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="95360-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="95360-107">De gateway configureren met een ILB is nuttig voor interne line-of-business-toepassingen niet blootgesteld aan internet.</span><span class="sxs-lookup"><span data-stu-id="95360-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="95360-108">Het is ook nuttig voor servicecategorieën binnen een toepassing met meerdere lagen, die zich binnen een beveiligingsgrens niet blootgesteld aan internet, maar nog steeds vereist verdeling van round-robin, sessiepersistentie of SSL-beëindiging.</span><span class="sxs-lookup"><span data-stu-id="95360-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="95360-109">In dit artikel worden de stappen beschreven voor het configureren van een toepassingsgateway met een ILB.</span><span class="sxs-lookup"><span data-stu-id="95360-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="95360-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="95360-110">Before you begin</span></span>

1. <span data-ttu-id="95360-111">Installeer de nieuwste versie van de Azure PowerShell-cmdlets met behulp van het Webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="95360-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="95360-112">U kunt downloaden en installeer de nieuwste versie van de **Windows PowerShell** sectie van de [downloadpagina](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="95360-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="95360-113">Controleer of u een werkend virtueel netwerk met een geldig subnetmasker.</span><span class="sxs-lookup"><span data-stu-id="95360-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="95360-114">Controleer of u back-endservers in het virtuele netwerk of een openbaar IP-/ VIP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="95360-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="95360-115">Als u wilt een toepassingsgateway maken, moet u de volgende stappen uitvoeren in de volgorde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="95360-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="95360-116">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="95360-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="95360-117">De gateway configureren</span><span class="sxs-lookup"><span data-stu-id="95360-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="95360-118">Configuratie van de gateway instellen</span><span class="sxs-lookup"><span data-stu-id="95360-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="95360-119">Start de gateway</span><span class="sxs-lookup"><span data-stu-id="95360-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="95360-120">Controleer of de gateway</span><span class="sxs-lookup"><span data-stu-id="95360-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="95360-121">Een toepassingsgateway maken:</span><span class="sxs-lookup"><span data-stu-id="95360-121">Create an application gateway:</span></span>

<span data-ttu-id="95360-122">**De gateway te maken**, gebruiken de `New-AzureApplicationGateway` cmdlet, waarbij de waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="95360-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="95360-123">Er worden op dit moment nog geen kosten in rekening gebracht voor gebruik van de gateway.</span><span class="sxs-lookup"><span data-stu-id="95360-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="95360-124">De kosten zijn pas vanaf een latere stap van toepassing, wanneer de gateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="95360-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

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

<span data-ttu-id="95360-125">**Valideren** dat de gateway is gemaakt, kunt u de `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95360-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="95360-126">In het voorbeeld *beschrijving*, *InstanceCount*, en *GatewaySize* zijn optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="95360-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="95360-127">De standaardwaarde voor *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="95360-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="95360-128">De standaardwaarde voor *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="95360-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="95360-129">Kleine en grote andere beschikbare waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="95360-129">Small and Large are other available values.</span></span> <span data-ttu-id="95360-130">*VIP* en *DnsName* leeg worden weergegeven omdat de gateway is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="95360-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="95360-131">Deze parameters worden ingevuld zodra de gateway wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="95360-131">These are created once the gateway is in the running state.</span></span> 

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

## <a name="configure-the-gateway"></a><span data-ttu-id="95360-132">De gateway configureren</span><span class="sxs-lookup"><span data-stu-id="95360-132">Configure the gateway</span></span>
<span data-ttu-id="95360-133">Een toepassingsgateway configuratie bestaat uit meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="95360-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="95360-134">De waarden kunnen worden gekoppeld samen te stellen de configuratie.</span><span class="sxs-lookup"><span data-stu-id="95360-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="95360-135">De waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="95360-135">The values are:</span></span>

* <span data-ttu-id="95360-136">**Back-end-servergroep:** de lijst met IP-adressen van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="95360-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="95360-137">De IP-adressen moeten ofwel deel uitmaken van het VNet subnet, ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="95360-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="95360-138">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="95360-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="95360-139">Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.</span><span class="sxs-lookup"><span data-stu-id="95360-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="95360-140">**Front-Endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="95360-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="95360-141">Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.</span><span class="sxs-lookup"><span data-stu-id="95360-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="95360-142">**Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig), en de SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="95360-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="95360-143">**Regel:** de regel verbindt de listener met de back-end-servergroep en definieert naar welke back-end-servergroep die het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="95360-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="95360-144">Momenteel wordt alleen de regel *basic* ondersteund.</span><span class="sxs-lookup"><span data-stu-id="95360-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="95360-145">De regel *basic* is een vorm van round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="95360-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="95360-146">U kunt de configuratie maken door het maken van een configuratieobject of met behulp van een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="95360-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="95360-147">Kan de configuratie met behulp van een XML-configuratiebestand, gebruik het voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="95360-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="95360-148">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="95360-148">Note the following:</span></span>

* <span data-ttu-id="95360-149">De *FrontendIPConfigurations* element beschrijft de ILB details die relevant zijn voor het configureren van Application Gateway met een ILB.</span><span class="sxs-lookup"><span data-stu-id="95360-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="95360-150">De Frontend IP *Type* moet worden ingesteld op 'Privé'</span><span class="sxs-lookup"><span data-stu-id="95360-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="95360-151">De *StaticIPAddress* moet worden ingesteld op het gewenste interne IP-adres waarop de gateway verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="95360-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="95360-152">Houd er rekening mee dat de *StaticIPAddress* element is optioneel.</span><span class="sxs-lookup"><span data-stu-id="95360-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="95360-153">Als dat niet is ingesteld, een beschikbare intern IP-adres van het geïmplementeerde subnet is gekozen.</span><span class="sxs-lookup"><span data-stu-id="95360-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="95360-154">De waarde van de *naam* opgegeven element in *FrontendIPConfiguration* moet worden gebruikt in de HTTPListener *FrontendIP* element om te verwijzen naar de FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="95360-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="95360-155">**Configuratie-XML-voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="95360-155">**Configuration XML sample**</span></span>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="95360-156">Configuratie van de gateway instellen</span><span class="sxs-lookup"><span data-stu-id="95360-156">Set the gateway configuration</span></span>
<span data-ttu-id="95360-157">Vervolgens stelt u de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="95360-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="95360-158">U kunt de `Set-AzureApplicationGatewayConfig` cmdlet met een configuratieobject of met een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="95360-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-the-gateway"></a><span data-ttu-id="95360-159">De gateway openen</span><span class="sxs-lookup"><span data-stu-id="95360-159">Start the gateway</span></span>

<span data-ttu-id="95360-160">Nadat de gateway is geconfigureerd, gebruikt u de cmdlet `Start-AzureApplicationGateway` om de gateway te activeren.</span><span class="sxs-lookup"><span data-stu-id="95360-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="95360-161">Voor een toepassingsgateway worden pas kosten doorberekend wanneer de gateway is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="95360-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="95360-162">De `Start-AzureApplicationGateway` cmdlet mogelijk maximaal 15-20 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="95360-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
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

## <a name="verify-the-gateway-status"></a><span data-ttu-id="95360-163">De gatewaystatus controleren</span><span class="sxs-lookup"><span data-stu-id="95360-163">Verify the gateway status</span></span>

<span data-ttu-id="95360-164">Gebruik de `Get-AzureApplicationGateway` cmdlet om de status van gateway te controleren.</span><span class="sxs-lookup"><span data-stu-id="95360-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="95360-165">Als `Start-AzureApplicationGateway` is voltooid in de vorige stap, de status moet *met*, en het Vip en DnsName moet geldige vermeldingen hebben.</span><span class="sxs-lookup"><span data-stu-id="95360-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="95360-166">Dit voorbeeld ziet u de cmdlet op de eerste regel weergegeven, gevolgd door de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="95360-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="95360-167">In dit voorbeeld wordt de gateway wordt uitgevoerd en gereed is voor verkeer.</span><span class="sxs-lookup"><span data-stu-id="95360-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="95360-168">De toepassingsgateway is geconfigureerd voor het accepteren van verkeer op de geconfigureerde ILB-eindpunt van 10.0.0.10 in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="95360-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="95360-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95360-169">Next steps</span></span>
<span data-ttu-id="95360-170">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="95360-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="95360-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="95360-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="95360-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="95360-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

