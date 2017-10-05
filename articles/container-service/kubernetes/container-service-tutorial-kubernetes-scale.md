---
title: Zelfstudie voor Azure Container Service - toepassing schalen | Microsoft Docs
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
ms.openlocfilehash: 62e70e34d06f5220734ff85c70a0c9b475f9579b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="a7019-104">Schaal Kubernetes gehele product en Kubernetes infrastructuur</span><span class="sxs-lookup"><span data-stu-id="a7019-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="a7019-105">Als u de zelfstudies volgt hebt, hebt u een werkende Kubernetes cluster in Azure Container Service en u de app Azure stemmen hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a7019-105">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="a7019-106">In deze zelfstudie maakt deel uit vijf zeven, uitbreiden van het gehele product in de app en probeer het schil automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="a7019-106">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="a7019-107">U leert ook hoe schalen het aantal knooppunten van de Azure VM-agent wijzigen van het cluster capaciteit voor het hosten van werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="a7019-107">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="a7019-108">Taken zijn voltooid, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="a7019-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7019-109">Handmatig schalen Kubernetes gehele product</span><span class="sxs-lookup"><span data-stu-id="a7019-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="a7019-110">Automatisch schalen gehele product met de front-end van de app configureren</span><span class="sxs-lookup"><span data-stu-id="a7019-110">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="a7019-111">De agent Kubernetes Azure knooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="a7019-111">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="a7019-112">In volgende zelfstudies leert de stem van de Azure-toepassing wordt bijgewerkt en Operations Management Suite is geconfigureerd voor het controleren van het cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a7019-112">In subsequent tutorials, the Azure Vote application is updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7019-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a7019-113">Before you begin</span></span>

<span data-ttu-id="a7019-114">In vorige zelfstudies is een toepassing worden verpakt in een installatiekopie van een container, deze installatiekopie geüpload naar het register van Azure-Container en een Kubernetes-cluster gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a7019-114">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="a7019-115">De toepassing is vervolgens op het cluster Kubernetes uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a7019-115">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="a7019-116">Als u deze stappen nog niet hebt gedaan en u wilt volgen, terug naar de [zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7019-116">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="a7019-117">Deze zelfstudie vereist ten minste een Kubernetes-cluster met een actieve toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7019-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="a7019-118">Handmatig schalen gehele product</span><span class="sxs-lookup"><span data-stu-id="a7019-118">Manually scale pods</span></span>

<span data-ttu-id="a7019-119">Dus helemaal, de Azure-stem front-end- en het Redis-exemplaar zijn geïmplementeerd, elk met een enkele replica.</span><span class="sxs-lookup"><span data-stu-id="a7019-119">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="a7019-120">Uitvoeren om te controleren, de [kubectl ophalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7019-120">To verify, run the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="a7019-121">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a7019-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="a7019-122">Handmatig wijzigen van het nummer van het gehele product in de `azure-vote-front` implementatie met behulp van de [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7019-122">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="a7019-123">In dit voorbeeld verhoogt het aantal op 5.</span><span class="sxs-lookup"><span data-stu-id="a7019-123">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="a7019-124">Voer [kubectl ophalen gehele product](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) Kubernetes maken van het gehele product controleren.</span><span class="sxs-lookup"><span data-stu-id="a7019-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="a7019-125">Na een minuut of dat worden het extra gehele product uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a7019-125">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="a7019-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a7019-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="a7019-127">Gehele product automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="a7019-127">Autoscale pods</span></span>

<span data-ttu-id="a7019-128">Biedt ondersteuning voor Kubernetes [horizontale schil automatisch schalen](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) aanpassen zodat het nummer van het gehele product in een implementatie, afhankelijk van de CPU-gebruik of andere metrische gegevens selecteren.</span><span class="sxs-lookup"><span data-stu-id="a7019-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="a7019-129">Voor het gebruik van de autoscaler hebt uw gehele product CPU-aanvragen en limieten die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a7019-129">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="a7019-130">In de `azure-vote-front` voor implementatie, de front-container aanvragen 0,25 CPU, met een limiet van 0,5 CPU.</span><span class="sxs-lookup"><span data-stu-id="a7019-130">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="a7019-131">De instellingen eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="a7019-131">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="a7019-132">Het volgende voorbeeld wordt de [kubectl automatisch schalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) opdracht die moet worden automatisch schalen het aantal gehele product in de `azure-vote-front` implementatie.</span><span class="sxs-lookup"><span data-stu-id="a7019-132">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="a7019-133">Als het CPU-gebruik hoger is dan 50%, verhoogt de autoscaler hier het gehele product tot maximaal 10.</span><span class="sxs-lookup"><span data-stu-id="a7019-133">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="a7019-134">Overzicht van de status van de autoscaler, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a7019-134">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="a7019-135">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a7019-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="a7019-136">Na een paar minuten, met minimale belasting van de app Azure stem vermindert het aantal replica's schil automatisch in 3.</span><span class="sxs-lookup"><span data-stu-id="a7019-136">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="a7019-137">De agents schalen</span><span class="sxs-lookup"><span data-stu-id="a7019-137">Scale the agents</span></span>

<span data-ttu-id="a7019-138">Als u uw Kubernetes-cluster met standaardopdrachten in de vorige zelfstudie hebt gemaakt, heeft deze drie knooppunten van de agent.</span><span class="sxs-lookup"><span data-stu-id="a7019-138">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="a7019-139">Als u van plan meer of minder container werkbelastingen uw cluster bent, kunt u het aantal agents handmatig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a7019-139">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="a7019-140">Gebruik de [az acs schalen](/cli/azure/acs#scale) opdracht in en geef het aantal agents met de `--new-agent-count` parameter.</span><span class="sxs-lookup"><span data-stu-id="a7019-140">Use the [az acs scale](/cli/azure/acs#scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="a7019-141">Het volgende voorbeeld verhoogt het aantal knooppunten tot en met 4 in het Kubernetes-cluster met de naam agent *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="a7019-141">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="a7019-142">De opdracht duurt enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a7019-142">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="a7019-143">Uitvoer van de opdracht toont het aantal agent knooppunten in de waarde van `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="a7019-143">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7019-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7019-144">Next steps</span></span>

<span data-ttu-id="a7019-145">In deze zelfstudie kunt u verschillende functies die schalen in uw cluster Kubernetes gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7019-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="a7019-146">Taken aan de orde opgenomen:</span><span class="sxs-lookup"><span data-stu-id="a7019-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7019-147">Handmatig schalen Kubernetes gehele product</span><span class="sxs-lookup"><span data-stu-id="a7019-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="a7019-148">Automatisch schalen gehele product met de front-end van de app configureren</span><span class="sxs-lookup"><span data-stu-id="a7019-148">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="a7019-149">De agent Kubernetes Azure knooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="a7019-149">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="a7019-150">Ga naar de volgende zelfstudie voor meer informatie over het bijwerken van de toepassing in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a7019-150">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7019-151">Bijwerken van een toepassing in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a7019-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

