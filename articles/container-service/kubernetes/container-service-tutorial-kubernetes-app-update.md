---
title: zelfstudie voor aaaAzure Container Service - Update-toepassing | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Update-toepassing
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="768a0-104">Bijwerken van een toepassing in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="768a0-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="768a0-105">Nadat u een toepassing in Kubernetes hebt geïmplementeerd, kan deze worden bijgewerkt door te geven van een nieuwe container afbeeldings- of image versie.</span><span class="sxs-lookup"><span data-stu-id="768a0-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="768a0-106">Wanneer u een toepassing bijwerkt, update-implementatie Hallo tijdelijk worden opgeslagen zodat alleen een deel van Hallo implementatie gelijktijdig worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="768a0-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="768a0-107">Deze update gefaseerde kan Hallo toepassing tookeep uitgevoerd tijdens het bijwerken van Hallo en biedt een terugdraaimechanisme als een implementatie-fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="768a0-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="768a0-108">In deze zelfstudie maakt wordt deel uit zes van zeven, hello Azure stem voorbeeldapp bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="768a0-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="768a0-109">Taken die u uitvoert, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="768a0-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="768a0-110">Hallo-front-toepassingscode bijwerken</span><span class="sxs-lookup"><span data-stu-id="768a0-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="768a0-111">Maken van een installatiekopie van een bijgewerkte container</span><span class="sxs-lookup"><span data-stu-id="768a0-111">Creating an updated container image</span></span>
> * <span data-ttu-id="768a0-112">Hallo container installatiekopie tooAzure Container register pushen</span><span class="sxs-lookup"><span data-stu-id="768a0-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="768a0-113">Hallo bijgewerkte container installatiekopie implementeren</span><span class="sxs-lookup"><span data-stu-id="768a0-113">Deploying hello updated container image</span></span>

<span data-ttu-id="768a0-114">In volgende zelfstudies is Operations Management Suite geconfigureerde toomonitor hello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="768a0-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="768a0-115">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="768a0-115">Before you begin</span></span>

<span data-ttu-id="768a0-116">In vorige zelfstudies, een toepassing is ingepakt in een installatiekopie van een container, Hallo afbeelding geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="768a0-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="768a0-117">Hallo toepassing is klikt u vervolgens op Hallo Kubernetes cluster uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="768a0-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="768a0-118">Als u deze stappen niet zijn voltooid en toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="768a0-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="768a0-119">Toepassing bijwerken</span><span class="sxs-lookup"><span data-stu-id="768a0-119">Update application</span></span>

<span data-ttu-id="768a0-120">toocomplete hello stappen in deze zelfstudie, u moet hebt gekloond een kopie van hello Azure stem toepassing.</span><span class="sxs-lookup"><span data-stu-id="768a0-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="768a0-121">Indien nodig, maakt u deze gekloonde kopie met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="768a0-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="768a0-122">Open Hallo `config_file.cfg` bestand met een code- of teksteditor.</span><span class="sxs-lookup"><span data-stu-id="768a0-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="768a0-123">U vindt dit bestand onder Hallo-map van Hallo gekloond opslagplaats te volgen.</span><span class="sxs-lookup"><span data-stu-id="768a0-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="768a0-124">Hallo-waarden voor `VOTE1VALUE` en `VOTE2VALUE`, en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="768a0-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="768a0-125">Gebruik [docker compose](https://docs.docker.com/compose/) toore-Hallo front-installatiekopie en Voer Hallo bijgewerkt toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="768a0-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="768a0-126">Toepassing lokaal testen</span><span class="sxs-lookup"><span data-stu-id="768a0-126">Test application locally</span></span>

<span data-ttu-id="768a0-127">Te bladeren`http://localhost:8080` toosee Hallo toepassing bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="768a0-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="768a0-129">Installatiekopieën van het label en pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="768a0-129">Tag and push images</span></span>

<span data-ttu-id="768a0-130">Tag Hallo *azure stem voorgrond* installatiekopie met de Hallo loginServer van Hallo container register.</span><span class="sxs-lookup"><span data-stu-id="768a0-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="768a0-131">Als u Azure Container register, de naam van de aanmelding Hallo Hello ophalen [az acr lijst](/cli/azure/acr#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="768a0-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="768a0-132">Gebruik [docker-tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag Hallo installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="768a0-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="768a0-133">Vervang `<acrLoginServer>` met uw Azure-Container register server aanmeldingsnaam of openbare register hostnaam.</span><span class="sxs-lookup"><span data-stu-id="768a0-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="768a0-134">Gebruik [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload Hallo installatiekopie tooyour register.</span><span class="sxs-lookup"><span data-stu-id="768a0-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="768a0-135">Vervang `<acrLoginServer>` met uw Azure-Container register server aanmeldingsnaam of openbare register hostnaam.</span><span class="sxs-lookup"><span data-stu-id="768a0-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="768a0-136">Updatetoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="768a0-136">Deploy update application</span></span>

<span data-ttu-id="768a0-137">maximale uptime tooensure, meerdere exemplaren van Hallo toepassing schil moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="768a0-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="768a0-138">Controleer de configuratie met Hallo [kubectl ophalen schil](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.</span><span class="sxs-lookup"><span data-stu-id="768a0-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="768a0-139">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="768a0-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="768a0-140">Als u geen meerdere gehele product met hello azure-stem-front-installatiekopie, schalen Hallo *azure stem voorgrond* implementatie.</span><span class="sxs-lookup"><span data-stu-id="768a0-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="768a0-141">Gebruik Hallo-toepassing hello tooupdate [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="768a0-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="768a0-142">Update `<acrLoginServer>` met Hallo server- of host aanmeldingsnaam van het register van de container.</span><span class="sxs-lookup"><span data-stu-id="768a0-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="768a0-143">Gebruik Hallo-implementatie Hallo toomonitor [kubectl ophalen schil](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.</span><span class="sxs-lookup"><span data-stu-id="768a0-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="768a0-144">Als de toepassing hello bijgewerkt is geïmplementeerd, worden uw gehele product is beëindigd en opnieuw gemaakt met de nieuwe container installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="768a0-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="768a0-145">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="768a0-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="768a0-146">Bijgewerkte toepassing testen</span><span class="sxs-lookup"><span data-stu-id="768a0-146">Test updated application</span></span>

<span data-ttu-id="768a0-147">Het externe IP-adres Hallo Hallo *azure stem voorgrond* service.</span><span class="sxs-lookup"><span data-stu-id="768a0-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="768a0-148">Bladeren toohello IP-adres toosee Hallo toepassing bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="768a0-148">Browse toohello IP address toosee hello updated application.</span></span>

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="768a0-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="768a0-150">Next steps</span></span>

<span data-ttu-id="768a0-151">In deze zelfstudie die u kunt een toepassing bijgewerkt en deze update tooa Kubernetes cluster uitgerold.</span><span class="sxs-lookup"><span data-stu-id="768a0-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="768a0-152">Hallo na taken zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="768a0-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="768a0-153">Bijgewerkte Hallo front-code</span><span class="sxs-lookup"><span data-stu-id="768a0-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="768a0-154">Een installatiekopie van een bijgewerkte container gemaakt</span><span class="sxs-lookup"><span data-stu-id="768a0-154">Created an updated container image</span></span>
> * <span data-ttu-id="768a0-155">Hallo container installatiekopie tooAzure Container register gepusht</span><span class="sxs-lookup"><span data-stu-id="768a0-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="768a0-156">Toepassing van de geïmplementeerde Hallo bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="768a0-156">Deployed hello updated application</span></span>

<span data-ttu-id="768a0-157">Toohello volgende zelfstudie toolearn over het vooraf toomonitor Kubernetes bij Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="768a0-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="768a0-158">Kubernetes bewaken met OMS</span><span class="sxs-lookup"><span data-stu-id="768a0-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)