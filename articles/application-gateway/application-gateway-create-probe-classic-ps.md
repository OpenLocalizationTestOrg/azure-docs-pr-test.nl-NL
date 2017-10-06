---
title: een aangepaste test - Azure Application Gateway - PowerShell-klassiek aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste test voor Application Gateway met behulp van PowerShell in het klassieke implementatiemodel Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="3ff21-103">Maak een aangepaste test voor Azure Application Gateway (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff21-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ff21-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ff21-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="3ff21-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff21-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="3ff21-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff21-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="3ff21-107">In dit artikel voegt u een aangepaste test tooan bestaande application gateway met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ff21-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="3ff21-108">Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op Hallo standaardwebtoepassing geen bieden.</span><span class="sxs-lookup"><span data-stu-id="3ff21-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ff21-109">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3ff21-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3ff21-110">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3ff21-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3ff21-111">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3ff21-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3ff21-112">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3ff21-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="3ff21-113">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="3ff21-113">Create an application gateway</span></span>

<span data-ttu-id="3ff21-114">toocreate een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="3ff21-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="3ff21-115">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="3ff21-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="3ff21-116">Maak een XML-configuratiebestand of een configuratieobject.</span><span class="sxs-lookup"><span data-stu-id="3ff21-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="3ff21-117">Doorvoeren Hallo configuratie toohello nieuw gemaakte toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="3ff21-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="3ff21-118">Een toepassingsgatewayresource maken met een aangepaste test</span><span class="sxs-lookup"><span data-stu-id="3ff21-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="3ff21-119">Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="3ff21-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="3ff21-120">Facturering voor Hallo-gateway op dit moment niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="3ff21-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="3ff21-121">Facturering begint met een latere stap Hallo gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="3ff21-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="3ff21-122">Hallo volgende voorbeeld wordt een application gateway met behulp van een virtueel netwerk 'testvnet1' en een subnet met de naam 'subnet 1' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3ff21-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="3ff21-123">toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ff21-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="3ff21-124">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="3ff21-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="3ff21-125">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="3ff21-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="3ff21-126">U kunt kiezen tussen een klein, middelgroot en groot.</span><span class="sxs-lookup"><span data-stu-id="3ff21-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="3ff21-127">*VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="3ff21-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="3ff21-128">Deze waarden worden gemaakt nadat Hallo gateway Hallo status actief is.</span><span class="sxs-lookup"><span data-stu-id="3ff21-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="3ff21-129">Een toepassingsgateway configureren met XML</span><span class="sxs-lookup"><span data-stu-id="3ff21-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="3ff21-130">In Hallo voorbeeld te volgen, gebruiken een XML-bestand tooconfigure alle instellingen voor de toepassingsgateway en ze toohello toepassingsgatewayresource doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="3ff21-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="3ff21-131">Kopieer Hallo tekst tooNotepad te volgen.</span><span class="sxs-lookup"><span data-stu-id="3ff21-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="3ff21-132">Hallo waarden tussen haakjes Hallo voor Hallo configuratie-items bewerken.</span><span class="sxs-lookup"><span data-stu-id="3ff21-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="3ff21-133">Hallo-bestand opslaan met de bestandsextensie .xml.</span><span class="sxs-lookup"><span data-stu-id="3ff21-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="3ff21-134">Hallo volgende voorbeeld ziet u hoe een configuration file tooset up Hallo application gateway tooload toouse saldo HTTP-verkeer via de openbare poort 80 en netwerkverkeer tooback-endpoort 80 tussen twee IP-adressen met behulp van een aangepaste test verzenden.</span><span class="sxs-lookup"><span data-stu-id="3ff21-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ff21-135">Hallo protocolitem Http of Https is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="3ff21-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="3ff21-136">Een nieuwe configuratie-item \<Probe\> tooconfigure aangepaste tests wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3ff21-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="3ff21-137">Hallo-configuratieparameters zijn:</span><span class="sxs-lookup"><span data-stu-id="3ff21-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="3ff21-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="3ff21-138">Parameter</span></span>|<span data-ttu-id="3ff21-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3ff21-139">Description</span></span>|
|---|---|
|<span data-ttu-id="3ff21-140">**Naam**</span><span class="sxs-lookup"><span data-stu-id="3ff21-140">**Name**</span></span> |<span data-ttu-id="3ff21-141">De referentienaam voor aangepaste test.</span><span class="sxs-lookup"><span data-stu-id="3ff21-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="3ff21-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="3ff21-142">* **Protocol**</span></span> | <span data-ttu-id="3ff21-143">Protocol dat wordt gebruikt (mogelijke waarden zijn HTTP of HTTPS).</span><span class="sxs-lookup"><span data-stu-id="3ff21-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="3ff21-144">**Host** en **pad**</span><span class="sxs-lookup"><span data-stu-id="3ff21-144">**Host** and **Path**</span></span> | <span data-ttu-id="3ff21-145">Volledige URL-pad dat wordt opgeroepen door Hallo gateway toodetermine Hallo toepassingsstatus van het Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3ff21-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="3ff21-146">Als u een http://contoso.com/ website hebt en vervolgens de aangepaste test Hallo kan worden geconfigureerd voor controleert 'http://contoso.com/path/custompath.htm' voor de test toohave geslaagde HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="3ff21-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="3ff21-147">**Interval**</span><span class="sxs-lookup"><span data-stu-id="3ff21-147">**Interval**</span></span> | <span data-ttu-id="3ff21-148">Hiermee configureert u Hallo test interval controles in seconden.</span><span class="sxs-lookup"><span data-stu-id="3ff21-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="3ff21-149">**Time-out**</span><span class="sxs-lookup"><span data-stu-id="3ff21-149">**Timeout**</span></span> | <span data-ttu-id="3ff21-150">Hiermee definieert u Hallo test time-outwaarde voor de controle van een HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="3ff21-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="3ff21-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="3ff21-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="3ff21-152">aantal mislukte HTTP-antwoorden Hallo nodig tooflag Hallo backend-exemplaar als *slecht*.</span><span class="sxs-lookup"><span data-stu-id="3ff21-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="3ff21-153">naam van de test Hello wordt verwezen in Hallo \<BackendHttpSettings\> configuratie tooassign welke back-end-pool aangepaste test-instellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3ff21-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="3ff21-154">Een aangepaste test tooan bestaande toepassingsgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ff21-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="3ff21-155">Veranderende Hallo huidige configuratie van een toepassingsgateway zijn drie stappen vereist: ophalen van huidige XML-configuratiebestand hello, toohave een aangepaste test wijzigen en Hallo-toepassingsgateway met Hallo nieuwe XML-instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="3ff21-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="3ff21-156">Hallo XML-bestand ophalen met behulp van `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="3ff21-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3ff21-157">Deze cmdlet uitvoer Hallo configuration XML toobe gewijzigd tooadd testinstelling.</span><span class="sxs-lookup"><span data-stu-id="3ff21-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="3ff21-158">Hallo XML-bestand openen in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="3ff21-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="3ff21-159">Voeg een `<probe>` sectie na `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="3ff21-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="3ff21-160">Voeg in Hallo backendHttpSettings sectie Hallo XML Hallo test naam zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="3ff21-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="3ff21-161">Hallo XML-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="3ff21-161">Save hello XML file.</span></span>

1. <span data-ttu-id="3ff21-162">Update Hallo toepassingsgateway configuratie met Hallo nieuwe XML-bestand met behulp van `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="3ff21-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3ff21-163">Deze cmdlet werkt uw toepassingsgateway met een nieuwe configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="3ff21-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="3ff21-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3ff21-164">Next steps</span></span>

<span data-ttu-id="3ff21-165">Als u tooconfigure Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="3ff21-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="3ff21-166">Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="3ff21-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

