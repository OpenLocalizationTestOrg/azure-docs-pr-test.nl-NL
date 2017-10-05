---
title: Time-out bij inactiviteit voor Load Balancer TCP configureren | Microsoft Docs
description: Time-out bij inactiviteit voor Load Balancer TCP configureren
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="867d2-103">TCP-time-out voor inactiviteit instellingen configureren voor Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="867d2-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="867d2-104">In de standaardconfiguratie heeft Azure Load Balancer een instelling voor time-out voor inactiviteit van vier minuten.</span><span class="sxs-lookup"><span data-stu-id="867d2-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="867d2-105">Als een periode van inactiviteit langer dan de time-outwaarde is, is er geen garantie dat de TCP- of HTTP-sessie wordt onderhouden tussen de client en de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="867d2-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="867d2-106">Wanneer de verbinding is gesloten, wordt de clienttoepassing het volgende foutbericht weergegeven: ' de onderliggende verbinding is gesloten: een verbinding waarvan wordt verwacht dat worden behouden door de server is gesloten. "</span><span class="sxs-lookup"><span data-stu-id="867d2-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="867d2-107">Vaak is het gebruik van een TCP-keepalive.</span><span class="sxs-lookup"><span data-stu-id="867d2-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="867d2-108">Hierdoor blijft de verbinding actief voor een langere periode.</span><span class="sxs-lookup"><span data-stu-id="867d2-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="867d2-109">Zie voor meer informatie deze [voorbeelden .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="867d2-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="867d2-110">Met keep-alive is ingeschakeld, pakketten worden verzonden tijdens perioden van inactiviteit op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="867d2-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="867d2-111">Deze keepalive-pakketten Zorg dat de waarde voor time-out voor inactiviteit nooit bereikt is en gedurende een lange periode wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="867d2-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="867d2-112">Deze instelling is geschikt voor binnenkomende verbindingen alleen.</span><span class="sxs-lookup"><span data-stu-id="867d2-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="867d2-113">Om te voorkomen dat de verbinding verloren gaan, moet u de TCP-keepalive configureren met een interval van minder dan de instelling voor time-out voor inactiviteit of verhoog de waarde voor time-out voor inactiviteit.</span><span class="sxs-lookup"><span data-stu-id="867d2-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="867d2-114">Toegevoegd ter ondersteuning van dergelijke scenario's, ondersteuning voor een configureerbare time-out voor inactiviteit.</span><span class="sxs-lookup"><span data-stu-id="867d2-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="867d2-115">U kunt het nu instellen voor een duur van 4 tot en met 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="867d2-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="867d2-116">TCP-keepalive geschikt is voor scenario's waarin batterij niet een beperking.</span><span class="sxs-lookup"><span data-stu-id="867d2-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="867d2-117">Dit wordt niet aanbevolen voor mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="867d2-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="867d2-118">Met een TCP-keepalive in een mobiele toepassing kan de accu raakt door apparaat sneller.</span><span class="sxs-lookup"><span data-stu-id="867d2-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![TCP-time](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="867d2-120">De volgende secties wordt beschreven hoe wijzig de instellingen van de time-out voor inactiviteit in virtuele machines en cloudservices.</span><span class="sxs-lookup"><span data-stu-id="867d2-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="867d2-121">De TCP-time configureren voor uw openbare IP op exemplaarniveau tot 15 minuten</span><span class="sxs-lookup"><span data-stu-id="867d2-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="867d2-122">`IdleTimeoutInMinutes` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="867d2-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="867d2-123">Als deze niet is ingesteld, wordt de standaardtime-out vier minuten.</span><span class="sxs-lookup"><span data-stu-id="867d2-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="867d2-124">Het bereik van acceptabele time-out is 4 tot en met 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="867d2-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="867d2-125">De time-out voor inactiviteit ingesteld bij het maken van een Azure-eindpunt op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="867d2-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="867d2-126">Als u wilt wijzigen van de instelling voor time-out voor een eindpunt, gebruikt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="867d2-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="867d2-127">Gebruik de volgende opdracht voor het ophalen van de time-out voor inactiviteit-configuratie:</span><span class="sxs-lookup"><span data-stu-id="867d2-127">To retrieve your idle timeout configuration, use the following command:</span></span>

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="867d2-128">De TCP-out instellen op een eindpuntset met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="867d2-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="867d2-129">Als eindpunten deel van een eindpuntset met gelijke taakverdeling uitmaken, kan de TCP-out moet worden ingesteld op de eindpuntset met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="867d2-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="867d2-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="867d2-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="867d2-131">Time-outinstellingen voor cloudservices wijzigen</span><span class="sxs-lookup"><span data-stu-id="867d2-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="867d2-132">U kunt de Azure SDK gebruiken om bij te werken van uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="867d2-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="867d2-133">U eindpuntinstellingen voor cloudservices in het csdef-bestand.</span><span class="sxs-lookup"><span data-stu-id="867d2-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="867d2-134">Bijwerken van de TCP-out voor de implementatie van een cloudservice, moet een upgrade van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="867d2-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="867d2-135">Een uitzondering hierop is als de time-out voor de TCP-alleen voor een openbaar IP-adres is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="867d2-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="867d2-136">Openbare IP-instellingen zijn in het .cscfg-bestand en u die kunt bijwerken via de implementatie-update en de upgrade.</span><span class="sxs-lookup"><span data-stu-id="867d2-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="867d2-137">De wijzigingen csdef voor eindpuntinstellingen zijn:</span><span class="sxs-lookup"><span data-stu-id="867d2-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="867d2-138">De wijzigingen cscfg-bestand voor de instelling voor de time-out voor openbare IP-adressen zijn:</span><span class="sxs-lookup"><span data-stu-id="867d2-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a><span data-ttu-id="867d2-139">REST-API-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="867d2-139">REST API example</span></span>

<span data-ttu-id="867d2-140">U kunt de time-out voor inactiviteit TCP configureren met behulp van de servicebeheer-API.</span><span class="sxs-lookup"><span data-stu-id="867d2-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="867d2-141">Zorg ervoor dat de `x-ms-version` header is ingesteld op versie `2014-06-01` of hoger.</span><span class="sxs-lookup"><span data-stu-id="867d2-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="867d2-142">Werk de configuratie van de opgegeven taakverdeling invoer-eindpunten op alle virtuele machines in een implementatie.</span><span class="sxs-lookup"><span data-stu-id="867d2-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="867d2-143">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="867d2-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="867d2-144">Antwoord</span><span class="sxs-lookup"><span data-stu-id="867d2-144">Response</span></span>

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a><span data-ttu-id="867d2-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="867d2-145">Next steps</span></span>

[<span data-ttu-id="867d2-146">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="867d2-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="867d2-147">Configureren van een Internet gerichte load balancer aan de slag</span><span class="sxs-lookup"><span data-stu-id="867d2-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="867d2-148">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="867d2-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
