---
title: Een interne load balancer maken - klassieke Azure CLI | Microsoft Docs
description: Meer informatie over hoe u met de Azure CLI een interne load balancer maakt in het klassieke implementatiemodel
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
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="c4173-103">Aan de slag met het maken van een interne load balancer (klassiek) met behulp van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4173-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4173-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4173-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="c4173-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4173-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="c4173-106">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="c4173-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="c4173-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c4173-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c4173-108">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c4173-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c4173-109">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4173-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c4173-110">Lees [meer informatie over het uitvoeren van deze stappen met het Resource Manager-model](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c4173-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="c4173-111">Een interne load balancer-set maken voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c4173-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="c4173-112">Ga als volgt te werk om een interne load balancer-set te maken, evenals de servers die hun verkeer naar deze load balancer verzenden:</span><span class="sxs-lookup"><span data-stu-id="c4173-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="c4173-113">Maak een exemplaar van Interne taakverdeling dat het eindpunt wordt van binnenkomend verkeer dat gelijkmatig moet worden verdeeld over de servers van een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="c4173-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="c4173-114">Voeg eindpunten toe die overeenkomen met de virtuele machines die het binnenkomende verkeer ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c4173-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="c4173-115">Configureer de servers die het verkeer voor gelijke taakverdeling verzenden, zodanig dat het verkeer wordt verzonden naar het VIP-adres (virtuele IP) van het exemplaar van Interne taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="c4173-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="c4173-116">Stapsgewijze instructies voor het maken van een interne load balancer met behulp van CLI</span><span class="sxs-lookup"><span data-stu-id="c4173-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="c4173-117">In deze handleiding wordt beschreven hoe u een interne load balancer maakt op basis van bovenstaand scenario.</span><span class="sxs-lookup"><span data-stu-id="c4173-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="c4173-118">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="c4173-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c4173-119">Voer de opdracht **azure config mode** uit om over te schakelen naar de klassieke modus, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4173-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="c4173-120">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c4173-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="c4173-121">Set met eindpunten en load balancer maken</span><span class="sxs-lookup"><span data-stu-id="c4173-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="c4173-122">In dit scenario wordt ervan uitgegaan dat de virtuele machines DB1 en DB2 zich in een cloudservice met de naam 'mytestcloud' bevinden.</span><span class="sxs-lookup"><span data-stu-id="c4173-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="c4173-123">Beide virtuele machines maken gebruik van het virtuele netwerk 'testvnet' met subnet 'subnet-1'.</span><span class="sxs-lookup"><span data-stu-id="c4173-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="c4173-124">In deze handleiding wordt een interne load balancer-set gemaakt die poort 1433 als particuliere poort en 1433 als lokale poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c4173-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="c4173-125">Dit is een algemeen scenario met virtuele SQL-machines aan de back-end die een interne load balancer gebruiken om ervoor te zorgen dat de databaseservers niet direct worden blootgesteld via een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c4173-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="c4173-126">Stap 1</span><span class="sxs-lookup"><span data-stu-id="c4173-126">Step 1</span></span>

<span data-ttu-id="c4173-127">Maak een interne load balancer-set met behulp van `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="c4173-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="c4173-128">Zie `azure service internal-load-balancer --help` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4173-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="c4173-129">U kunt de eigenschappen van de interne load balancer controleren met de opdracht `azure service internal-load-balancer list` *cloudservicenaam*.</span><span class="sxs-lookup"><span data-stu-id="c4173-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="c4173-130">Hier volgt een voorbeeld van de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c4173-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="c4173-131">Stap 2</span><span class="sxs-lookup"><span data-stu-id="c4173-131">Step 2</span></span>

<span data-ttu-id="c4173-132">U configureert de interne load balancer-set wanneer u het eerste eindpunt toevoegt.</span><span class="sxs-lookup"><span data-stu-id="c4173-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="c4173-133">In deze stap koppelt u het eindpunt, de virtuele machine en de testpoort aan de interne load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="c4173-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="c4173-134">Stap 3</span><span class="sxs-lookup"><span data-stu-id="c4173-134">Step 3</span></span>

<span data-ttu-id="c4173-135">Controleer de configuratie van de load balancer met behulp van `azure vm show` *naam van virtuele machine*</span><span class="sxs-lookup"><span data-stu-id="c4173-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="c4173-136">De uitvoer is:</span><span class="sxs-lookup"><span data-stu-id="c4173-136">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="c4173-137">Een eindpunt voor een extern bureaublad maken voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c4173-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="c4173-138">U kunt met `azure vm endpoint create` een eindpunt voor een extern bureaublad maken om voor een bepaalde virtuele machine netwerkverkeer van een openbare poort door te sturen naar een lokale poort.</span><span class="sxs-lookup"><span data-stu-id="c4173-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="c4173-139">Virtuele machine verwijderen uit load balancer</span><span class="sxs-lookup"><span data-stu-id="c4173-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="c4173-140">U kunt een virtuele machine verwijderen uit een interne load balancer-set door het bijbehorende eindpunt te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c4173-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="c4173-141">Wanneer het eindpunt is verwijderd, maakt de virtuele machine geen deel meer uit van de load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="c4173-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="c4173-142">Op basis van bovenstaand voorbeeld kunt u het eindpunt dat is gemaakt voor de virtuele machine DB1, met de opdracht `azure vm endpoint delete` verwijderen uit interne load balancer ilbset.</span><span class="sxs-lookup"><span data-stu-id="c4173-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="c4173-143">Zie `azure vm endpoint --help` voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4173-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4173-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4173-144">Next steps</span></span>

[<span data-ttu-id="c4173-145">Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="c4173-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c4173-146">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="c4173-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
