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
# <a name="configure-the-distribution-mode-for-load-balancer"></a>De distributie-modus voor de load balancer configureren

## <a name="hash-based-distribution-mode"></a>Distributiepunten in de hash-modus

De standaard distributie-algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash verkeer toewijzen aan beschikbare servers. Het biedt gebruikerspad alleen een transportsessie. Pakketten in dezelfde sessie wordt doorgestuurd naar het hetzelfde exemplaar van datacenter IP (DIP) achter het eindpunt van de taakverdeling. Wanneer de client wordt gestart van een nieuwe sessie van dezelfde bron-IP, wordt de bronpoort wijzigt en zorgt ervoor dat het verkeer naar een ander DIP-eindpunt.

![hash op basis van load balancer](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Afbeelding 1-5-tuple distributie

## <a name="source-ip-affinity-mode"></a>Affiniteitsmodus voor IP-bron

We hebben een ander distributiepunt installatiemodus bron-IP-affiniteit (ook wel bekend als sessie affiniteit of IP-clientaffiniteit). Azure Load Balancer kan worden geconfigureerd voor het gebruik van een 2-tuple (bron-IP, doel-IP) of 3-tuple (bron-IP, doel-IP, Protocol) verkeer toewijzen aan de beschikbare servers. Met behulp van de bron-IP-affiniteit verbindingen geïnitieerd door dezelfde clientcomputer gaat naar hetzelfde DIP-eindpunt.

Het volgende diagram ziet u een configuratie met 2-tuple. U ziet hoe de 2-tuple via de load balancer voor virtuele machine, 1 (VM1) die vervolgens back-up door VM2 en VM3 wordt uitgevoerd.

![sessie-affiniteit](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Afbeelding 2-2-tuple distributie

Bron-IP-affiniteit is opgelost incompatibiliteit tussen de Load Balancer van Azure en de Gateway van de extern bureaublad (RD). U kunt nu een farm RD-gateway in een enkel cloudservice maken.

Voorbeeldscenario voor een andere gebruik is media uploaden waar het uploaden van gegevens gebeurt via UDP, maar het besturingselement vlak wordt geregeld via TCP:

* Een client eerst een TCP-sessie in het openbare adres van de taakverdeling initieert, wordt omgeleid naar een specifieke DIP dit kanaal blijft aanwezig voor het bewaken van de status van de verbinding
* Een nieuwe sessie UDP van dezelfde clientcomputer aan hetzelfde taakverdeling openbaar eindpunt wordt gestart, wordt hier de verwachting is dat deze verbinding, ook wordt omgeleid naar hetzelfde DIP eindpunt, zoals de vorige TCP-verbinding zodat media uploaden kan worden uitgevoerd op hoog de doorvoer en tegelijkertijd ook een besturingskanaal via TCP.

> [!NOTE]
> Wanneer een set met gelijke taakverdeling wordt gewijzigd (een virtuele machine toevoegen of verwijderen), de distributie van aanvragen van clients opnieuw berekend. U kunt geen afhankelijk van nieuwe verbindingen van bestaande clients op dezelfde server loopt. Bovendien met behulp van de bron-IP affiniteitsmodus voor verdeling kan leiden tot een ongelijke distributie van verkeer. Clients met achter proxy's kunnen worden gezien als een unieke client-toepassing.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Configureren affiniteit van bron-IP-instellingen voor de load balancer

Voor virtuele machines, kunt u PowerShell time-out-instellingen te wijzigen:

Een Azure-eindpunt toevoegen aan een virtuele Machine en load balancer distributie modus instellen

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution kan worden ingesteld op sourceIP voor 2-tuple (bron-IP, doel-IP) voor de load balancer, sourceIPProtocol voor taakverdeling van 3-tuple (bron-IP, doel-IP, protocol) of none als u wilt dat het standaardgedrag van 5-tuple taakverdeling.

Gebruik de volgende voor het ophalen van een load balancer distributie modus eindpuntconfiguratie:

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

Als de LoadBalancerDistribution-element niet aanwezig is gebruikt de 5-tuple standaardalgoritme met de Azure Load balancer.

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a>De distributie-modus instellen op een set met gelijke taakverdeling eindpunt

Als eindpunten deel van een set met gelijke taakverdeling eindpunt uitmaken, moet u de distributie-modus instellen op de set met gelijke taakverdeling eindpunt:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a>Configuratie voor cloud-Service om distributie-modus te wijzigen

U kunt gebruikmaken van de Azure SDK voor .NET 2.5 (om te worden uitgebracht in November) voor het bijwerken van uw Cloud-Service. Instellingen voor endpoint voor Cloudservices zijn aangebracht in het csdef. Bijwerken van de load balancer distributie-modus voor een Cloud Services-implementatie, is een upgrade van een implementatie vereist.
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

U kunt configureren dat de load balancer-distributie met behulp van de servicebeheer-API. Zorg ervoor dat u toevoegt de `x-ms-version` header is ingesteld op versie `2014-09-01` of hoger.

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a>De configuratie van de opgegeven set taakverdeling in een implementatie bijwerken

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

De waarde van LoadBalancerDistribution mag sourceIP voor affiniteit tussen de 2-tuple, sourceIPProtocol voor affiniteit tussen de 3-tuple of none (voor geen relatie. dat wil zeggen 5-tuple)

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
