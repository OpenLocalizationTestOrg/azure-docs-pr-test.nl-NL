---
title: Maken van een aangepaste test - Azure Application Gateway - PowerShell-klassiek | Microsoft Docs
description: Informatie over het maken van een aangepaste test voor Application Gateway met behulp van PowerShell in het klassieke implementatiemodel
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="a121f-103">Maak een aangepaste test voor Azure Application Gateway (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="a121f-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a121f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a121f-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="a121f-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a121f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="a121f-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="a121f-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="a121f-107">In dit artikel kunt u een aangepaste test toevoegen aan een bestaande application gateway met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a121f-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="a121f-108">Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op de standaardwebtoepassing geen bieden.</span><span class="sxs-lookup"><span data-stu-id="a121f-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a121f-109">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a121f-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a121f-110">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a121f-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a121f-111">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a121f-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a121f-112">Lees [meer informatie over het uitvoeren van deze stappen met het Resource Manager-model](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a121f-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="a121f-113">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="a121f-113">Create an application gateway</span></span>

<span data-ttu-id="a121f-114">Ga als volgt te werk om een toepassingsgateway te maken:</span><span class="sxs-lookup"><span data-stu-id="a121f-114">To create an application gateway:</span></span>

1. <span data-ttu-id="a121f-115">Maak een toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="a121f-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="a121f-116">Maak een XML-configuratiebestand of een configuratieobject.</span><span class="sxs-lookup"><span data-stu-id="a121f-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="a121f-117">Voer de configuratie door voor de zojuist gemaakte toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="a121f-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="a121f-118">Een toepassingsgatewayresource maken met een aangepaste test</span><span class="sxs-lookup"><span data-stu-id="a121f-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="a121f-119">Gebruik de cmdlet `New-AzureApplicationGateway` en vervang de waarden door uw eigen waarden om een gateway te maken.</span><span class="sxs-lookup"><span data-stu-id="a121f-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="a121f-120">Er worden op dat moment nog geen kosten in rekening gebracht voor gebruik van de gateway.</span><span class="sxs-lookup"><span data-stu-id="a121f-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="a121f-121">De kosten zijn pas vanaf een latere stap van toepassing, wanneer de gateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a121f-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="a121f-122">In het volgende voorbeeld wordt een toepassingsgateway gemaakt met een virtueel netwerk met de naam testvnet1 en een subnet met de naam subnet-1.</span><span class="sxs-lookup"><span data-stu-id="a121f-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="a121f-123">Gebruik de cmdlet `Get-AzureApplicationGateway` om te controleren of de gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a121f-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="a121f-124">De standaardwaarde voor *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="a121f-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a121f-125">De standaardwaarde voor *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="a121f-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a121f-126">U kunt kiezen tussen een klein, middelgroot en groot.</span><span class="sxs-lookup"><span data-stu-id="a121f-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="a121f-127">*VirtualIPs* en *DnsName* zijn leeg, omdat de gateway nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="a121f-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="a121f-128">Deze waarden worden gemaakt nadat de gateway uitgevoerd is.</span><span class="sxs-lookup"><span data-stu-id="a121f-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="a121f-129">Een toepassingsgateway configureren met XML</span><span class="sxs-lookup"><span data-stu-id="a121f-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="a121f-130">In het volgende voorbeeld gebruikt u een XML-bestand om alle instellingen voor de toepassingsgateway te configureren en deze door te voeren voor de toepassingsgatewayresource.</span><span class="sxs-lookup"><span data-stu-id="a121f-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="a121f-131">Kopieer de volgende tekst naar Kladblok.</span><span class="sxs-lookup"><span data-stu-id="a121f-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="a121f-132">Bewerk de waarden tussen de haakjes voor de configuratie-items.</span><span class="sxs-lookup"><span data-stu-id="a121f-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="a121f-133">Sla het bestand op met de bestandsextensie .xml.</span><span class="sxs-lookup"><span data-stu-id="a121f-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="a121f-134">Het volgende voorbeeld ziet hoe u een configuratiebestand gebruiken om de toepassingsgateway taakverdeling van HTTP-verkeer via de openbare poort 80 en verzenden van netwerkverkeer naar de back-endpoort 80 tussen twee IP-adressen met behulp van een aangepaste test te stellen.</span><span class="sxs-lookup"><span data-stu-id="a121f-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a121f-135">Het protocolitem Http of Https is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="a121f-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="a121f-136">Een nieuwe configuratie-item \<Probe\> wordt toegevoegd aan het configureren van aangepaste tests.</span><span class="sxs-lookup"><span data-stu-id="a121f-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="a121f-137">De configuratieparameters zijn:</span><span class="sxs-lookup"><span data-stu-id="a121f-137">The configuration parameters are:</span></span>

|<span data-ttu-id="a121f-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="a121f-138">Parameter</span></span>|<span data-ttu-id="a121f-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a121f-139">Description</span></span>|
|---|---|
|<span data-ttu-id="a121f-140">**Naam**</span><span class="sxs-lookup"><span data-stu-id="a121f-140">**Name**</span></span> |<span data-ttu-id="a121f-141">De referentienaam voor aangepaste test.</span><span class="sxs-lookup"><span data-stu-id="a121f-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="a121f-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="a121f-142">* **Protocol**</span></span> | <span data-ttu-id="a121f-143">Protocol dat wordt gebruikt (mogelijke waarden zijn HTTP of HTTPS).</span><span class="sxs-lookup"><span data-stu-id="a121f-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="a121f-144">**Host** en **pad**</span><span class="sxs-lookup"><span data-stu-id="a121f-144">**Host** and **Path**</span></span> | <span data-ttu-id="a121f-145">Volledige URL-pad dat wordt opgeroepen door de toepassingsgateway de status van het exemplaar te bepalen.</span><span class="sxs-lookup"><span data-stu-id="a121f-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="a121f-146">Bijvoorbeeld, hebt u een website http://contoso.com/, kan vervolgens aangepaste test worden geconfigureerd voor 'http://contoso.com/path/custompath.htm' voor de controle te hebben van een geslaagde reactie van de HTTP-test.</span><span class="sxs-lookup"><span data-stu-id="a121f-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="a121f-147">**Interval**</span><span class="sxs-lookup"><span data-stu-id="a121f-147">**Interval**</span></span> | <span data-ttu-id="a121f-148">Hiermee configureert u de controles van de test-interval in seconden.</span><span class="sxs-lookup"><span data-stu-id="a121f-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="a121f-149">**Time-out**</span><span class="sxs-lookup"><span data-stu-id="a121f-149">**Timeout**</span></span> | <span data-ttu-id="a121f-150">Hiermee definieert u de test-time-outwaarde voor de controle van een HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="a121f-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="a121f-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="a121f-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="a121f-152">Het aantal mislukte HTTP-antwoorden die nodig zijn voor de back-end-instantie als vlag *slecht*.</span><span class="sxs-lookup"><span data-stu-id="a121f-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="a121f-153">Naam van de test wordt verwezen in de \<BackendHttpSettings\> configuratie om toe te wijzen welke back-end-adresgroep maakt gebruik van aangepaste test-instellingen.</span><span class="sxs-lookup"><span data-stu-id="a121f-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="a121f-154">Een aangepaste test toevoegen aan een bestaande application gateway</span><span class="sxs-lookup"><span data-stu-id="a121f-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="a121f-155">Wijzigen van de huidige configuratie van een toepassingsgateway drie stappen vereist: ophalen van het huidige XML-configuratiebestand, als u een aangepaste test wilt wijzigen en de toepassingsgateway configureren met de nieuwe XML-instellingen.</span><span class="sxs-lookup"><span data-stu-id="a121f-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="a121f-156">Ophalen van het XML-bestand met behulp van `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="a121f-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="a121f-157">Deze cmdlet exporteert u de configuratie-XML om toe te voegen testinstelling worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a121f-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="a121f-158">Open het XML-bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="a121f-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="a121f-159">Voeg een `<probe>` sectie na `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="a121f-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="a121f-160">Toevoegen in de sectie backendHttpSettings van de XML-naam van de test zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a121f-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="a121f-161">Sla het XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="a121f-161">Save the XML file.</span></span>

1. <span data-ttu-id="a121f-162">De configuratie van de application gateway met het nieuwe XML-bestand bijwerken met behulp van `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="a121f-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="a121f-163">Deze cmdlet werkt de toepassingsgateway van uw met de nieuwe configuratie.</span><span class="sxs-lookup"><span data-stu-id="a121f-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="a121f-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a121f-164">Next steps</span></span>

<span data-ttu-id="a121f-165">Als u configureren van Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a121f-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a121f-166">Als u een toepassingsgateway wilt configureren voor gebruik met een interne load balancer, raadpleegt u [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Een toepassingsgateway met een interne load balancer (ILB) maken).</span><span class="sxs-lookup"><span data-stu-id="a121f-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

