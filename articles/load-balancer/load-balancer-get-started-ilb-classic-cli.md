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
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="a0f53-103">Maken van een interne load balancer (klassiek) met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0f53-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0f53-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0f53-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="a0f53-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0f53-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="a0f53-106">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="a0f53-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a0f53-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a0f53-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a0f53-108">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0f53-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a0f53-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0f53-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a0f53-110">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a0f53-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="a0f53-111">toocreate een interne load balancer voor virtuele machines instellen</span><span class="sxs-lookup"><span data-stu-id="a0f53-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="a0f53-112">toocreate een interne load balancer ingesteld en Hallo servers die hun tooit verkeer wordt verzonden, moet u doen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a0f53-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="a0f53-113">Een instantie van de interne Load Balancing die Hallo-eindpunt van het binnenkomende verkeer toobe gelijkmatig verdeeld zijn over Hallo-servers van een set met gelijke taakverdeling maken.</span><span class="sxs-lookup"><span data-stu-id="a0f53-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="a0f53-114">Het toevoegen van eindpunten overeenkomt toohello virtuele machines die Hallo binnenkomend verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="a0f53-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="a0f53-115">Hallo-servers die worden verzonden hello verkeer toobe met gelijke taakverdeling toosend hun verkeer toohello virtuele IP-adres (VIP) van Hallo interne Load Balancing-exemplaar te configureren.</span><span class="sxs-lookup"><span data-stu-id="a0f53-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="a0f53-116">Stapsgewijze instructies voor het maken van een interne load balancer met behulp van CLI</span><span class="sxs-lookup"><span data-stu-id="a0f53-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="a0f53-117">Deze handleiding wordt getoond hoe toocreate een interne load balancer op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="a0f53-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="a0f53-118">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="a0f53-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a0f53-119">Voer Hallo **azure config mode** opdracht tooswitch tooclassic modus, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a0f53-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="a0f53-120">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a0f53-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="a0f53-121">Set met eindpunten en load balancer maken</span><span class="sxs-lookup"><span data-stu-id="a0f53-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="a0f53-122">Hallo scenario veronderstelt Hallo virtuele machines 'DB1' en 'DB2' in een cloudservice 'mytestcloud' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a0f53-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="a0f53-123">Beide virtuele machines maken gebruik van het virtuele netwerk 'testvnet' met subnet 'subnet-1'.</span><span class="sxs-lookup"><span data-stu-id="a0f53-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="a0f53-124">In deze handleiding wordt een interne load balancer-set gemaakt die poort 1433 als particuliere poort en 1433 als lokale poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0f53-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="a0f53-125">Dit is een veelvoorkomend scenario waarin u virtuele machines van SQL op Hallo back-end met behulp van die een interne load balancer tooguarantee Hallo databaseservers won't worden blootgesteld rechtstreeks via een openbaar IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="a0f53-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="a0f53-126">Stap 1</span><span class="sxs-lookup"><span data-stu-id="a0f53-126">Step 1</span></span>

<span data-ttu-id="a0f53-127">Maak een interne load balancer-set met behulp van `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="a0f53-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="a0f53-128">Zie `azure service internal-load-balancer --help` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a0f53-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="a0f53-129">U kunt eigenschappen Hallo interne load balancer met de opdracht Hallo controleren `azure service internal-load-balancer list` *cloudservicenaam*.</span><span class="sxs-lookup"><span data-stu-id="a0f53-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="a0f53-130">Hier volgt een voorbeeld van uitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="a0f53-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="a0f53-131">Stap 2</span><span class="sxs-lookup"><span data-stu-id="a0f53-131">Step 2</span></span>

<span data-ttu-id="a0f53-132">U configureert Hallo interne load balancer ingesteld wanneer u het eerste eindpunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0f53-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="a0f53-133">U koppelt Hallo eindpunt, de virtuele machine en de test poort toohello interne load balancer in deze stap hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0f53-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="a0f53-134">Stap 3</span><span class="sxs-lookup"><span data-stu-id="a0f53-134">Step 3</span></span>

<span data-ttu-id="a0f53-135">Controleren of de Hallo load balancer configuratie `azure vm show` *naam virtuele machine*</span><span class="sxs-lookup"><span data-stu-id="a0f53-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="a0f53-136">Hallo-uitvoer zijn:</span><span class="sxs-lookup"><span data-stu-id="a0f53-136">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="a0f53-137">Een eindpunt voor een extern bureaublad maken voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a0f53-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="a0f53-138">U kunt een externe bureaublad eindpunt tooforward-netwerkverkeer maken van een openbare poort tooa lokale poort voor een specifieke virtuele machine met `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="a0f53-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="a0f53-139">Virtuele machine verwijderen uit load balancer</span><span class="sxs-lookup"><span data-stu-id="a0f53-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="a0f53-140">U kunt een virtuele machine verwijderen uit een interne load balancer ingesteld door het Hallo gekoppeld-eindpunt wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a0f53-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="a0f53-141">Zodra Hallo-eindpunt is verwijderd, won't Hallo virtuele machine toohello load balancer meer ingesteld behoren.</span><span class="sxs-lookup"><span data-stu-id="a0f53-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="a0f53-142">Hallo bovenstaande voorbeeld gebruikt, kunt u Hallo-eindpunt gemaakt voor de virtuele machine 'DB1' van de interne load balancer 'ilbset' verwijderen met behulp van de opdracht Hallo `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="a0f53-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="a0f53-143">Zie `azure vm endpoint --help` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a0f53-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0f53-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0f53-144">Next steps</span></span>

[<span data-ttu-id="a0f53-145">Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="a0f53-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a0f53-146">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="a0f53-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
