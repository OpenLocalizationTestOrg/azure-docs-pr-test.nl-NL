---
title: aaaConfigure Load Balancer-distributie modus | Microsoft Docs
description: Hoe tooconfigure Azure load balancer distributie modus toosupport bron-IP-affiniteit
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="d6615-103">Hallo distributie modus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d6615-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="d6615-104">Distributiepunten in de hash-modus</span><span class="sxs-lookup"><span data-stu-id="d6615-104">Hash-based distribution mode</span></span>

<span data-ttu-id="d6615-105">Hallo standaard distributie-algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash-toomap verkeer tooavailable servers.</span><span class="sxs-lookup"><span data-stu-id="d6615-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="d6615-106">Het biedt gebruikerspad alleen een transportsessie.</span><span class="sxs-lookup"><span data-stu-id="d6615-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="d6615-107">Pakketten in dezelfde sessie worden Hallo omgeleid toohello dezelfde datacenter IP (DIP) achter Hallo taakverdeling endpoint-instantie.</span><span class="sxs-lookup"><span data-stu-id="d6615-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="d6615-108">Als Hallo client start een nieuwe sessie van Hallo dezelfde bron-IP, bronpoort Hallo wijzigingen en zorgt ervoor dat Hallo verkeer toogo tooa ander DIP eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d6615-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![hash op basis van load balancer](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="d6615-110">Afbeelding 1-5-tuple distributie</span><span class="sxs-lookup"><span data-stu-id="d6615-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="d6615-111">Affiniteitsmodus voor IP-bron</span><span class="sxs-lookup"><span data-stu-id="d6615-111">Source IP affinity mode</span></span>

<span data-ttu-id="d6615-112">We hebben een ander distributiepunt installatiemodus bron-IP-affiniteit (ook wel bekend als sessie affiniteit of IP-clientaffiniteit).</span><span class="sxs-lookup"><span data-stu-id="d6615-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="d6615-113">Azure Load Balancer kan geconfigureerde toouse 2-tuple (bron-IP, doel-IP) of 3-tuple (bron-IP, doel-IP, Protocol) toomap verkeer toohello beschikbare servers.</span><span class="sxs-lookup"><span data-stu-id="d6615-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="d6615-114">Met behulp van de bron-IP-affiniteit verbindingen geïnitieerd vanaf Hallo dezelfde clientcomputer gaat toohello hetzelfde DIP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d6615-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="d6615-115">Hallo volgende diagram ziet u een configuratie met 2-tuple.</span><span class="sxs-lookup"><span data-stu-id="d6615-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="d6615-116">U ziet hoe Hallo 2-tuple via Hallo load balancer toovirtual machine 1 (VM1) die vervolgens back-up door VM2 en VM3 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d6615-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![sessie-affiniteit](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="d6615-118">Afbeelding 2-2-tuple distributie</span><span class="sxs-lookup"><span data-stu-id="d6615-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="d6615-119">Bron-IP-affiniteit is opgelost incompatibiliteit tussen hello Azure Load Balancer en extern bureaublad (RD)-Gateway.</span><span class="sxs-lookup"><span data-stu-id="d6615-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="d6615-120">U kunt nu een farm RD-gateway in een enkel cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="d6615-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="d6615-121">Voorbeeldscenario voor een andere gebruik is media uploaden waar Hallo gegevens uploaden gebeurt via UDP, maar Hallo besturingselement vlak wordt geregeld via TCP:</span><span class="sxs-lookup"><span data-stu-id="d6615-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="d6615-122">Een client eerst een openbaar adres met gelijke taakverdeling toohello TCP-sessie start, gerichte tooa specifieke DIP, dit kanaal is de status van de verbinding Hallo links active toomonitor opgehaald</span><span class="sxs-lookup"><span data-stu-id="d6615-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="d6615-123">Een nieuwe sessie UDP van Hallo dezelfde clientcomputer wordt geïnitieerd toohello dezelfde taakverdeling openbaar eindpunt, hier Hallo verwachting dat deze verbinding ook gerichte toohello dezelfde DIP eindpunt als Hallo vorige TCP-verbinding zodat media uploaden mag uitgevoerd op maximale doorvoer en tegelijkertijd ook een besturingskanaal via TCP.</span><span class="sxs-lookup"><span data-stu-id="d6615-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="d6615-124">Wanneer een set met gelijke taakverdeling wordt gewijzigd (verwijderen of toevoegen van een virtuele machine), worden de Hallo distributie van clientaanvragen herberekend.</span><span class="sxs-lookup"><span data-stu-id="d6615-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="d6615-125">U kan niet afhankelijk zijn van de nieuwe verbindingen van bestaande clients loopt op Hallo dezelfde server.</span><span class="sxs-lookup"><span data-stu-id="d6615-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="d6615-126">Bovendien met behulp van de bron-IP affiniteitsmodus voor verdeling kan leiden tot een ongelijke distributie van verkeer.</span><span class="sxs-lookup"><span data-stu-id="d6615-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="d6615-127">Clients met achter proxy's kunnen worden gezien als een unieke client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6615-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="d6615-128">Configureren affiniteit van bron-IP-instellingen voor de load balancer</span><span class="sxs-lookup"><span data-stu-id="d6615-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="d6615-129">Voor virtuele machines, kunt u PowerShell toochange time-outinstellingen:</span><span class="sxs-lookup"><span data-stu-id="d6615-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="d6615-130">Toevoegen van een Azure-eindpunt tooa virtuele Machine en het instellen van de load balancer-distributie-modus</span><span class="sxs-lookup"><span data-stu-id="d6615-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="d6615-131">LoadBalancerDistribution kan toosourceIP voor 2-tuple (bron-IP, doel-IP) voor de load balancer, sourceIPProtocol voor taakverdeling van 3-tuple (bron-IP, doel-IP, protocol) of none als u wilt dat de standaardgedrag Hallo van 5-tuple taakverdeling worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d6615-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="d6615-132">Gebruik Hallo tooretrieve een load balancer distributie modus eindpuntconfiguratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6615-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

<span data-ttu-id="d6615-133">Als Hallo LoadBalancerDistribution element niet aanwezig is gebruikt hello Azure Load balancer Hallo standaard 5-tuple algoritme.</span><span class="sxs-lookup"><span data-stu-id="d6615-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="d6615-134">Hallo distributie modus instellen op een set met gelijke taakverdeling eindpunt</span><span class="sxs-lookup"><span data-stu-id="d6615-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="d6615-135">Als eindpunten deel van een set met gelijke taakverdeling eindpunt uitmaken, moet Hallo distributie modus worden ingesteld op Hallo eindpuntset met gelijke taakverdeling:</span><span class="sxs-lookup"><span data-stu-id="d6615-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="d6615-136">Cloud Service toochange distributie configuratiemodus</span><span class="sxs-lookup"><span data-stu-id="d6615-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="d6615-137">U kunt gebruikmaken van hello Azure SDK voor .NET 2.5 (toobe uitgebracht in November) tooupdate uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="d6615-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="d6615-138">Instellingen voor endpoint voor Cloudservices zijn aangebracht in Hallo csdef.</span><span class="sxs-lookup"><span data-stu-id="d6615-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="d6615-139">De upgrade van een implementatie is in de volgorde tooupdate Hallo load balancer distributie-modus voor een Cloud Services-implementatie vereist.</span><span class="sxs-lookup"><span data-stu-id="d6615-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="d6615-140">Hier volgt een voorbeeld van wijzigingen voor eindpuntinstellingen csdef:</span><span class="sxs-lookup"><span data-stu-id="d6615-140">Here is an example of .csdef changes for endpoint settings:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a><span data-ttu-id="d6615-141">API-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d6615-141">API example</span></span>

<span data-ttu-id="d6615-142">U kunt Hallo load balancer distributie op basis van de API voor servicebeheer Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="d6615-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="d6615-143">Zorg ervoor dat tooadd hello `x-ms-version` header is ingesteld tooversion `2014-09-01` of hoger.</span><span class="sxs-lookup"><span data-stu-id="d6615-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="d6615-144">Configuratie van de update Hallo Hallo opgegeven set met gelijke taakverdeling in een implementatie</span><span class="sxs-lookup"><span data-stu-id="d6615-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="d6615-145">Voorbeeld van de aanvraag</span><span class="sxs-lookup"><span data-stu-id="d6615-145">Request example</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

<span data-ttu-id="d6615-146">Hallo-waarden voor LoadBalancerDistribution zijn sourceIP voor affiniteit tussen de 2-tuple, sourceIPProtocol voor affiniteit tussen de 3-tuple of none (voor geen relatie.</span><span class="sxs-lookup"><span data-stu-id="d6615-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="d6615-147">dat wil zeggen 5-tuple)</span><span class="sxs-lookup"><span data-stu-id="d6615-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="d6615-148">Antwoord</span><span class="sxs-lookup"><span data-stu-id="d6615-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="d6615-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6615-149">Next Steps</span></span>

[<span data-ttu-id="d6615-150">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="d6615-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="d6615-151">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="d6615-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d6615-152">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d6615-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
