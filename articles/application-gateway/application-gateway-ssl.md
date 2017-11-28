---
title: aaaConfigure SSL-offload - Azure Application Gateway - PowerShell-klassiek | Microsoft Docs
description: In dit artikel bevat instructies toocreate een toepassingsgateway met SSL-offload met behulp van hello Azure klassieke implementatiemodel.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="32907-103">Een toepassingsgateway voor SSL-offload configureren met behulp van het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="32907-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="32907-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="32907-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="32907-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="32907-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="32907-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="32907-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="32907-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="32907-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="32907-108">Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm.</span><span class="sxs-lookup"><span data-stu-id="32907-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="32907-109">SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="32907-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32907-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="32907-110">Before you begin</span></span>

1. <span data-ttu-id="32907-111">Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="32907-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="32907-112">U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="32907-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="32907-113">Controleer of u een werkend virtueel netwerk hebt met een geldig subnet.</span><span class="sxs-lookup"><span data-stu-id="32907-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="32907-114">Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn.</span><span class="sxs-lookup"><span data-stu-id="32907-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="32907-115">Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.</span><span class="sxs-lookup"><span data-stu-id="32907-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="32907-116">Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="32907-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="32907-117">tooconfigure SSL offload op een toepassingsgateway, Hallo stappen te volgen in Hallo volgorde:</span><span class="sxs-lookup"><span data-stu-id="32907-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="32907-118">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="32907-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="32907-119">SSL-certificaten uploaden</span><span class="sxs-lookup"><span data-stu-id="32907-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="32907-120">Hallo-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="32907-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="32907-121">De configuratie van een set Hallo-gateway</span><span class="sxs-lookup"><span data-stu-id="32907-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="32907-122">Hallo gateway starten</span><span class="sxs-lookup"><span data-stu-id="32907-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="32907-123">Controleer of de status van de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="32907-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="32907-124">Een toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="32907-124">Create an application gateway</span></span>

<span data-ttu-id="32907-125">Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="32907-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="32907-126">Facturering voor Hallo-gateway op dit moment niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="32907-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="32907-127">Facturering begint met een latere stap Hallo gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="32907-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="32907-128">toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32907-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="32907-129">In voorbeeld Hallo *beschrijving*, *InstanceCount*, en *GatewaySize* zijn optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="32907-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="32907-130">de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="32907-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="32907-131">de standaardwaarde voor Hallo *GatewaySize* is normaal.</span><span class="sxs-lookup"><span data-stu-id="32907-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="32907-132">Kleine en grote andere beschikbare waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="32907-132">Small and Large are other available values.</span></span> <span data-ttu-id="32907-133">*VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="32907-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="32907-134">Deze waarden worden gemaakt nadat Hallo gateway Hallo status actief is.</span><span class="sxs-lookup"><span data-stu-id="32907-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="32907-135">SSL-certificaten uploaden</span><span class="sxs-lookup"><span data-stu-id="32907-135">Upload SSL certificates</span></span>

<span data-ttu-id="32907-136">Gebruik `Add-AzureApplicationGatewaySslCertificate` tooupload Hallo-servercertificaat in *pfx* indeling toohello toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="32907-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="32907-137">Hallo certificaatnaam is de naam van een gebruiker zijn gekozen en moet uniek zijn binnen de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="32907-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="32907-138">Dit certificaat is waarnaar wordt verwezen tooby deze naam in alle certificaat beheerbewerkingen op Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="32907-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="32907-139">Deze volgende voorbeeld toont Hallo-cmdlet Hallo-waarden in Hallo voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="32907-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="32907-140">Vervolgens valideren Hallo-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="32907-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="32907-141">Gebruik Hallo `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32907-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="32907-142">Dit voorbeeld toont Hallo cmdlet op de eerste regel hello, gevolgd door Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="32907-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="32907-143">Hallo certificaatwachtwoord heeft toobe tussen 4 too12 tekens, letters of cijfers.</span><span class="sxs-lookup"><span data-stu-id="32907-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="32907-144">Speciale tekens worden niet geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="32907-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="32907-145">Hallo-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="32907-145">Configure hello gateway</span></span>

<span data-ttu-id="32907-146">Een toepassingsgateway configuratie bestaat uit meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="32907-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="32907-147">Hallo-waarden kunnen worden gekoppeld samen tooconstruct Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="32907-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="32907-148">Hallo-waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="32907-148">hello values are:</span></span>

* <span data-ttu-id="32907-149">**Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="32907-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="32907-150">Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.</span><span class="sxs-lookup"><span data-stu-id="32907-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="32907-151">**Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit.</span><span class="sxs-lookup"><span data-stu-id="32907-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="32907-152">Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="32907-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="32907-153">**Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="32907-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="32907-154">Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.</span><span class="sxs-lookup"><span data-stu-id="32907-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="32907-155">**Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).</span><span class="sxs-lookup"><span data-stu-id="32907-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="32907-156">**Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt.</span><span class="sxs-lookup"><span data-stu-id="32907-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="32907-157">Op dit moment alleen Hallo *basic* regel wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="32907-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="32907-158">Hallo *basic* regel is round-robinbelastingverdeling.</span><span class="sxs-lookup"><span data-stu-id="32907-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="32907-159">**Aanvullende configuratieopmerkingen**</span><span class="sxs-lookup"><span data-stu-id="32907-159">**Additional configuration notes**</span></span>

<span data-ttu-id="32907-160">Hallo-protocol in voor de configuratie van SSL-certificaten, **HttpListener** moet ook wijzigen*Https* (hoofdlettergevoelig).</span><span class="sxs-lookup"><span data-stu-id="32907-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="32907-161">Hallo **SslCert** element te toegevoegd**HttpListener** Hello waarde ingesteld toohello dezelfde naam als in Hallo laden van de voorgaande sectie voor SSL-certificaten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32907-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="32907-162">Hallo front-endpoort moet bijgewerkte too443.</span><span class="sxs-lookup"><span data-stu-id="32907-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="32907-163">**tooenable cookies gebaseerde affiniteit**: een application gateway kan worden geconfigureerd tooensure is een aanvraag van een clientsessie altijd gerichte toohello dezelfde virtuele machine in de webfarm Hallo.</span><span class="sxs-lookup"><span data-stu-id="32907-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="32907-164">Dit scenario wordt gedaan door het injecteren van een sessiecookie waarmee Hallo gateway toodirect verkeer op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="32907-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="32907-165">tooenable cookies gebaseerde affiniteit ingesteld **CookieBasedAffinity** te*ingeschakeld* in Hallo **BackendHttpSettings** element.</span><span class="sxs-lookup"><span data-stu-id="32907-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="32907-166">U kunt de configuratie maken door het maken van een configuratieobject of met behulp van een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="32907-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="32907-167">uw configuratie met behulp van een configuratie-XML-bestand, gebruikt u tooconstruct Hallo volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="32907-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="32907-168">**Configuratie-XML-voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="32907-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="32907-169">De configuratie van een set Hallo-gateway</span><span class="sxs-lookup"><span data-stu-id="32907-169">Set hello gateway configuration</span></span>

<span data-ttu-id="32907-170">Vervolgens stelt u de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="32907-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="32907-171">U kunt Hallo `Set-AzureApplicationGatewayConfig` cmdlet met een configuratieobject of met een XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="32907-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="32907-172">Hallo gateway starten</span><span class="sxs-lookup"><span data-stu-id="32907-172">Start hello gateway</span></span>

<span data-ttu-id="32907-173">Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="32907-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="32907-174">Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart.</span><span class="sxs-lookup"><span data-stu-id="32907-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="32907-175">Hallo `Start-AzureApplicationGateway` cmdlet toofinish too15-20 minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="32907-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="32907-176">Controleer of de status van de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="32907-176">Verify hello gateway status</span></span>

<span data-ttu-id="32907-177">Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="32907-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="32907-178">Als `Start-AzureApplicationGateway` is voltooid in de vorige stap Hallo *status* moet worden uitgevoerd, en *VirtualIPs* en *DnsName* geldige waarden.</span><span class="sxs-lookup"><span data-stu-id="32907-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="32907-179">Dit voorbeeld wordt een application gateway die wordt weergegeven, wordt uitgevoerd, en is klaar tootake verkeer.</span><span class="sxs-lookup"><span data-stu-id="32907-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="32907-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32907-180">Next steps</span></span>

<span data-ttu-id="32907-181">Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="32907-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="32907-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="32907-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="32907-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="32907-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

