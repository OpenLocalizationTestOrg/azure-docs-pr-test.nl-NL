---
title: aaaConfigure Load Balancer TCP time-out bij inactiviteit voor | Microsoft Docs
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
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="e2873-103">TCP-time-out voor inactiviteit instellingen configureren voor Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e2873-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="e2873-104">In de standaardconfiguratie heeft Azure Load Balancer een instelling voor time-out voor inactiviteit van vier minuten.</span><span class="sxs-lookup"><span data-stu-id="e2873-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="e2873-105">Als een periode van inactiviteit langer dan de time-outwaarde hello is, er is geen garantie dat Hallo TCP of HTTP-sessie wordt onderhouden tussen Hallo-client en de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e2873-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="e2873-106">Wanneer Hallo verbinding is gesloten, wordt de clienttoepassing Hallo volgende foutbericht weergegeven: ' hello onderliggende verbinding is gesloten: een verbinding waarvan wordt verwacht in stand gehouden toobe is gesloten door Hallo-server. '</span><span class="sxs-lookup"><span data-stu-id="e2873-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="e2873-107">Een gebruikelijk is toouse een keep-alive TCP.</span><span class="sxs-lookup"><span data-stu-id="e2873-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="e2873-108">Hierdoor blijft Hallo verbinding actief voor een langere periode.</span><span class="sxs-lookup"><span data-stu-id="e2873-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="e2873-109">Zie voor meer informatie deze [voorbeelden .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2873-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="e2873-110">Met keep-alive is ingeschakeld, pakketten worden verzonden tijdens perioden van inactiviteit op Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="e2873-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="e2873-111">Deze keepalive-pakketten Zorg dat Hallo inactief time-outwaarde nooit bereikt is en hello wordt bijgehouden voor een lange periode.</span><span class="sxs-lookup"><span data-stu-id="e2873-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="e2873-112">Deze instelling is geschikt voor binnenkomende verbindingen alleen.</span><span class="sxs-lookup"><span data-stu-id="e2873-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="e2873-113">tooavoid overdragende Hallo verbinding, moet u Hallo TCP keepalive-configureren met een interval dat kleiner is dan Hallo time-out voor inactiviteit instelling of vergroot Hallo waarde time-out voor inactiviteit.</span><span class="sxs-lookup"><span data-stu-id="e2873-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="e2873-114">toosupport dergelijke scenario's, ondersteuning voor een configureerbare time-out voor inactiviteit toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e2873-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="e2873-115">U kunt het nu instellen voor een duur van 4 too30 minuten.</span><span class="sxs-lookup"><span data-stu-id="e2873-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="e2873-116">TCP-keepalive geschikt is voor scenario's waarin batterij niet een beperking.</span><span class="sxs-lookup"><span data-stu-id="e2873-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="e2873-117">Dit wordt niet aanbevolen voor mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e2873-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="e2873-118">Met een TCP-keepalive in een mobiele toepassing kunt verwijderen uit de Hallo apparaat accu sneller.</span><span class="sxs-lookup"><span data-stu-id="e2873-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![TCP-time](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="e2873-120">Hallo volgende secties wordt beschreven hoe toochange inactief time-outinstellingen in virtuele machines en cloudservices.</span><span class="sxs-lookup"><span data-stu-id="e2873-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="e2873-121">Hallo TCP-time configureren voor uw instantieniveau openbare IP-too15 minuten</span><span class="sxs-lookup"><span data-stu-id="e2873-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="e2873-122">`IdleTimeoutInMinutes` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e2873-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="e2873-123">Als deze niet is ingesteld, is Hallo standaardtime-out vier minuten.</span><span class="sxs-lookup"><span data-stu-id="e2873-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="e2873-124">Hallo time-out acceptabele bereik is 4 too30 minuten.</span><span class="sxs-lookup"><span data-stu-id="e2873-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="e2873-125">Time-out voor inactiviteit van Hallo ingesteld bij het maken van een Azure-eindpunt op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e2873-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="e2873-126">toochange Hallo time-out instellen voor een eindpunt, gebruikt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e2873-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="e2873-127">tooretrieve uw configuratie van de time-out voor inactiviteit, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2873-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="e2873-128">Hallo TCP-out instellen op een eindpuntset met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="e2873-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="e2873-129">Als eindpunten deel van een eindpuntset met gelijke taakverdeling uitmaken, moet TCP-time Hallo zijn ingesteld op Hallo taakverdeling eindpuntset.</span><span class="sxs-lookup"><span data-stu-id="e2873-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="e2873-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2873-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="e2873-131">Time-outinstellingen voor cloudservices wijzigen</span><span class="sxs-lookup"><span data-stu-id="e2873-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="e2873-132">U kunt uw cloudservice hello Azure SDK tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e2873-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="e2873-133">U eindpuntinstellingen voor cloudservices in Hallo csdef-bestand.</span><span class="sxs-lookup"><span data-stu-id="e2873-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="e2873-134">Hallo TCP-out voor de implementatie van een cloudservice bijwerken, moet een upgrade van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="e2873-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="e2873-135">Een uitzondering hierop is als Hallo TCP-time alleen voor een openbaar IP-adres is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e2873-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="e2873-136">Openbare IP-instellingen zijn in Hallo .cscfg-bestand en u die kunt bijwerken via de implementatie-update en de upgrade.</span><span class="sxs-lookup"><span data-stu-id="e2873-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="e2873-137">Hallo csdef wijzigingen voor eindpuntinstellingen zijn:</span><span class="sxs-lookup"><span data-stu-id="e2873-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="e2873-138">Hallo .cscfg wijzigingen voor de time-outinstelling Hallo op openbare IP-adressen zijn:</span><span class="sxs-lookup"><span data-stu-id="e2873-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="e2873-139">REST-API-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e2873-139">REST API example</span></span>

<span data-ttu-id="e2873-140">U kunt Hallo TCP time-out bij inactiviteit voor configureren met behulp van Hallo servicebeheer-API.</span><span class="sxs-lookup"><span data-stu-id="e2873-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="e2873-141">Zorg ervoor dat Hallo `x-ms-version` header is ingesteld tooversion `2014-06-01` of hoger.</span><span class="sxs-lookup"><span data-stu-id="e2873-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="e2873-142">Configuratie van de update Hallo Hallo opgegeven invoereindpunten taakverdeling op alle virtuele machines in een implementatie.</span><span class="sxs-lookup"><span data-stu-id="e2873-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="e2873-143">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="e2873-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="e2873-144">Antwoord</span><span class="sxs-lookup"><span data-stu-id="e2873-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e2873-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2873-145">Next steps</span></span>

[<span data-ttu-id="e2873-146">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="e2873-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="e2873-147">Configureren van een Internet gerichte load balancer aan de slag</span><span class="sxs-lookup"><span data-stu-id="e2873-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="e2873-148">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="e2873-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
