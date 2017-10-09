---
title: zelfstudie voor aaaAzure Container Service - toepassing implementeren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - toepassing implementeren
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="bf490-104">Toepassingen uitvoeren in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bf490-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="bf490-105">In deze zelfstudie maakt deel uit van vier van zeven, een voorbeeld van een toepassing wordt geïmplementeerd in een cluster met Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bf490-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="bf490-106">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="bf490-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bf490-107">Kubernetes manifest-bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="bf490-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="bf490-108">Toepassing uitvoert in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bf490-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="bf490-109">Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="bf490-109">Test hello application</span></span>

<span data-ttu-id="bf490-110">In volgende zelfstudies deze toepassing is uitgebreid, bijgewerkt, en Operations Management Suite toomonitor hello Kubernetes cluster geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bf490-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="bf490-111">Deze zelfstudie wordt ervan uitgegaan dat een basiskennis van Kubernetes concepten, Zie voor gedetailleerde informatie over Kubernetes hello [Kubernetes documentatie](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="bf490-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bf490-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bf490-112">Before you begin</span></span>

<span data-ttu-id="bf490-113">In vorige zelfstudies een toepassing in een installatiekopie van een container is verpakt, deze installatiekopie is geüploade tooAzure register van de Container en een Kubernetes-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf490-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="bf490-114">Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="bf490-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="bf490-115">Deze zelfstudie vereist ten minste een Kubernetes-cluster.</span><span class="sxs-lookup"><span data-stu-id="bf490-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="bf490-116">Manifestbestand ophalen</span><span class="sxs-lookup"><span data-stu-id="bf490-116">Get manifest file</span></span>

<span data-ttu-id="bf490-117">Voor deze zelfstudie [Kubernetes objecten](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) zijn geïmplementeerd met een Kubernetes manifest.</span><span class="sxs-lookup"><span data-stu-id="bf490-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="bf490-118">Een manifest Kubernetes is een YAML of JSON opgemaakte met Kubernetes object implementatie en configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="bf490-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="bf490-119">Hallo toepassing manifestbestand voor deze zelfstudie is beschikbaar in hello Azure stem toepassing opslagplaats, die in een vorige zelfstudie is gekloond.</span><span class="sxs-lookup"><span data-stu-id="bf490-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="bf490-120">Als u dit nog niet hebt gedaan, klonen Hallo opslagplaats Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bf490-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="bf490-121">Hallo-manifestbestand is gevonden in het Hallo-map van Hallo gekloond opslagplaats te volgen.</span><span class="sxs-lookup"><span data-stu-id="bf490-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="bf490-122">Manifestbestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="bf490-122">Update manifest file</span></span>

<span data-ttu-id="bf490-123">Als Azure-Container register toostore Hallo container installatiekopieën gebruikt, Hallo manifest behoeften toobe bijgewerkt met Hallo ACR loginServer-naam.</span><span class="sxs-lookup"><span data-stu-id="bf490-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="bf490-124">Hallo ACR server aanmeldingsnaam Hello ophalen [az acr lijst](/cli/azure/acr#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="bf490-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="bf490-125">Hallo voorbeeld manifest is vooraf gemaakt met de naam van een opslagplaats van *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="bf490-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="bf490-126">Hallo-bestand openen met een teksteditor en vervang Hallo *microsoft* waarde met de naam van de aanmelding Hallo van uw ACR-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="bf490-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="bf490-127">Toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="bf490-127">Deploy application</span></span>

<span data-ttu-id="bf490-128">Gebruik Hallo [kubectl maken](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) opdracht toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bf490-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="bf490-129">Deze opdracht parseert Hallo manifestbestand en Hallo gedefinieerd Kubernetes objecten maken.</span><span class="sxs-lookup"><span data-stu-id="bf490-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="bf490-130">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bf490-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="bf490-131">Toepassing testen</span><span class="sxs-lookup"><span data-stu-id="bf490-131">Test application</span></span>

<span data-ttu-id="bf490-132">Een [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) wordt gemaakt die beschrijft Hallo toepassing toohello internet.</span><span class="sxs-lookup"><span data-stu-id="bf490-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="bf490-133">Dit proces kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="bf490-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="bf490-134">toomonitor gemaakt, maar gebruik Hallo [kubectl ophalen service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) opdracht Hello `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="bf490-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="bf490-135">In eerste instantie Hallo **extern IP-** voor Hallo *azure stem voorgrond* service wordt weergegeven als *in behandeling*.</span><span class="sxs-lookup"><span data-stu-id="bf490-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="bf490-136">Nadat u Hallo extern IP-adres is gewijzigd van *in behandeling* tooan *IP-adres*, gebruik `CTRL-C` toostop hello kubectl controle proces.</span><span class="sxs-lookup"><span data-stu-id="bf490-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="bf490-137">toosee hello toepassing bladeren toohello externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="bf490-137">toosee hello application, browse toohello external IP address.</span></span>

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="bf490-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf490-139">Next steps</span></span>

<span data-ttu-id="bf490-140">In deze zelfstudie is hello Azure stem toepassing geïmplementeerde tooan Kubernetes van Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="bf490-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="bf490-141">Taken zijn voltooid, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="bf490-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="bf490-142">Kubernetes manifest-bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="bf490-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="bf490-143">Hallo-toepassing uitvoeren in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bf490-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="bf490-144">Geteste Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="bf490-144">Tested hello application</span></span>

<span data-ttu-id="bf490-145">Toohello volgende zelfstudie toolearn over het schalen van een Kubernetes toepassing en de onderliggende infrastructuur Kubernetes Hallo gaan.</span><span class="sxs-lookup"><span data-stu-id="bf490-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf490-146">Schaal Kubernetes toepassingen en infrastructuur</span><span class="sxs-lookup"><span data-stu-id="bf490-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)