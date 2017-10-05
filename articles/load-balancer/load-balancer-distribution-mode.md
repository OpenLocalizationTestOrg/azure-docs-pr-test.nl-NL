---
title: Modus voor Load Balancer-distributie configureren | Microsoft Docs
description: Het configureren van Azure load balancer distributie modus om ondersteuning voor affiniteit tussen bron-IP
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="63b98-103">De distributie-modus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="63b98-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="63b98-104">Distributiepunten in de hash-modus</span><span class="sxs-lookup"><span data-stu-id="63b98-104">Hash-based distribution mode</span></span>

<span data-ttu-id="63b98-105">De standaard distributie-algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash verkeer toewijzen aan beschikbare servers.</span><span class="sxs-lookup"><span data-stu-id="63b98-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="63b98-106">Het biedt gebruikerspad alleen een transportsessie.</span><span class="sxs-lookup"><span data-stu-id="63b98-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="63b98-107">Pakketten in dezelfde sessie wordt doorgestuurd naar het hetzelfde exemplaar van datacenter IP (DIP) achter het eindpunt van de taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="63b98-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="63b98-108">Wanneer de client wordt gestart van een nieuwe sessie van dezelfde bron-IP, wordt de bronpoort wijzigt en zorgt ervoor dat het verkeer naar een ander DIP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="63b98-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![hash op basis van load balancer](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="63b98-110">Afbeelding 1-5-tuple distributie</span><span class="sxs-lookup"><span data-stu-id="63b98-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="63b98-111">Affiniteitsmodus voor IP-bron</span><span class="sxs-lookup"><span data-stu-id="63b98-111">Source IP affinity mode</span></span>

<span data-ttu-id="63b98-112">We hebben een ander distributiepunt installatiemodus bron-IP-affiniteit (ook wel bekend als sessie affiniteit of IP-clientaffiniteit).</span><span class="sxs-lookup"><span data-stu-id="63b98-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="63b98-113">Azure Load Balancer kan worden geconfigureerd voor het gebruik van een 2-tuple (bron-IP, doel-IP) of 3-tuple (bron-IP, doel-IP, Protocol) verkeer toewijzen aan de beschikbare servers.</span><span class="sxs-lookup"><span data-stu-id="63b98-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="63b98-114">Met behulp van de bron-IP-affiniteit verbindingen geïnitieerd door dezelfde clientcomputer gaat naar hetzelfde DIP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="63b98-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="63b98-115">Het volgende diagram ziet u een configuratie met 2-tuple.</span><span class="sxs-lookup"><span data-stu-id="63b98-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="63b98-116">U ziet hoe de 2-tuple via de load balancer voor virtuele machine, 1 (VM1) die vervolgens back-up door VM2 en VM3 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63b98-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![sessie-affiniteit](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="63b98-118">Afbeelding 2-2-tuple distributie</span><span class="sxs-lookup"><span data-stu-id="63b98-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="63b98-119">Bron-IP-affiniteit is opgelost incompatibiliteit tussen de Load Balancer van Azure en de Gateway van de extern bureaublad (RD).</span><span class="sxs-lookup"><span data-stu-id="63b98-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="63b98-120">U kunt nu een farm RD-gateway in een enkel cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="63b98-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="63b98-121">Voorbeeldscenario voor een andere gebruik is media uploaden waar het uploaden van gegevens gebeurt via UDP, maar het besturingselement vlak wordt geregeld via TCP:</span><span class="sxs-lookup"><span data-stu-id="63b98-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="63b98-122">Een client eerst een TCP-sessie in het openbare adres van de taakverdeling initieert, wordt omgeleid naar een specifieke DIP dit kanaal blijft aanwezig voor het bewaken van de status van de verbinding</span><span class="sxs-lookup"><span data-stu-id="63b98-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="63b98-123">Een nieuwe sessie UDP van dezelfde clientcomputer aan hetzelfde taakverdeling openbaar eindpunt wordt gestart, wordt hier de verwachting is dat deze verbinding, ook wordt omgeleid naar hetzelfde DIP eindpunt, zoals de vorige TCP-verbinding zodat media uploaden kan worden uitgevoerd op hoog de doorvoer en tegelijkertijd ook een besturingskanaal via TCP.</span><span class="sxs-lookup"><span data-stu-id="63b98-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="63b98-124">Wanneer een set met gelijke taakverdeling wordt gewijzigd (een virtuele machine toevoegen of verwijderen), de distributie van aanvragen van clients opnieuw berekend.</span><span class="sxs-lookup"><span data-stu-id="63b98-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="63b98-125">U kunt geen afhankelijk van nieuwe verbindingen van bestaande clients op dezelfde server loopt.</span><span class="sxs-lookup"><span data-stu-id="63b98-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="63b98-126">Bovendien met behulp van de bron-IP affiniteitsmodus voor verdeling kan leiden tot een ongelijke distributie van verkeer.</span><span class="sxs-lookup"><span data-stu-id="63b98-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="63b98-127">Clients met achter proxy's kunnen worden gezien als een unieke client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="63b98-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="63b98-128">Configureren affiniteit van bron-IP-instellingen voor de load balancer</span><span class="sxs-lookup"><span data-stu-id="63b98-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="63b98-129">Voor virtuele machines, kunt u PowerShell time-out-instellingen te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="63b98-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="63b98-130">Een Azure-eindpunt toevoegen aan een virtuele Machine en load balancer distributie modus instellen</span><span class="sxs-lookup"><span data-stu-id="63b98-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="63b98-131">LoadBalancerDistribution kan worden ingesteld op sourceIP voor 2-tuple (bron-IP, doel-IP) voor de load balancer, sourceIPProtocol voor taakverdeling van 3-tuple (bron-IP, doel-IP, protocol) of none als u wilt dat het standaardgedrag van 5-tuple taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="63b98-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="63b98-132">Gebruik de volgende voor het ophalen van een load balancer distributie modus eindpuntconfiguratie:</span><span class="sxs-lookup"><span data-stu-id="63b98-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="63b98-133">Als de LoadBalancerDistribution-element niet aanwezig is gebruikt de 5-tuple standaardalgoritme met de Azure Load balancer.</span><span class="sxs-lookup"><span data-stu-id="63b98-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="63b98-134">De distributie-modus instellen op een set met gelijke taakverdeling eindpunt</span><span class="sxs-lookup"><span data-stu-id="63b98-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="63b98-135">Als eindpunten deel van een set met gelijke taakverdeling eindpunt uitmaken, moet u de distributie-modus instellen op de set met gelijke taakverdeling eindpunt:</span><span class="sxs-lookup"><span data-stu-id="63b98-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="63b98-136">Configuratie voor cloud-Service om distributie-modus te wijzigen</span><span class="sxs-lookup"><span data-stu-id="63b98-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="63b98-137">U kunt gebruikmaken van de Azure SDK voor .NET 2.5 (om te worden uitgebracht in November) voor het bijwerken van uw Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="63b98-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="63b98-138">Instellingen voor endpoint voor Cloudservices zijn aangebracht in het csdef.</span><span class="sxs-lookup"><span data-stu-id="63b98-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="63b98-139">Bijwerken van de load balancer distributie-modus voor een Cloud Services-implementatie, is een upgrade van een implementatie vereist.</span><span class="sxs-lookup"><span data-stu-id="63b98-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="63b98-140">Hier volgt een voorbeeld van wijzigingen voor eindpuntinstellingen csdef:</span><span class="sxs-lookup"><span data-stu-id="63b98-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="63b98-141">API-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="63b98-141">API example</span></span>

<span data-ttu-id="63b98-142">U kunt configureren dat de load balancer-distributie met behulp van de servicebeheer-API.</span><span class="sxs-lookup"><span data-stu-id="63b98-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="63b98-143">Zorg ervoor dat u toevoegt de `x-ms-version` header is ingesteld op versie `2014-09-01` of hoger.</span><span class="sxs-lookup"><span data-stu-id="63b98-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="63b98-144">De configuratie van de opgegeven set taakverdeling in een implementatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="63b98-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="63b98-145">Voorbeeld van de aanvraag</span><span class="sxs-lookup"><span data-stu-id="63b98-145">Request example</span></span>

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

<span data-ttu-id="63b98-146">De waarde van LoadBalancerDistribution mag sourceIP voor affiniteit tussen de 2-tuple, sourceIPProtocol voor affiniteit tussen de 3-tuple of none (voor geen relatie.</span><span class="sxs-lookup"><span data-stu-id="63b98-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="63b98-147">dat wil zeggen 5-tuple)</span><span class="sxs-lookup"><span data-stu-id="63b98-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="63b98-148">Antwoord</span><span class="sxs-lookup"><span data-stu-id="63b98-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="63b98-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63b98-149">Next Steps</span></span>

[<span data-ttu-id="63b98-150">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="63b98-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="63b98-151">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="63b98-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="63b98-152">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="63b98-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
