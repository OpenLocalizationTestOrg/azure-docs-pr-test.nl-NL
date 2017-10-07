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
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="d461e-103">Aan de slag met het maken van een interne load balancer (klassiek) voor cloudservices</span><span class="sxs-lookup"><span data-stu-id="d461e-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d461e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d461e-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="d461e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d461e-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="d461e-106">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="d461e-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="d461e-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d461e-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d461e-108">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d461e-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d461e-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d461e-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d461e-110">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d461e-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="d461e-111">Een interne load balancer configureren voor cloudservices</span><span class="sxs-lookup"><span data-stu-id="d461e-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="d461e-112">Een interne load balancer wordt ondersteund voor zowel virtuele machines als cloudservices.</span><span class="sxs-lookup"><span data-stu-id="d461e-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="d461e-113">Een interne load balancer-eindpunt gemaakt in een cloudservice die buiten een regionaal virtueel netwerk zijn alleen binnen het Hallo-cloudservice toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="d461e-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="d461e-114">Hallo interne load balancer-configuratie heeft toobe ingesteld tijdens het Hallo maken van de eerste implementatie Hallo in Hallo-cloudservice, zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="d461e-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d461e-115">Een vereiste toorun Hallo volgende stappen uit een virtueel netwerk al is gemaakt voor de implementatie van de cloud Hallo toohave is.</span><span class="sxs-lookup"><span data-stu-id="d461e-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="d461e-116">U moet Hallo virtueel netwerk en het subnet naam toocreate Hallo interne Load Balancing.</span><span class="sxs-lookup"><span data-stu-id="d461e-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="d461e-117">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d461e-117">Step 1</span></span>

<span data-ttu-id="d461e-118">Hallo-service-configuratiebestand (.cscfg) voor uw cloudimplementatie in Visual Studio openen en toevoegen van de volgende sectie toocreate Hallo interne Load Balancing onder Hallo laatste Hallo '`</Role>`'-item voor Hallo-netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="d461e-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="d461e-119">Laten we Hallo waarden toevoegen voor Hallo network configuration file tooshow hoe het eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="d461e-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="d461e-120">In Hallo voorbeeld wordt ervan uitgegaan dat u een VNet 'test_vnet' aangeroepen met een subnet 10.0.0.0/24 test_subnet en een statisch IP-adres 10.0.0.4 gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d461e-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="d461e-121">Hallo load balancer worden testLB benoemd.</span><span class="sxs-lookup"><span data-stu-id="d461e-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="d461e-122">Zie voor meer informatie over Hallo load balancer schema [toevoegen load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="d461e-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="d461e-123">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d461e-123">Step 2</span></span>

<span data-ttu-id="d461e-124">Hallo service definition (.csdef) bestand tooadd eindpunten toohello interne Load Balancing wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d461e-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="d461e-125">Hallo momenteel een rolinstantie is gemaakt, servicedefinitiebestand Hallo Hallo rol exemplaren toohello interne Load Balancing wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d461e-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="d461e-126">Volgende Hallo dezelfde van Hallo in bovenstaand voorbeeld waarden, gaan we toevoegen Hallo waarden toohello servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="d461e-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="d461e-127">Hallo-netwerkverkeer worden evenredig verdeeld met behulp van Hallo testLB load balancer met behulp van poort 80 voor inkomende aanvragen en verzenden van tooworker rolinstanties ook op poort 80.</span><span class="sxs-lookup"><span data-stu-id="d461e-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d461e-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d461e-128">Next steps</span></span>

[<span data-ttu-id="d461e-129">Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="d461e-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d461e-130">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d461e-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

