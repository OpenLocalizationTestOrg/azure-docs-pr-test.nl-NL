---
title: aaaAzure Containerexemplaren en Container Orchestration
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
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="e3c8d-103">Azure Container-exemplaren en container orchestrators</span><span class="sxs-lookup"><span data-stu-id="e3c8d-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="e3c8d-104">Vanwege de klein en de afdrukstand van de toepassing zijn containers uitermate geschikt is voor flexibele levering omgevingen en op basis van microservice-architecturen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="e3c8d-105">Hallo-taak van automatiseren en beheren van een groot aantal containers en hun werking wordt ook wel *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="e3c8d-106">Populaire container orchestrators zijn Kubernetes DC/OS en Docker Swarm dit allemaal beschikbaar in Hallo zijn [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="e3c8d-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="e3c8d-107">Azure Containerexemplaren staan enkele Hallo basic planfuncties orchestration-platforms, maar ze omvatten geen Hallo hogere waarde services dat deze platforms bieden en in feite aanvullende met hen worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="e3c8d-108">Dit artikel wordt beschreven Hallo bereik van wat Azure Containerexemplaren verwerkt en hoe vol container orchestrators ermee kunnen communiceren.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="e3c8d-109">Traditionele orchestration</span><span class="sxs-lookup"><span data-stu-id="e3c8d-109">Traditional orchestration</span></span>

<span data-ttu-id="e3c8d-110">Hallo standaarddefinitie van orchestration bevat Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3c8d-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="e3c8d-111">**Planning**: een geschikte machine op welke toorun Hallo container gezien een installatiekopie van een container en een resource-aanvraag, vinden.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="e3c8d-112">**Affiniteit /-affinity**: opgeven dat een set van containers moet worden uitgevoerd in de buurt van elkaar (prestaties) of voldoende ver uit elkaar (voor beschikbaarheid).</span><span class="sxs-lookup"><span data-stu-id="e3c8d-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="e3c8d-113">**Statuscontrole**: Bekijk bij fouten van de container en automatisch opnieuw te plannen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="e3c8d-114">**Failover**: bijhouden wat wordt uitgevoerd op elke machine en plannen van containers van mislukte machines toohealthy knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="e3c8d-115">**Schalen**: toevoegen of verwijderen van container exemplaren toomatch vraag handmatig of automatisch.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="e3c8d-116">**Networking**: een overlaynetwerk bieden voor het coördineren van containers toocommunicate over meerdere hostmachines.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="e3c8d-117">**Servicedetectie**: inschakelen containers toolocate elkaar automatisch zelfs als ze worden verplaatst tussen hostmachines en IP-adressen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="e3c8d-118">**Coördinatie toepassingsupgrades**: container upgrades tooavoid toepassing uitvaltijd te beheren en terugdraaien als er iets mis gaat.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="e3c8d-119">Orchestration met exemplaren van Azure-Container: een gelaagde benadering.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="e3c8d-120">Azure Containerexemplaren Hiermee een tooorchestration beheerslaag bieden alle Hallo planning- en beheermogelijkheden vereist toorun een enkele container en tegelijkertijd orchestrator platforms toomanage container meerdere taken toe.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="e3c8d-121">Omdat alle Hallo onderliggende infrastructuur voor exemplaren van de Container door Azure wordt beheerd, heeft een orchestrator-platform tooconcern zelf bij het zoeken van een geschikte host-machine op welke toorun een enkele container niet nodig.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="e3c8d-122">Hallo elasticiteit van Hallo cloud zorgt ervoor dat een altijd beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="e3c8d-123">In plaats daarvan kunt Hallo orchestrator zich richten op Hallo-taken die het Hallo-ontwikkeling van meerdere container architecturen, met inbegrip van schalen en gecoördineerde upgrades vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="e3c8d-124">Mogelijke scenario 's</span><span class="sxs-lookup"><span data-stu-id="e3c8d-124">Potential scenarios</span></span>

<span data-ttu-id="e3c8d-125">Orchestrator-integratie met Azure Containerexemplaren is nog steeds opkomende, verwachten we dat er een paar verschillende omgevingen kunnen ontstaan:</span><span class="sxs-lookup"><span data-stu-id="e3c8d-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="e3c8d-126">Orchestration van Containerexemplaren uitsluitend</span><span class="sxs-lookup"><span data-stu-id="e3c8d-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="e3c8d-127">Omdat ze snel starten en door Hallo factureren tweede, een omgeving met uitsluitend op op basis van exemplaren van Azure-Container biedt de snelste manier tooget Hallo gestart en toodeal met maximaal variabele werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="e3c8d-128">Combinatie van Containerexemplaren en Containers in virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="e3c8d-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="e3c8d-129">Voor langdurige wordt stabiele werkbelastingen, organiseren containers in een cluster toegewezen virtuele machines doorgaans goedkoper dan Hallo dezelfde containers uitgevoerd met exemplaren van de Container.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="e3c8d-130">Containerexemplaren bieden echter een uitstekende oplossing voor het snel uitbreiden en verdragsluitende uw algehele capaciteit toodeal met onverwachte of tijdelijke pieken in gebruik.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="e3c8d-131">In plaats van het aantal virtuele machines in uw cluster Hallo uitbreiden, vervolgens extra containers op die computers implementeert, Hallo orchestrator kunt gewoon Hallo extra containers met instanties van de Container plannen en verwijderen wanneer ze zijn geen meer nodig.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="e3c8d-132">Voorbeeldimplementatie: Azure Container exemplaren-Connector voor Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e3c8d-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="e3c8d-133">toodemonstrate hoe container orchestration platforms met Azure Containerexemplaren integreren kunnen, hebben we gebouw gestart een [voorbeeld-connector voor Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="e3c8d-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="e3c8d-134">Hallo connector voor Kubernetes lijkt op Hallo [kubelet] [ kubelet-doc] door te registreren als een knooppunt met onbeperkte capaciteit en tijdens het verzenden van Hallo maken van [gehele product] [ pod-doc] als containergroepen in Azure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="e3c8d-135">Connectors voor andere orchestrators kunnen die op dezelfde manier worden geïntegreerd met platform primitieven toocombine Hallo power van Hallo orchestrator API met Hallo snelheid en eenvoud van het beheer van containers in Azure Containerexemplaren worden gebouwd.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="e3c8d-136">Hallo ACI connector voor Kubernetes is *experimentele* en mag niet worden gebruikt in productie.</span><span class="sxs-lookup"><span data-stu-id="e3c8d-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3c8d-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3c8d-137">Next steps</span></span>

<span data-ttu-id="e3c8d-138">Uw eerste container maken met Azure Container-exemplaren die gebruikmaken van Hallo [snelstartgids](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e3c8d-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/