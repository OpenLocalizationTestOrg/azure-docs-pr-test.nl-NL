---
title: zelfstudie voor aaaAzure Container Service - Cluster implementeren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Cluster implementeren
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="cd732-104">Een cluster Kubernetes in Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="cd732-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="cd732-105">Kubernetes biedt een gedistribueerde platform voor beperkte toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cd732-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="cd732-106">Met Azure Container Service is het inrichten van een cluster met productie gereed Kubernetes snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="cd732-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="cd732-107">In deze zelfstudie maakt deel 3 van 7, wordt een Azure Container Service Kubernetes-cluster geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cd732-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="cd732-108">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="cd732-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd732-109">Een Kubernetes ACS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="cd732-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="cd732-110">Installatie van Hallo Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="cd732-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="cd732-111">Configuratie van kubectl</span><span class="sxs-lookup"><span data-stu-id="cd732-111">Configuration of kubectl</span></span>

<span data-ttu-id="cd732-112">In volgende zelfstudies hello Azure stem toepassing is geïmplementeerd toohello cluster geschaald, bijgewerkt en Operations Management Suite geconfigureerde toomonitor hello Kubernetes cluster is.</span><span class="sxs-lookup"><span data-stu-id="cd732-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cd732-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="cd732-113">Before you begin</span></span>

<span data-ttu-id="cd732-114">In vorige zelfstudies een installatiekopie van een container is gemaakt en tooan Azure Container register exemplaar geüpload.</span><span class="sxs-lookup"><span data-stu-id="cd732-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="cd732-115">Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="cd732-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="cd732-116">Een Kubernetes-cluster maken</span><span class="sxs-lookup"><span data-stu-id="cd732-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="cd732-117">In Hallo [vorige zelfstudie](./container-service-tutorial-kubernetes-prepare-acr.md), een resourcegroep met de naam *myResourceGroup* is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cd732-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="cd732-118">Als u dit niet gedaan hebt, nu deze resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="cd732-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="cd732-119">Een cluster Kubernetes maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cd732-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="cd732-120">Hallo volgende voorbeeld wordt een cluster met de naam *myK8sCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="cd732-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="cd732-121">Hallo-opdracht is voltooid na een paar minuten en json retourneert informatie over de implementatie van Hallo ACS geformatteerd.</span><span class="sxs-lookup"><span data-stu-id="cd732-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="cd732-122">Hallo kubectl CLI installeren</span><span class="sxs-lookup"><span data-stu-id="cd732-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="cd732-123">tooconnect toohello Kubernetes-cluster van de clientcomputer gebruik [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), Hallo Kubernetes opdrachtregelprogramma client.</span><span class="sxs-lookup"><span data-stu-id="cd732-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="cd732-124">Als u Azure CloudShell gebruikt, is `kubectl` al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cd732-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="cd732-125">Als u wilt dat tooinstall het lokaal hello gebruiken [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cd732-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="cd732-126">Als in de Linux- of Mac OS uitgevoerd, moet u mogelijk toorun met sudo.</span><span class="sxs-lookup"><span data-stu-id="cd732-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="cd732-127">In Windows, zorg ervoor dat uw shell is uitgevoerd als administrator.</span><span class="sxs-lookup"><span data-stu-id="cd732-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="cd732-128">Op Windows hello standaardinstallatie is *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="cd732-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="cd732-129">U moet mogelijk tooadd toohello Windows bestandspad.</span><span class="sxs-lookup"><span data-stu-id="cd732-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="cd732-130">Verbinden met kubectl</span><span class="sxs-lookup"><span data-stu-id="cd732-130">Connect with kubectl</span></span>

<span data-ttu-id="cd732-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster uitvoeren Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cd732-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="cd732-132">tooverify hello verbinding tooyour cluster uitvoeren Hallo [kubectl ophalen knooppunten](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cd732-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="cd732-133">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="cd732-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="cd732-134">Zelfstudie is voltooid hebt u een ACS-Kubernetes cluster gereed voor werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="cd732-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="cd732-135">In volgende zelfstudies is een toepassing met meerdere container geïmplementeerde toothis cluster, uitgebreid, bijgewerkt en bewaakt.</span><span class="sxs-lookup"><span data-stu-id="cd732-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd732-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd732-136">Next steps</span></span>

<span data-ttu-id="cd732-137">In deze zelfstudie is een Azure Container Service Kubernetes-cluster is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cd732-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="cd732-138">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="cd732-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd732-139">Implementatie van een cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="cd732-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="cd732-140">Geïnstalleerde Hallo Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="cd732-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="cd732-141">Geconfigureerde kubectl</span><span class="sxs-lookup"><span data-stu-id="cd732-141">Configured kubectl</span></span>

<span data-ttu-id="cd732-142">Ga toohello volgende zelfstudie toolearn over het uitvoeren van toepassing op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd732-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd732-143">De toepassing in Kubernetes implementeren</span><span class="sxs-lookup"><span data-stu-id="cd732-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
