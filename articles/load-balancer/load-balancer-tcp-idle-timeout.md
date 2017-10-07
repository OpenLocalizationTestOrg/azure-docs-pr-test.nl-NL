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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>TCP-time-out voor inactiviteit instellingen configureren voor Azure Load Balancer

In de standaardconfiguratie heeft Azure Load Balancer een instelling voor time-out voor inactiviteit van vier minuten. Als een periode van inactiviteit langer dan de time-outwaarde hello is, er is geen garantie dat Hallo TCP of HTTP-sessie wordt onderhouden tussen Hallo-client en de cloudservice.

Wanneer Hallo verbinding is gesloten, wordt de clienttoepassing Hallo volgende foutbericht weergegeven: ' hello onderliggende verbinding is gesloten: een verbinding waarvan wordt verwacht in stand gehouden toobe is gesloten door Hallo-server. '

Een gebruikelijk is toouse een keep-alive TCP. Hierdoor blijft Hallo verbinding actief voor een langere periode. Zie voor meer informatie deze [voorbeelden .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Met keep-alive is ingeschakeld, pakketten worden verzonden tijdens perioden van inactiviteit op Hallo-verbinding. Deze keepalive-pakketten Zorg dat Hallo inactief time-outwaarde nooit bereikt is en hello wordt bijgehouden voor een lange periode.

Deze instelling is geschikt voor binnenkomende verbindingen alleen. tooavoid overdragende Hallo verbinding, moet u Hallo TCP keepalive-configureren met een interval dat kleiner is dan Hallo time-out voor inactiviteit instelling of vergroot Hallo waarde time-out voor inactiviteit. toosupport dergelijke scenario's, ondersteuning voor een configureerbare time-out voor inactiviteit toegevoegd. U kunt het nu instellen voor een duur van 4 too30 minuten.

TCP-keepalive geschikt is voor scenario's waarin batterij niet een beperking. Dit wordt niet aanbevolen voor mobiele toepassingen. Met een TCP-keepalive in een mobiele toepassing kunt verwijderen uit de Hallo apparaat accu sneller.

![TCP-time](./media/load-balancer-tcp-idle-timeout/image1.png)

Hallo volgende secties wordt beschreven hoe toochange inactief time-outinstellingen in virtuele machines en cloudservices.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Hallo TCP-time configureren voor uw instantieniveau openbare IP-too15 minuten

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` is optioneel. Als deze niet is ingesteld, is Hallo standaardtime-out vier minuten. Hallo time-out acceptabele bereik is 4 too30 minuten.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Time-out voor inactiviteit van Hallo ingesteld bij het maken van een Azure-eindpunt op een virtuele machine

toochange Hallo time-out instellen voor een eindpunt, gebruikt u de volgende Hallo:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve uw configuratie van de time-out voor inactiviteit, gebruik Hallo volgende opdracht:

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Hallo TCP-out instellen op een eindpuntset met gelijke taakverdeling

Als eindpunten deel van een eindpuntset met gelijke taakverdeling uitmaken, moet TCP-time Hallo zijn ingesteld op Hallo taakverdeling eindpuntset. Bijvoorbeeld:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Time-outinstellingen voor cloudservices wijzigen

U kunt uw cloudservice hello Azure SDK tooupdate. U eindpuntinstellingen voor cloudservices in Hallo csdef-bestand. Hallo TCP-out voor de implementatie van een cloudservice bijwerken, moet een upgrade van een implementatie. Een uitzondering hierop is als Hallo TCP-time alleen voor een openbaar IP-adres is opgegeven. Openbare IP-instellingen zijn in Hallo .cscfg-bestand en u die kunt bijwerken via de implementatie-update en de upgrade.

Hallo csdef wijzigingen voor eindpuntinstellingen zijn:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

Hallo .cscfg wijzigingen voor de time-outinstelling Hallo op openbare IP-adressen zijn:

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

## <a name="rest-api-example"></a>REST-API-voorbeeld

U kunt Hallo TCP time-out bij inactiviteit voor configureren met behulp van Hallo servicebeheer-API. Zorg ervoor dat Hallo `x-ms-version` header is ingesteld tooversion `2014-06-01` of hoger. Configuratie van de update Hallo Hallo opgegeven invoereindpunten taakverdeling op alle virtuele machines in een implementatie.

### <a name="request"></a>Aanvraag

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Antwoord

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

## <a name="next-steps"></a>Volgende stappen

[Interne load balancer-overzicht](load-balancer-internal-overview.md)

[Configureren van een Internet gerichte load balancer aan de slag](load-balancer-get-started-internet-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)
