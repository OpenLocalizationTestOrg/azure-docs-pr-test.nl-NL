---
title: aaaAzure Container exemplaren Containergroepen
description: Begrijpen hoe Containergroepen werken in Azure Containerexemplaren
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="d3ad6-103">Containergroepen in Azure Containerexemplaren</span><span class="sxs-lookup"><span data-stu-id="d3ad6-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="d3ad6-104">Hallo op het hoogste niveau resource in Azure Containerexemplaren is een containergroep.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="d3ad6-105">Dit artikel wordt beschreven wat containergroepen zijn en wat voor soort scenario's die ze inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="d3ad6-106">De werking van een containergroep</span><span class="sxs-lookup"><span data-stu-id="d3ad6-106">How a container group works</span></span>

<span data-ttu-id="d3ad6-107">Een containergroep is een verzameling van containers die ophalen gepland op Hallo dezelfde machine hosten en levenscyclus, lokale netwerk en opslagvolumes delen.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="d3ad6-108">Het is vergelijkbaar toohello concept van een *schil* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) en [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="d3ad6-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="d3ad6-109">Hallo toont volgende diagram een voorbeeld van een containergroep met meerdere containers.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Voorbeeld van de container-groepen][container-groups-example]

<span data-ttu-id="d3ad6-111">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="d3ad6-111">Note that:</span></span>

- <span data-ttu-id="d3ad6-112">Hallo-groep is gepland op een machine één host.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="d3ad6-113">Hallo-groep wordt één openbaar IP-adres, met één blootgestelde poort.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="d3ad6-114">Hallo-groep bestaat uit twee containers.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-114">hello group is made up of two containers.</span></span> <span data-ttu-id="d3ad6-115">Een container luistert op poort 80, terwijl andere Hallo op poort 5000 luistert.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="d3ad6-116">Hallo-groep bevat twee Azure-bestandsshares als volume koppelingen en elke container koppelt een lokaal Hallo shares.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="d3ad6-117">Netwerken</span><span class="sxs-lookup"><span data-stu-id="d3ad6-117">Networking</span></span>

<span data-ttu-id="d3ad6-118">Containergroepen delen een IP-adres en een poort-naamruimte op dat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="d3ad6-119">tooenable externe clients tooreach een container in de groep Hallo tonen Hallo-poort op Hallo IP-adres en uit Hallo-container op.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="d3ad6-120">Omdat containers in de groep Hallo een naamruimte poort delen, worden poorttoewijzing wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="d3ad6-121">Containers in een groep kunnen bereiken elkaar via localhost op Hallo poorten die ze beschikbaar zijn gesteld, zelfs als deze poorten niet extern worden weergegeven op Hallo van de groep IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="d3ad6-122">Storage</span><span class="sxs-lookup"><span data-stu-id="d3ad6-122">Storage</span></span>

<span data-ttu-id="d3ad6-123">U kunt externe volumes toomount binnen een containergroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="d3ad6-124">U kunt deze volumes toewijzen aan specifieke paden binnen Hallo afzonderlijke containers in een groep.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="d3ad6-125">Algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="d3ad6-125">Common scenarios</span></span>

<span data-ttu-id="d3ad6-126">Meerdere container groepen zijn handig in gevallen waar u toodivide van een enkele functionele taak in een klein aantal installatiekopieën van de container, die kunnen worden geleverd door verschillende teams en afzonderlijke resourcevereisten hebben.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="d3ad6-127">Voorbeeld van syntaxis kan omvatten:</span><span class="sxs-lookup"><span data-stu-id="d3ad6-127">Example usage could include:</span></span>

- <span data-ttu-id="d3ad6-128">Een toepassingscontainer en een container voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-128">An application container and a logging container.</span></span> <span data-ttu-id="d3ad6-129">Hallo logboekregistratie container Hallo logboeken en uitvoer van de metrische gegevens verzamelt door de hoofdtoepassing Hallo en schrijft deze toolong-termijn opslag.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="d3ad6-130">Een toepassing en een controle container.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-130">An application and a monitoring container.</span></span> <span data-ttu-id="d3ad6-131">Hallo container periodiek bewaking kunt u een aanvraag toohello toepassing tooensure dat het actief is en correct reageert en wordt een waarschuwing gegeven als dat niet.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="d3ad6-132">Een container voor een webtoepassing en een container binnenhalen van de meest recente inhoud Hallo vanuit resourcebeheer.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3ad6-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3ad6-133">Next steps</span></span>

<span data-ttu-id="d3ad6-134">Meer informatie over hoe te[implementeren van een groep met meerdere container](container-instances-multi-container-group.md) met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d3ad6-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png