---
title: aaaMonitor Azure Kubernetes cluster - Sysdig | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Sysdig
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="23c13-103">Een Azure Container Service Kubernetes-cluster met behulp van Sysdig bewaken</span><span class="sxs-lookup"><span data-stu-id="23c13-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23c13-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="23c13-104">Prerequisites</span></span>
<span data-ttu-id="23c13-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="23c13-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="23c13-106">Ook wordt ervan uitgegaan dat u hello azure cli en kubectl hulpprogramma's geïnstalleerd hebt.</span><span class="sxs-lookup"><span data-stu-id="23c13-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="23c13-107">U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="23c13-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="23c13-108">Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="23c13-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="23c13-109">U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="23c13-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="23c13-110">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="23c13-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="23c13-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="23c13-111">Sysdig</span></span>
<span data-ttu-id="23c13-112">Sysdig is een externe controle als een servicebedrijf die containers in uw Kubernetes cluster worden uitgevoerd in Azure kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="23c13-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="23c13-113">Sysdig, moet een actieve Sysdig-account.</span><span class="sxs-lookup"><span data-stu-id="23c13-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="23c13-114">U kunt aanmelden voor een account op hun [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="23c13-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="23c13-115">Nadat u bent aangemeld op toohello Sysdig cloud website, klikt u op uw gebruikersnaam en op de pagina Hallo ziet u uw 'toegangssleutel'.</span><span class="sxs-lookup"><span data-stu-id="23c13-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API-sleutel](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="23c13-117">Hallo Sysdig agents tooKubernetes installeren</span><span class="sxs-lookup"><span data-stu-id="23c13-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="23c13-118">uw containers, Sysdig wordt uitgevoerd een proces op elke computer met behulp van een Kubernetes toomonitor `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="23c13-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="23c13-119">DaemonSets zijn Kubernetes API-objecten die één exemplaar van een container per computer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="23c13-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="23c13-120">Ze zijn ideaal voor het installeren van hulpprogramma's als Hallo van Sysdig-bewakingsagent.</span><span class="sxs-lookup"><span data-stu-id="23c13-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="23c13-121">tooinstall hello Sysdig daemonset, moet u eerst downloaden [Hallo sjabloon](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) van sysdig.</span><span class="sxs-lookup"><span data-stu-id="23c13-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="23c13-122">Sla dit bestand op als `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="23c13-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="23c13-123">Op Linux en OS X kunt u het volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="23c13-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="23c13-124">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23c13-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="23c13-125">Vervolgens bewerken dat bestand tooinsert uw toegangssleutel die u hebt ontvangen van uw account Sysdig.</span><span class="sxs-lookup"><span data-stu-id="23c13-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="23c13-126">Maak ten slotte Hallo DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="23c13-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="23c13-127">De bewaking weergeven</span><span class="sxs-lookup"><span data-stu-id="23c13-127">View your monitoring</span></span>
<span data-ttu-id="23c13-128">Eenmaal geïnstalleerd en wordt uitgevoerd, moeten Hallo agents gegevens back tooSysdig pomp.</span><span class="sxs-lookup"><span data-stu-id="23c13-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="23c13-129">Ga terug toothe [sysdig dashboard](https://app.sysdigcloud.com) en ziet u informatie over uw containers.</span><span class="sxs-lookup"><span data-stu-id="23c13-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="23c13-130">U kunt ook installeren Kubernetes-specifieke dashboards via de [wizard Nieuw dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="23c13-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
