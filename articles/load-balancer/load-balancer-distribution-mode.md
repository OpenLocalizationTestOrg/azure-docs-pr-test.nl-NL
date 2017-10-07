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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Hallo distributie modus voor de load balancer configureren

## <a name="hash-based-distribution-mode"></a>Distributiepunten in de hash-modus

Hallo standaard distributie-algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash-toomap verkeer tooavailable servers. Het biedt gebruikerspad alleen een transportsessie. Pakketten in dezelfde sessie worden Hallo omgeleid toohello dezelfde datacenter IP (DIP) achter Hallo taakverdeling endpoint-instantie. Als Hallo client start een nieuwe sessie van Hallo dezelfde bron-IP, bronpoort Hallo wijzigingen en zorgt ervoor dat Hallo verkeer toogo tooa ander DIP eindpunt.

![hash op basis van load balancer](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Afbeelding 1-5-tuple distributie

## <a name="source-ip-affinity-mode"></a>Affiniteitsmodus voor IP-bron

We hebben een ander distributiepunt installatiemodus bron-IP-affiniteit (ook wel bekend als sessie affiniteit of IP-clientaffiniteit). Azure Load Balancer kan geconfigureerde toouse 2-tuple (bron-IP, doel-IP) of 3-tuple (bron-IP, doel-IP, Protocol) toomap verkeer toohello beschikbare servers. Met behulp van de bron-IP-affiniteit verbindingen geïnitieerd vanaf Hallo dezelfde clientcomputer gaat toohello hetzelfde DIP-eindpunt.

Hallo volgende diagram ziet u een configuratie met 2-tuple. U ziet hoe Hallo 2-tuple via Hallo load balancer toovirtual machine 1 (VM1) die vervolgens back-up door VM2 en VM3 wordt uitgevoerd.

![sessie-affiniteit](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Afbeelding 2-2-tuple distributie

Bron-IP-affiniteit is opgelost incompatibiliteit tussen hello Azure Load Balancer en extern bureaublad (RD)-Gateway. U kunt nu een farm RD-gateway in een enkel cloudservice maken.

Voorbeeldscenario voor een andere gebruik is media uploaden waar Hallo gegevens uploaden gebeurt via UDP, maar Hallo besturingselement vlak wordt geregeld via TCP:

* Een client eerst een openbaar adres met gelijke taakverdeling toohello TCP-sessie start, gerichte tooa specifieke DIP, dit kanaal is de status van de verbinding Hallo links active toomonitor opgehaald
* Een nieuwe sessie UDP van Hallo dezelfde clientcomputer wordt geïnitieerd toohello dezelfde taakverdeling openbaar eindpunt, hier Hallo verwachting dat deze verbinding ook gerichte toohello dezelfde DIP eindpunt als Hallo vorige TCP-verbinding zodat media uploaden mag uitgevoerd op maximale doorvoer en tegelijkertijd ook een besturingskanaal via TCP.

> [!NOTE]
> Wanneer een set met gelijke taakverdeling wordt gewijzigd (verwijderen of toevoegen van een virtuele machine), worden de Hallo distributie van clientaanvragen herberekend. U kan niet afhankelijk zijn van de nieuwe verbindingen van bestaande clients loopt op Hallo dezelfde server. Bovendien met behulp van de bron-IP affiniteitsmodus voor verdeling kan leiden tot een ongelijke distributie van verkeer. Clients met achter proxy's kunnen worden gezien als een unieke client-toepassing.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Configureren affiniteit van bron-IP-instellingen voor de load balancer

Voor virtuele machines, kunt u PowerShell toochange time-outinstellingen:

Toevoegen van een Azure-eindpunt tooa virtuele Machine en het instellen van de load balancer-distributie-modus

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution kan toosourceIP voor 2-tuple (bron-IP, doel-IP) voor de load balancer, sourceIPProtocol voor taakverdeling van 3-tuple (bron-IP, doel-IP, protocol) of none als u wilt dat de standaardgedrag Hallo van 5-tuple taakverdeling worden ingesteld.

Gebruik Hallo tooretrieve een load balancer distributie modus eindpuntconfiguratie te volgen:

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

Als Hallo LoadBalancerDistribution element niet aanwezig is gebruikt hello Azure Load balancer Hallo standaard 5-tuple algoritme.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Hallo distributie modus instellen op een set met gelijke taakverdeling eindpunt

Als eindpunten deel van een set met gelijke taakverdeling eindpunt uitmaken, moet Hallo distributie modus worden ingesteld op Hallo eindpuntset met gelijke taakverdeling:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Cloud Service toochange distributie configuratiemodus

U kunt gebruikmaken van hello Azure SDK voor .NET 2.5 (toobe uitgebracht in November) tooupdate uw Cloud-Service. Instellingen voor endpoint voor Cloudservices zijn aangebracht in Hallo csdef. De upgrade van een implementatie is in de volgorde tooupdate Hallo load balancer distributie-modus voor een Cloud Services-implementatie vereist.
Hier volgt een voorbeeld van wijzigingen voor eindpuntinstellingen csdef:

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

## <a name="api-example"></a>API-voorbeeld

U kunt Hallo load balancer distributie op basis van de API voor servicebeheer Hallo configureren. Zorg ervoor dat tooadd hello `x-ms-version` header is ingesteld tooversion `2014-09-01` of hoger.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Configuratie van de update Hallo Hallo opgegeven set met gelijke taakverdeling in een implementatie

#### <a name="request-example"></a>Voorbeeld van de aanvraag

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

Hallo-waarden voor LoadBalancerDistribution zijn sourceIP voor affiniteit tussen de 2-tuple, sourceIPProtocol voor affiniteit tussen de 3-tuple of none (voor geen relatie. dat wil zeggen 5-tuple)

#### <a name="response"></a>Antwoord

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Volgende stappen

[Interne load balancer-overzicht](load-balancer-internal-overview.md)

[De load balancer van een Internetgericht configureren aan de slag](load-balancer-get-started-internet-arm-ps.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
