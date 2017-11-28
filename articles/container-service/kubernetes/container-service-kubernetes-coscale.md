---
title: een Azure-Kubernetes aaaMonitor cluster met CoScale | Microsoft Docs
description: Een cluster Kubernetes in Azure Container Service met behulp van CoScale bewaken
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="9d7c1-103">Een Azure Container Service Kubernetes-cluster met CoScale bewaken</span><span class="sxs-lookup"><span data-stu-id="9d7c1-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="9d7c1-104">In dit artikel wordt uitgelegd hoe u dat toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor alle knooppunten en containers in uw Kubernetes-cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="9d7c1-105">U moet een account met CoScale voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="9d7c1-106">Over CoScale</span><span class="sxs-lookup"><span data-stu-id="9d7c1-106">About CoScale</span></span> 

<span data-ttu-id="9d7c1-107">CoScale is een controle platform waarmee metrische gegevens en gebeurtenissen verzameld uit alle containers in verschillende orchestration-platforms.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="9d7c1-108">CoScale biedt volledige stack bewaking voor Kubernetes omgevingen.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="9d7c1-109">Biedt visualisaties en analytics voor alle lagen in Hallo-stack: Hallo OS, Kubernetes, Docker en toepassingen die worden uitgevoerd binnen uw containers.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="9d7c1-110">CoScale biedt diverse ingebouwde bewaking dashboards en hieraan de ingebouwde afwijkingsdetectie detectie tooallow operators en ontwikkelaars toofind infrastructuur- en problemen snel.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![CoScale gebruikersinterface](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="9d7c1-112">Zoals u in dit artikel, kunt u agents installeren op een Kubernetes cluster toorun CoScale als een SaaS-oplossing.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="9d7c1-113">Als u tookeep uw gegevens op de locatie wilt, is CoScale ook beschikbaar voor lokale installatie.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9d7c1-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d7c1-114">Prerequisites</span></span>

<span data-ttu-id="9d7c1-115">U moet eerst te[maken van een account CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="9d7c1-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="9d7c1-116">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9d7c1-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="9d7c1-117">Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure CLI en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="9d7c1-118">U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="9d7c1-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="9d7c1-119">Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9d7c1-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="9d7c1-120">U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="9d7c1-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="9d7c1-121">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d7c1-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="9d7c1-122">Hallo CoScale agent installeren met een DaemonSet</span><span class="sxs-lookup"><span data-stu-id="9d7c1-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="9d7c1-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="9d7c1-124">Ze zijn ideaal voor bewaking agenten zoals Hallo CoScale agent uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="9d7c1-125">Nadat u zich aanmeldt tooCoScale, gaat u toohello [agent pagina](https://app.coscale.com/) tooinstall CoScale agents op uw cluster met behulp van een DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="9d7c1-126">Hallo CoScale gebruikersinterface biedt begeleide configuratie stappen toocreate een agent en de controle van uw volledige Kubernetes cluster starten.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![De agentconfiguratie coScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="9d7c1-128">toostart Hallo-agent op Hallo cluster Hallo opgegeven opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d7c1-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Hallo CoScale agent starten](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="9d7c1-130">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-130">That's it!</span></span> <span data-ttu-id="9d7c1-131">Zodra Hallo agents actief en werkend zijn, moet u gegevens in de console Hallo zien over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="9d7c1-132">Ga naar Hallo [agent pagina](https://app.coscale.com/) toosee een samenvatting van uw cluster aanvullende configuratiestappen uitvoeren en dashboards zoals Hallo Zie **Kubernetes cluster overzicht**.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Overzicht van de cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="9d7c1-134">Hallo CoScale agent wordt automatisch geïmplementeerd op nieuwe computers in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="9d7c1-135">Hallo-agent wordt automatisch bijgewerkt wanneer een nieuwe versie wordt uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d7c1-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d7c1-136">Next steps</span></span>

<span data-ttu-id="9d7c1-137">Zie Hallo [CoScale documentatie](http://docs.coscale.com/) en [blog](https://www.coscale.com/blog) voor meer informatie over CoScale bewakingsoplossingen.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

