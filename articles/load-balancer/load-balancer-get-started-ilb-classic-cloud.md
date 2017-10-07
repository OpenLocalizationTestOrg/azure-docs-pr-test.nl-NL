---
title: een interne load balancer voor Azure Cloud Services aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een interne netwerktaakverdeler met PowerShell in het klassieke implementatiemodel Hallo
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Aan de slag met het maken van een interne load balancer (klassiek) voor cloudservices

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloudservices](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Een interne load balancer configureren voor cloudservices

Een interne load balancer wordt ondersteund voor zowel virtuele machines als cloudservices. Een interne load balancer-eindpunt gemaakt in een cloudservice die buiten een regionaal virtueel netwerk zijn alleen binnen het Hallo-cloudservice toegankelijk.

Hallo interne load balancer-configuratie heeft toobe ingesteld tijdens het Hallo maken van de eerste implementatie Hallo in Hallo-cloudservice, zoals weergegeven in Hallo voorbeeld hieronder.

> [!IMPORTANT]
> Een vereiste toorun Hallo volgende stappen uit een virtueel netwerk al is gemaakt voor de implementatie van de cloud Hallo toohave is. U moet Hallo virtueel netwerk en het subnet naam toocreate Hallo interne Load Balancing.

### <a name="step-1"></a>Stap 1

Hallo-service-configuratiebestand (.cscfg) voor uw cloudimplementatie in Visual Studio openen en toevoegen van de volgende sectie toocreate Hallo interne Load Balancing onder Hallo laatste Hallo '`</Role>`'-item voor Hallo-netwerkconfiguratie.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Laten we Hallo waarden toevoegen voor Hallo network configuration file tooshow hoe het eruit ziet. In Hallo voorbeeld wordt ervan uitgegaan dat u een VNet 'test_vnet' aangeroepen met een subnet 10.0.0.0/24 test_subnet en een statisch IP-adres 10.0.0.4 gemaakt. Hallo load balancer worden testLB benoemd.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Zie voor meer informatie over Hallo load balancer schema [toevoegen load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Stap 2

Hallo service definition (.csdef) bestand tooadd eindpunten toohello interne Load Balancing wijzigen. Hallo momenteel een rolinstantie is gemaakt, servicedefinitiebestand Hallo Hallo rol exemplaren toohello interne Load Balancing wordt toegevoegd.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Volgende Hallo dezelfde van Hallo in bovenstaand voorbeeld waarden, gaan we toevoegen Hallo waarden toohello servicedefinitiebestand.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

Hallo-netwerkverkeer worden evenredig verdeeld met behulp van Hallo testLB load balancer met behulp van poort 80 voor inkomende aanvragen en verzenden van tooworker rolinstanties ook op poort 80.

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

