---
title: een Azure Load Balancer-regel voor een cluster aaaCreate
description: Een Azure Load Balancer tooopen poorten voor uw Azure Service Fabric-cluster configureren.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="de9cc-103">Open poorten voor een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="de9cc-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="de9cc-104">Hallo load balancer geïmplementeerd met uw Azure Service Fabric-cluster stuurt verkeer tooyour app die op een knooppunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="de9cc-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="de9cc-105">Als u uw app toouse een andere poort wijzigt, moet u die poort (of een andere poort routeren) in hello Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="de9cc-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="de9cc-106">Wanneer u uw service fabric-cluster tooAzure hebt geïmplementeerd, kan een load balancer automatisch voor u is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de9cc-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="de9cc-107">Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de9cc-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="de9cc-108">Het service fabric configureren</span><span class="sxs-lookup"><span data-stu-id="de9cc-108">Configure service fabric</span></span>

<span data-ttu-id="de9cc-109">Service Fabric-toepassing **ServiceManifest.xml** configuratiebestand definieert het Hallo-eindpunten die uw toepassing toouse wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="de9cc-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="de9cc-110">Nadat het Hallo-configuratiebestand is bijgewerkte toodefine een eindpunt, Hallo load balancer moet bijgewerkte tooexpose die (of een ander) poort.</span><span class="sxs-lookup"><span data-stu-id="de9cc-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="de9cc-111">Zie voor meer informatie over hoe toocreate service fabric-eindpunt hello, [Setup een eindpunt](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="de9cc-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="de9cc-112">Een load balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="de9cc-112">Create a load balancer rule</span></span>

<span data-ttu-id="de9cc-113">Een load balancer-regel wordt een internetgerichte poort geopend en stuurt verkeer toohello interne van knooppunt poort wordt gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="de9cc-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="de9cc-114">Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de9cc-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="de9cc-115">toocreate een load balancer-regel moet u toocollect Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="de9cc-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="de9cc-116">Naam van load balancer.</span><span class="sxs-lookup"><span data-stu-id="de9cc-116">Load balancer name.</span></span>
- <span data-ttu-id="de9cc-117">Resourcegroep Hallo load balancer en service fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="de9cc-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="de9cc-118">Externe poort.</span><span class="sxs-lookup"><span data-stu-id="de9cc-118">External port.</span></span>
- <span data-ttu-id="de9cc-119">Interne poort.</span><span class="sxs-lookup"><span data-stu-id="de9cc-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="de9cc-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="de9cc-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="de9cc-121">Als u toodetermine Hallo naam Hallo load balancer moet, gebruikt u deze opdracht tooquickly get een lijst met alle load balancers en de resourcegroepen Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="de9cc-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="de9cc-122">Het duurt maar een toocreate één opdracht een load balancer-regel Hello **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="de9cc-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="de9cc-123">U hoeft alleen maar tooknow zowel Hallo-naam van Hallo load balancer en resource groep toocreate een nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="de9cc-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="de9cc-124">Hello Azure CLI-opdracht heeft een aantal parameters die worden beschreven in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="de9cc-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="de9cc-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="de9cc-125">Parameter</span></span> | <span data-ttu-id="de9cc-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de9cc-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="de9cc-127">Hallo poort Hallo service fabric-toepassing luistert.</span><span class="sxs-lookup"><span data-stu-id="de9cc-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="de9cc-128">Hallo poort Hallo load balancer zichtbaar gemaakt voor externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="de9cc-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="de9cc-129">Hallo-naam van Hallo balancer toochange laden.</span><span class="sxs-lookup"><span data-stu-id="de9cc-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="de9cc-130">Hallo-resourcegroep die Hallo load balancer- en service fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="de9cc-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="de9cc-131">Hallo gekozen naam van regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="de9cc-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="de9cc-132">Voor meer informatie over hoe toocreate een load balancer Hello Azure CLI zien [een load balancer maken met Azure CLI Hallo](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="de9cc-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="de9cc-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de9cc-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="de9cc-134">Als u toodetermine Hallo naam Hallo load balancer moet, gebruikt u deze opdracht tooquickly get een lijst met alle load balancers en bijbehorende resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="de9cc-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="de9cc-135">PowerShell is iets gecompliceerder dan hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="de9cc-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="de9cc-136">Conceptueel gezien doen Hallo toocreate stappen te volgen, een regel.</span><span class="sxs-lookup"><span data-stu-id="de9cc-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="de9cc-137">Hallo load balancer ophalen uit Azure.</span><span class="sxs-lookup"><span data-stu-id="de9cc-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="de9cc-138">Een regel maken.</span><span class="sxs-lookup"><span data-stu-id="de9cc-138">Create a rule.</span></span>
3. <span data-ttu-id="de9cc-139">Hallo regel toohello load balancer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de9cc-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="de9cc-140">Hallo load balancer bijwerken.</span><span class="sxs-lookup"><span data-stu-id="de9cc-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="de9cc-141">Met betrekking tot Hallo `New-AzureRmLoadBalancerRuleConfig` opdracht hello `-FrontendPort` vertegenwoordigt Hallo poort Hallo load balancer wordt voor externe verbindingen en Hallo `-BackendPort` vertegenwoordigt Hallo poort Hallo service fabric-app wordt beluisterd.</span><span class="sxs-lookup"><span data-stu-id="de9cc-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="de9cc-142">Voor meer informatie over hoe toocreate een load balancer met PowerShell, Zie [een load balancer maken met PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="de9cc-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

