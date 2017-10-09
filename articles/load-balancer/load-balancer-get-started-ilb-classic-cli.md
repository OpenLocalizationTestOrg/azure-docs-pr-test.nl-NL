---
title: klassieke Azure-CLI de load balancer - aaaCreate een intern | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer met behulp van Azure CLI Hallo Hallo klassieke implementatiemodel
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Maken van een interne load balancer (klassiek) met behulp van hello Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloudservices](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate een interne load balancer voor virtuele machines instellen

toocreate een interne load balancer ingesteld en Hallo servers die hun tooit verkeer wordt verzonden, moet u doen Hallo volgende:

1. Een instantie van de interne Load Balancing die Hallo-eindpunt van het binnenkomende verkeer toobe gelijkmatig verdeeld zijn over Hallo-servers van een set met gelijke taakverdeling maken.
2. Het toevoegen van eindpunten overeenkomt toohello virtuele machines die Hallo binnenkomend verkeer ontvangt.
3. Hallo-servers die worden verzonden hello verkeer toobe met gelijke taakverdeling toosend hun verkeer toohello virtuele IP-adres (VIP) van Hallo interne Load Balancing-exemplaar te configureren.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Stapsgewijze instructies voor het maken van een interne load balancer met behulp van CLI

Deze handleiding wordt getoond hoe toocreate een interne load balancer op basis van Hallo bovenstaande scenario.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure config mode** opdracht tooswitch tooclassic modus, zoals hieronder wordt weergegeven.

    ```azurecli
    azure config mode asm
    ```

    Verwachte uitvoer:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Set met eindpunten en load balancer maken

Hallo scenario veronderstelt Hallo virtuele machines 'DB1' en 'DB2' in een cloudservice 'mytestcloud' genoemd. Beide virtuele machines maken gebruik van het virtuele netwerk 'testvnet' met subnet 'subnet-1'.

In deze handleiding wordt een interne load balancer-set gemaakt die poort 1433 als particuliere poort en 1433 als lokale poort gebruikt.

Dit is een veelvoorkomend scenario waarin u virtuele machines van SQL op Hallo back-end met behulp van die een interne load balancer tooguarantee Hallo databaseservers won't worden blootgesteld rechtstreeks via een openbaar IP-adres hebben.

### <a name="step-1"></a>Stap 1

Maak een interne load balancer-set met behulp van `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Zie `azure service internal-load-balancer --help` voor meer informatie.

U kunt eigenschappen Hallo interne load balancer met de opdracht Hallo controleren `azure service internal-load-balancer list` *cloudservicenaam*.

Hier volgt een voorbeeld van uitvoer Hallo:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Stap 2

U configureert Hallo interne load balancer ingesteld wanneer u het eerste eindpunt Hallo toevoegen. U koppelt Hallo eindpunt, de virtuele machine en de test poort toohello interne load balancer in deze stap hebt ingesteld.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Stap 3

Controleren of de Hallo load balancer configuratie `azure vm show` *naam virtuele machine*

```azurecli
azure vm show DB1
```

Hallo-uitvoer zijn:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Een eindpunt voor een extern bureaublad maken voor een virtuele machine

U kunt een externe bureaublad eindpunt tooforward-netwerkverkeer maken van een openbare poort tooa lokale poort voor een specifieke virtuele machine met `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Virtuele machine verwijderen uit load balancer

U kunt een virtuele machine verwijderen uit een interne load balancer ingesteld door het Hallo gekoppeld-eindpunt wordt verwijderd. Zodra Hallo-eindpunt is verwijderd, won't Hallo virtuele machine toohello load balancer meer ingesteld behoren.

Hallo bovenstaande voorbeeld gebruikt, kunt u Hallo-eindpunt gemaakt voor de virtuele machine 'DB1' van de interne load balancer 'ilbset' verwijderen met behulp van de opdracht Hallo `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Zie `azure vm endpoint --help` voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
