---
title: aaaMonitor Azure Kubernetes cluster met Datadog | Microsoft Docs
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
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="8aaa7-103">Een Azure Container Service-cluster met DataDog bewaken</span><span class="sxs-lookup"><span data-stu-id="8aaa7-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8aaa7-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8aaa7-104">Prerequisites</span></span>
<span data-ttu-id="8aaa7-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8aaa7-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="8aaa7-106">Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure cli en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="8aaa7-107">U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="8aaa7-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="8aaa7-108">Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="8aaa7-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="8aaa7-109">U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="8aaa7-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="8aaa7-110">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8aaa7-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="8aaa7-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="8aaa7-111">DataDog</span></span>
<span data-ttu-id="8aaa7-112">Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="8aaa7-113">Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="8aaa7-114">Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="8aaa7-115">Datadog splitst metrische gegevens in containers en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="8aaa7-116">U moet eerst te[een account maken](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="8aaa7-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="8aaa7-117">Hallo Datadog Agent installeren met een DaemonSet</span><span class="sxs-lookup"><span data-stu-id="8aaa7-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="8aaa7-118">DaemonSets worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="8aaa7-119">Ze zijn ideaal voor bewaking agenten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="8aaa7-120">Nadat u zich bij Datadog hebt aangemeld, kunt u volgen Hallo [Datadog instructies](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents op uw cluster met behulp van een DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8aaa7-121">Conclusie</span><span class="sxs-lookup"><span data-stu-id="8aaa7-121">Conclusion</span></span>
<span data-ttu-id="8aaa7-122">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-122">That's it!</span></span> <span data-ttu-id="8aaa7-123">Zodra het Hallo-agents actief zijn en gegevens in de console Hallo waarop uitgevoerd. u ziet in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="8aaa7-124">U kunt ook bezoeken Hallo geïntegreerd [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee een samenvatting van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="8aaa7-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
