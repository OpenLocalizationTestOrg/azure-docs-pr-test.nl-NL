---
title: zelfstudie voor aaaAzure Container Service - toepassing schalen | Microsoft Docs
description: Zelfstudie voor Azure Container Service - toepassing schalen
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="821a5-104">Schaal Kubernetes gehele product en Kubernetes infrastructuur</span><span class="sxs-lookup"><span data-stu-id="821a5-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="821a5-105">Als u Hallo zelfstudies volgt hebt, hebt u een werkende Kubernetes cluster in Azure Container Service en u hello Azure stemmen app hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="821a5-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="821a5-106">In deze zelfstudie maakt deel uit vijf zeven, uitbreiden Hallo gehele product in Hallo-app en probeer het schil automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="821a5-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="821a5-107">U leert ook hoe tooscale Hallo aantal Azure VM-agent knooppunten toochange Hallo capaciteit voor het hosten van werkbelastingen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="821a5-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="821a5-108">Taken zijn voltooid, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="821a5-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="821a5-109">Handmatig schalen Kubernetes gehele product</span><span class="sxs-lookup"><span data-stu-id="821a5-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="821a5-110">Configureren voor automatisch schalen gehele product Hallo app-front-end uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="821a5-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="821a5-111">Hallo Kubernetes Azure-agent knooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="821a5-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="821a5-112">In volgende zelfstudies hello Azure stem toepassing wordt bijgewerkt en Operations Management Suite toomonitor hello Kubernetes cluster geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="821a5-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="821a5-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="821a5-113">Before you begin</span></span>

<span data-ttu-id="821a5-114">In vorige zelfstudies, een toepassing is ingepakt in een installatiekopie van een container, maar deze installatiekopie geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="821a5-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="821a5-115">Hallo toepassing is klikt u vervolgens op Hallo Kubernetes cluster uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="821a5-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="821a5-116">Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, retourneren toohello [zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="821a5-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="821a5-117">Deze zelfstudie vereist ten minste een Kubernetes-cluster met een actieve toepassing.</span><span class="sxs-lookup"><span data-stu-id="821a5-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="821a5-118">Handmatig schalen gehele product</span><span class="sxs-lookup"><span data-stu-id="821a5-118">Manually scale pods</span></span>

<span data-ttu-id="821a5-119">Tot dusver hello Azure stem front-end- en Redis-exemplaar zijn geïmplementeerd, elk met een enkele replica.</span><span class="sxs-lookup"><span data-stu-id="821a5-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="821a5-120">tooverify, Voer Hallo [kubectl ophalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.</span><span class="sxs-lookup"><span data-stu-id="821a5-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="821a5-121">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="821a5-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="821a5-122">Hallo-nummer van het gehele product in Hallo handmatig wijzigen `azure-vote-front` implementatie met behulp van Hallo [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) opdracht.</span><span class="sxs-lookup"><span data-stu-id="821a5-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="821a5-123">In dit voorbeeld verhoogt Hallo nummer too5.</span><span class="sxs-lookup"><span data-stu-id="821a5-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="821a5-124">Voer [kubectl ophalen gehele product](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes maken van Hallo gehele product.</span><span class="sxs-lookup"><span data-stu-id="821a5-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="821a5-125">Na een minuut of zo worden Hallo aanvullende gehele product uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="821a5-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="821a5-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="821a5-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="821a5-127">Gehele product automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="821a5-127">Autoscale pods</span></span>

<span data-ttu-id="821a5-128">Biedt ondersteuning voor Kubernetes [horizontale schil automatisch schalen](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust Hallo aantal gehele product in een implementatie, afhankelijk van de CPU-gebruik of andere metrische gegevens selecteren.</span><span class="sxs-lookup"><span data-stu-id="821a5-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="821a5-129">toouse hello autoscaler, moeten uw gehele product hebben met het aanvragen van de CPU en limieten die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="821a5-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="821a5-130">In Hallo `azure-vote-front` implementatie, front-container aanvragen 0,25 CPU, met een limiet van 0,5 Hallo CPU.</span><span class="sxs-lookup"><span data-stu-id="821a5-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="821a5-131">Hallo instellingen eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="821a5-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="821a5-132">Hallo volgende voorbeeld wordt Hallo [kubectl automatisch schalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale Hallo aantal gehele product in Hallo opdracht `azure-vote-front` implementatie.</span><span class="sxs-lookup"><span data-stu-id="821a5-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="821a5-133">Als het CPU-gebruik hoger is dan 50%, verhoogt Hallo autoscaler hier Hallo gehele product tooa maximaal 10.</span><span class="sxs-lookup"><span data-stu-id="821a5-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="821a5-134">status van de toosee Hallo van Hallo autoscaler, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="821a5-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="821a5-135">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="821a5-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="821a5-136">Na een paar minuten, met een minimale belasting op Hallo Azure stem app, verlaagt Hallo aantal replica's schil automatisch too3.</span><span class="sxs-lookup"><span data-stu-id="821a5-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="821a5-137">Schaal Hallo agents</span><span class="sxs-lookup"><span data-stu-id="821a5-137">Scale hello agents</span></span>

<span data-ttu-id="821a5-138">Als u uw Kubernetes-cluster met standaardopdrachten in de vorige Hallo-zelfstudie hebt gemaakt, heeft deze drie knooppunten van de agent.</span><span class="sxs-lookup"><span data-stu-id="821a5-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="821a5-139">Als u van plan meer of minder container werkbelastingen uw cluster bent, kunt u het aantal agents Hallo handmatig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="821a5-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="821a5-140">Gebruik Hallo [az acs schalen](/cli/azure/acs#scale) opdracht en geeft u het aantal agents Hallo Hello `--new-agent-count` parameter.</span><span class="sxs-lookup"><span data-stu-id="821a5-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="821a5-141">Hallo volgende voorbeeld worden verhoogd Hallo agent knooppunten too4 in Hallo Kubernetes cluster met de naam aantal *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="821a5-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="821a5-142">Hallo opdracht duurt enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="821a5-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="821a5-143">Hallo opdrachtuitvoer toont Hallo aantal agent knooppunten in Hallo-waarde van `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="821a5-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="821a5-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="821a5-144">Next steps</span></span>

<span data-ttu-id="821a5-145">In deze zelfstudie kunt u verschillende functies die schalen in uw cluster Kubernetes gebruikt.</span><span class="sxs-lookup"><span data-stu-id="821a5-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="821a5-146">Taken aan de orde opgenomen:</span><span class="sxs-lookup"><span data-stu-id="821a5-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="821a5-147">Handmatig schalen Kubernetes gehele product</span><span class="sxs-lookup"><span data-stu-id="821a5-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="821a5-148">Configureren voor automatisch schalen gehele product Hallo app-front-end uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="821a5-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="821a5-149">Hallo Kubernetes Azure-agent knooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="821a5-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="821a5-150">Toohello volgende zelfstudie toolearn over het bijwerken van de toepassing in Kubernetes gaan.</span><span class="sxs-lookup"><span data-stu-id="821a5-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="821a5-151">Bijwerken van een toepassing in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="821a5-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

