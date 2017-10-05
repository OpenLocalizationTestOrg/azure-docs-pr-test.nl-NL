---
title: Monitor Azure Kubernetes cluster met Datadog | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Datadog
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 40b34457447a8f80d8cdf77579750e0c42df22d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="7e05e-103">Een Azure Container Service-cluster met DataDog bewaken</span><span class="sxs-lookup"><span data-stu-id="7e05e-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e05e-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e05e-104">Prerequisites</span></span>
<span data-ttu-id="7e05e-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7e05e-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="7e05e-106">Ook wordt ervan uitgegaan dat u hebt de `az` Azure cli en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7e05e-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="7e05e-107">U kunt testen, hebt u de `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="7e05e-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="7e05e-108">Als u hebt de `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="7e05e-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="7e05e-109">U kunt testen, hebt u de `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="7e05e-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="7e05e-110">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7e05e-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="7e05e-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="7e05e-111">DataDog</span></span>
<span data-ttu-id="7e05e-112">Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e05e-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="7e05e-113">Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien.</span><span class="sxs-lookup"><span data-stu-id="7e05e-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="7e05e-114">Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o.</span><span class="sxs-lookup"><span data-stu-id="7e05e-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="7e05e-115">Datadog splitst metrische gegevens in containers en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="7e05e-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="7e05e-116">U moet eerst [een account maken](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="7e05e-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="7e05e-117">De Datadog-Agent installeren met een DaemonSet</span><span class="sxs-lookup"><span data-stu-id="7e05e-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="7e05e-118">DaemonSets worden gebruikt door Kubernetes één exemplaar van een container uitvoeren op elke host in het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e05e-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="7e05e-119">Ze zijn ideaal voor bewaking agenten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7e05e-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="7e05e-120">Nadat u zich bij Datadog hebt aangemeld, kunt u volgen de [Datadog instructies](https://app.datadoghq.com/account/settings#agent/kubernetes) Datadog om agents te installeren op uw cluster met behulp van een DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="7e05e-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7e05e-121">Conclusie</span><span class="sxs-lookup"><span data-stu-id="7e05e-121">Conclusion</span></span>
<span data-ttu-id="7e05e-122">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7e05e-122">That's it!</span></span> <span data-ttu-id="7e05e-123">Wanneer de agents actief en werkend zijn ziet u gegevens in de console in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="7e05e-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="7e05e-124">Ga naar de geïntegreerde [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) voor een overzicht van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e05e-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
