---
title: Exemplaren van de Azure-Container en Container Orchestration
description: Begrijpen hoe Azure Containerexemplaren communiceren met de container orchestrators
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
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="edb27-103">Azure Container-exemplaren en container orchestrators</span><span class="sxs-lookup"><span data-stu-id="edb27-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="edb27-104">Vanwege de klein en de afdrukstand van de toepassing zijn containers uitermate geschikt is voor flexibele levering omgevingen en op basis van microservice-architecturen.</span><span class="sxs-lookup"><span data-stu-id="edb27-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="edb27-105">De taak van automatiseren en beheren van een groot aantal containers en hun werking wordt ook wel *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="edb27-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="edb27-106">Populaire container orchestrators zijn Kubernetes DC/OS en Docker Swarm dit zijn allemaal beschikbaar in de [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="edb27-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="edb27-107">Azure Containerexemplaren biedt enkele van de mogelijkheden voor basic planning van de orchestration-platforms, maar dit geldt niet voor de services van de hogere waarde dat deze platforms bieden en kunnen in feite worden aanvullende mee.</span><span class="sxs-lookup"><span data-stu-id="edb27-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="edb27-108">Dit artikel wordt beschreven voor het bereik van wat Azure Containerexemplaren verwerkt en hoe vol container orchestrators ermee kunnen communiceren.</span><span class="sxs-lookup"><span data-stu-id="edb27-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="edb27-109">Traditionele orchestration</span><span class="sxs-lookup"><span data-stu-id="edb27-109">Traditional orchestration</span></span>

<span data-ttu-id="edb27-110">De definitie van het standaard van orchestration omvat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="edb27-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="edb27-111">**Planning**: een geschikte machine waarop moet worden uitgevoerd van de container gezien een installatiekopie van een container en een resource-aanvraag, vinden.</span><span class="sxs-lookup"><span data-stu-id="edb27-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="edb27-112">**Affiniteit /-affinity**: opgeven dat een set van containers moet worden uitgevoerd in de buurt van elkaar (prestaties) of voldoende ver uit elkaar (voor beschikbaarheid).</span><span class="sxs-lookup"><span data-stu-id="edb27-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="edb27-113">**Statuscontrole**: Bekijk bij fouten van de container en automatisch opnieuw te plannen.</span><span class="sxs-lookup"><span data-stu-id="edb27-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="edb27-114">**Failover**: wat wordt uitgevoerd op elke machine en bijhouden van mislukte machines containers in orde knooppunten plannen.</span><span class="sxs-lookup"><span data-stu-id="edb27-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="edb27-115">**Schalen**: toevoegen of verwijderen van containerexemplaren zodat deze overeenkomen met de vraag, handmatig of automatisch.</span><span class="sxs-lookup"><span data-stu-id="edb27-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="edb27-116">**Networking**: een overlaynetwerk bieden voor het coördineren van containers om te communiceren over meerdere hostmachines.</span><span class="sxs-lookup"><span data-stu-id="edb27-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="edb27-117">**Servicedetectie**: containers naar elkaar automatisch vinden zelfs als ze worden verplaatst tussen hostmachines en wijzigen van IP-adressen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="edb27-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="edb27-118">**Coördinatie toepassingsupgrades**: upgrades van de container voor de toepassing uitvaltijd voorkomen en terugdraaien als er iets mis gaat beheren.</span><span class="sxs-lookup"><span data-stu-id="edb27-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="edb27-119">Orchestration met exemplaren van Azure-Container: een gelaagde benadering.</span><span class="sxs-lookup"><span data-stu-id="edb27-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="edb27-120">Azure Container-exemplaren kunnen een gelaagde benadering orchestration, alle vereist voor het uitvoeren van een enkele container en tegelijkertijd orchestrator platforms voor het beheren van taken met meerdere container boven op het plannings- en mogelijkheden bieden.</span><span class="sxs-lookup"><span data-stu-id="edb27-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="edb27-121">Omdat alle van de onderliggende infrastructuur voor exemplaren van de Container wordt beheerd door Azure, hoeft een orchestrator-platform niet naar zichzelf betrekking hebben op bij het zoeken van een geschikte host-machine waarop een enkele container uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="edb27-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="edb27-122">De elasticiteit van de cloud zorgt ervoor dat een altijd beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="edb27-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="edb27-123">In plaats daarvan kunt de orchestrator zich richten op de taken die de ontwikkeling van meerdere container architecturen, met inbegrip van schalen en gecoördineerde upgrades vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="edb27-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="edb27-124">Mogelijke scenario 's</span><span class="sxs-lookup"><span data-stu-id="edb27-124">Potential scenarios</span></span>

<span data-ttu-id="edb27-125">Orchestrator-integratie met Azure Containerexemplaren is nog steeds opkomende, verwachten we dat er een paar verschillende omgevingen kunnen ontstaan:</span><span class="sxs-lookup"><span data-stu-id="edb27-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="edb27-126">Orchestration van Containerexemplaren uitsluitend</span><span class="sxs-lookup"><span data-stu-id="edb27-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="edb27-127">Omdat ze snel starten en door het tweede factureren, biedt een omgeving op basis van exemplaren van Azure-Container uitsluitend de snelste manier om te beginnen en om te gaan met maximaal variabele werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="edb27-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="edb27-128">Combinatie van Containerexemplaren en Containers in virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="edb27-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="edb27-129">Voor langdurige, stabiele werkbelastingen wordt organiseren containers in een cluster toegewezen virtuele machines doorgaans goedkoper dan het uitvoeren van de dezelfde containers met exemplaren van de Container.</span><span class="sxs-lookup"><span data-stu-id="edb27-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="edb27-130">Containerexemplaren bieden echter een uitstekende oplossing voor het snel uitbreiden en verdragsluitende uw algehele capaciteit om te gaan met onverwachte of tijdelijke pieken in gebruik.</span><span class="sxs-lookup"><span data-stu-id="edb27-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="edb27-131">In plaats van het aantal virtuele machines in uw cluster uitbreiden, vervolgens extra containers op die computers implementeert, de orchestrator kunt gewoon de extra containers met instanties van de Container plannen en verwijderen wanneer ze niet meer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="edb27-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="edb27-132">Voorbeeldimplementatie: Azure Container exemplaren-Connector voor Kubernetes</span><span class="sxs-lookup"><span data-stu-id="edb27-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="edb27-133">Om te demonstreren hoe container orchestration platforms kunnen integreren met Azure Containerexemplaren, hebben we gebouw gestart een [voorbeeld-connector voor Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="edb27-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="edb27-134">De connector voor Kubernetes lijkt de [kubelet] [ kubelet-doc] door te registreren als een knooppunt met onbeperkte capaciteit en tijdens het verzenden van het maken van [gehele product] [ pod-doc] als containergroepen in Azure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="edb27-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="edb27-135">Connectors voor andere orchestrators kunnen die op dezelfde manier worden geïntegreerd met platform primitieven combineren de kracht van de orchestrator-API met de snelheid en eenvoud van het beheer van containers in Azure Containerexemplaren te worden gebouwd.</span><span class="sxs-lookup"><span data-stu-id="edb27-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="edb27-136">De connector ACI voor Kubernetes is *experimentele* en mag niet worden gebruikt in productie.</span><span class="sxs-lookup"><span data-stu-id="edb27-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb27-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edb27-137">Next steps</span></span>

<span data-ttu-id="edb27-138">Uw eerste container maken met het gebruik van Azure Containerexemplaren de [snelstartgids](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="edb27-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/