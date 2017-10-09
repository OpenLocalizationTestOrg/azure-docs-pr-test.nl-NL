---
title: klassieke Azure-CLI de load balancer - aaaCreate een internetgerichte | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer aan classic deployment model met toocreate hello Azure CLI
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="ae2ca-103">Maken van een load balancer (klassiek) hello Azure CLI voor Internetgericht aan de slag</span><span class="sxs-lookup"><span data-stu-id="ae2ca-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae2ca-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae2ca-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="ae2ca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae2ca-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="ae2ca-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae2ca-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="ae2ca-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ae2ca-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ae2ca-108">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ae2ca-109">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="ae2ca-110">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="ae2ca-111">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="ae2ca-112">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ae2ca-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="ae2ca-113">Stapsgewijze instructies voor het maken van een internetgerichte load balancer met behulp van CLI</span><span class="sxs-lookup"><span data-stu-id="ae2ca-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="ae2ca-114">Deze handleiding wordt getoond hoe toocreate een load balancer van Internet op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="ae2ca-115">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ae2ca-116">Voer Hallo **azure config mode** opdracht tooswitch tooclassic modus, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="ae2ca-117">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ae2ca-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="ae2ca-118">Set met eindpunten en load balancer maken</span><span class="sxs-lookup"><span data-stu-id="ae2ca-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="ae2ca-119">Hallo scenario veronderstelt Hallo virtuele machines 'web1' en 'web2' zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="ae2ca-120">In deze handleiding wordt een set met gelijke taakverdeling gemaakt die poort 80 als openbare poort en 80 als lokale poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="ae2ca-121">Een testpoort ook is geconfigureerd op poort 80 en benoemde Hallo load balancer 'lbset' ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="ae2ca-122">Stap 1</span><span class="sxs-lookup"><span data-stu-id="ae2ca-122">Step 1</span></span>

<span data-ttu-id="ae2ca-123">Het eerste eindpunt Hallo maken en de load balancer met een set `azure network vm endpoint create` voor de virtuele machine 'web1'.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="ae2ca-124">Stap 2</span><span class="sxs-lookup"><span data-stu-id="ae2ca-124">Step 2</span></span>

<span data-ttu-id="ae2ca-125">Een tweede virtuele machine 'web2' toohello load balancer-set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="ae2ca-126">Stap 3</span><span class="sxs-lookup"><span data-stu-id="ae2ca-126">Step 3</span></span>

<span data-ttu-id="ae2ca-127">Controleren of de Hallo load balancer configuratie `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="ae2ca-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="ae2ca-128">Hallo-uitvoer zijn:</span><span class="sxs-lookup"><span data-stu-id="ae2ca-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="ae2ca-129">Een eindpunt voor een extern bureaublad maken voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="ae2ca-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="ae2ca-130">U kunt een externe bureaublad eindpunt tooforward-netwerkverkeer maken van een openbare poort tooa lokale poort voor een specifieke virtuele machine met `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="ae2ca-131">Virtuele machine verwijderen uit load balancer</span><span class="sxs-lookup"><span data-stu-id="ae2ca-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="ae2ca-132">U hebt toodelete Hallo eindpunt gekoppeld toohello balancer set laden van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="ae2ca-133">Zodra Hallo-eindpunt is verwijderd, behoort Hallo virtuele machine niet toohello load balancer meer instellen.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="ae2ca-134">Hallo bovenstaande voorbeeld gebruikt, kunt u Hallo-eindpunt gemaakt voor de virtuele machine 'web1' verwijderen uit de load balancer 'lbset' hello opdracht `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="ae2ca-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="ae2ca-135">U kunt meer opties toomanage eindpunten met Hallo opdracht verkennen`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="ae2ca-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae2ca-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae2ca-136">Next steps</span></span>

[<span data-ttu-id="ae2ca-137">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="ae2ca-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="ae2ca-138">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="ae2ca-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ae2ca-139">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="ae2ca-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
