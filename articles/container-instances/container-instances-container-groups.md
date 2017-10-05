---
title: Azure-Container exemplaren Containergroepen
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
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="0c8a0-103">Containergroepen in Azure Containerexemplaren</span><span class="sxs-lookup"><span data-stu-id="0c8a0-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="0c8a0-104">De resource op het hoogste niveau in Azure Containerexemplaren is een containergroep.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="0c8a0-105">Dit artikel wordt beschreven wat containergroepen zijn en wat voor soort scenario's die ze inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="0c8a0-106">De werking van een containergroep</span><span class="sxs-lookup"><span data-stu-id="0c8a0-106">How a container group works</span></span>

<span data-ttu-id="0c8a0-107">Een containergroep is een verzameling van containers die ophalen gepland op dezelfde hostcomputer en dezelfde levenscyclus, het lokale netwerk en opslagvolumes.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="0c8a0-108">Het is vergelijkbaar met het concept van een *schil* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) en [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="0c8a0-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="0c8a0-109">Het volgende diagram toont een voorbeeld van een containergroep met meerdere containers.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Voorbeeld van de container-groepen][container-groups-example]

<span data-ttu-id="0c8a0-111">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="0c8a0-111">Note that:</span></span>

- <span data-ttu-id="0c8a0-112">De groep is gepland op een machine één host.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="0c8a0-113">De groep wordt één openbaar IP-adres, met één blootgestelde poort.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="0c8a0-114">De groep bestaat uit twee containers.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-114">The group is made up of two containers.</span></span> <span data-ttu-id="0c8a0-115">Een container luistert op poort 80, terwijl de andere luistert op poort 5000.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="0c8a0-116">De groep bevat twee Azure-bestandsshares als volume koppelingen en elke container koppelt een van de shares lokaal.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="0c8a0-117">Netwerken</span><span class="sxs-lookup"><span data-stu-id="0c8a0-117">Networking</span></span>

<span data-ttu-id="0c8a0-118">Containergroepen delen een IP-adres en een poort-naamruimte op dat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="0c8a0-119">Voor het inschakelen van externe clients een container in de groep bereikt, moet u de poort van het IP-adres en de container beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="0c8a0-120">Aangezien containers in de groep een naamruimte poort delen, worden poorttoewijzing wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="0c8a0-121">Containers in een groep kunnen bereiken elkaar via localhost op de poorten die ze beschikbaar zijn gesteld, zelfs als deze poorten niet extern worden weergegeven op de groep IP-adres.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="0c8a0-122">Storage</span><span class="sxs-lookup"><span data-stu-id="0c8a0-122">Storage</span></span>

<span data-ttu-id="0c8a0-123">U kunt externe volumes te koppelen in een container wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="0c8a0-124">U kunt deze volumes toewijzen aan specifieke paden binnen de afzonderlijke containers in een groep.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="0c8a0-125">Algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="0c8a0-125">Common scenarios</span></span>

<span data-ttu-id="0c8a0-126">Meerdere container groepen zijn handig in gevallen waarin u wilt delen van een enkele functionele taak in een klein aantal installatiekopieën van de container, die kunnen worden geleverd door verschillende teams en afzonderlijke resourcevereisten hebben.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="0c8a0-127">Voorbeeld van syntaxis kan omvatten:</span><span class="sxs-lookup"><span data-stu-id="0c8a0-127">Example usage could include:</span></span>

- <span data-ttu-id="0c8a0-128">Een toepassingscontainer en een container voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-128">An application container and a logging container.</span></span> <span data-ttu-id="0c8a0-129">De container logboekregistratie verzamelt uitvoer van de logboeken en metrische gegevens van de hoofdtoepassing en schrijft deze naar langetermijnopslag.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="0c8a0-130">Een toepassing en een controle container.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-130">An application and a monitoring container.</span></span> <span data-ttu-id="0c8a0-131">De bewaking container doet een aanvraag periodiek naar de toepassing om ervoor te zorgen dat het actief is en correct reageert en wordt een waarschuwing gegeven als dat niet.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="0c8a0-132">Een container voor een webtoepassing en een container binnenhalen van de meest recente inhoud vanuit resourcebeheer.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c8a0-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c8a0-133">Next steps</span></span>

<span data-ttu-id="0c8a0-134">Meer informatie over hoe [implementeren van een groep met meerdere container](container-instances-multi-container-group.md) met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="0c8a0-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png